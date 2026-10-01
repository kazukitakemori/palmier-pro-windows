# Premiere Clone Lab direction

This fork is the active Windows codebase for the user's personal video editor project.

## Source of truth

- Upstream Windows base: `MadeNavaneeth/palmier-pro-windows`
- Product/reference implementation: Palmier Pro GPL-era source
- Working branch for this fork: `premiere-clone-lab`
- The previous Premiere Clone Lab 0.34 WIP is frozen. Reuse pieces only when they solve a concrete gap here.

## Product goal

Build a Windows video editor for personal use that keeps as much of Palmier Pro Windows intact as practical, while moving the interaction model toward the parts of Adobe Premiere Pro the user actually needs.

Primary workflow:

1. Import iPhone-shot video, audio, and stills.
2. Edit reliably on a multi-track timeline.
3. Trim, split, ripple edit, move, snap, link audio/video, and undo/redo.
4. Preview smoothly on Windows.
5. Save/reopen projects without loss.
6. Export H.264/H.265 video suitable for YouTube, including 1920x1080 landscape and 1080x1920 vertical projects.
7. Keep Agent/MCP editing available so AI can operate the same validated editor commands as the UI.

## Engineering policy

Prefer reuse over rewrite.

- Keep the existing Electron/React/TypeScript editor shell.
- Keep `EditorController`, shared command surfaces, project schema, timeline math, Agent/MCP contracts, and tests unless a concrete defect requires change.
- Keep Rust/wgpu + FFmpeg as the Windows media/render direction.
- Do not port macOS SwiftUI/AppKit/AVFoundation/Metal code literally when the Windows implementation already covers the same responsibility.
- Compare against upstream Palmier behavior before reimplementing an editor operation.
- Make changes in small, test-backed slices.
- Avoid adding speculative features before the basic edit/preview/export path is dependable.

## Immediate validation order

1. CI is green on this fork.
2. Windows development build launches.
3. Project creation/open/save works.
4. iPhone media imports and metadata/thumbnails resolve.
5. Timeline placement and basic editing work.
6. Preview path produces real frames.
7. Export path produces a valid YouTube-compatible MP4.
8. Only after these gates: Premiere-like UI/shortcut refinements.

## Licensing and data hygiene

This project remains GPL-3.0-or-later as required by its upstream derivative status.

Never commit:
- API keys or credentials
- customer/personal data
- private video footage
- proprietary Adobe binaries/assets/code

## Build validation

GitHub Actions is enabled on this fork. The dedicated Windows smoke workflow is the first release gate for this branch.
