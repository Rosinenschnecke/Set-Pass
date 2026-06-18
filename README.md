# Crew-Ausweis Generator

A crew ID-card ("Ausweis") generator for the school film production
**XY Pictures · Heinrich-Hertz-Gymnasium** (film: *The Massacre of Love*).

This is a real implementation of the Claude Design prototype
(`design/Ausweis-Generator.dc.html`), rebuilt as a dependency-free static web
app in vanilla HTML/CSS/JS.

## Features

- **Teilnehmer-Liste** with live search and department colour bars.
- **Editor** for each person: name, pronouns, pass number, department,
  role/function, optional in-film role name, and `HEAD` / `MEDIA` markers.
- **Live preview** of the crew card in credit-card format (85 × 54 mm).
- **„Alle drucken“** lays out every card at true card size on A4 for print/PDF.
- **Auto-save** to `localStorage` — data and film title persist in the browser.

Six departments are colour-coded: Regie, Produktion, Technik, Kostüm,
Szenenbild and Cast.

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
