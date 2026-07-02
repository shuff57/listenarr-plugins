# shuff57 Listenarr plugins

One catalog for all of my [Listenarr](https://github.com/Listenarrs/Listenarr) plugins — the index
and every plugin package live in **this** repository. Add a single repository URL in Listenarr and
all of the plugins below show up in **Settings → Plugins**, ready to install individually.

Listenarr plugins are **runtime-installable** add-ons: they add backend API endpoints, frontend
views and navigation, and their own data storage, without rebuilding Listenarr or changing its
core. Adding this repository does **not** install anything — it populates a menu, and you install
only what you want.

## Add the catalog

In Listenarr, go to **Settings → Plugins → Add repository**, and paste:

```
https://raw.githubusercontent.com/shuff57/listenarr-plugins/main/listenarr-plugins.json
```

The plugins appear in the list. Click **Install** on the ones you want (the app restarts briefly to
load each). **Update** and **Uninstall** work the same way. Install what you need, ignore the rest,
and remove anything later without a trace.

## Plugins

| Plugin | id | What it does |
|--------|----|--------------|
| **Profiles** | `profiles` | Multi-user accounts: per-user "My Library" shelves on the shared pool, admin user management, self-service password change. |
| **Inline Player** | `player` | In-app audiobook player — chapters, bookmarks, resume, and a Listen library page. |
| **Discover** | `discovery` | Suggests audiobooks you might like, seeded from the authors and genres you already have, with one-click hand-off into Add New. |
| **Library Stats** | `stats` | A dashboard: totals, top authors/narrators, and (with the player) in-progress/finished counts. |
| **Theme** | `theme` | Inject custom CSS at runtime — accent presets, a full CSS editor, and Apply/Save/Reset. |
| **Library Export** | `export` | Export your library to JSON or CSV in one click. |
| **Backup** | `backup` | Download your config directory as a zip. Admin-gated. |
| **Health** | `health` | File-integrity scan: flags missing, zero-byte, or unreadable audiobook files on disk. Admin-gated. |

## How it works

- **A repository is a catalog, not a bundle.** The index (`listenarr-plugins.json`) lists each
  plugin's `id`, `name`, `version`, `description`, and a `package` URL. You install per-plugin.
- **Each plugin is a small zip** with a `plugin.json` manifest and any of: a backend `.dll`, a
  frontend bundle (`ui/<id>.js` + `ui/<id>.css`). Every package here is published as a GitHub
  **release** on this repo (tags like `player-v1.1.0`).
- **Backend** assemblies load at startup and their controllers run in Listenarr's own API pipeline
  (sharing auth, CSRF, routing). A plugin owns its **own** data — its own SQLite file or config —
  and never touches the core schema.
- **Frontend** bundles are injected at runtime and register their own routes, sidebar items, and an
  optional always-mounted root component, against a small stable host SDK (`window.LISTENARR`).
- **Install / update / uninstall** write to the plugins directory and restart the app so the change
  loads on the next boot.

> **Trust:** installing a plugin downloads and runs its code — the same trust model as *arr custom
> repositories. Only add repositories you trust, and keep the Plugins page behind authentication /
> your local network.

## Run your own repository

A repository is just a static JSON file you host anywhere (a GitHub repo, a release asset, any web
server). Point Listenarr at its URL and it appears in the list.

```json
{
  "name": "My Listenarr plugins",
  "plugins": [
    {
      "id": "example",
      "name": "Example",
      "version": "1.0.0",
      "description": "What it does.",
      "author": "you",
      "package": "https://example.com/example.zip"
    }
  ]
}
```

Each `package` is a zip laid out as:

```
plugin.json                      # { "id", "name", "version", "frontend"?, "styles"? }
Listenarr.Plugins.Example.dll    # optional backend (implements IListenarrPlugin)
ui/example.js                    # optional frontend bundle
ui/example.css                   # optional styles
```

This repository is a working example — see `listenarr-plugins.json` and the Releases tab.
