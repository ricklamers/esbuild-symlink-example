## Support for optional symlink resolve in esbuild

This repo demonstrates the use case for allowing users to configure resolve behavior for symlinks in `esbuild`.

In particular, when `moduleA/utils` references modules that are available in the `app/package.json` dependencies it will fail to resolve correctly without the ability to _not_ resolve symlinks in the build system.

The symlink in this example repo is in:

```.
|-- README.md
|-- app
|   |-- dist
|   |   `-- main.js
|   |-- package.json
|   |-- src
|   |   |-- index.js
|   |   `-- moduleA <-- relative symlink to top level moduleA/
|   |       `-- utils.js
|   `-- webpack.config.js
`-- moduleA
    `-- utils.js
```

This use case is particularly useful in the context of larger monorepos.

### Reproducing

Clone the repo. Observe:

`npm run build` succeeds in building, as webpack is configured to not resolve symlinks.

`npm run esbuild` fails as esbuild resolves the symlink and cannot find `lodash` as a result.