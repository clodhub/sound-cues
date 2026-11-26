# Sound cues instructions

## For the agent
Select `pkg:clod/com.clodhub/sound-cues`; connect `preferences` to the preferences component's output. Set `soundManifest` to the folder the recipe's sound files and manifest live in, and `defaultMuted` only if the user wants sound off to begin with. The event names in the manifest come from the recipe; do not invent them here.

- Select package `pkg:clod/com.clodhub/sound-cues` version `0.11.0`.
- Settings to configure:
  - `soundManifest` (string, slug; optional; default `sounds`)
  - `defaultMuted` (boolean; optional; default `false`)
- Connect the provided `sound-cues` (com.clodhub/sound-cues 1.0.0, OpenRPC 1.3.2 document `interfaces/sound-cues.json`; its `Manifest` schema is the shape of `manifest.json`) to the consumer that needs it.
- Supply `preferences` (com.clodhub/preferences 1.0.0) from the component that provides it.
- No accounts or keys are needed.

## For the developer
Supply the sound files and a `manifest.json` in the folder named by `soundManifest`; keep them short and quiet if microphones may be open. On the web serve the folder next to the page and pass its URL as `baseUrl`; on Apple add the files to the bundle; on Android add them as raw resources named as `rawResourceName` says. Call `unlock` (or `unlockOn`) from a user tap on the web.

## How to check
From the component directory:

- `node --test tests/web.test.ts` (web, required-local; tools: node 26.5)
- `python3 tests/native.py apple` (apple, platform; tools: python3 3.12, swiftc 6.4, xcrun 72)
- `python3 tests/native.py android` (android, platform; tools: python3 3.12, kotlinc 2.2, java 26.0)
- `python3 -m clod review <digest> --store STORE --policy POLICY --trusted --allow-network` checks an archive fetched with `python3 -m clod fetch sound-cues@VERSION --store STORE --from https://clodhub.com` and runs its suites.
