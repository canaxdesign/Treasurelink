# Netlify Deploy Troubleshooting

## Fix Applied
The deployment error during dependency installation was caused by Netlify using `npm` by default while your project uses `pnpm` (as indicated by `pnpm-lock.yaml`).

**Changes made:**
1. Added `.nvmrc` with Node version `20` (matches your local setup).
2. Updated `netlify.toml` to specify `PNPM_VERSION = "10.4.1"` and `NODE_VERSION = "20"` in build environment.
3. Updated `netlify.toml` build command from `npm run build` to `pnpm build`.
4. Updated GitHub Actions workflow to use pnpm:
   - Added `pnpm/action-setup@v2` step.
   - Changed install command to `pnpm install --frozen-lockfile`.
   - Changed build command to `pnpm build`.

## Next Steps
1. Commit and push these changes to your repository:
   ```bash
   git add .nvmrc netlify.toml .github/workflows/deploy-netlify.yml
   git commit -m "Fix: configure pnpm for Netlify deployment"
   git push origin main
   ```

2. Trigger a new Netlify deployment:
   - Go to Netlify Dashboard → Deployments → "Trigger deploy" → "Deploy site" (or make a new push).
   - Monitor the build log in the Netlify UI.

3. If the build still fails after these changes, check:
   - Full Netlify build log for any error messages beyond "Starting to install dependencies".
   - Verify environment variables are set in Netlify (check Site Settings → Build & deploy → Environment).
   - Ensure `pnpm-lock.yaml` is committed to the repository (it should be).

## GitHub Actions
- The workflow now builds with `pnpm` locally and deploys to Netlify.
- Previews are created on pull requests; production deploys on push to `main`.
