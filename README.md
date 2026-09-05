# Captured

Get footage off a card and onto your Mac, organized, in one pass.

Captured is a small macOS app for the part of the job nobody enjoys: plugging in a card reader, finding the clips, copying them somewhere sensible, and naming them so they still make sense a month later. Point it at a card, tick the clips you want, choose where they go, and it handles the rest.

## What it does

- **Finds your cards.** Mounted volumes are listed automatically, with removable drives and anything containing a `DCIM` folder called out first. You can also point it at any folder.
- **Shows you the clips, not the clutter.** Every card gets scanned for video — MP4, MOV, MTS, MXF, BRAW, R3D, INSV and more — with thumbnails rendered by the same previewer Finder uses. Nothing to install.
- **Sorts by shoot date.** Files can drop into dated folders (`2026/2026-09-03`, `2026-09-03`, or `2026/09/03`). Folders that already exist get reused instead of duplicated, so a second card from the same day lands beside the first.
- **Renames on the way in.** Give the import a name and clips come out as `Japan_1`, `Japan_2`, … numbered in the order they were shot, across every date folder.
- **Labels the frame rate.** Turn it on and `C1850.MP4` arrives as `C1850_120fps.MP4`, read straight from the file itself. Its `C1850.XML` sidecar follows along as `C1850_120fps.XML`.
- **Keeps sidecars with their clips.** Matching `.XML`, `.SRT`, `.THM` and `.CPI` files are imported alongside the footage and renamed to match, including Sony's `C0001M01.XML` tagging.
- **Skips the junk.** DJI's low-res `.LRF` and `.LRV` proxies are never mistaken for takes, so you don't import every clip twice.
- **Won't overwrite anything.** Files already in the destination can be skipped as duplicates, and a name clash parks the new clip beside the old one as `-1` rather than replacing it.
- **Preserves capture times.** The date a clip was shot survives the trip off the card.

Copying shows live progress and can be cancelled mid-file; when it finishes, one click reveals the results in Finder.

## Install

Download the `.dmg` from [Releases](https://github.com/Lmar-O/captured/releases/latest), open it, and drag **Captured** to your Applications folder. The build is universal — it runs natively on both Apple Silicon and Intel Macs. macOS 10.15 or later.

### First launch

macOS blocks the app the first time you open it, because Captured is signed ad-hoc rather than with a paid Apple Developer ID. This is a one-time step:

1. Try to open Captured. macOS refuses.
2. Open **System Settings → Privacy & Security** and scroll down to **Security**.
3. Click **Open Anyway** next to the message about Captured.
4. Open the app again and confirm.

> Control-clicking the app and choosing *Open* does **not** work on macOS 15 (Sequoia) or later — Apple removed that shortcut. Older advice you may find elsewhere is out of date.

If you'd rather do it in one line:

```bash
xattr -dr com.apple.quarantine /Applications/Captured.app
```

## Using it

The window is three columns, left to right:

1. **Source** — pick the card or folder to import from. *Include subfolders* is on by default, which is what you want for the `DCIM/100MEDIA` layout cameras use.
2. **Files** — every clip found, with thumbnails, sizes and capture dates. Select the ones you want, or take the whole card.
3. **Destination** — where the footage lands, how it's organized into folders, whether it gets renamed, and what to do about sidecars and duplicates.

Hit **Import** and watch it run.

## Development

Captured is an Electron app with no runtime dependencies beyond Electron itself.

```bash
npm install
npm start      # run from source
npm test       # unit tests
npm run dist   # build a universal .dmg into dist/
```

To regenerate the app icon after editing `build/icon-source.png`:

```bash
npx electron build/make-icon.js
```

Releases are built by GitHub Actions: pushing a `v*` tag builds the universal DMG on a macOS runner and attaches it to the release. `.github/workflows/release.yml` can also be run manually against an existing tag.

## License

[MIT](LICENSE) © 2026 Lmar Oria
