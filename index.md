# Apps I've built and shipped

I lead financial-crime and regulatory technology programmes in banking, and I build and ship my own iOS apps. Each app here is live on the App Store. I designed it, built it in Swift/SwiftUI with AI coding assistants, tested it and published it as the sole developer.

The source code is private. These pages explain what each app does, how it works and the engineering decisions behind it, without exposing keys, infrastructure details or user data.

| App | What it is | Highlights | Page |
|---|---|---|---|
| **KidDrop: Kids Days Out** | Find family-friendly places and events nearby | Multi-source data integration, a serverless events API, on-device AI summaries, maps, widgets | [Read more](kiddrop.md) |
| **Kidooks: Bedtime Stories** | Ten animated, interactive picture books | On-device neural text-to-speech, an animation engine, Live Activities, privacy by design | [Read more](kidooks.md) |
| **Lucarne: Painted Wallpapers** | A new AI-painted wallpaper scene every day | An open-licence AI image pipeline with provenance, on-device solar calculations, Shortcuts | [Read more](lucarne.md) |

**App Store developer page:** [Badrinath G](https://apps.apple.com/ie/developer/badrinath-g/id6790133758)
**LinkedIn:** [linkedin.com/in/badrinathgovindan](https://www.linkedin.com/in/badrinathgovindan)

## How I build

1. **Spec first.** A written build spec and design direction for each release, with clear "done" criteria.
2. **AI-assisted implementation, human-owned decisions.** I use AI coding assistants to write and refactor code. I decide the architecture, review the output, and check licences and privacy.
3. **Command-line builds and automated tests.** `xcodebuild` is the source of truth. Unit tests cover the logic that is easy to get wrong, such as solar maths, event filtering and data persistence.
4. **Handover-quality documentation.** Every app has an engineering handover, an architecture overview and a list of known pitfalls, so someone else could pick it up.
5. **Privacy by default.** No ads, no tracking, and no server that holds personal data in any of the three apps.

## Common stack

Swift · SwiftUI (iOS 26, Liquid Glass) · MapKit · CoreLocation · WeatherKit · EventKit · WidgetKit · App Intents · ActivityKit · Apple Foundation Models (on-device LLM) · ONNX Runtime · Cloudflare Workers + KV · Python tooling · XcodeGen · XCTest / Swift Testing
