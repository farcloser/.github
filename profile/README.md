# Farcloser

An organization focused on developer tooling and core (mostly go) libraries.

Small, dependency-light, aggressively pinned. Everything here is built the same way, because
the rules are written down and a tool enforces them.

> 🔒 marks a private repository

## Workstation & repository setup

- [**limen**](https://github.com/farcloser/limen) — every rule written, verifiable,
  enforceable. Checks, fixes and bootstraps our repositories: mandatory files, pinned
  tooling, GitHub settings. Its [engineering handbook](https://github.com/farcloser/limen/blob/main/book/index.md)
  is the doctrine the rest of this organization follows.
- [**limen-install**](https://github.com/farcloser/limen-install) — one script to make a
  machine ready for development: aqua and limen, pinned and signature-verified, on macOS,
  Linux and Windows.
- [**homebrew-brews**](https://github.com/farcloser/homebrew-brews) — our Homebrew tap: our
  own tools, plus hardened forks of upstream formulas (openssh without OpenSSL, ed25519-only,
  baked-in config).
- [**mumbrew**](https://github.com/farcloser/mumbrew) — keep your brews updated
  automatically.
- [**tarmac**](https://github.com/farcloser/tarmac) — a dependency-free shell script that
  installs a per-user Homebrew on a blank macOS, and seeds `.profile`.
- [**ssh-agent**](https://github.com/farcloser/ssh-agent) — a macOS user launch agent for
  `ssh-agent`, for YubiKeys and other `sk-` keys the vanilla macOS agent does not support.
- 🔒 [**onboarding**](https://github.com/farcloser/onboarding) — workstation provisioning:
  shell dotfiles and a bootstrap on top of tarmac.

## Containers & virtualization

- [**ossein**](https://github.com/farcloser/ossein) — a minimalistic, rootless, daemonless,
  microVM-based container runtime and image builder for macOS.
- [**ossein-kernel**](https://github.com/farcloser/ossein-kernel) — a Linux kernel image
  builder for macOS: baseline configuration and patches tuned for Apple VZ, producing
  sub-10MB images.
- [**lepton**](https://github.com/farcloser/lepton) — a modern containerd CLI (Linux, kernel
  5.13+, containerd 2.0+).
- [**quark**](https://github.com/farcloser/quark) — a declarative container image management
  SDK in Go: build, sync, scan and audit images across platforms and registries, plus SSH
  and secret primitives.
- [**hadron**](https://github.com/farcloser/hadron) — a declarative Docker deployment tool
  that brings remote Docker hosts to a desired state over SSH.
- [**gluon**](https://github.com/farcloser/gluon) — deployment plans and helpers built on
  quark.
- [**godolint**](https://github.com/farcloser/godolint) — a Dockerfile linter, written in Go.
- [**healthcheckers**](https://github.com/farcloser/healthcheckers) — tiny http, dns and rtsp
  clients meant to be used as container `HEALTHCHECK`s.
- 🔒 [**go-vz**](https://github.com/farcloser/go-vz) — Go bindings for Apple's
  Virtualization.framework.

## Go libraries

- [**go-core**](https://github.com/farcloser/go-core) — the basics every one of our Go
  projects uses: logging, error reporting, telemetry, network/TLS settings, exec, and
  human-readable units and durations.
- [**go-containers**](https://github.com/farcloser/go-containers) — basics for the containers
  ecosystem, deriving from containerd, nerdctl and moby.
- [**go-mdns**](https://github.com/farcloser/go-mdns) — mDNS, on top of third-party Go
  libraries.
- [**go.farcloser.world**](https://github.com/farcloser/go.farcloser.world) — the vanity
  import root for our Go packages.

## Documentation & infrastructure

- [**open-source-help-desk**](https://github.com/farcloser/open-source-help-desk) —
  documentation easing the mundane hurdles of contributing to open source, starting with a
  thorough git cheat sheet (DCO, signing, rebasing, squashing).
- [**.github**](https://github.com/farcloser/.github) — this repository: the organization
  profile and the community health files every other repository inherits.

## Forks

- [**tigron**](https://github.com/farcloser/tigron) — a modern testing framework for
  command-line applications. Superseded upstream: use
  `github.com/containerd/nerdctl/mod/tigron`.
- [**tag**](https://github.com/farcloser/tag) — ID3, MP4 and OGG/FLAC metadata parsing in Go.

## Contributing & support

Projects here are provided as-is, best-effort, without warranty.

- [Contributing guide](https://github.com/farcloser/.github/blob/main/.github/CONTRIBUTING.md)
  — sign-off (DCO), mandatory commit signing, commit rules, pull request flow.
- [Security policy](https://github.com/farcloser/.github/blob/main/.github/SECURITY.md) —
  **never** report a vulnerability in a public issue; use private vulnerability reporting.
- Bugs and ideas go to the issue tracker of the repository they concern.
