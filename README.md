<!-- ![XLibre on Artix Linux](./docs/img/screenshot.jpg) -->

# XLibre Testing Packages for Artix Linux

This third-party repository provides [XLibre](https://xlibre.net) x86_64 binary packages for [Artix Linux](https://artixlinux.org) for testing purposes. XLibre is the community-managed display server for the [X Window System Protocol Version 11 (Wikipedia)](https://en.wikipedia.org/wiki/X_Window_System_core_protocol), in short, X11. You can learn more about XLibre at [xlibre.net](https://xlibre.net/).

## Installing XLibre Manually

### Adding the Public Package Signing Key to pacman

First, please download the public OpenPGP signing key [`xlibre-artixlinux.asc`](xlibre-artixlinux.asc) used to sign the packages and add it to the pacman keyring:

```shell
curl -O https://xlibre-artix.github.io/xlibre-artixlinux.asc
sudo pacman-key --add xlibre-artixlinux.asc
sudo pacman-key --finger 2AFFCD7B42ADD2E7
sudo pacman-key --lsign-key 2AFFCD7B42ADD2E7
```

You can read more about package signing on the [pacman/Package signing - ArchWiki](https://wiki.archlinux.org/title/Pacman/Package_signing#Adding_unofficial_keys) page.

### Adding the Repository to Pacman

Once you added the public key, also add an entry for the XLibre repository to the file [`/etc/pacman.conf`](https://man.archlinux.org/man/pacman.conf.5) using [`sudo`](https://wiki.archlinux.org/title/Sudo) and your favorite editor.

> [!IMPORTANT]
> The following entry has to be added after the `[system]` key, but **before** the `[world]` key. Artix ships its own version of XLibre in the `world` repository and that needs to be overridden.

```ini
[xlibre]
Server = https://xlibre-artix.github.io/stable/$arch
```

Run `pacman` to update all package indexes and installed packages:

```shell
sudo pacman -Syyu
```

### Installing XLibre

Installing XLibre is as easy as installing the `xlibre-meta` package:

```shell
sudo pacman -S xlibre-meta
```

The included packages will replace any of their installed X.Org counterparts. When asked, just answer with `y `. To make use of XLibre, log out of your desktop or X session and log in again.

In case you get kicked out of a running desktop or X session while you're installing XLibre, just re-run `pacman` after you logged in again and let it install the missing packages:

```shell
sudo pacman -S xlibre-meta
```

When done, install the program `xorg-xdpyinfo` and filter its output for the `vendor` tags:

```shell
sudo pacman -S xorg-xdpyinfo
xdpyinfo | grep 'vendor'
```

It says XLibre? Congratulations!

## Getting in Contact

Please report any enhancement requests or issues with this repository at [Issues · xlibre-artix/xlibre-artix](https://github.com/xlibre-artix/xlibre-artix/issues). If you have a specific issue, please see the [list of package repositories](https://github.com/orgs/xlibre-artix/repositories?q=topic%3Apackage) and report it there. In case you need help, want to report success or talk about other aspects, please also check the official XLibre channels.
