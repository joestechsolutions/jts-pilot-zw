# jts-pilot-intake-template

The template for spinning up a JTS client intake form on GitHub Pages.

**This is a template repo, not a real client form.** To create a real form for a client, use the spin-up script or follow the manual steps below.

## How to spin up a new client form

### One command (recommended)

```bash
~/bin/jts-pilot-new acme
# Optional second arg: client display name (defaults to slug)
~/bin/jts-pilot-new acme "Acme Construction"
```

The script:
1. Creates a new public repo `joblas/jts-pilot-acme` from this template
2. Clones it locally
3. Substitutes `{{CLIENT_NAME}}` placeholders in `index.html` and `thanks.html`
4. Commits and pushes
5. Enables GitHub Pages on `main`
6. Prints the live URL (e.g. `https://joblas.github.io/jts-pilot-acme/`)

First-time setup for a new email endpoint: open the URL, submit the form, click the activation link in the FormSubmit email.

### Manual (if the script isn't installed)

```bash
# 1. Create repo from template
gh repo create joblas/jts-pilot-<slug> --public --template joblas/jts-pilot-intake-template

# 2. Clone + customize
git clone https://github.com/joblas/jts-pilot-<slug>.git
cd jts-pilot-<slug>
sed -i "s/{{CLIENT_NAME}}/Acme Construction/g" index.html thanks.html

# 3. Push + enable Pages
git add . && git commit -m "Customize for Acme Construction"
git push -u origin main
gh repo edit joblas/jts-pilot-<slug> --enable-pages --pages-source-branch main --pages-source-path /

# Live in ~60s: https://joblas.github.io/jts-pilot-<slug>/
```

## Files

- `index.html` — the 9-question intake form
- `thanks.html` — the post-submit confirmation page
- `.nojekyll` — tells GitHub Pages to serve the HTML as-is

## FormSubmit endpoint

Currently: `joe@joestechsolutions.com`

The spin-up script routes all client submissions to the same inbox. Each submission's subject line is prefixed with the client name (e.g. `Acme Construction — New Intake Submission`) so you can filter in Gmail.

To route a specific client to a different email, edit `index.html` after creation.

## Placeholders

| Placeholder | Replaced with | Example |
|---|---|---|
| `{{CLIENT_NAME}}` | Display name | `ZW Home Construction` |
| `{{SUBJECT_LINE}}` | (reserved, not used yet) | — |

## Naming convention

| Repo | Purpose |
|---|---|
| `joblas/jts-pilot-intake-template` | This template (one source of truth) |
| `joblas/jts-pilot-<slug>` | One repo per client (e.g. `jts-pilot-zw`, `jts-pilot-acme`) |
| Live URL | `https://joblas.github.io/jts-pilot-<slug>/` |
