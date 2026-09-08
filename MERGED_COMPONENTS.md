# Stream 22 — merged components

This project is based on the existing Stream 22 repository and incorporates the useful provider/integration material already present there.

## Preserved from the old Stream 22 project
- Compose UI under `app/src/main/java/com/ahmed/streamgit101/ui`.
- Facebook OAuth configuration under `data/FacebookOAuthConfig.kt`.
- YouTube/Google OAuth client and secure token storage under `lib/services/`.
- YouTube/Facebook/Twitch/TikTok destination configuration under `data/StreamSettings.kt`.
- Existing Cloudflare backend contract under `backend/` and `src/`.

## Replaced
The old simulated stream state in `StreamViewModel` is no longer the path used by the main GO LIVE action. The GO LIVE action opens `Red5LiveActivity`.

## Added
- `red5/Red5Config.kt`
- `red5/Red5LiveActivity.kt`
- `scripts/download_red5_android_sdk.sh`
- Current Red5 Android SDK dependency declarations.
- CI that downloads the current Red5 AAR, builds `:app:assembleRelease`, validates APK signing, and uploads the APK.

## Red5 runtime configuration
Set these in CI:
- Repository Variable: `RED5_STREAM_MANAGER_HOST`
- Repository Secret: `RED5_SDK_LICENSE_KEY`

The host is not embedded in source. The SDK license is never committed.

## Important
The open Red5 `streaming-android` repository contains a legacy/deprecated SDK. The project therefore uses the current Red5 Android SDK API documented by Red5 instead of copying that legacy SDK into the app.
