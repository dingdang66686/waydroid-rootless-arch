# waydroid-rootless Arch repository

Pacman repository for the rootless Waydroid backend fork.

## Install

Add to `/etc/pacman.conf`:

```ini
[waydroid-rootless]
Server = https://dingdang66686.github.io/waydroid-rootless-arch/$arch
SigLevel = Optional TrustAll
```

Then:

```sh
sudo pacman -Sy
sudo pacman -S waydroid-rootless
systemctl --user enable --now waydroid-rootless.service
```

The package:

- installs `/usr/bin/waydroid-rootless` and a `/usr/local/bin/waydroid` launcher
  (root still uses the distro binary);
- installs the user unit `waydroid-rootless.service`;
- disables the rootful `waydroid-container.service`.

The base image is `ghcr.io/dingdang66686/waydroid-rootless-image:13`, pulled by
the runtime if needed.  Local file-tree overlays are supported in
`~/.local/state/waydroid/overlay`.

## Build locally

```sh
makepkg -si
```

## Notes

- Requires a rootless podman setup and at least 131072 sub-UID/GID range.
- The repository is unsigned; `SigLevel = Optional TrustAll` is required.
