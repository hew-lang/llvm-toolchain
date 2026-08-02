# llvm-toolchain

Pre-built LLVM toolchain releases consumed by [hew-lang/hew](https://github.com/hew-lang/hew) CI and release builds.

This repo exists so that LLVM toolchain artifacts don't clutter hew's own
release history. Nothing published here is a Hew language release — it's
build infrastructure.

## What's here

- `.github/workflows/prebuild-llvm.yml` — builds LLVM from source for
  windows-msvc (Windows lacks a usable upstream prebuilt LLVM tarball for
  Hew's linker requirements) and publishes it as a versioned GitHub Release
  asset, verified with a SHA-256 checksum and SLSA build provenance
  attestation.

Runs weekly and on manual dispatch. hew's `.github/actions/setup-llvm`
action and `release.yml` download the published asset directly from this
repo's releases.
