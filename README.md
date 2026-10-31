# PagePerfect — Free Document Scanner

A free, offline, ad-free document scanner for Android.
Auto crop · auto lighting · both-side scan · exact A4 PDF · ID card mode.

**No ads. No subscription. No account. No internet permission.**

---

## Download

**[→ Get the latest APK](https://github.com/hypergrx7-droid/PAGE-PERFETT/releases/latest)**

| File | Size | Use if |
|---|---|---|
| `app-arm64-v8a-release.apk` | 20.2 MB | **Most phones from 2017 onwards — start here** |
| `app-release.apk` | 57.5 MB | Not sure / any phone (works on every CPU type) |
| `app-armeabi-v7a-release.apk` | 18.2 MB | Older 32-bit phones |
| `app-x86_64-release.apk` | 21.7 MB | Emulators / x86 tablets |

Requires **Android 7.0 (API 24)** or newer.

### Install

1. Tap the download and wait for it to finish.
2. Open the file. Android will warn that installing from this source is blocked.
3. Tap **Settings** → enable **Allow from this source** → go back.
4. Tap **Install**.

This is normal for any app installed outside a store. You can revoke that permission right after.

---

## What it does

### Scanning
- Camera preview with framing guide, grid, torch and tap-to-focus
- Automatic edge detection right after capture
- Perspective correction — an angled photo becomes a flat page
- Manual 8-handle crop (4 corners + 4 edge midpoints) when detection guesses wrong
- Rotate in 90° steps, import photos from the gallery

### Enhancement
- **Auto** — removes shadows and uneven lighting, stretches contrast, sharpens
- **Magic** — white balance + contrast + slight saturation boost
- **B&W** — adaptive threshold, print-ready text
- **Grey**, **Lighten**, **Original**
- Before/after toggle while cropping

### Multi-page & duplex
- Unlimited pages per document
- **Auto-flip mode** — scan a front, get a flip prompt, scan the back
- **Batch mode** — scan every front, flip the whole stack, scan every back;
  the app reverses the back order and pairs F1↔B1, F2↔B2 automatically
- Reorder by drag, rotate, re-crop, change filter, delete, share a page as an image

### Output
- **True A4** PDF — the page box is exactly 595.28 × 841.89 pt (also A5, Letter, Legal)
- Fit / Fill / Stretch fitting, 0–15 mm margins, optional page numbers
- Written on the device, then handed to any app via Share or Open

### ID cards
- Scan the front, scan the back, both land on one A4 sheet
- Cards drawn at ID-1 size (85.6 × 54 mm) with cut guides

### Reading
- Page reader with pinch zoom and page navigation

---

## Privacy

The app declares **no `INTERNET` permission**. The OS blocks all network access, so
documents physically cannot leave the device.

- No analytics SDK
- No crash reporting SDK
- No advertising SDK
- No account system
- Files live in the app's private storage

See the [privacy policy](https://hypergrx7-droid.github.io/PAGE-PERFETT/privacy.html).

---

## Not in this version

- **No OCR.** This is a scanner, not a text extractor.
- No cloud sync, no accounts, no analytics.
- No folders, tags, app lock or encrypted vault.
- No password-protected PDF output.
- No live edge overlay on the preview (detection runs on the captured frame).

---

## Source code

The application source is not published in this repository — this repository only
hosts the release builds and the website.

---

## Licence

The PagePerfect application is free to download and use at no cost.
