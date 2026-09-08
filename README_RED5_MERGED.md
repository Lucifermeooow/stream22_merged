# Stream 22 — Red5 Merged Build

The project keeps the previous Stream 22 app/provider work and adds a dedicated real Red5 streaming activity.

Execution order:
1. Build the native Android app.
2. Open the Red5 Live screen.
3. Verify camera preview.
4. Publish a real stream to Red5.
5. Stop it and verify the real state.
6. Keep Facebook/Google/Twitch/TikTok integration work available from the prior project.
7. Add Supabase only after Red5 publish/playback is proven.

Do not put Red5 license secrets or OAuth client secrets in source control.
