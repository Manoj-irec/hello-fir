# Firebase Production Deployment

This repository uses GitHub Actions to deploy to Firebase Hosting automatically.

## Deployment Triggers

- Push to `production` branch: runs CI and deploys to live Firebase Hosting.
- Pull request targeting `production`: runs CI and deploys a preview channel.

## Workflow Behavior

Both workflows perform these steps before deploy:

1. Check out source code.
2. Set up Node.js 20.
3. Install dependencies (`npm ci` when `package-lock.json` exists, otherwise `npm install`).
4. Run tests (`npm run test --if-present`).
5. Run build (`npm run build --if-present`).
6. Deploy to Firebase Hosting.

Deploy does not run if an earlier step fails.

## Required GitHub Secrets

Add this repository secret in GitHub:

- `FIREBASE_SERVICE_ACCOUNT_STUDIO_4339004962_F947E`

The value must be the Firebase service account JSON content for project `studio-4339004962-f947e`.

## Operations Notes

- Logs are available in GitHub Actions for each workflow run.
- If deployment fails, inspect the failed step in Actions logs and fix before the next push.
