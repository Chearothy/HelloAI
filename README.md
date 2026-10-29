# HelloAI — Telegram Video Library (Vercel-only edition)

## Deploy to Vercel
1. Upload this project to GitHub without any `.env` file or Telegram session.
2. Import the repository into Vercel.
3. Framework Preset: **Other**.
4. Root Directory: `./`.
5. Build Command: leave empty (no build step is required).
6. Output Directory: leave empty so Vercel serves `index.html` from the project root.
7. Install Command: `npm install` (the project has no runtime npm dependencies).
8. Add Environment Variable `TELEGRAM_CHANNEL_USERNAME` with the public channel username, without `@`. Optional: `TELEGRAM_WEB_BASE=https://t.me`.
9. Deploy.

The `/api/videos` route is implemented in `api/videos.js`. It fetches the public Telegram channel preview when called and Vercel caches the response briefly.

## Important limitations
- This version uses Telegram's **public web preview**. The channel must be public and its posts must be visible at `https://t.me/s/<channel>`.
- Telegram only exposes a limited recent page through the public preview. This API does not perform a full historical scan or persistent background sync.
- Direct playback is available only when Telegram's public preview provides a direct video URL. For other posts, the site falls back to Telegram's embedded player.
- This version does not use the Telegram user MTProto session, `/stream/:id`, or `/thumb/:id`; it therefore does not proxy arbitrary large private/full-size videos through Vercel.
- Vercel Functions are request-driven and short-lived. They are not an always-on worker. A real-time, persistent full-channel crawler requires a persistent worker or an external webhook plus persistent storage.

## Security
Never commit `.env`, `TG_SESSION`, `TG_API_HASH`, or other secrets. If a session or API secret was committed or shared, revoke/rotate it before using the project again.
