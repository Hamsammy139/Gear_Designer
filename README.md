# RC Gear Designer

A browser tool for designing 3D-printable involute gears for 1/10 scale RC crawlers and general hobby use. It previews the gear live in 3D, checks it against gear-geometry and FDM printing limits, and exports **binary STL** and **STEP**.

Everything runs in one self-contained HTML file. There's nothing to install and no server.

## Use it

- **Online:** open the GitHub Pages link for this repo (see *Publishing* below).
- **Offline:** download `index.html` and open it in any modern browser.

## Features

- Spur, helical (left/right hand) and herringbone gears
- Internal (ring) gears
- **Single gear** and **Mesh pair** modes. Mesh pair shows centre distance, ratio and contact ratio for a pinion and the gear it drives.
- Module or diametral pitch, 14.5° / 20° / 25° pressure angle, full-depth or stub teeth
- Profile shift, with an **Auto** button that picks the smallest shift that avoids undercut
- Tip truncation and root fillet
- Round bores (including 1/8" / 3.175 mm), hub, set-screw hole and lightening-hole web
- Print-fit controls: backlash per flank, bore compensation and elephant's-foot chamfers
- Material and nozzle checks that flag teeth too thin to print, plus a mass estimate
- Presets for common RC pinions and spurs
- A shareable link: every setting is saved in the page URL

## Printing tips

- Print flat on the bed, with the chamfered face down.
- Start with 0.08–0.15 mm backlash per flank, then print a calibration pair to tune it for your filament.
- PETG or Nylon hold up better than PLA for motor pinions, because PLA softens near 55 °C.

## Project layout

```
index.html          Built page -- this is what people open (generated, but committed for GitHub Pages)
build.js            Combines src/ into index.html
src/app.html        Page template: layout, styles, controls, 3D preview
src/gear-core.js    Gear geometry, mesh building, STL and STEP writers (no DOM)
docs/               Design spec
```

## Editing and rebuilding

Don't edit `index.html` directly. Make changes in `src/`, then rebuild:

```
node build.js
```

This needs [Node.js](https://nodejs.org/) and has no other dependencies. Open the new `index.html` in a browser to check it, then commit both the `src/` changes and the rebuilt `index.html`.

`src/app.html` won't work on its own. It holds a placeholder that `build.js` replaces with `gear-core.js`.

## Publishing with GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Under *Build and deployment*, choose **Deploy from a branch**, then select branch `main` and folder `/ (root)`.
4. After a minute the tool is live at `https://<your-username>.github.io/<repo-name>/`.

## Notes

- STEP export is a faceted solid (flat faces). It imports into CAD as a solid body, not a mesh.
- Preset sizes are typical community and RC-hobby values. Check them against your own parts before printing.

## License

MIT. See [LICENSE](LICENSE).
