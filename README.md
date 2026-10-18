# llvm-toolchain

Pre-built LLVM toolchain releases consumed by [hew-lang/hew](https://github.com/hew-lang/hew) CI and release builds.

This repo exists so that LLVM toolchain artifacts don't clutter hew's own
release history. Nothing published here is a Hew language release — it's
build infrastructure.

## What's here

`.github/workflows/prebuild-llvm.yml` keeps one Windows MSVC LLVM toolchain per
release series (for example `23.1`), built from source from the latest stable
llvm-project release in that series. Windows lacks a usable upstream prebuilt
LLVM tarball for Hew's linker requirements.

A daily run compares llvm-project's release tags with the releases published
here. It builds a series when LLVM has released a newer patch version, and
starts tracking a series when LLVM ships one newer than any tracked. With
nothing new, only a seconds-long planning job runs. Run the workflow manually
with `llvm_series` to rebuild one series, for example after changing the build
recipe.

## Releases

| | |
|---|---|
| Tag | `toolchain/llvm-<series>-windows-msvc` |
| Name | `LLVM <version> Windows MSVC toolchain`, the exact version inside |
| Asset | `hew-llvm-<series>-windows-msvc.tar.gz` and `.sha256` |
| Provenance | SLSA build-provenance attestation on the archive |
| Layout | `llvm-<major>/`, extracting to `C:\llvm-<major>` |

Each release floats: a new patch release replaces the assets in place. hew's
`.github/actions/setup-llvm` action and `release.yml` request a series and
verify the checksum. The older `toolchain/llvm-<version>-windows-msvc-v<n>`
releases remain for reference and are not updated.
