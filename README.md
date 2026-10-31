# PagePerfect — Free Document Scanner

A free, ad-free document scanner for Android.
Auto crop · auto lighting · both-side scan · exact A4 PDF · ID card mode ·
folders · tags · search · trash · self-updating.

**No ads. No subscription. No account. No tracking.**

---

## Download

**[→ Get the latest APK](https://github.com/hypergrx7-droid/PAGE-PERFETT/releases/latest/download/app-release.apk)**

One file, every phone. `app-release.apk`, 42.6 MB, Android 7.0 (API 24)+,
64-bit and 32-bit ARM.

Install: tap the download → Android asks to allow "Install unknown apps" → allow → Install.
You only do this once; after that the app updates itself.

---

## Updating

Every build carries a version code. On launch the app fetches a tiny
[`version.json`](https://hypergrx7-droid.github.io/PAGE-PERFETT/version.json) from the
download site. If a newer build exists it:

1. replaces the whole UI with an update screen (no "later" button — everybody stays current),
2. downloads the new APK into its own cache,
3. hands it to Android's package installer.

Your documents, folders, tags and notes are untouched. If the check cannot be made
(no connection, server down) the app opens normally — an offline scanner must never
be blocked by a network call.

This is why the app now declares `INTERNET`. It is used for exactly two things: that
version file, and the APK download. Nothing about you or your documents is transmitted.

---

## Why this exists

Most scanner apps put the basics behind a subscription: watermark-free export, page limits,
duplex scanning, ID card sheets. This one doesn't. There is no paid tier, so there is nothing
to hold back.

---

## What v1.3 does

### Scanning
- Camera preview with a framing guide, grid, torch and tap-to-focus
- Automatic edge detection right after capture (Otsu threshold → largest bright
  region → extreme-point quad → convexity check)
- Perspective correction, so a photo taken at an angle becomes a flat page
- Manual 8-handle crop (4 corners + 4 edge midpoints) when detection guesses wrong
- Rotate in 90° steps while cropping
- Import existing photos from the gallery

### Enhancement
- **Auto** — removes shadows and uneven lighting, stretches contrast, unsharp mask
- **Magic** — grey-world white balance + contrast + slight saturation boost
- **B&W** — adaptive threshold (local mean), print-ready text
- **Grey**, **Lighten**, **Original**
- Live before/after toggle in the crop screen

### Multi-page & duplex
- Unlimited pages per document
- **Auto-flip mode** — scan a front, get a flip prompt, scan the back, auto-paired
- **Batch mode** — scan every front, flip the whole stack, scan every back; the app
  reverses the back order and pairs F1↔B1, F2↔B2 automatically
- Reorder pages by drag, rotate, re-crop, change filter, delete

### Reviewing a scan
- Every page of a document in one list, in order, drag to reorder
- **Six actions at the bottom, same as the reference scanner:**
  **Back** · **Edit** · **Edit all** · **Open PDF** · **Share** · **Save**
- **Edit** re-crops the selected page; tap a page to select it
- **Edit all** applies one filter — and optionally a 90° turn — to every page at once
- **Open PDF** builds the PDF and hands it to your viewer
- **Share** sends the PDF to WhatsApp, Gmail, Drive, anything
- **Save** writes it to `Download/PagePerfect/` on the phone itself

### Output
- **True A4** PDF: the page box is exactly 595.28 × 841.89 pt (also A5, Letter, Legal)
- Fit / Fill / Stretch page fitting, 0–15 mm margins
- Optional page numbers
- PDF is written on the device, then handed to any app via Share or Open
- Per-page JPEG export

### Organising
- **Folders** — create, rename and delete; a document belongs to one folder or none
- **Tags** — free-form labels, reuse suggestions from tags you already use
- **Favourites** — one tap to star, one filter to see only those
- **Search** — matches document name, note text and tags as you type
- **Notes** — a short note per document, shown on its card
- **Trash** — deleting is undoable; restore or empty the trash explicitly
- Combine filters freely: folder + tag + search word at the same time

### ID cards
- Scan the front, scan the back, both land on one A4 sheet
- Cards are drawn at ID-1 size (85.6 × 54 mm) — the same footprint as Aadhaar, PAN,
  driving licence, voter ID and most credit cards — with thin cut guides

### Reading
- Page reader with pinch zoom and page navigation
- One tap opens the exported PDF in whichever viewer you already have

### Staying up to date
- The app checks one small `version.json` at launch
- If a newer build exists, the whole UI is replaced by an update screen — no
  "later" button, so nobody is left on an old build
- The APK downloads inside the app with a progress bar, then Android's own
  installer takes over. Documents are kept.
- Offline or server down? The app opens normally. A network check must never
  block a scanner.

---

## Not in v1.3 (deliberately)

- **No OCR.** This is a scanner, not a text extractor.
- No cloud sync, no accounts, no analytics — by design, not as a limitation.
- No app lock or encrypted vault yet.
- No password-protected PDF output yet.
- No real-time edge overlay on the live preview (detection runs on the captured frame).

These are the honest boundaries. See the roadmap below.

### Roadmap
1. Real-time preview detection (native OpenCV / C++ port of the OSS-DocumentScanner engine)
2. Blank-side detection and skipping
3. PDF password protection, compression quality, watermark and header/footer
4. Book scan mode, passport photo sheet, signature placement
5. App lock and an encrypted vault

---

## Privacy

Documents never leave the device. There is no cloud, no sync, no backup service, no
analytics SDK, no crash-reporting SDK, no advertising SDK and no account system.
Scans live in the app's private storage.

The app declares `INTERNET` for exactly one purpose: checking
[`version.json`](https://hypergrx7-droid.github.io/PAGE-PERFETT/version.json) on the
download site and, when a newer build exists, downloading its APK. That request carries
no identifier, no file name and nothing about your documents.

`REQUEST_INSTALL_PACKAGES` lets the app hand a downloaded update to Android's own
installer.

See [docs/privacy.html](docs/privacy.html).

---

## Building it yourself

### Requirements
- Flutter stable (3.24+)
- JDK 17
- Android SDK with platform 35 + build-tools 35.0.0

### Local build

```bash
cd app
flutter pub get
flutter build apk --release --target-platform android-arm,android-arm64
# output: build/app/outputs/flutter-apk/app-release.apk
```

One APK for every phone. Run `flutter clean` first if you have ever built with
`--split-per-abi`: stale intermediates would otherwise pull x86_64 libraries into
the universal file.

The build is only usable for updates if it is signed with the release key in
`android/key.properties`. Without it Gradle falls back to the debug key, which
Android refuses to install over a release install.

### Free cloud build (no local setup)

Push to `main` — GitHub Actions builds the APK for free and uploads it as an artifact.
Push a tag like `v1.0.0` and it publishes a Release automatically.

```bash
git tag v1.0.0
git push origin v1.0.0
```

Workflow: [.github/workflows/build-apk.yml](.github/workflows/build-apk.yml)

---

## Repositories

Source and distribution are deliberately split, because GitHub Pages from a
**private** repo needs a paid plan:

| Repo | Visibility | Contains |
|---|---|---|
| [`PAGE-PERFETT-source`](https://github.com/hypergrx7-droid/PAGE-PERFETT-source) | **private** | this project — all source, tests, build scripts |
| [`PAGE-PERFETT`](https://github.com/hypergrx7-droid/PAGE-PERFETT) | **public** | only `README.md`, `docs/` and the release APKs |

Public site: <https://hypergrx7-droid.github.io/PAGE-PERFETT/>

The public repo is a generated artifact. Do not develop in it — rebuild and
republish from here.

---

## Publishing a release

Everything is automated by one script:

```powershell
powershell -File setup\release.ps1 -Version 1.2.1
```

It sets `version: 1.2.1+10201` in `pubspec.yaml` (version code = `major*10000 +
minor*100 + patch`, always increasing), does a clean build of the **single**
universal APK, runs `verify-apk.ps1`, creates the release on the **public** repo,
uploads `app-release.apk`, and finally writes `docs/version.json` there. That file
is what makes every installed copy offer the update.

`verify-apk.ps1` refuses to publish if:

- there is more than one APK in `dist/` (users must never choose a file),
- the package id drifts from `com.pageperfect.app`,
- the APK is signed with the debug key (an update could never install over it),
- `v2`/`v3` signing is missing,
- any camera-audio, contacts, location, advertising or billing permission appears.

Signing uses `app/android/key.properties` and
`app/android/app/pageperfect-release.jks`. **Both must be preserved forever** —
losing them means future builds can no longer install over an existing install.
They live in the private source repo.

### Updating the website

`docs/` here is the source of truth (except `version.json`, which the release
script writes). After editing, copy it across:

```powershell
$tmp = "$env:TEMP\pp_public"
git clone https://github.com/hypergrx7-droid/PAGE-PERFETT.git $tmp
Copy-Item docs\* $tmp\docs\ -Force
git -C $tmp add -A
git -C $tmp commit -m "Update site"
git -C $tmp push
```

### Free hosting

| Piece | Service | Cost |
|---|---|---|
| APK distribution | GitHub Releases (public repo) | Free |
| Landing page | GitHub Pages (`/docs`) | Free |
| Privacy policy | GitHub Pages (`/docs/privacy.html`) | Free |
| Update manifest | GitHub Pages (`/docs/version.json`) | Free |
| CI builds | GitHub Actions | Free |
| Backend | none | Free |

---

## Project layout

```
.
├── app/                          Flutter application
│   ├── lib/
│   │   ├── core/                 theme, constants, paper sizes
│   │   ├── models/               Document, PageItem, Folder
│   │   ├── services/             storage, pdf, image, detection, id cards,
│   │   │                         update (the only network code)
│   │   ├── screens/              home, camera, crop, pages, export, reader,
│   │   │                         trash, update gate
│   │   └── widgets/              8-handle crop editor
│   ├── test/                     unit tests for the pipeline, models, updater
│   └── android/
│       ├── key.properties        release key config   (private repo only)
│       └── app/
│           └── pageperfect-release.jks
├── docs/                         free static site (GitHub Pages)
│   ├── index.html
│   ├── privacy.html
│   └── version.json              written by release.ps1 on every release
├── setup/
│   ├── install-toolchain.ps1     one-shot Windows toolchain installer
│   ├── bootstrap.ps1             create project, add deps, patch manifest
│   ├── verify-apk.ps1            single APK + signing + permission gate
│   ├── release.ps1               build, verify, upload, publish version.json
│   └── make-icon.ps1             draw the launcher icon at all densities
├── .github/workflows/
│   └── build-apk.yml             free APK builds
├── THIRD_PARTY_LICENSES.md
└── LICENSE
```

---

## How the pipeline works

```
camera JPEG
   ↓  bake EXIF orientation, cap at 3000 px          (CapturePipeline.normalize)
stored original
   ↓  downscale to 1200 → Otsu → largest blob → quad (DetectorService)
4 corners
   ↓  homography (8×8 solve, bilinear resample)      (ImageService._warp)
flat page
   ↓  rotation → filter → JPEG 92                    (ImageService._applyFilter)
stored page
   ↓  one PDF page per image, exact paper box        (PdfService)
A4 PDF
```

All of it runs in background isolates on the phone. No image, page or PDF ever
touches the network — the only network code in the project is
`lib/services/update_service.dart`, which fetches a version number and an APK.

---

## Credits

The scan engine is a clean-room Dart port of ideas and code from these permissively
licensed projects:

- **[OSS-DocumentScanner](https://github.com/ossappscollective/OSS-DocumentScanner)** (MIT) — multi-pass document detection, shadow removal, colour simplification
- **[Kuama android-document-scanner](https://github.com/Kuama-IT/android-document-scanner)** (MIT) — camera preview + crop flow pattern
- **[DocSkanner](https://github.com/mars885/doc-skanner)** (Apache-2.0) — 8-handle crop UI, adaptive threshold tuning

Full notices in [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md).

---

## Licence

MIT — see [LICENSE](LICENSE). Do whatever you want with it.
