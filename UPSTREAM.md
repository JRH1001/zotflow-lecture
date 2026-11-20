# Pinned upstream versions

| Project | Commit | What it is |
|---|---|---|
| [duanxianpi/zotflow](https://github.com/duanxianpi/zotflow) | `7e58e5fa43bd389972310a694d96793e7e7200b3` | ZotFlow 1.7.1 |
| [duanxianpi/obsidian-zotero-reader](https://github.com/duanxianpi/obsidian-zotero-reader) | `e6dfec2857b1e008a416832e1bd9df868513b035` | the reader ZotFlow 1.7.1 embeds (submodule `reader/reader`) |

The patches in `patches/` are made against exactly these commits. The build refuses to run if they no longer apply.

## Updating to a newer ZotFlow
Upstream moves fast. To move to a newer version, the pins above and `ZOTFLOW_REF` in `.github/workflows/build.yml` are
changed and the patches are re-created against the new commits (the patches are small and isolated on purpose).
