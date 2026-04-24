# Oyster Community Apps

The registry of community-built apps for [Oyster](https://oyster.to).

This repo is read by:
- **[oyster.to/apps](https://oyster.to/apps)** — the public browse page
- The `oyster install <id>` CLI — resolves the given id here, then pulls the latest release from the app's repo
- The Oyster in-app browser (future)

One source of truth — `community-apps.json` — drives all three surfaces.

## List your app here

Open a PR adding one entry to `community-apps.json`:

```json
{
  "id": "your-app-id",
  "name": "Your App",
  "author": "Your Name",
  "authorUrl": "https://github.com/you",
  "description": "One-line summary of what it does.",
  "repo": "your-username/your-app-repo"
}
```

## Requirements

Your app's GitHub repo must:

1. **Have a `manifest.json` at the repo root** conforming to the [Oyster app manifest schema](https://github.com/mattslight/oyster-os/blob/main/docs/plans/apps-system.md).
2. **Use a unique `id`** — lowercase, hyphenated, `^[a-z0-9][a-z0-9-]{0,63}$`. This is what users type — `oyster install <id>` — and also the folder name when installed. IDs are first-come-first-served. **Never change the `id` after release** (it lives in user configs and install paths).
3. **Publish a GitHub Release** (tagged with the version in `manifest.json`, prefixed `v` — e.g. `v0.1.0`). Attach:
   - `manifest.json`
   - An app bundle zip (for static apps) OR `main.js` (+ `styles.css` for future `bundle` runtime)
4. **Have an OSI-approved licence** in the repo root. MIT is recommended.

## Review process

PRs are reviewed for:

- Correct manifest shape
- Unique, non-reserved `id`
- No malicious code (spot-check of the latest release)
- No duplicate functionality of an existing app with a trivially different name

Reviews are best-effort, single-maintainer today. If you're blocked, ping on the Oyster Discord (link in [oyster-os](https://github.com/mattslight/oyster-os)).

## Removing an app

Open a PR removing the entry. Reasons to remove:

- App is abandoned and incompatible with current Oyster
- Security issue and no response from the author within 14 days
- Author request

## Fields

| Field | Required | Purpose |
|---|---|---|
| `id` | yes | App ID. Must match the app's `manifest.json`. Used as the CLI install argument (`oyster install <id>`) and the folder name on install. |
| `name` | yes | Human-readable display name. |
| `author` | yes | Your name or handle. |
| `authorUrl` | no | Link to your homepage / GitHub. |
| `description` | yes | One-line summary shown in the browser. |
| `repo` | yes | `owner/name` on GitHub. Used to fetch releases. |

## License

MIT — the registry metadata is freely reusable.
