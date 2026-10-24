# waydroid-rootless Arch repository

Pacman repository for a Waydroid build with the rootless podman backend.

The package is named `waydroid` and replaces the distro package of the same
name.

## Install

Add to `/etc/pacman.conf`, **before** `[core]`/`[extra]` (repository order
decides which `waydroid` package wins):

```ini
[waydroid-rootless]
Server = https://dingdang66686.github.io/waydroid-rootless-arch/$arch
SigLevel = Optional TrustAll
```

Then:

```sh
podman pull ghcr.io/dingdang66686/waydroid-rootless-image:13
sudo pacman -Sy
sudo pacman -S waydroid
systemctl --user enable --now waydroid.service
```

The package replaces the distro `waydroid` package, installs `/usr/bin/waydroid`
with the rootless launcher, and disables the rootful
`waydroid-container.service`.

Local overlays are supported in `~/.local/state/waydroid/overlay`.

## Build locally

```sh
makepkg -si
```

## Notes

- Requires a rootless podman setup and at least 131072 sub-UID/GID range.
- The repository is unsigned; `SigLevel = Optional TrustAll` is required.
