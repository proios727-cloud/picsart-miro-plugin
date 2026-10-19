# Local Setup

Run the Picsart Miro plugin on your machine and load it into a Miro board.

## Prerequisites

| Requirement | Notes |
| --- | --- |
| Node.js 22+ | Matches the CI workflow. |
| Chromium-based browser | Safari blocks plain-HTTP `localhost` inside Miro. |
| Miro Developer team | Free: <https://developers.miro.com/docs/create-a-developer-team> |
| Picsart API key | <https://console.picsart.io/> — remove background and upscale use your Picsart credits. |

## 1. Install and run

```bash
cd picsart-miro-plugin
npm ci
npm start            # http://localhost:3000
```

`.npmrc` points the `@picsart` scope at a private GitLab registry. No `@picsart/*`
packages are in the lockfile, so no token is needed. If npm warns about the
unset variable, prefix the install with `GITLAB_REG_TOKEN=unused`.

## 2. Register the app in Miro

1. **Profile → Your apps → Create new app** and choose your Developer team.
2. **App URL:** `http://localhost:3000`
3. **Permissions:** `boards:read`, `boards:write`
4. **Install app and get OAuth token** → install it to your Developer team.

## 3. Use it

1. Open a board in the Developer team and click the Picsart icon in the app toolbar.
2. Paste your Picsart API key when prompted. It's saved in board-level app storage
   (`miro.board.storage`), so anyone using the app on that board shares the key and its credits.
3. Select an image on the board, then run **Remove Background** or **Upscale**.
   The result is added to the board next to the original.

## Build and host

```bash
npm run build        # static output in dist/
npm run serve        # preview dist/ on :3000
```

Host `dist/` on any static HTTPS host, then change the **App URL** in Miro to point at it.
