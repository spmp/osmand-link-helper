# OsmAnd Link Helper (userscript)

Convert an address or coordinates in any focused text field into an **OsmAnd** pin link.  
Works with plain `<input>/<textarea>` and rich editors (`contenteditable`).  
Includes a floating **split pill** (left/right actions) and a configurable hotkey.

- **Split pill**: left half can insert just the link, right half can insert “address + link” (both configurable).
- **Hotkey**: default **Alt + O** (customizable).
- **Geocoding**: OpenStreetMap **Nominatim** (no API key).
- **Coordinates passthrough**: `lat, lon` in the field converts directly to an OsmAnd link.
- **Clipboard safety**: optionally copies the previous field value before writing.

> Tested with Violentmonkey on Firefox. Should also work with Tampermonkey/Greasemonkey.

---

## Install

1. Install a userscript manager:
   - [Violentmonkey](https://violentmonkey.github.io/) (Firefox/Chrome/Edge)
   - [Tampermonkey](https://www.tampermonkey.net/)
   - [Greasemonkey](https://www.greasespot.net/)

2. Install the script:
   - **Direct (recommended)**: open the raw URL and your manager will prompt to install:
     ```
     https://raw.githubusercontent.com/spmp/osmand-link-helper/main/osmand-link-helper.user.js
     ```
   - Or create a new userscript in your manager and paste the file contents.

3. Scope where it runs:
   - The script header uses `@match` patterns. To limit it (and avoid running on every site), use **one per line**, e.g.:
     ```js
     // @match        https://ksuite.infomaniak.com/*/calendar/*
     // @match        https://calendar.google.com/calendar/*
     ```
   - In Violentmonkey → your script → **Settings**, you can add or remove Includes if you want different targets.

---

## Usage

1. Focus any editable field (Location, Notes, etc.).
2. Click the **pill** near the field:
   - **Left half** → uses `appendModeLeft` (e.g. just the link)
   - **Right half** → uses `appendModeRight` (e.g. address + link)
3. Or press the **hotkey** (default **Alt + O**); this uses the single `appendMode`.

If the field already contains **coordinates** like `39.7392, -104.9903`, the script skips geocoding and creates the OsmAnd link immediately.  
If it contains an **address**, it runs a Nominatim search and shows a small picker (Cancel closes cleanly).

---

## Link formats

- **map (pin)**  
