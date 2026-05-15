# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single educational web game: **Vesting Maastricht – Tijdlijn Spel**. Players place historical figures on the correct era of a Maastricht-fortification timeline.

## Running

No build step, no dependencies, no tests. Open `index.html` directly in a browser, or serve it (e.g. `python3 -m http.server`) and visit `localhost:8000`. Only external resource is Google Fonts (Cinzel + Nunito) — needs network on first load.

UI text is Dutch; keep it that way when editing user-facing strings.

## Architecture

Everything lives in one file: `index.html` (HTML + `<style>` + `<script>`, ~640 lines). Vanilla JS, no framework, no modules, globals on `window`, inline `onclick=` handlers in the markup.

**Data-driven core** — two arrays at the top of the script are the single source of truth:
- `zones[]` (`index.html:375`): the 6 timeline eras. Each has `id`, `startYear`, `endYear`, `label`, `color`, `emoji`. Bounds `START_YEAR`/`END_YEAR` (`:373`) frame the rope.
- `persons[]` (`:384`): the cards to place. Each links to a zone via `correctZone` (FK to `zones[].id`). `color` should match the target zone's color (used for the card's era stripe).

Add an entry to either array and the timeline, legend, drop-zones, and scoring all adapt automatically — no other changes needed.

**State** (`:395-397`): three globals.
- `placement`: `{ zoneId: [personId, ...] }` — which cards are in which zone.
- `selectedId`: currently tapped card (tap-to-select, then tap zone to place).
- `checked`: locks interaction after `checkAnswers()` runs.

**Render pipeline**: `buildTimeline()` and `buildCards()` wipe and rebuild their DOM subtrees from the data arrays. `createCard()` is the card factory; it attaches drag + click handlers per card. Zone widths are proportional via `yearToPercent()` so the visual scale matches actual years.

**Three input modes coexist** on the same elements: HTML5 drag-and-drop (desktop), tap-to-select-then-tap-zone (touch primary path), and a `touchstart`/`touchend` highlight purely for visual feedback. When changing interaction code, verify all three still work — they overlap on the same listeners.

**DOM is the source of truth for visuals; `placement` is the source of truth for logic.** They're kept in sync manually inside `placeCard()` / `returnCardToPool()`. Any new mutation path must update both, or scoring will desync from what the user sees.

**Scoring** (`checkAnswers()`, `:574`): compares each person's actual zone vs. `correctZone`, tallies, picks a seal/title/stars tier by percentage (100 / ≥75 / ≥50 / ≥25 / else), and renders the result overlay. Tier thresholds and copy are inline in that function.
