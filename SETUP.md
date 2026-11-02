# Fix your GitHub profile metrics

Repository: `https://github.com/SiphiweRadebe/SiphiweRadebe`

## What changed

- Uses a dedicated classic personal access token (`METRICS_TOKEN`) for GitHub-account metrics instead of the limited workflow `GITHUB_TOKEN`.
- Fixes invalid coding-habits chart type (`bar` → `classic`).
- Replaces two publicly inaccessible repository names with four verified public repositories.
- Includes `push` events in recent activity and looks back 90 days.
- Changes Metrics to `output_action: none` and commits all six validated images in a single push, using GitHub Actions' default `GITHUB_TOKEN`.
- Stops publishing if a generated SVG is missing, malformed, or contains an `Unexpected error` message.
- Removes empty starred-topics and flaky achievements panels from the README. Links to the native GitHub profile for achievements instead.

## Step 1 — Set up the token securely

Open `https://github.com/settings/tokens/new` and create a **classic** personal access token for Metrics. Use the **fewest scopes necessary**. For public repositories, start with no scopes; only grant other permissions if a specific desired feature demonstrably requires them. **Do not grant broad `repo` access just to show company/private work.** Follow employer policies for workplace repositories. Set an expiry and rotate the token as necessary.

Save it in the profile repository under **Settings → Secrets and variables → Actions → New repository secret**, with name **`METRICS_TOKEN`**. Never put the token in README files, workflow source, or chat messages.

For this Metrics action, a classic token is the upstream documented option. Do not confuse the data-access token with `GITHUB_TOKEN` used to commit the generated images.

## Step 2 — Update the two repository files

Copy this package's `README.md` to the root of your profile repository.

Copy `.github/workflows/metrics.yml` to the same path in your profile repository, replacing the old workflow.

You can leave the old `metrics.topics.svg` and `metrics.achievements.svg` in the repository or delete them after you are happy with the new profile. The revised README no longer displays them.

## Step 3 — Run and verify

Open `https://github.com/SiphiweRadebe/SiphiweRadebe/actions/workflows/metrics.yml`, select **Run workflow**, then inspect each step's log.

The workflow should generate six SVG files, validate them, and commit changes once to `main`.

If it fails, check the failing step. Don't disable `plugins_errors_fatal` to hide plugin failures—fix the failing plugin or temporarily remove that panel and its README reference.

### What still may legitimately be empty

- Recent activity only reflects activity accessible to the token and the plugin's upstream API. Employer/private repository activity is often not shown.
- Coding habits are based on recent observable events, not all your historical commits.
- Some metrics may depend on an upstream service and cannot be guaranteed before the workflow runs in your GitHub account.

Docs: `https://github.com/lowlighter/metrics`
