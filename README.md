# Bevraging Platform — Quarto + Tally.so Template

Een statische website gebouwd met Quarto waarmee organisaties hun eigen Tally.so bevraging kunnen laden en tonen.

## Bestanden

```
survey-template/
├── index.qmd       ← Hoofdpagina (bewerk dit bestand)
├── styles.css      ← Opmaak van de pagina
└── README.md       ← Deze handleiding
```

## Vereisten

- [Quarto](https://quarto.org/docs/get-started/) geïnstalleerd
- R of Python (voor Quarto rendering)
- Een Netlify account (gratis)

## Lokaal bekijken

```bash
quarto preview index.qmd
```

## Publiceren op Netlify

### Optie 1: Via Netlify CLI

```bash
# Rendeer de statische site
quarto render index.qmd

# Publiceer naar Netlify
netlify deploy --dir=. --prod
```

### Optie 2: Via GitHub + Netlify (aanbevolen)

1. Zet de bestanden in een GitHub repository
2. Verbind de repository met Netlify
3. Stel in Netlify de build-opdracht in:
   - **Build command**: `quarto render`
   - **Publish directory**: `.` (of de output map)

## Aanpassen

### Titel en teksten wijzigen
Bewerk `index.qmd` — zoek naar de teksten in de HTML-blokken.

### Kleuren aanpassen
Bewerk de CSS-variabelen bovenaan `styles.css`:
```css
:root {
  --kleur-accent: #2D6BE4;  /* hoofdkleur */
  /* ... */
}
```

### Logo toevoegen
Vervang in `index.qmd`:
```html
<span class="logo-dot"></span>
<span class="logo-text">Bevraging Platform</span>
```
door:
```html
<img src="jouw-logo.png" alt="Logo" style="height:32px;">
```

## Hoe werkt de Tally embed?

Wanneer een gebruiker een Tally-link invult (bv. `https://tally.so/r/abc123`),
extraheert de JavaScript de form ID en laadt de bevraging als iframe:

```
https://tally.so/embed/{formId}?alignLeft=1&transparentBackground=1&dynamicHeight=1
```

De parameters zorgen voor:
- `alignLeft=1` — meer ruimte voor lange stellingen (links uitlijnen)
- `transparentBackground=1` — integreert naadloos in de pagina
- `dynamicHeight=1` — past de hoogte automatisch aan de inhoud aan

## Noot over CSS in iframe

Tally-forms worden geladen in een iframe. Door browser-beveiligingsregels 
(cross-origin policy) kan externe CSS de interne opmaak van het iframe **niet** 
aanpassen. Om matrix-vragen toch goed leesbaar te maken zijn er twee opties:

1. **Brede modus** op de pagina (knop beschikbaar)
2. **Tally Pro** met custom CSS rechtstreeks in de Tally builder

## Tally template delen

Exporteer jouw Tally-survey als JSON:
1. Open de survey in Tally
2. Ga naar Settings → Export
3. Exporteer als `.json`
4. Voeg het bestand toe aan deze repository als `survey-template.json`

Andere organisaties kunnen het importeren via:
Tally → New form → Import
