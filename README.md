# Waydroid Image

Containerfile for building a Waydroid image.

This image is based on top of [`vanillaos/pico`](https://github.com/Vanilla-OS/core-image/pkgs/container/pico) and offers a Waydroid
installation.

> Note: this is an experiment of providing waydroid via Apx (dbox). It still require the `binder_linux` kernel module at host side.

## Build

### Requirements

- [Vib](https://github.com/Vanilla-OS/Vib)
- Podman or Docker

## Build the image

```bash
vib build recipe.yml
podman image build -t vanillaos/waydroid .
```

## Run

### Requirements

- Podman or Docker
- [Distrobox](https://github.com/89luca89/distrobox) (suggested) [1](#note1)
- [binder_linux](https://github.com/choff/anbox-modules) installed on host

### Usage

> Currently, the container needs to be rootfull, since it has to modprobe the needed kernel
> modules and mount the binder filesystem. This could change in the future.

```bash
distrobox create --root --init --unshare-all -i ghcr.io/vanilla-os/waydroid:main -n waydroid # replace with your local image if you built it
distrobox enter --root waydroid
```

Wait for the `waydroid-init` service to end, check with `systemctl status waydroid-init`.
Then start using waydroid with [2](#note2):

```bash
ewaydroid --help
```

## Note

- <a name="note1">1</a>: At the time of writing, the `--unshare-all` option is not yet released
so you need to use the latest version from git.

- <a name="note2">2</a>: The `ewaydroid` script is a wrapper around `waydroid` that
automatically points the `XDG_RUNTIME_DIR` and `DBUS_SESSION_BUS_ADDRESS` environment
variables to the host ones. This is needed to make the waydroid services work by
properly communicating with the host.
