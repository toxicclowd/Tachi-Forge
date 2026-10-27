# Tachi-Forge
A drawing and painting application specifically designed for Drawing Manga. Built for my daughter, Raylynn for her birthday.

Happy Birthday Raylynn, I know you said you were done with drawing on your phone, but this app was already built at the time, I hope you like it anyway.

This application is a full featured, professional grade drawing/painting application, it is designed specifically for drawing Manga and i built it just for you.

You WILL find it a bit complicated, there are a lot of features, many you won't use at first. The good news is that since i built it, i can change it. I can add new features that you ask for, i can re-arrange the user interface to put tools exactly where you want them or hide tools that are getting in your way, just tell me what you need and I'll make it happen. 

Here is an exhaustive feature list of everything the app can do and an installation guide, keep in mind there are both PC and Android versions, both are identical in features. I will help you with installing if you have trouble.

# Tachi Forge — Features and Installation Guide

**Current distribution: 1.0.0, built October 26, 2026.** Tachi Forge is a drawing and manga-production application for Windows and Android. It supports inking, painting, editable vector ink, panels, screentones, lettering, 3D drawing references and multi-page chapters. Normal drawing works locally without an account. Shared editing uses an external folder-sync tool.

This guide describes the implemented application. Hardware-dependent capabilities and unfinished features are identified below; the original planning documents include features that are not yet available.

## Contents

