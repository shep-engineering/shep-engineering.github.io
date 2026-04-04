# Deployment (Option A: single source repo)

This repo (`personal-website`) is the **only** repo you edit.

The root GitHub Pages site (`https://shep-engineering.github.io/`) is served from a separate repo:

- `shep-engineering/shep-engineering.github.io`

A GitHub Actions workflow in this repo automatically syncs the website files into the root Pages repo on every push to `main`.

## How to deploy changes (day-to-day)

1. Make edits in this repo.
2. Commit and push to `main`.
3. GitHub Actions runs the workflow **Deploy to Root Pages Repo**.
4. The workflow clones `shep-engineering/shep-engineering.github.io`, rsyncs the site content, commits, and pushes.

That’s it—**do not manually edit** the `shep-engineering.github.io` repo for content changes.

## Verify a deploy

1. GitHub → `shep-engineering/personal-website` → **Actions**
2. Open the latest **Deploy to Root Pages Repo** run
3. Confirm it completed successfully
4. Check the live site:
   - https://shep-engineering.github.io/

## One-time setup (required)

### A) Create a deploy keypair

Run locally:

```bash
ssh-keygen -t ed25519 -C "personal-website -> shep-engineering.github.io deploy" -f ~/.ssh/personal_website_pages_deploy
```

- Private key: `~/.ssh/personal_website_pages_deploy`
- Public key: `~/.ssh/personal_website_pages_deploy.pub`

Important:
- Use **no passphrase** for this deploy key (GitHub Actions cannot prompt).

### B) Add the PUBLIC key to the target repo (write access)

GitHub → `shep-engineering/shep-engineering.github.io` → **Settings** → **Deploy keys** → **Add deploy key**

- Title: `Deploy from personal-website`
- Key: paste contents of `~/.ssh/personal_website_pages_deploy.pub`
- Check: **Allow write access**

### C) Add the PRIVATE key to the source repo as an Actions secret

GitHub → `shep-engineering/personal-website` → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

- Name: `PAGES_DEPLOY_KEY`
- Value: the private key contents from `~/.ssh/personal_website_pages_deploy`

IMPORTANT:
- The secret name must be exactly:

`PAGES_DEPLOY_KEY`

If it’s named differently, the workflow will receive an empty `DEPLOY_KEY` and fail.

### Recommended: store the private key as base64

This avoids formatting/newline issues when pasting into GitHub secrets.

```bash
base64 -i ~/.ssh/personal_website_pages_deploy | tr -d '\n'
```

Paste that base64 string into the `PAGES_DEPLOY_KEY` secret.

## Troubleshooting

### Error: "Load key ... error in libcrypto"

Cause: the key stored in `PAGES_DEPLOY_KEY` is malformed due to copy/paste formatting.

Fix:
- Re-save `PAGES_DEPLOY_KEY` as **base64** (recommended), or
- Re-paste the raw private key ensuring the full block is included.

### Error: "Permission denied (publickey)"

Cause:
- Deploy key not added to the target repo, or
- Deploy key added without **Allow write access**, or
- `PAGES_DEPLOY_KEY` secret does not match the deploy key.

## Local machine SSH config

No local `~/.ssh/config` changes are required for the GitHub Actions deploy key.

Your local SSH config/keys are only for *your* interactive `git push` operations.
