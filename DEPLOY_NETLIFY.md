# Deploying to Netlify

1. Connect repository
   - In Netlify, click "New site from Git" and connect your git provider.
   - Choose the repository for this project.

2. Build settings
   - Build command: `npm run build`
   - Publish directory: `dist/public`

3. Environment variables (Netlify UI -> Site settings -> Build & deploy -> Environment)
   - `OAUTH_SERVER_URL` : https://your-oauth-server
   - `OAUTH_CLIENT_ID` : your-client-id
   - `OAUTH_CLIENT_SECRET` : your-client-secret
   - (Optional) `NODE_ENV` : production

4. SPA routing
   - The project includes `client/public/_redirects` to route all paths to `index.html`.

5. Server/backend
   - This repo builds a server bundle at `dist/index.js`. Netlify static hosting will only serve the client from `dist/public`.
   - For the server you can deploy separately (recommended) to a platform that supports long-running Node servers such as Render, Railway, Fly, or Heroku. Configure the platform to run `node dist/index.js` and set the same environment variables there.

6. Quick local deploy using Netlify CLI (optional)
   - Install and login: `npm i -g netlify-cli && netlify login`
   - Run a one-off deploy (requires build to be present):
     ```powershell
     cd "c:\Users\Admin\Desktop\Canax design\february\PROFILE AND  WEBSITE\website 4"
     npm run build
     netlify deploy --prod --dir=dist/public
     ```

If you want, I can:
- Add a minimal README with production env placeholders (done here),
- Prepare a `render` or `railway` deploy configuration for the server bundle, or
- Configure GitHub Actions to auto-build and publish to Netlify on push.