- [Download files and requirements](#download-files-and-requirements)
- [Install on Windows](#install-on-windows)
- [Install on Android](#install-on-android)
- [Move from the development phone app to the release APK](#move-from-the-development-phone-app-to-the-release-apk)
- [First launch and a first page](#first-launch-and-a-first-page)
- [Complete feature list](#complete-feature-list)
- [Import and export reference](#import-and-export-reference)
- [Default keyboard shortcuts and gestures](#default-keyboard-shortcuts-and-gestures)
- [Current limitations](#current-limitations)
- [Troubleshooting](#troubleshooting)
- [Backups, updates and uninstalling](#backups-updates-and-uninstalling)
- [Publisher and package notes](#publisher-and-package-notes)

## Download files and requirements

| | Windows desktop | Android phone/tablet |
| --- | --- | --- |
| File | [Tachi-Forge-1.0.0-Windows-x64-Setup.msi](artifacts/distribution/1.0.0/Tachi-Forge-1.0.0-Windows-x64-Setup.msi) | [Tachi-Forge-1.0.0-Android.apk](artifacts/distribution/1.0.0/Tachi-Forge-1.0.0-Android.apk) |
| Download size | About 73 MiB | About 68 MiB |
| Processor | Intel/AMD x64 | ARM64 or ARM32; both are in the one APK |
| Operating system | Windows 11 is the tested desktop platform | Android 10/API 29 or newer |
| Extra runtime | None to install: .NET is included | None to install: runtime is included |
| Installation access | Administrator permission for the per-machine MSI | Permission for the browser/file manager to install this APK |

The desktop package is not a 32-bit Windows installer or a native Windows ARM build. Microsoft currently lists supported .NET 10 configurations for Windows 11 and selected Windows 10 LTSC/Enterprise editions; this app has not been qualified across those older configurations. Windows 7/8.1 are not supported targets. [Microsoft Windows/.NET support information](https://learn.microsoft.com/en-us/dotnet/core/install/windows).

The installed Windows payload is approximately 210 MiB. Allow additional space for the installer cache, temporary files, drawings, recovery copies and undo storage. Android also needs space beyond the APK itself. A formal minimum RAM/GPU specification has not been established: large canvases, high DPI, many layers and large textured brushes increase memory and processing costs.

These are standalone distribution files, not Microsoft Store or Google Play installations. The Android file is a single APK: no split-APK installer, Android Studio or USB debugging is normally required.

## Install on Windows

1. Download or copy `Tachi-Forge-1.0.0-Windows-x64-Setup.msi` to the computer.
2. Save your drawings and close any running copy of Tachi Forge.
3. Double-click the MSI.
4. Review Windows' publisher/security prompt. This build has a **self-signed Pixonix Studios certificate**, so Windows does not automatically trust its publisher. If SmartScreen presents **More info → Run anyway**, proceed only for the package you intended to obtain from the publisher. Managed computers may not offer an override. No system-wide security setting needs to be disabled. [Microsoft explains self-signed app warnings](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/smartscreen-reputation).
5. Approve the administrator prompt if you want to install it, then let installation finish.
6. Open **Start**, search for **Tachi Forge**, and launch it.

The normal install directory is `C:\Program Files\Tachi Forge`. A Start Menu shortcut is included; a desktop application shortcut is not required. You do not need to install the .NET SDK or a separate .NET runtime. Open drawings from **File → Open…** inside the app; do not rely on a Windows `.tachi` file association.

**For the owner of this workspace:** the automatic copy of the two packages to Desktop was blocked by the coding session's filesystem permissions. The built files remain in `artifacts/distribution/1.0.0`. To copy them to Desktop, run this in a regular PowerShell window outside that restricted session:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File "C:\Users\Administrator\source\repos\Tachi Forge\tools\Distribution\Copy-ToDesktop.ps1"
```

## Install on Android

For a device without the development/debug build already installed:

1. Download or transfer `Tachi-Forge-1.0.0-Android.apk` to the device, for example into **Downloads**.
2. Open it using the device's Files app, file manager or download notification.
3. If Android asks about this installation source, open **Settings** from that prompt and enable **Allow from this source** for that specific file manager/browser.
4. Return to the APK and tap **Install**.
5. Tap **Open**, or launch **Tachi Forge** from the app drawer.
6. When saving or opening artwork, use the system file picker to choose the file/folder you want.

The usual settings route is **Settings → Apps → Special app access → Install unknown apps**. Labels vary by manufacturer. You can turn that source permission off after installation. [Google's installation instructions](https://support.google.com/pixelphone/answer/7391672?hl=en).

Some current Android devices may show an additional **unverified developer** restriction. If that specific message appears, follow [Google's unverified-developer installation guidance](https://support.google.com/android/answer/17588095?hl=en); its advanced flow includes a 24-hour delay. That is separate from the ordinary per-source APK permission and is not a requirement to enable developer options on every device.

Android may offer notification permission for background-export status. The app uses system file pickers rather than needing unrestricted access to all your files. The current APK includes ARM64 and ARM32, not x86/x64 Android emulator binaries.

## Move from the development phone app to the release APK

**The release APK cannot update the existing debug-signed development app in place.** They share the app ID `com.pixonixstudios.tachiforge` but use different signing certificates. Android compares certificates when accepting updates. [Android signing and update rules](https://developer.android.com/studio/publish/app-signing).

Use this order if you decide to migrate:

1. Open the existing development app.
2. If it offers recovery, choose **Restore** for work you want to retain.
3. Use **File → Save As…** to save every chapter you want to keep as a `.tachi` file in a normal user-selected folder, such as Documents or Downloads. One chapter file contains its pages.
4. Verify the saved files exist. Preferably copy them to a computer or another backup location and check that they can be reopened.
5. Back up any custom presets, palettes, imported tips/papers and settings you also want to keep. These are app-local data, not automatically carried by a saved chapter. There is no complete one-click settings migration UI; arrange an app-data backup before uninstalling if those items matter.
6. Only after those backups are secure, uninstall the debug/development app.
7. Install the release APK using the Android steps above.
8. Open **File → Open…** and choose your backed-up `.tachi` chapter files.

Do not count a recovery banner or private working copy as an external backup. Android removes app-specific files when the app is uninstalled. [Android app-storage behavior](https://developer.android.com/training/data-storage/app-specific). No app removal or data migration was performed just to build these distribution files.

## First launch and a first page

1. Close the introductory **Gestures & shortcuts** sheet after reading it. Open it again with **F1** or the **⋯** menu.
2. Android may show the recent-project gallery when it has saved recent entries. Open a page there, or choose **File → New…**.
3. A new blank document defaults to **B5 JIS, 182 × 257 mm, 300 DPI, Color**: **2150 × 3035 pixels**.
4. Open the small corner arrow on the drawing-tool icon to choose **Pen** or **Paint**. Other grouped tools use the same pattern.
5. Pick a preset and adjust **Size**, **Opacity** and the appropriate tool controls in the property bar. Use **More tool settings** for the complete editor.
6. Tap the color swatch beside those settings for **Quick colors**. **More colors…** opens the full Color panel.
7. Add layers for sketch, inks and color. Mark a sketch as Draft if you want it omitted from flattened final exports.
8. Save the editable work with **File → Save As…** as `.tachi`.
9. Create a delivery copy using **File → Export…**. Exporting an image does not replace saving the editable chapter.

To explore a worked example, use **File → Open the sample page**. The sample includes layered manga-production elements and opens as an unsaved document.

## Complete feature list

### Workspace, navigation and controls

- Adaptive desktop layout and collapsible phone/tablet side panels.
- Icon toolbars with labels/tooltips and accessible control names.
- Grouped popouts for drawing, fill, selection/vector, and shape/layout/reference tools; each group remembers its last selected tool.
- Tool property bar with frequently used settings; it wraps on narrow screens.
- Tap a numeric property chip to open a larger control, or drag horizontally across it to adjust the value.
- Full settings popup and side panel stay synchronized; advanced settings have sliders and numeric entry fields.
- Reserved scrollbar space and touch-aware brush sliders: vertical gestures scroll, while taps/horizontal drags edit values.
- Light, dark and system themes.
- Left-handed layout, moving tools to the right and panels to the left.
- Remembered open panel sections and wide-layout panel visibility.
- Pan, cursor-centered zoom, canvas rotation and horizontal view flip.
- Fit-page, 100% pixel view, print-size view and reset rotation.
- Navigator thumbnail with a view outline; tap or drag it to move around the page.
- Paper visibility and transparency checkerboard.
- Touch-friendly quick-action bar with selectable buttons.

**View flip is a viewing aid.** Use transform's flip controls when you want to change the artwork itself.

### Documents and paper settings

- Native editable `.tachi` documents and multi-page chapters.
- Existing single-page `.tachi` files open as one-page chapters.
- New, Open, Save, Save As, recent files and thumbnail gallery.
- First layer can be Color, Gray or Mono.
- Eighteen paper presets, listed below.
- DPI choices: **72, 96, 150, 200, 300, 350, 400, 600 and 1200**.
- Pixel-size preview before creating the page, with memory-related size warnings where available.
- Print guides for templates that include trim, bleed and safe areas.
- Opening a supported image as a new document uses the image's pixel dimensions; importing it as a layer keeps the current page dimensions.

| Preset family | Available choices |
| --- | --- |
| Manga/manuscript | B4 manuscript, 257 × 364 mm |
| Finished-size templates with bleed | B5 comic, A5 doujinshi, A4, B6 manga, A6 pocket, A3 |
| Plain ISO A sheets | A2, A3, A4, A5, A6 |
| Plain JIS B sheets | B5, B6 |
| US sheets | Letter, Legal, Tabloid |
| Other | Square, 210 × 210 mm |

**B5 JIS and B5 comic are different choices.** The default plain B5 sheet is exactly 182 × 257 mm, without added bleed. B5 comic is 188 × 263 mm overall, giving a 182 × 257 mm finished page plus 3 mm bleed on each edge. Choose the bleed template for artwork extending to a trimmed print edge.

Image-as-new-page import currently assigns 600 DPI to images at least 4000 pixels on their longest side and 350 DPI to smaller images. It does not use the blank-document 300-DPI default; importing into an existing page avoids changing that page's settings.

### Inking, painting and erasing

- Pen and Paint modes remember separate brushes; custom painting presets are accessible from both.
- Brush size, stroke opacity, flow, hardness, dab spacing and anti-aliasing controls.
- Anti-aliasing choices: Off, Weak and Strong.
- Smooth stabilization and Lazy rope stabilization, with adjustable strength.
- Real pressure, synthetic pressure from stroke speed, Auto pressure selection and pressure disabled.
- Per-brush pressure-response curve and a separate device pressure-response curve.
- Pressure effects on size/opacity, minimum diameter, entry/exit tapering and sharp pen ends.
- Pen tilt response when the device reports tilt.
- Actual-size brush cursor for mouse/pen hover.
- Hard and soft erasers, pen eraser-tip support when available, and **Clear** color to erase with a brush's own shape.
- Ordinary stroke coverage avoids repeatedly darkening its own overlapping dabs; build-up/flow permits deliberate accumulation.
- Wet edges, paper grain, color pickup, wet mixing, blending and smudging on supported raster layers.
- Live brush-stroke preview.
- Save named custom presets; change/delete your own presets while retaining built-ins.

**Twenty built-in presets:**

| Group | Presets |
| --- | --- |
| Inking/drawing | G-Pen, Maru-Pen, Pencil, Marker, Airbrush |
| Painting | Watercolor, Watercolor wash, Gouache / tempera, Bristle (oil), Pastel, Chalk, Charcoal, Sponge, Splatter, Watercolor wet-on-wet, Oil (wet), Blender, Smudge |
| Erasing | Eraser (hard), Soft eraser |

### Advanced brush editor

These are Photoshop-style categories in Tachi Forge's own brush engine, not Photoshop preset-file compatibility.

| Category | Available controls |
| --- | --- |
| Brush Tip Shape | Tip image, tip import, hardness, spacing up to 500%, fixed angle |
| Shape Dynamics | Size jitter/minimum diameter; fixed, stroke-direction, random and initial-direction rotation; angle jitter/modulation; roundness, roundness jitter/minimum; fixed and random X/Y flips |
| Scattering | Scatter up to 1000%, perpendicular/both axes, count from 1–16 dabs, count jitter and scatter control |
| Texture | Paper image/import, depth, scale, brightness, contrast, inversion, depth jitter/minimum, page or per-tip anchoring; Height, Multiply and Subtract modes |
| Dual Brush | A second tip mask, relative size and angle, cutting texture into the primary dab |
| Color Dynamics | Main/sub-color blending jitter, hue/saturation/brightness jitter, purity, per-tip or per-stroke color variation |
| Transfer | Opacity/flow variation, minimums, pressure/tilt/fade controls and build-up |
| Painting Effects | Wet edge, mix with the layer, color pickup, tilt response, noise and entry/exit tapers |

Parameters that expose a control source can use Off, Pen pressure, Pen tilt or Fade. Fade length is measured in stamp positions. Real tilt requires supporting hardware; Auto pressure can use a synthetic response when real pressure is unavailable.

**Flow versus opacity:** flow controls how much each dab contributes; opacity caps the completed stroke. Lowering spacing places more dabs along the same distance.

### Custom tips and paper textures

- Eighteen bundled tips and four bundled paper textures, with thumbnail pickers.
- Import custom tips/papers from PNG, JPEG or WebP images.
- Import GIMP `.gbr` brushes and `.gih` multi-image pipes; up to 16 pipe images can be used as successive dabs.
- Imported tips are fitted to a maximum 256-pixel size; papers to 512 pixels.
- Imported assets appear as your own entries and can be deleted.
- User assets live on that device. A preset referencing a missing asset falls back to a round tip or smooth paper.

### Color controls

- HSV color wheel: hue ring with saturation/value square.
- Main and sub colors, swap, and hexadecimal entry.
- Recent colors used while drawing/filling, saved between sessions.
- Multiple named palettes: create, rename, select, delete, add/remove colors.
- Quick palette beside Pen/Paint settings: eight recent colors, up to 18 colors from the selected palette, and main/sub swap.
- **More colors…** opens the full Color panel.
- Eyedropper sampling from the composited page; temporary picker through Alt with Pen/Fill and a one-shot quick-bar picker.
- Selecting a drawing color leaves Clear/transparent-brush mode.

The eyedropper currently samples the composited page, not an optional active-layer-only mode. Separate RGB/HSV channel sliders are not implemented.

### Layers and masks

- Color, Gray and Mono raster layers; convert between those storage/color types.
- Mono ink coverage with a configurable ink color.
- Nested folders, collapse/expand, grouping/ungrouping and moving layers into/out of folders.
- Mouse drag or touch-hold-and-drag reordering; move-up/down actions.
- Layer names, visibility, opacity, full lock and lock-transparent-pixels.
- Clip to the layer below.
- Normal, Multiply, Screen, Overlay and Add blend modes; Pass-through for folders.
- Layer masks: edit, enable/disable, apply and delete. In the mask workflow, painting hides and erasing reveals.
- Reference flags for fill/selection boundaries and Draft flags for working material.
- Duplicate, merge down and flatten visible layers.
- Undo/redo for layer operations and property changes.
- Generated content such as frames, tones, line effects, text and 3D references can retain editable parameters until rasterized.

### Selections and transforms

- Rectangular, elliptical, freehand-lasso and polygon-lasso selections.
- New, Add, Subtract and Intersect combination modes.
- Select all, deselect, invert, clear and fill selection.
- Selection-aware strokes, fills, mask painting, shapes and gradients.
- Marching-ants outlines and undoable selection changes.
- Magic wand by color or inside line art, with reference choice, tolerance/gap handling and expansion as appropriate.
- Transform a selection, full layer or mask: move, resize/stretch, rotate, skew/distort and flip horizontally/vertically.
- Live transform preview, touch-sized handles, and resampling when the edit is applied.
- Apply or cancel the transform. Saving/exporting applies a pending transform first.

### Fill, shape and gradient tools

- Tap-to-fill with gap closing, line-opacity threshold and expansion under outlines.
- Boundary sources: this layer, visible layers or marked reference layers; hidden layers do not become boundaries.
- Lasso fill: draw an enclosed freehand area and release to fill it.
- Line, rectangle, ellipse, regular polygon and star shapes.
- Polygon/star choices from 3–16 sides/points.
- Filled or brush-width outlined shapes, live preview and constrained drawing with Shift.
- Shapes can erase using Clear color or the applicable erase modifier.
- Linear and radial gradients, from main color to transparency or main color to sub color.
- Dithered gradients to reduce banding; gradients on tone layers become changing tone density.

### Manga panels, tones and rulers

- Frame borders, adjustable row/column gutters, panel splitting and panel clipping masks.
- Frame layout follows the safe area when the template provides print guides.
- Screentones as editable layer settings, including selection-to-tone creation.
- Tone density, 20–150 LPI, angle, and round/square/line/grain patterns.
- Zoom-aware tone preview: at small zoom levels a gray preview replaces unresolved tiny dots; full-resolution outputs render the dots.
- Straight and curved rulers.
- One-, two- and three-point perspective rulers, editable vanishing points and guides.
- Concentric circle/ellipse rulers with roundness/orientation controls.
- Mirror and rotational symmetry, up to 24 generated strokes.
- Toggle ruler snapping, temporarily bypass it, and edit ruler handles.
- Editable radial focus lines and parallel speed lines: count, thickness, extent, direction and controlled variation; regenerate a pattern or rasterize it.

**DPI** is the document's pixel resolution for its physical size. **LPI** is the frequency of the printed tone pattern. They are separate settings.

### Vector ink

- Vector ink layers store editable stroke paths and width/opacity information.
- Draw with the pen engine, then edit points or pull/smooth the line locally.
- Thicken or thin existing ink with a width-editing brush.
- Vector eraser choices: touched part, whole stroke, or the section between intersections.
- Undo/redo of vector edits, with vector data saved in `.tachi`.
- Rasterize a vector layer for pixel painting and other raster-only tools.

Textured painting brushes use a simplified round form on vector ink. Keep a native `.tachi` master when you need editable vector paths; PSD/image export does not preserve those native paths as Tachi Forge vector objects.

### Text and speech balloons

- Basic horizontal lettering, explicit line breaks and automatic wrapping inside balloons.
- Bundled Comic Neue regular and bold font choices.
- Font size, line spacing and border width.
- Text-only, speech/ellipse, rounded-box and burst balloon styles.
- Place/move balloons, drag/remove a tail, and keep text/settings editable.
- Android on-screen keyboard entry.
- Rasterize lettering/balloons for direct pixel editing.

Vertical Japanese lettering and a full professional typesetting system are not included.

### 3D drawing references

- Editable 3D reference scene stored in the native document.
- Mannequins with 22 body joints; wrist/ankle inverse-kinematics posing, body movement, bone twisting and turning.
- Articulated hands with thumb/finger controls and six hand shapes: Relaxed, Open, Fist, Pointing, Peace sign and Gripping.
- Apply hand shapes to either or both hands; reset a body pose.
- Add box, ball, cylinder and cone props.
- Move figures, props and selected joints; axis arrows constrain movement.
- Orbit/slide/zoom camera, lens, distance, perspective and size-on-page controls.
- **Look at** the selected item/hand for closer work.
- Ground grid, outlines, ambient lighting and up to four movable lights.
- Figure height and prop size/orientation/elevation controls.
- Undoable posing/movement and optional rasterization.

New reference scenes are draft material for drawing over. Whole-body pose libraries/mirroring, imported OBJ models, realistic joint limits, body-type presets and cast shadows are not implemented.

### Multi-page chapters

- Several pages in one `.tachi` file.
- Page thumbnails and facing-page/spread previews.
- Add, duplicate, delete and reorder pages; hold then drag on touch.
- Right-to-left or left-to-right reading order.
- Option to show the first page on its own before paired spreads.
- Open a page from the page view.
- Undo/redo for page-list operations; a chapter retains at least one page.
- Only the active page is fully loaded, helping memory use.
- Current-page or whole-chapter export.

New pages follow the chapter's page settings. **A page's drawing undo history is cleared when switching away and reloading it.** Chapter page-list undo is a separate operation history; save files do not provide permanent historical editing sessions.

### Folder-based collaborative editing — developing feature

- **File → Share chapter…**, **Open shared chapter…**, and **Sharing setup…**.
- Shared folders contain the chapter and per-device edit logs.
- An external utility keeps that real local folder synchronized between devices; Tachi Forge does not provide its own cloud service or account system.
- Changes are picked up after synchronization, including work done offline.
- Shared editing covers raster changes, layer changes and editable vector/scene content.
- Undo is designed to preserve other artists' contributions.

Basic workflow: synchronize a folder, share a chapter into a new empty subfolder, wait for the copy on the other device, then open it there using **Open shared chapter…**.

Organize pages before sharing: later additions/deletions/reordering are not currently merged across devices. Real two-device synchronization and Android document-provider behavior have less testing than ordinary local editing; Android may require selecting the shared folder again after restart. Treat this as a developing collaboration workflow and retain ordinary `.tachi` backups.

### Saving, recovery and performance support

- Snapshot-based background saves, allowing drawing to continue.
- Manual saving and private recovery copies are separate: autosave does not replace choosing a permanent document file.
- Recovery prompt after interruption, with Restore/Discard.
- Default autosave interval of 30 seconds; choices of 15/30 seconds and 1/2/5 minutes.
- Autosave when Android backgrounds the application, subject to completion of active edits.
- Undo/redo with automatic memory budgets or choices from 256 MiB through 4 GiB.
- Older undo data can move to compressed private disk storage.
- Automatic cache/memory management on Android.
- Background exports with progress; Android foreground-export notification/service support.
- Cancel exports before destination commit and between pages. A final destination copy already underway finishes to avoid leaving a partial provider file.
- Recent fixes protect a new document from a previous save's late completion and preserve an export destination when cancellation occurs before writing it.

### Preferences, help and diagnostics

- Custom keyboard shortcuts, conflict reassignment and reset-to-defaults.
- Tap a tool key to select it; hold supported tool keys for temporary switching.
- Select which of 12 quick-bar actions are visible: Undo, Redo, Pen/Eraser, Pick, Ruler snap, Hand, Fill, Swap colors, Deselect, Fit, Smaller and Bigger.
- Pen/finger input capability display, per-device pressure curve, side-button action and touch-contact-size settings.
- Built-in sample page and gesture/shortcut help.
- About screen and third-party notices.
- Local rolling logs and crash reports, with user-triggered sharing; no automatic crash-report upload.
- After-crash recovery options, including continuing without GPU textures.
- Technical tools in the ⋯ menu: pen test, render statistics, engine self-test, canvas benchmark, file-access test and memory test.

The memory test intentionally closes the app. Save normal work before using diagnostic tools. A pressure/tilt setting cannot add sensors that a stylus does not have: the tested Moto G stylus 5G (2024) pen reports finger-like input without real pressure/tilt, so synthetic pressure and touch-size settings are relevant there.

## Import and export reference

### Input

| Input | Supported use |
| --- | --- |
| `.tachi` | Editable single-page document or chapter; transfer between desktop and Android |
| PNG, JPEG, WebP, BMP | Open as a new image-sized page or import centered as a layer |
| PNG, JPEG, WebP | Custom brush tips and paper textures |
| GIMP `.gbr`, `.gih` | Brush-tip import, including multi-image pipes |
| Layered PSD, Photoshop `.abr` | Not supported as imports |

### Output

| Format | Layers/editability | Typical use |
| --- | --- | --- |
| `.tachi` | Native editable structures, layer data and chapter pages | Master document, backup and device transfer |
| PNG | Flattened; optional transparency in Color mode | Lossless image/web artwork |
| JPEG | Flattened with paper/background | Compact image delivery |
| TIFF | Flattened RGB/RGBA, 8-bit gray or 1-bit black/white; resolution tags | Print image delivery |
| PDF | Flattened pages in one file; physical page sizing and optional crop marks | Chapter delivery/printing |
| PSD | 8-bit RGB layered output, groups, masks, names, visibility, clipping, opacity and supported blend modes | Handoff to another art application |

PNG/JPEG/TIFF/PDF offer Color, Grayscale and Black-and-white conversion. A grayscale/black-and-white PNG/JPEG is not the same as a true one-bit TIFF file; use TIFF's Mono option for that delivery requirement. PSD's color/area selectors are disabled because this exporter writes the full layered RGB page.

- Choose **This page** or **Whole chapter**.
- Multi-page PNG/JPEG/TIFF/PSD output produces numbered files in the selected folder; PDF holds its pages in one file.
- Choose whole page, finished trim, or trim plus bleed when the document has guides. A plain template without guides exports the whole page for those area choices.
- PDF can add crop marks when guides exist; spread previews do not perform booklet imposition.
- Transparent background is available for Color PNG/TIFF.
- Android **Share…** sends exported files through the system share sheet.
- Flattened raster/PDF output omits Draft layers. **PSD preserves the layer stack, including draft/reference content**; inspect those layers before using the PSD as final artwork.
- PSD keeps layer organization, but native text, tone, vector and 3D objects are represented as their rendered pixels. PSD pages are limited to 30,000 pixels per side.
- TIFF, PDF and PSD write resolution/physical-size information. The current PNG/JPEG writer does not explicitly embed the document's print-DPI metadata; set the intended size/resolution in the receiving publishing/printing tool. The exported pixel dimensions are retained.

## Default keyboard shortcuts and gestures

These are defaults while working on the canvas. Custom assignments are reflected in the app's F1 help.

| Action | Default |
| --- | --- |
| New / Open / Save | Ctrl+N / Ctrl+O / Ctrl+S |
| Save As / Export | Ctrl+Shift+S / Ctrl+E |
| Undo | Ctrl+Z |
| Redo | Ctrl+Y or Ctrl+Shift+Z |
| Pen/brush / Eraser | B / E |
| Fill / Lasso fill | G / L |
| Eyedropper / Selection | I / M |
| Ruler / Frame / Text | U / K / T |
| Temporary Hand/pan | Hold Space and drag |
| Smaller / Larger brush | [ / ] |
| Swap main/sub colors | X |
| Select all / Deselect | Ctrl+A / Ctrl+D |
| Invert selection | Ctrl+Shift+I |
| Clear selected pixels | Delete or Backspace |
| Transform | Ctrl+T |
| Rotate view left/right | Ctrl+[ / Ctrl+] |
| Reset rotation / Flip view | R / H |
| Fit page / 100% / Print size | F / 1 / 2 |
| Side panels / Help | Tab / F1 |

| Gesture/control | Result |
| --- | --- |
| Two-finger drag / pinch / twist | Pan / zoom / rotate |
| Two-finger tap / Three-finger tap | Undo / redo |
| Touch-hold, then drag layer/page | Reorder |
| Mouse wheel | Zoom the page in the ordinary canvas workflow |
| Alt with Pen/Fill | Temporary composited-page color picking |
| Pen side button, when reported | Configurable temporary eraser/picker/nothing |
| Polygon lasso | Tap corners; close on first corner, double-click or Enter; Backspace removes a corner; Esc cancels |

In **Pen & touch**, choose touch drawing, gesture-only navigation, or small-tip drawing with larger finger contacts navigating. Palm rejection depends on recognizable pen input; passive styluses are not equivalent to active pressure pens.

## Current limitations

- Some pen hardware paths, including specific Wacom/S Pen side buttons and tilt, still need broader device validation.
- Very large brushes, high-DPI pages and many layers can be demanding, particularly on phones. Minimum-spec certification and extended soak coverage remain incomplete.
- Page drawing undo does not survive switching/reopening pages; use saved backups for lasting versions.
- Brush/palette/settings libraries and imported brush assets are local to the app/device, rather than a complete portable settings package inside every `.tachi` file.
- Wet mixing samples the active layer, not the entire visible stack, and does not remove existing paint while dragging into empty space.
- Raster-only tools require rasterizing vector/generated content before painting directly on it.
- Pass-through folders below full opacity can have a different on-canvas preview from the exact export composite.
- Ruler edits are not currently undoable.
- Full desktop floating/detachable panel docking is unfinished.
- No mesh/warp transform, multi-stop editable gradient system, rounded-corner shape rectangle control, or native shape drawing on vector ink layers.
- No layered PSD import, `.abr` import, CBZ export, CMYK/ICC-managed print workflow, vertical Japanese text, or native SVG/vector export.
- No OBJ import, complete pose library, pose mirroring, body-type system or cast-shadow rendering.
- Sharing has the page-list/sync limitations described above; it is not a built-in hosted collaboration service.
- This distribution does not include macOS, Linux, iOS/iPadOS, native Windows ARM or x86 Android packages. Android DeX/multi-window configurations are not fully qualified.
- Installation/uninstallation was not exercised system-wide during distribution packaging. Package validation included MSI database/cabinet inspection, all 230 payload hashes, launch of the extracted Windows app, and Android manifest/ABI/signature checks. These are not claims of bug-free software.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Windows says Unknown publisher or unrecognized app | Expected for this self-signed build. Verify the intended file/source. If policy blocks it, contact the computer administrator rather than changing protection globally. |
| Windows says this package is not for the processor | Use an Intel/AMD x64 Windows installation; this is not a 32-bit or native ARM installer. |
| No desktop app icon | Launch Tachi Forge from Start. The MSI includes a Start Menu shortcut. |
| Android says package conflicts/app not installed | An installed debug build with the same app ID and a different certificate is a likely cause; follow the backup-first migration instructions. Also check Android version, ARM support and free space. |
| APK source is not allowed | Grant Install unknown apps to the specific file manager/browser opening it, then retry. |
| Android shows an unverified-developer restriction | Use Google's linked guidance for that specific additional screen. |
| Stylus has no pressure/tilt | Check Pen & touch capabilities. Use Auto/Synthetic pressure for hardware without those sensors. |
| Fingers leave marks while navigating | Change the touch mode to navigation-only or adjust the small-tip threshold. |
| Cannot find a tool | Open the small corner arrow on the appropriate grouped tool icon. |
| Cannot enter an exact advanced brush value | Open More tool settings; use the numeric field beside its label. |
| Brush unexpectedly erases | Check Eraser, Clear color and mask-editing state. |
| Cannot paint on a layer | Check lock, lock transparency, selection, mask mode, vector/generated content and active transform. Rasterize when appropriate. |
| Sketch/reference missing from PNG/PDF | Check whether the layer is marked Draft or hidden. |
| PSD has a reference that the PNG omits | PSD retains the layer stack; hide/delete draft/reference layers in the receiving editor for final delivery. |
| Tone looks gray when zoomed out | Normal small-scale preview; inspect closer or examine full-resolution print output. |
| PNG/JPEG prints at an unexpected physical size | Set the intended DPI/size in the receiving print/layout application, or use TIFF/PDF for explicit print-size metadata. |
| App feels slow | Reduce brush size or high-cost mixing/texture effects; use a smaller/lower-DPI page; reduce active layers and other memory pressure. |
| Work appears missing after interruption | Choose Restore if offered, then immediately save a permanent `.tachi` copy. |

## Backups, updates and uninstalling

Save editable masters as `.tachi`. A flattened PNG/JPEG cannot restore your layers, vector paths, lettering settings or chapter structure. Keep independent copies of important chapters.

Drawings are stored wherever you choose with Save/Save As. Settings, palettes, presets, imported assets, working copies and recovery data are separate app-local files. On Windows their normal root is `%LOCALAPPDATA%\TachiForge`; close the app before making a complete app-data backup. Android private storage is not an ordinary Documents folder you can assume a file manager can copy.

For Windows updates, save and close the application, then run the new MSI. Uninstall through **Settings → Apps → Installed apps → Tachi Forge → Uninstall**. This MSI manages its installed application files, not external chapter files or the separate user-data folder.

For Android updates, use a release signed with the same release identity. Before uninstalling or clearing app storage, save chapters outside app-specific storage and arrange backups of app-local customizations. Uninstalling is not a settings-preserving migration method.

## Publisher and package notes

The Android package's application ID is `com.pixonixstudios.tachiforge`; Android currently displays version `1.0`, version code `1`. Windows MSI product version is `1.0.0`.

For the publisher, distribute the MSI, APK and this guide. Keep the signing keystore/PFX and passwords private, and retain the same Android signing identity for future updates. Builder-specific signing and backup details are in [the distribution notes](tools/Distribution/README.md).

SHA256 checksums of these exact distribution files:

```text
8EC6BC6B168F8D25898AD472C6ED784D30A68D9DF93953A06C039D36B98EE8CE  Tachi-Forge-1.0.0-Windows-x64-Setup.msi
027CF9686D6DC59FFE5E53FBB42E53E1962F483581689AB214A3710C1FB32593  Tachi-Forge-1.0.0-Android.apk
```

To inspect a downloaded file in PowerShell, run `Get-FileHash -Algorithm SHA256` followed by its path and compare the result. A checksum comparison checks that you have this build; it does not turn a self-signed certificate into a publicly trusted one.


