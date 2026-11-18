# mako plugins

The registry [mako](https://github.com/ironpark/mako) starts with: the
plugins its store lists before you add a registry of your own.

**Nothing here is reviewed.** A listing says who published a plugin, by
which key, and what it asks to do; mako checks that the package is the one
listed and is signed by that key, and asks you before a plugin does
anything outside its own block. Whether to trust a publisher is yours to
decide. Any git repository with a `mako-registry.json` at its root is a
registry as much as this one, and is added in Settings ▸ Plugins or with
`mako plugins registries add <url>`.

## Listing a plugin

1. Make a key once, and keep it: `mako plugins keygen ~/keys/mako-publisher.key`.
   Updates must be signed by the key a plugin was first installed with.
2. Pack and sign the plugin's folder:
   `mako plugins pack <folder> -key ~/keys/mako-publisher.key`.
3. Put the `.makoplugin` file somewhere it can be downloaded by https, a
   release of your repository say.
4. Add it to `mako-registry.json` with
   `mako plugins index <checkout of this repository> <package> -url <download URL>`,
   which writes the entry from the package itself, and open a pull request
   with the change.

The formats of the package and of the index, and what a plugin can do,
are in [docs/plugins.md](https://github.com/ironpark/mako/blob/main/docs/plugins.md).

## Blocklist

`blocklist` in the index stops a plugin on every node that reads this
registry, by its ID, one version of it, or its publisher's key, with the
reason shown to the user. Open an issue to report a plugin that does harm.
