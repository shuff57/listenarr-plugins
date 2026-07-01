# shuff57 Listenarr plugins

One catalog for all of my [Listenarr](https://github.com/Listenarrs/Listenarr) plugins. Add a **single** repository URL in Listenarr and every plugin below shows up in **Settings → Plugins**.

## Add the catalog

Settings → Plugins → **Add repository**, paste:

```
https://raw.githubusercontent.com/shuff57/listenarr-plugins/main/listenarr-plugins.json
```

## Plugins

| Plugin | id | Description |
|--------|----|-------------|
| Inline Player | `player` | In-app audiobook player — chapters, bookmarks, resume, Listen library page. |
| Library Stats | `stats` | Library + listening dashboard: totals, top authors/narrators. |
| Theme | `theme` | Inject custom CSS at runtime — accent presets + full editor. |
| Library Export | `export` | Export your library to JSON or CSV. |
| Backup | `backup` | Download your config directory as a zip. Admin-gated. |
| Discover | `discovery` | Suggests audiobooks from authors you already own. |
| Health | `health` | File-integrity scan — missing / zero-byte / unreadable files. |

Each plugin also lives in its own `shuff57/listenarr-<id>` repo; this catalog just aggregates them so you only add one URL.

> Installing a plugin downloads and runs code from its release. Only add repositories you trust.
