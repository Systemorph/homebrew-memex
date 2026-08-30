# Systemorph/homebrew-memex — the MeshWeaver Homebrew tap

```bash
brew tap systemorph/memex
brew trust systemorph/memex       # Homebrew refuses to load a third-party tap's formulae until you trust the tap
brew install memex-local          # the local prod-like memex stack on Colima k3s (Mac)
```

| What | Kind | Source of truth |
|---|---|---|
| `memex-local` | formula | [`deploy/homebrew/`](https://github.com/Systemorph/MeshWeaver/tree/main/deploy/homebrew) in **Systemorph/MeshWeaver** |
| `memex` (the desktop app — the React Native shell over LocalMesh) | cask (planned) | `clients/desktop/macos` in **Systemorph/MeshWeaver.Plugins** |

**Nothing here is edited by hand.** `Formula/memex-local.rb` is rendered and committed by the
platform repository's [`Homebrew (memex-local)` workflow](https://github.com/Systemorph/MeshWeaver/blob/main/.github/workflows/homebrew.yml)
on every merge to `main`: it attaches a tarball of `deploy/homebrew` + `deploy/helm` to a release
of this repository (`v0.2.<main commit count>`) and pins its `sha256` in the formula, so
`brew upgrade memex-local` follows main. Change the formula in the platform repository's
`deploy/homebrew/Formula/memex-local.rb` — the template CI renders from.

After installing, point the local stack at the cloud plugin registry and bring it up
(a platform admin mints the registration key on memex.meshweaver.cloud, Settings ▸
Administration ▸ Instance grants):

```bash
memex-local registry https://memex.meshweaver.cloud --key mwr_…
memex-local up
```

Docs: [Local memex on Colima k3s (Mac)](https://github.com/Systemorph/MeshWeaver/blob/main/src/MeshWeaver.Documentation/Data/Architecture/LocalColimaMac.md).
