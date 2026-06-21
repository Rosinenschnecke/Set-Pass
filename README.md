# XY Pictures · Crew-Tools

Two tools for the school film production **XY Pictures · Heinrich-Hertz-Gymnasium**
(film: *The Massacre of Love*), built as one dependency-free static web app with
two tabs that share a single **personnel database**:

1. **Crew-Ausweise** — the crew ID-card generator (the personnel database lives here).
2. **Set-Schilder** — A4 set signage (Aufnahme/Ruhe, Verbote, Wegweiser, Pfeile,
   Gefahr, Crew-Liste, Telefonliste, Set-Regeln, Drehplan-Aushang, Drehtag-Trenner,
   Fortschritt) in two styles (dark/light), portrait/landscape, with compare and
   full-page printing.
3. **Drehplan** — a live control interface (tick off scenes, log shot minutes,
   step day/team counters) plus a fullscreen **motivational board** (Statistik-Board,
   1920×1080) for the big screen in the base. Both read the same board data, which
   is part of the shared, cloud-synced database, so updates appear live.

Both tabs implement the Claude Design prototypes
(`design/Ausweis-Generator.dc.html`, `design/Set-Schilder.dc.html` + `Schild.dc.html`).

## Shared personnel database

A single people store is the source of truth. The Ausweise tab edits it; the
Set-Schilder **„Crew am Set"** name list is generated **automatically** from it —
add a person and they appear on that sign instantly. Everything is auto-saved.

> **Storage:** the whole state (people + signs + film title) is synced to a
> **Supabase** table (`crew_state`, single `main` row holding a JSON snapshot),
> so it is shared **across devices**. `localStorage` is kept as an offline cache,
> and changes are pulled periodically (last-write-wins). The publishable/anon key
> is browser-safe and committed by design; access is governed by the table's RLS
> policies.

## Features

- **Editable table** of all participants — name, department, role/function,
  in-film role, and markers, all edited inline.
- **Automatic numbering** — the pass number follows the row order (001, 002, …).
- **Reorderable rows** — drag the ⠿ handle or use the ▲▼ arrows; numbers update
  automatically.
- **Sort by department** — a toggle groups the table by department for overview
  **without changing the assigned pass numbers** (numbering stays tied to the
  manual order).
- **Markers**: `HEAD` (department head), `LEHRER` (teacher), `MEDIA` (photo/video
  release) and a golden `LEGACY` badge for crew who have taken part multiple times.
- **Role picker** — a datalist of typical film-set jobs (free text still allowed).
- **Long names** are auto-sized down so they always fit the card.
- **Live preview** of the selected crew card in credit-card format (85 × 54 mm),
  with square corners for clean trimming.
- **Printing** — „Alle drucken“ lays every card at true size on A4 (each card kept
  whole, never split across a page break), and each row has its own „Drucken“
  button to print a single pass.
- **Light/dark card design** — toggle "Design: Hell/Dunkel"; the light variant uses
  a pure-white background to save toner.
- **Set-Schilder** — light style (Stil B) is pure white; long lists (Crew-Liste,
  Regeln, Drehplan) auto-paginate across several A4 pages on print.
- **Real date pickers** — the Drehtag uses a date input and derives the weekday
  automatically. From the first day you can **generate all shooting days**,
  skipping weekends and configurable off-days.

## Password & privacy

The app is gated by a project password. The full state is **encrypted in the
browser** (AES-GCM, key derived from the password via PBKDF2) before being stored
in Supabase, so the cloud data is unreadable without the password. The first
password entered becomes the project password; enter it once per session.
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
