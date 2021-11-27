# openformation/gitpod-node

Image with a configured Node.js environment.

## Features

- [fnm](https://github.com/Schniz/fnm) - The Fast Node Manager installed.
- Installs the latest Node.js LTS when the container starts.
- `use-on-cd` activated. Whenever you switch into a directory where a `.nvmrc` or `.node-version` lives, `fnm` asks you if you want to install this configured version.
