# Wayflyer Ad Studio

A single-page tool for making social ad images for Instagram, Facebook and LinkedIn. It walks you through a few setup steps, opens a canvas editor, and exports a finished PNG or JPG at the right size for the placement.

Everything lives in one file, [index.html](index.html): HTML, CSS and JavaScript, with no build step and no dependencies apart from Google Fonts.

## Running it

Open `index.html` in a browser. If you want a local server instead:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## How it works

The app is a guided flow with seven steps:

1. **Welcome**
2. **Platform**: Instagram, Facebook or LinkedIn
3. **Placement**: Post or Story
4. **Dimensions**: the sizes available for the chosen placement
5. **Layout**: a preset layout to start from
6. **Content**: headline, body text, button, background image, colours and font
7. **Guides and export**: the full editor, with drag-to-position elements, snapping, guides and export

### Sizes

| Size        | Ratio | Name        | Placement |
|-------------|-------|-------------|-----------|
| 1080 × 1080 | 1:1   | Square      | Post      |
| 1080 × 1350 | 4:5   | Portrait    | Post      |
| 1080 × 1920 | 9:16  | Full screen | Story     |

LinkedIn has no Stories placement. If you pick Story for LinkedIn, the app warns you that you'll get a 9:16 image.

### Layouts

- **Default:** Bottom stack, Centered, Headline first, Text card
- **Custom:** Quote, Silhouette, Product

The custom layouts come with their own starter copy and colours.

### Editor features

- Elements you can select and move: headline, body, button, logo, brand name, eyebrow, quote mark, text card, product card and frame lines
- Guides for margins, centre lines, rule of thirds and platform safe zones, plus snap-to-guide
- Colour themes (Midnight, Citrus, Coral, Forest, Paper) or your own colours
- Fonts: Inter, Bricolage Grotesque, Archivo, Space Grotesk and DM Serif Display
- Background image with zoom and position, an image overlay, and an optional grain effect
- Light and dark mode that follows the system setting

### Export

Ads are drawn on a `<canvas>` and exported at full resolution as PNG or JPG (you can set the JPG quality).

## Library and Live Ads

The app has two shared areas:

- **Library:** reusable images, in two tabs, *Imagery* and *Silhouettes*. Accepts JPG, PNG, WebP and GIF.
- **Live Ads:** a record of exported ads, which you can filter by platform, download again or delete.

What these can do depends on where the page runs:

| Mode         | When                                                                      | Behaviour                                                                                   |
|--------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **cloud**    | Published as a Claude artifact with the `db` and `assets` capabilities    | The library and Live Ads sync for everyone with access, and uploaded files are stored as assets |
| **readonly** | `db` is available but `assets` is not                                     | You can browse the shared library, but you can't upload to it                               |
| **local**    | Opened as a plain file, or with no runtime                                | Uses the images bundled in the file, and Live Ads last only until you close the tab         |

The app reaches these capabilities through `window.claude.use(...)`: `db`, `assets` and `downloads`. When they aren't available, it falls back to local mode without errors.

## Code layout

`index.html` is organised roughly like this:

- **Styles:** design tokens on `:root` with dark-mode overrides, followed by component styles
- **Config:** `STEPS`, `PLATFORMS`, `SIZES`, `PLACEMENT_SIZES`, `LAYOUTS`, `THEMES`, `FONTS` and the preset copy and colours
- **State:** a single `S` object holding the current step, choices, content, styling, element positions, guides and export settings
- **Rendering:** `renderStep`, `renderRail` and `renderInspector` for the UI, and `render`, `buildLayout` and the `draw*` helpers for the canvas
- **Library and Live Ads:** `initLibrary`, `addToLibrary`, `archiveExport` and the views that go with them
- **Export:** `exportAd`

To add a size, platform or layout, start by editing the config objects near the top of the script.
