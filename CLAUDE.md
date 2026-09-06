# web-macker-baukasten

## Zweck
Quell-Bibliothek für Kundenwebsites kleiner Betriebe im DACH-Raum.
Wiederverwendet wird der CODE, niemals das Erscheinungsbild.
Harte Regel: Zwei Kundenseiten dürfen sich nie ähnlich sehen.

Dies ist eine Bibliothek zum KOPIEREN, kein Build-System.
Kein npm, kein Bundler, kein Tailwind-Compile – gearbeitet wird
ausschließlich auf einem iPad. Plain HTML + plain CSS.

## Struktur
core/
  base.css              Reset, Typo-Skala, Utilities
  sections/             hero-a.html, grid-a.html, about-a.html, footer.html
shopify/                dünne Liquid-Hüllen mit {% schema %} um core/-Markup
tokens/
  _template.css         Vorlage aller CSS-Variablen
  kunde-<slug>.css      eine Datei pro Kunde
prompts/                kunden-fragebogen.md, produkttexte.md
kunden-register.md      Kunde | Ort | Sektionskombination | Token-Set | Datum

## Token-System
Alle Farb-, Typo-, Abstands- und Formwerte NUR über CSS-Variablen.
Kein hartcodierter Farbwert, keine feste px-Größe in den Sektionen.

```css
:root {
  --c-bg  --c-surface  --c-text  --c-muted
  --c-accent  --c-accent-contrast  --c-border
  --f-display  --f-body
  --fs-xs … --fs-3xl        (clamp-basiert, fluid)
  --lh-tight  --lh-body  --tracking-display
  --sp-1 … --sp-12          (Abstandsskala)
  --section-y               (vertikaler Sektionsrhythmus)
  --content-max
  --radius  --border-w  --shadow
}
```

## Differenzierungs-Pflicht
Zwei Kunden im selben Landkreis müssen sich in MINDESTENS VIER
dieser Punkte unterscheiden:
1. Sektionskombination
2. Schriftpaarung
3. Akzentfarbe (Farbton-Abstand > 60°)
4. Radius-Stufe (eckig / weich / rund)
5. Sektionsrhythmus (kompakt / luftig)
6. Bildbehandlung (vollflächig / gerahmt / freigestellt)
Vor jedem neuen Kunden zuerst kunden-register.md prüfen.

## Sektionsvarianten müssen STRUKTURELL verschieden sein
Nicht dieselbe Anordnung in anderer Farbe, sondern:
- hero-a: vollflächiges Bild, Text als Overlay, zentriert
- hero-b: 50/50-Split, Text links, Bild rechts, asymmetrisch
- hero-c: textdominant, kein großes Bild, große Headline + Trennlinie
Dieselbe Logik gilt für Grid- und About-Varianten.

## Qualitätsschwellen (nicht verhandelbar)
- Mobile-first. Breakpoints: 480 / 768 / 1100.
- Kein JavaScript, außer zwingend nötig. Dann Vanilla, < 3 KB.
- Jedes Bild: loading="lazy" + width + height (gegen Layout-Shift).
- Semantische Landmarks: header / nav / main / section / footer.
  Genau eine h1 pro Seite.
- :focus-visible sichtbar. Kontrast mindestens 4.5:1.
- Kein Text in Bildern.
- Ziel PageSpeed Insights mobil: Performance ≥ 90, A11y ≥ 95.

## DACH-Pflichtbausteine
- Footer verlinkt Impressum und Datenschutz.
- Kontakt mit echten tel:- und mailto:-Links, vollständige Anschrift.
- KEINE Google Fonts über CDN (DSGVO). Systemschriften oder
  selbst gehostete Schriften.
- Keine externen Skripte ohne Einwilligung.

## Verboten
- Bestehende Kundenseite als Startpunkt kopieren.
- Stock-Fotos als Standard (echtes Betriebsmaterial hat Vorrang).
- Fremd-Badges jeglicher Art.
- Eigene Standardpalette – Farben immer aus der Kundenmarke ableiten.

## Build-Reihenfolge
Ein Schritt pro Session. Nach jedem Schritt gegen die
Qualitätsschwellen prüfen, erst dann weiter.
1. tokens/_template.css + core/base.css
2. core/sections/footer.html (DACH-Pflicht)
3. hero-a  →  4. grid-a  →  5. about-a
6. tokens/kunde-koschmieder.css
7. Erst nach Kunde 1: hero-b/c, grid-b/c, about-b aus der
   echten Arbeit extrahieren – nicht auf Vorrat bauen.
8. prompts/ und shopify/ zuletzt.
