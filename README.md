# mirror-only-readme

This action wraps [filter-repo-action](https://codeberg.org/alinnow/filter-repo-action) to make it easy to maintain a README-only mirror of a repository on another git forge.

## Prerequisites

Before using this action, ensure:

- The target repository already exists on the remote forge (should be empty)
- You have a secret containing token with write access to the target repository. For GitHub, a [classic Personal Access Token](https://github.com/settings/tokens) with `public_repo` scope should suffice, assuming you're mirroring a public repository.

## Usage

```yml
on:
  push:
    branches:
      - main

jobs:
  mirror:
    runs-on: codeberg-tiny-lazy
    steps:
      - name: Check out repository
        uses: actions/checkout@v6
      - name: Mirror filtered repository
        uses: https://codeberg.org/alinnow/mirror-only-readme@v1
        with:
          other_forge_token: ${{ secrets.OTHER_FORGE_TOKEN }}
          prune_empty: never
          paths: |
            README.md
            LICENSE
```

### Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `other_forge_token` | Token for authenticating with the target git forge. | Yes | |
| `prune_empty` | When to prune empty commits (`always`, `auto`, `never`) | No | never |
| `paths` | List of paths to include in the mirror | No | README.md,LICENSE.md |
