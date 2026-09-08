# Stream 22 — Red5 Merge

This revision keeps the existing Stream 22 native Android UI and pulls the provider configuration/integration material already present in the previous project into the same repository:

- Facebook OAuth configuration: `app/src/main/java/com/ahmed/streamgit101/data/FacebookOAuthConfig.kt`
- Google/YouTube OAuth code and secure token storage remain under `lib/services/` and the previous native `StreamSettings` contains the configured provider metadata.
- Twitch/TikTok destination metadata remains in `StreamSettings`.
- The existing Cloudflare OAuth backend contract remains under `backend/` and `src/`.

## Red5

The streaming path now uses the current Red5 Android WebRTC client API rather than the previous fake `delay()`/random-status implementation.

Main integration:
- `app/src/main/java/com/ahmed/streamgit101/red5/Red5Config.kt`
- `app/src/main/java/com/ahmed/streamgit101/red5/Red5LiveActivity.kt`

`Red5LiveActivity` creates `IRed5WebrtcClient`, starts preview, publishes a real stream, stops publishing, switches camera, and mutes/unmutes audio. It polls `isPublishing()` for the visible LIVE state.

## Required Red5 SDK

Red5 documents the current Android SDK as an AAR and requires the AAR plus WebRTC/OkHttp/Gson/PubNub dependencies. The project is configured for `*.aar` under `app/libs`.

A GitHub Actions helper is included:

`scripts/download_red5_android_sdk.sh`

It downloads the public Red5 SDK index, finds the first `.aar` link, and stores it as `app/libs/red5-cloud-sdk.aar`.

## Secrets/config

Do not commit the Red5 license key or private provider secrets.
Inject these at build time:

- `RED5_STREAM_MANAGER_HOST`
- `RED5_SDK_LICENSE_KEY`

Example local Gradle properties:

`RED5_STREAM_MANAGER_HOST=your-host.cloud.red5.net`
`RED5_SDK_LICENSE_KEY=your-license`

For GitHub Actions use repository/environment secrets or variables.

## Important

The old public `red5pro/streaming-android` repository is an archived/legacy example and its wrapper is old. This merge uses the current Red5 Android SDK API documented by Red5 instead of copying that deprecated SDK into the app.
