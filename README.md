# Wayflyer Brand Guidelines

An interactive version of the Wayflyer Brand Guidelines v2.0. It covers the brand's principles, logo, colour, typography, illustration, imagery and assets as a set of pages, with live examples you can copy, adjust and export.

The site is one file, [index.html](index.html): HTML, CSS and JavaScript, with no build step. Images and videos are embedded in the file as base64, which is why it is about 16MB. The only external resources are Google Fonts (Inter) and, for PDF export, two scripts loaded from cdnjs when you need them.

> Looking for the ad-making tool? Wayflyer Ad Studio lives in its own repo: [ervinhalebic-brand/Wayflyer-Ad-Studio](https://github.com/ervinhalebic-brand/Wayflyer-Ad-Studio).

## Running it

Open `index.html` in a browser. If you want a local server instead:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Contents

The guidelines are split into sections, each with its own pages:

| Section          | Pages                                                                                                      |
|------------------|------------------------------------------------------------------------------------------------------------|
| **Introduction** | Cover, Welcome, Our mission, Our goal                                                                      |
| **Strategy**     | Principles (essence, purpose, vision), Brand pillars, Personality                                          |
| **Language**     | Voice & tone *(coming in v3)*                                                                              |
| **Logo**         | Primary logo, Brand symbol, Clear space, Placement and scale, Partnership lockup, Misuse                   |
| **Color**        | Primary palette, Full palette (Pulse and grey ramps), Gradients, Color combinations                        |
| **Typography**   | Typeface, Weights, Hierarchy, Styling, Formatting *(coming in v3)*                                         |
| **Illustration** | Iconography (Iconoir), Patterns, Illustrations                                                             |
| **Imagery**      | Photography, Silhouettes, Mockups                                                                          |
| **Assets**       | Collateral, UI, Cards, Campaigns, Product videos, Marketing videos, Event videos, Events                   |
| **Other**        | Contributors, Release notes                                                                                |

## Using the site

- **Navigation:** use the sidebar, the previous and next buttons, or the left and right arrow keys. Each page has its own URL hash (for example `#gradients`), so you can link straight to it.
- **Copying values:** click a colour swatch to copy its hex value. Logo pages can copy the wordmark as SVG in dark or light.
- **Interactive examples:** toggle clear-space guides, try logo sizes against the 32px digital minimum, switch type weights and edit the sample word, and step through the personality traits.
- **Partnership lockup:** upload a partner's SVG logo to build a Wayflyer + partner lockup, then export it as `wayflyer-partnership.svg`. The uploaded logo is sanitised before use and remembered in the browser.
- **PDF export:** exports every page as a 1920 × 1080 landscape PDF, using html2canvas and jsPDF. The browser's own print dialog uses the same layout.
- **Light and dark mode:** follows the system setting by default. Your choice is remembered in the browser.

Some buttons are placeholders in this prototype. Asset downloads, for example, show a notice instead of downloading a file.

## Code layout

`index.html` is organised roughly like this:

- **Styles:** design tokens on `:root` with light and dark themes, component styles, and print styles under `html.printing`
- **Brand data:** `WM_PATHS` and `SYMBOL_PATH` (logo artwork), `PERSONALITY`, `PRINCIPLES`, `PILLARS`, `GREYS`, `PULSES`, `GRADS`, `ICONOIR` and `TEAM`
- **Media:** the `*_IMG` and `*_VIDEO` constants, which hold the embedded images and videos
- **Pages:** `SECTIONS` and `BOTTOM` define every section and page. A page either has `left` and `right` content or is `full` with its own `render`, and can add a `switcher` for in-page toggles
- **Rendering:** `buildNav`, `render` and `go`, plus helpers such as `assetGrid`, `photoGrid`, `swatch` and `placementView`
- **Features:** `buildLockupSVG` and `exportLockup` for partnership lockups, `exportPDF` for PDF export, and `setTheme` for light and dark mode

To add or change a page, edit its entry in `SECTIONS`. Pages tagged `v3` are placeholders for guidelines that are still being written.
