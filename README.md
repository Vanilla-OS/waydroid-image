# Waydroid Image

Containerfile for building a Waydroid image.

This image is based on top of [`vanillaos/pico`](https://github.com/Vanilla-OS/core-image/pkgs/container/pico) and offers a Waydroid
installation.

> Note: this is an experiment of providing waydroid via Apx (dbox). It still require the `binder_linux` kernel module at host side.

## Build

```bash
sh prepare.sh
podman image build -t vanillaos/waydroid .
```
