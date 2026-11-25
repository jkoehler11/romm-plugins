# ROMulus plugin store

The index ROMulus reads for **Settings → Plugins → Add plugin → Store**.

`index.json` is the whole store. Each entry names a manifest by URL; ROMulus
fetches that URL when someone installs it, validates it exactly like a manifest
someone pasted, and writes it to the server's plugin folder. Nothing here is
executed, and ROMulus never fetches this index until the store tab is opened.

## Entry

```json
{
  "id": "rommarcade",
  "name": "RomMArcade",
  "version": "0.1.0",
  "description": "One sentence about what pressing it does.",
  "author": "you",
  "homepage": "https://github.com/you/your-plugin",
  "manifest_url": "https://raw.githubusercontent.com/you/your-plugin/main/plugin.json",
  "tags": ["launcher"]
}
```

`id` and `name` are required, and `manifest_url` must be http(s): a manifest on
a scheme ROMulus cannot fetch is dropped from the list rather than offered and then
failing.

## Submitting a plugin

1. Publish the plugin on its own. A plugin is a `plugin.json` plus a README —
   see [rommarcade-plugin](https://github.com/jkoehler11/rommarcade-plugin) for
   the shape, including the `settings` fields a plugin can declare and the
   `rommarcade://` handler that makes the button land on a game.
2. Open a pull request here that adds one entry to `index.json`, and say in the
   description what the plugin does and what it talks to.
3. What is checked: the manifest parses, every action's URL is http(s) or a
   custom scheme ROMulus hands to the browser, the plugin does nothing but open
   URLs, and the repository it points at is the one the entry names.

A plugin that ships a manifest with an unknown slot, an action without a label,
or a URL scheme the browser runs as markup (`javascript:`, `data:`) is refused
by ROMulus itself, so the store's review is about whether a plugin is *useful*, not
whether it is *safe to parse*.

## Where this comes from

ROMulus is a fork of RomM, and the plugin system is what the fork adds; the
AGPL-3.0 licence and its notices are in that repository. This store is only the
index it reads, and it holds no code.
