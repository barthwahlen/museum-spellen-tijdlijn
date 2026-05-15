# ⚔ Vesting Maastricht – Tijdlijn Spel

Een interactief educatief webspel waarin spelers historische sleutelfiguren op de juiste plek in de geschiedenis van Vesting Maastricht plaatsen. Van de Romeinse tijd tot de opheffing van de vesting in 1867.

## Spelen

Open `index.html` in een moderne browser. Geen installatie, geen build, geen server nodig.

Of serveer lokaal:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Hoe werkt het

1. Tik op een figuur in de kaartenpool (goud = geselecteerd).
2. Tik op het tijdvak waar de figuur volgens jou thuishoort.
3. Op een PC kun je ook slepen.
4. Tik op ✕ om een geplaatste kaart terug te zetten.
5. Klik op **Controleer mijn antwoorden** voor je score en uitleg.

Per figuur staat een hint klaar als je twijfelt.

## Tijdvakken

| # | Periode | Jaren |
|---|---|---|
| 1 | Romeinse Tijd | 50 – 400 |
| 2 | Vroege Middeleeuwen | 400 – 900 |
| 3 | Middeleeuwen | 900 – 1480 |
| 4 | Bourgondisch & Spaans | 1480 – 1635 |
| 5 | Republiek der Nederlanden | 1635 – 1794 |
| 6 | Frans Bestuur & Opheffing | 1794 – 1867 |

## Techniek

- Eén bestand: `index.html` (HTML + CSS + vanilla JS)
- Geen frameworks, geen dependencies, geen build-step
- Externe bron: Google Fonts (Cinzel + Nunito)
- Werkt op desktop (drag-and-drop) en mobiel (tap-to-place)
- Volledig responsief

## Uitbreiden

Het spel is data-gedreven. Voeg een tijdvak toe aan `zones[]` of een figuur aan `persons[]` bovenaan het `<script>`-blok, en de tijdlijn, legenda en scoring passen zich automatisch aan. Zie `CLAUDE.md` voor architectuurdetails.

## Doelgroep

Bedoeld voor museumbezoekers, scholieren en geschiedenisliefhebbers die op een speelse manier kennismaken met de vestinggeschiedenis van Maastricht.
