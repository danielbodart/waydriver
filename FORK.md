# danielbodart/waydriver

A fork of [BohdanTkachenko/waydriver](https://github.com/BohdanTkachenko/waydriver)
that adds a Nix binary cache for the `mcp` package. Everything else here is
upstream's: its README, workflows, releases, Docker image and crates. The fork
only adds `.github/workflows/cachix.yml`, `.github/workflows/update.yml` and
this file, and merges upstream's `main` every six hours (the `sync` job in
`cachix.yml`).

## Channels

- **Nix**: flake input `github:danielbodart/waydriver` (with
  `inputs.nixpkgs.follows = "nixpkgs"`), package `packages.<system>.mcp`
  (`waydriver-mcp` with its runtime stack), prebuilt for x86_64-linux and
  aarch64-linux in `https://danielbodart.cachix.org` against this flake's
  lock and the current nixos-26.05 and nixos-unstable heads, so a config that
  follows either channel substitutes it. No `nixosModules.default`: it is an
  MCP server a client launches, not a service.
- Not shipped: Docker — upstream publishes the image; the fork adds none.
- Not shipped: Tarball + systemd — upstream's releases (release-plz) are the
  ones to use; the fork publishes no releases of its own.

Updated weekly (Sunday 21:23 UTC): the flake's inputs (nixpkgs, on
nixos-unstable like upstream's flake, so the upstream sync never conflicts),
committed only once `.#mcp` builds on both architectures. Cargo.lock and the
Docker images move with upstream. No release is ever cut by the fork.
