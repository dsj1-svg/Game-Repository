# Neon Rush

A futuristic typing race with three laps, four theme packs, an original electronic soundtrack, single-player racing, and online rooms for up to 12 racers.

Play the full hosted game: https://neon-rush-arcade-dana.sparseridge16.chatgpt.site

## Play single-player locally

Open `index.html` in a desktop browser and use a physical keyboard. This file includes the complete single-player game. Multiplayer requires the hosted backend; opening this file locally does not start a multiplayer server.

## Source layout

- `web/index.html`: game interface and browser logic; contains build placeholders.
- `web/soundtrack.js`: original procedural electronic soundtrack.
- `worker/game.js`: theme packs and shared race rules.
- `worker/api.js`: multiplayer API, rooms, server progress and winners.
- `drizzle/`: database migration and migration journal.
- `scripts/`: build and verification scripts.
- `.openai/hosting.json`: existing Sites deployment configuration. It contains no credentials.
- `index.html`: ready-to-play single-player export.

## Build and verify

Use Node.js 24 or newer (the backend tests use Node's built-in SQLite support). No npm dependencies are required.

From this folder:

```sh
mkdir -p ../outputs
npm run build
npm test
node scripts/test-audio.mjs
```

The build creates `dist/server/index.js` for Cloudflare Worker hosting with a D1 `DB` binding and the migrations in `drizzle/`. It also writes a refreshed single-player HTML file to `../outputs/Neon-Rush.html`. Tests use an in-memory database and do not modify live game rooms.

## Upload to GitHub

1. Extract this ZIP.
2. Create a repository named `neon-rush` on GitHub.
3. Open the repository and choose **Add file → Upload files** (or **uploading an existing file** on a new empty repository).
4. Drag the contents of this folder into the upload area, keeping the folder structure. Upload the extracted files, rather than just the ZIP. On macOS, Command+Shift+Period reveals hidden configuration files.
5. Commit the files with a message such as `Add Neon Rush game`.

## Hosting

A GitHub repository stores the code. Uploading it does not deploy the multiplayer backend or change the existing live game.

GitHub Pages can serve the root `index.html` as a single-player version. Full multiplayer requires the Worker API, a provisioned D1 database, and applied migrations; the current hosted link already provides those. This package does not contain database contents, player sessions, credentials, or Git history.

## Credits

The game displays source links for its brief movie/TV quotes and lyric excerpts. The soundtrack is synthesized by the game's own code. Quoted excerpts remain attributable to their respective creators; no license for those underlying works is granted by this repository.
