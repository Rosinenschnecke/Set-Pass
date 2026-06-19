# Crew-Ausweis Generator

A crew ID-card ("Ausweis") generator for the school film production
**XY Pictures · Heinrich-Hertz-Gymnasium** (film: *The Massacre of Love*).

This is a real implementation of the Claude Design prototype
(`design/Ausweis-Generator.dc.html`), rebuilt as a dependency-free static web
app in vanilla HTML/CSS/JS.

## Features

- **Editable table** of all participants — name, department, role/function,
  in-film role, and markers, all edited inline.
- **Automatic numbering** — the pass number follows the row order (001, 002, …).
- **Reorderable rows** — drag the ⠿ handle or use the ▲▼ arrows; numbers update
  automatically.
- **Markers**: `HEAD` (department head), `MEDIA` (photo/video release) and a
  golden `LEGACY` badge for crew who have taken part multiple times.
- **Role picker** — a datalist of typical film-set jobs (free text still allowed).
- **Live preview** of the selected crew card in credit-card format (85 × 54 mm).
- **Printing** — „Alle drucken“ lays every card at true size on A4, and each row
  has its own „Drucken“ button to print a single pass.
- **Auto-save** to `localStorage` (migrates older saved data), with the film
  title persisted too.

Six departments are colour-coded: Regie, Produktion, Technik, Kostüm,
Szenenbild and Cast.

## iPhone / mobile

The app is fully responsive. On phones it collapses to a single column with a
bottom tab bar (**Liste · Bearbeiten · Vorschau**); the preview card scales to
fit the screen and the notch / home-indicator safe areas are respected. A web
app manifest plus Apple meta tags let you **Add to Home Screen** in Safari for a
standalone, full-screen experience.

## Run

It's a static site — just open `index.html`, or serve the folder:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## Layout

```
index.html                     – the app
assets/                        – qr-drehplan.svg, xy-pictures-logo.png, school-emblem-white.png
design/Ausweis-Generator.dc.html – original Claude Design prototype (reference)
```
