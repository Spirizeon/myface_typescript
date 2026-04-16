# MyFace

## Getting started.

To get setup, download this code, and then run the following commands in the root directory of the app.

```shell
npm install
npm run migrated
npm run seed
```

- `npm install` downloads all the libraries that we depend on.
- `npm run migrate` setups a database for us to use.
- `npm run seed` adds some sample data to our database.

Once you have run all of those, we can simply start the app with

```shell
npm start
```

This should start the app, and we can see it by going to http://localhost:3001 in the browser.

To update the application, just change any of the code, save it, and the app should automatically update.
Just refresh the page to see the impact of your changes.

### Resetting the data

If you ever need to reset the database, then:

- stop the app
- delete the `dev.sqlite3` file.
- run `npm run migrate` and `npm run seed` again to re-make and re-populate the database.

## GitHub Actions – AI Test Loop

This repo uses an AI-powered test-fix loop that runs automatically on every push and pull request (except `main`).

### Required: Add Repository Secrets

Before pushing, you must add the following secrets to your GitHub repository, or the workflow will fail:

| Secret Name | Description |
|---|---|
| `CLOUDFLARE_ACCOUNT_ID` | Your Cloudflare Account ID |
| `CLOUDFLARE_API_KEY` | Your Cloudflare API Key |

**How to add secrets:**
1. Go to your repository on GitHub
2. Navigate to **Settings -> Secrets and variables -> Actions**
3. Click **"New repository secret"**
4. Add each secret listed above

### What it does

On every push/PR to a non-`main` branch, the workflow:
1. Checks out your repository
2. Verifies Docker and Docker Compose are available
3. Runs the AI test-fix loop via `docker compose up`
4. Cleans up containers and volumes after completion

The workflow file lives at `.github/workflows/ai-test-loop.yml`.
