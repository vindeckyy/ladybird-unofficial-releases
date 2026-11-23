# Ladybird Unofficial Releases

> **This is an unofficial community mirror. It is not affiliated with, endorsed by, or
> produced by the Ladybird project ([LadybirdBrowser/ladybird](https://github.com/LadybirdBrowser/ladybird)).**

This repository republishes the **official release artifacts** built by the Ladybird
project's own CI ("Build Release" workflow) as proper, discoverable GitHub Releases.

Upstream builds its binaries but publishes them only as workflow-run artifacts in the
Actions tab — hard to find, hidden behind login, and deleted after 90 days. This mirror
tracks upstream release tags (e.g. `2026.47.7`) and republishes the user-facing
artifacts of each build as a GitHub Release with a stable URL.

**Nothing here is built by us.** Every asset is downloaded from the official
`LadybirdBrowser/ladybird` CI and uploaded unmodified. SHA-256 checksums are computed
over the downloaded files and published with each release.

## What gets mirrored

Per upstream release tag:

| Asset | For |
|---|---|
| `ladybird_<ver>-1~ubuntu24.04_*.deb` | Ubuntu 24.04 (amd64, arm64) |
| `ladybird_<ver>-1~ubuntu26.04_*.deb` | Ubuntu 26.04 (amd64, arm64) |
| `ladybird-<ver>-1.fc44.*.rpm` | Fedora 44 (x86_64, aarch64) |
| `ladybird-<ver>-Linux-*.flatpak` | Any distro with Flatpak (x86_64, aarch64) |
| `ladybird-<ver>-macOS-arm64.tar.xz` | macOS (Apple Silicon) |
| `ladybird-<ver>-source.tar.xz` | Source |
| `SHA256SUMS` | Checksums of everything above |

Debug-symbol packages and third-party source archives are intentionally not mirrored.

## Installing

> Ladybird is **pre-alpha** software. Expect broken websites, crashes, and missing
> features. It is not a daily-driver browser yet.

**Ubuntu / Debian (.deb):**
```sh
sudo apt install ./ladybird_2026.47.7-1~ubuntu26.04_amd64.deb
```

**Fedora (.rpm):**
```sh
sudo dnf install ./ladybird-2026.47.7-1.fc44.x86_64.rpm
```

**Any Linux distro (Flatpak bundle):**
```sh
flatpak install --user ./ladybird-2026.47.7-Linux-x86_64.flatpak
flatpak run org.ladybird.Ladybird
```

**macOS (Apple Silicon):** extract the `.tar.xz` and run the app inside. On first
launch, right-click → Open to bypass Gatekeeper (the build is not signed/notarized).

**Verify a download:**
```sh
sha256sum -c SHA256SUMS --ignore-missing
```

## How mirroring works

- A scheduled workflow runs every 6 hours (and can be triggered manually).
- It lists the latest successful official "Build Release" runs, keyed by their
  version tag (`2026.47.x`).
- Any version not yet released in this repository is downloaded and published.
- **First build wins:** if upstream re-runs the same version tag later, the existing
  release here is left untouched. Delete the release to force a re-mirror.
- Up to 3 new versions are mirrored per run (configurable; manual runs can seed more).

## Legal

- The browser is licensed under the BSD 2-Clause License (see [`LICENSE`](LICENSE)).
- Each package bundles its own third-party license information.
- "Ladybird" and the ladybird logo are used here solely to identify the software being
  mirrored. All trademarks belong to their respective owners.
- If the Ladybird project asks for this mirror to be taken down, it will be.
