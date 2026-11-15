# Kidooks: Bedtime Stories

**Ten original animated picture books for ages 2 to 8, that children can join in with, and that work fully offline.**

[App Store](https://apps.apple.com/ie/app/kidooks-bedtime-stories/id6829489694) · Current version 1.2 (7 Nov 2026) · iPhone (optimised for iPhone Duo) · [← All apps](index.md)

## What it does

- **Ten original stories**, written and animated for the app: Pip the Lamplighter Snail, Nimbus Sneezes Rainbows, Tilly's Teashop Under the Sea, The Sock Monsters Under the Bed, The Cardboard Rocket, The Whispering Mango Tree, Bumble Lost Her Buzz, The Giggle Express, Kiko in the Snow Globe and Lumi the Lantern Fish.
- **Interactive moments:** pop bubbles, hum along, shake the snow globe, count the stars. A hidden "Moon Buddy" appears in every story.
- **"Read to me":** a natural-sounding story voice that runs **entirely on the device**, with words highlighted as they're read, at a speed the parent chooses.
- **Read it in your own voice:** a parent can record any page so the child can still hear them when they're away.
- **Sticker books and personalisation:** each child's name appears in the stories, and finishing a story earns a sticker.
- **Bedtime routine:** choose how many stories tonight; Kidooks reads them in a row, then dims to a calm goodnight screen. Bedtime reminders and a Live Activity show what's being read.
- **iPhone Duo:** open the phone like a book, with page turns and covers that open. "Child view" shows only the moving picture while the parent keeps the words.

## How it works

| Layer | Approach |
|---|---|
| Story engine | Each story is a **scene** (what's drawn) plus a **director** (when things happen and how they move). The two are kept separate so new stories reuse the same engine. |
| Rendering | SwiftUI and Core Graphics, with page-curl book interactions, haptics and motion (shake) input |
| Text-to-speech | **sherpa-onnx** (Apache-2.0) running the **Kokoro-82M** neural voice model (int8) through ONNX Runtime on the device. No audio or text leaves the phone. |
| Voice delivery | The voice pack (about 148 MB) is downloaded on demand when first needed, keeping the App Store download small |
| Recording | The parent's own narration is recorded and stored on the device |
| System features | ActivityKit Live Activity ("now reading"), local notifications for bedtime reminders |
| Safety | A parent gate protects settings and recordings and locks again after the parent steps away |
| Tests | Swift Testing across the engine, scenes and views |

### Choosing the voice engine: licence and safety checks

Before adding text-to-speech, I wrote an engine decision record covering:

- **Licence check:** confirmed the engine version is free of GPL components. The GPL phoneme data was removed from the build, and no GPL symbols remain in the compiled libraries.
- **Model integrity:** checked the model file's hash against the published fixed version. Test runs produced no invalid (NaN) audio samples.
- **Size budget:** measured the effect on app size and download size, and moved the large voice data to on-demand delivery.

## Privacy

No ads, no in-app purchases, no accounts and no data collected. Everything, including the AI voice, runs on the device and works on a plane or in a tent.

## Engineering notes

- 136 commits; about 41,000 lines of Swift, including tests.
- Releases 1.0, 1.1 and 1.2. Version 1.2 added the app tour, the on-device story voice and iPhone Duo two-pane layouts.
- Launch kit, App Store assets and the public [support and privacy site](https://github.com/Badrinith/kidooks) are maintained alongside the app.

*Source code is private. This page describes the design without exposing keys or internal details.*
