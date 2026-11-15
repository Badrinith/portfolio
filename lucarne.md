# Lucarne: Painted Wallpapers

**A new painted scene every morning for your Lock and Home screens, made with an open-licence AI image model and labelled as AI-assisted.**

[App Store](https://apps.apple.com/ie/app/lucarne-painted-wallpapers/id6831792769) · Launched 7 Nov 2026 · iPhone (designed for iPhone Duo) · [← All apps](index.md)

## What it does

- **Two screens, one scene:** on iPhone Duo, the outer screen shows a glimpse of today's scene. Unfold the phone and the "window" widens with the hinge until the whole painting fills the inner screen.
- **Preview before setting:** a full-screen preview on the Lock and Home screens, in light and dark. One tap sets it through a Shortcut, or you can save to Photos.
- **Growing library:** new scenes download in the background with no app update needed. Includes favourites, style filters and a featured scene each week.
- **Sun Sync:** the same scene at dawn, day, dusk and night, timed to your own sunrise and sunset. The calculation happens on the phone and your location is never uploaded.
- **The Atlas:** a real moment from history on today's date, with links to sources.
- **Widgets:** today's scene, and the next change of light.

## How it works

| Layer | Approach |
|---|---|
| UI | SwiftUI on iOS 26 with Liquid Glass. Layouts adapt to the folded and unfolded postures, and controls stay clear of the fold. |
| Unfold reveal | An animated "keyhole" reveal with fold shading and haptics. With Reduce Motion on, it becomes a simple fade. |
| Sun Sync | Sunrise and sunset worked out **on the device** with NOAA solar equations, covered by unit tests; produces a dawn, day, dusk and night schedule |
| Catalogue | Scenes are synced from a remote catalogue, so new art arrives without an app release (sync logic is unit-tested) |
| Shortcuts | An App Intents action, "Get Lucarne Wallpaper" (choose screen, scene and light/dark), used with the iOS wallpaper action |
| Widgets & notifications | WidgetKit (Home and Lock Screen) through an App Group; at most one local notification a day |
| Photos | Add-only Photos permission when saving |
| Project | XcodeGen project file, a one-command setup script, and an App Store listing checker script |

### Responsible AI art pipeline

- **Open-licence model:** scenes are made with **FLUX.2 [klein] 4B** (Apache-2.0). It can run locally on Apple Silicon at no cost, or in small batches within a free cloud allowance.
- **Briefs to scenes:** a JSON brief file lists the scenes to make, rotating through four house styles (Windward, Haze Valley, Atelier Study, Dotlight). It uses invented places, not copies of real artworks.
- **Provenance log:** each generated scene is recorded with how it was made, and a contact sheet supports human review.
- **Originality audit:** documented checks that scenes don't imitate existing works.
- **Transparent labelling:** every scene is credited "Lucarne · AI-assisted", and the AI-written descriptions and back stories are labelled as AI-written.

## Privacy

No account, no ads, no tracking and no data collected. A privacy manifest ships with the app and the widget.

## Engineering notes

- About 5,400 lines of Swift across the app, widgets and tests.
- Unit tests for the solar calculations and the catalogue sync.
- Documentation covers the design for Liquid Glass and iPhone Duo, building the Shortcuts, the App Store listing and the originality audit.

*Source code is private. This page describes the design without exposing keys or internal details.*
