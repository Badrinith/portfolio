# KidDrop: Kids Days Out

**Find family-friendly places and events near you, with everything a parent needs to know before going.**

[App Store](https://apps.apple.com/ie/app/kiddrop-kids-days-out/id6790133756) · Current version 1.7.0 · iPhone (optimised for iPhone Duo) · [← All apps](index.md)

## The problem

Planning a day out with children usually means checking a dozen websites: what's on, what's open, what it costs, whether it suits the children's ages and what the weather will be. KidDrop brings that together in one app.

## What it does

- **Map of kid-friendly spots:** parks, beaches, playgrounds, aquariums, museums and libraries around you. Each spot has opening hours, typical visit length, cost, contact details and today's weather.
- **What's on near you:** fairs, story times, farm days, festivals and shows in a single feed. Each listing has the date, venue, distance, price (where published) and a link to the original source.
- **Filters:** by month, price and type of outing ("something free this weekend", "something indoors because it's raining").
- **On-device AI summary** for each place.
- **Planning:** save an outing to your calendar and bookmark favourites. Home Screen and Lock Screen widgets show nearby and saved spots.
- **iPhone Duo layouts:** when unfolded, a map with a place panel alongside, a timeline of events with a live map, or a magazine view. Fold it and you carry on where you left off.

## How it works

| Layer | Approach |
|---|---|
| UI | SwiftUI tab app with a custom floating glass tab bar; shared state through a few observable stores |
| Places | Curated "parent picks", plus a live Apple Maps points-of-interest search around the user's location, and search-as-you-type suggestions |
| Classification | One typed `PlaceCategory` enum is the single source of truth for every kind of place: label, symbol, colour and a keyword classifier. A kid-friendly filter keeps out shops and other unsuitable places. |
| Weather | WeatherKit with a 15-minute in-memory cache, so moving around the map doesn't trigger repeated calls |
| Nearby amenities | Nearest public transport and toilets for each spot |
| AI | Apple's on-device Foundation Models write a short summary of each place. Nothing is sent to a cloud LLM. |
| Calendar | EventKit reads and writes the device calendar (including synced Google calendars) without a third-party SDK |
| Widgets | WidgetKit extension fed through an App Group |
| Persistence | UserDefaults plus iCloud key-value sync, with change notifications so updates on one device show on another |
| Sign-in (optional) | Sign in with Apple and Google Sign-In; biometric parental lock |

### Events service (serverless)

Local events come from a small **Cloudflare Worker** that I built and run:

- **Two sources fetched in parallel:** the Ticketmaster Discovery API (family classification) and Fáilte Ireland's open-data feed. A failure in one source doesn't break the other.
- **Location queries:** latitude/longitude plus a radius (default 40 km, limited to 5–150 km). Searching by town name alone found 2 events for a small town, while searching by coordinates found 262. That finding changed how the app queries.
- **Family-friendly filter:** removes listings with adult age ratings (15A/16/18 and stated 18+/21+ limits), drink-led listings and adult formats.
- **Clean-up:** removes duplicate recurring events (same name and venue) and picks the best-ratio image for each listing.
- **Caching:** an edge key-value cache keeps results for 24 hours, dropping to 15 minutes if any source failed, so a temporary outage isn't cached all day.
- **Security:** the third-party API key exists only as a server-side secret. It is never shipped in the app.

## Privacy

There's no account requirement and no server holding family data. Profiles, favourites and plans stay on the device and, if the user signs in, in their own iCloud. Location is optional and used only to centre the map and work out distances.

## Engineering notes

- 118 commits; about 14,000 lines of Swift across the app, the widget and tests.
- Unit tests for the discovery feed, map location state, security and persistence.
- Five public releases, up to v1.7.0, including a redesign for the iPhone Duo foldable.
- A full engineering handover document with architecture, data flow, design-system rules and known pitfalls.
- One lesson recorded in the handover: the deployed Worker had drifted from the version in source control. I recovered the live code, documented the difference and made "the deployed version is the source of truth" a written rule.

*Source code is private. This page describes the design without exposing keys, infrastructure identifiers or endpoints.*
