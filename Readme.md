<span style="display:block;text-align:center">[![](https://raw.githubusercontent.com/XayOn/docker-kodi-beta/master/kodilovesdocker.png)](https://hub.docker.com/r/xayon/docker-kodi-beta) </span>

<center><h1> Dockerized KODI matrix (v19) </h1> </center>

<span style="display:block;text-align:center">![](https://github.com/XayOn/docker-kodi-beta/workflows/Publish%20to%20Docker/badge.svg) ![](https://img.shields.io/docker/pulls/xayon/docker-kodi-beta)</span>


Use Kodi matrix without any sweat. Made with :heartpulse: by David Francos.
Dockerized kodi master branch, fresh and nice!

> :warning: **This is the UNSTABLE version of KODI**

:computer: This repository contains a single Dockerfile implementing the [oficially recommended way][5] of KODI build on linux. It comes with Github Actions integration for automatic builds, for the current git on the KODI repository reference linked in this readme (Currently [3f78d7e][4]).


# What will you get

- Up to date bleeding edge kodi Docker image
- Complete set of KODI binary addons (pvr, visual representations)
- Libretro binary addons with multiple emulators (psx, snes...)
- Compatible with most matrix compatible addons (cryptodome etc installed)
- 500MB image

# Installation

**This image will work on any x64 system where you can run docker**.

## X11Docker

For simplicity, *x11docker* is recommended, wich will limit your options to any
system with linux and bash.

> :warning: ** ARM is not supported **

First install **x11docker** following its installation [guide][3].
Then, launch **xayon/docker-kodi-beta** with x11docker, the full extent of
x11docker options is not to be part of this guide, you can refer to its
documentation if you need advanced options.

For Xorg, with pulseaudio, you could launch it with the following command:

```bash
x11docker --xorg --pulseaudio --gpu --homedir $HOME/.kodi_matrix/ xayon/docker-kodi-beta
```

## Direct display (no Xorg) with GBM

If you don't want Xorg, and can have your system without Xorg running, you can
use a GBM enabled kodi version.

It's available with the tag "gbm" under this same repository, you can execute
it directly with docker, as in:

```bash
docker run -P8080:8080 --restart=always --privileged xayon/docker-kodi-beta:gbm
```

Or with docker-compose, with for example:

```bash
  kodi:
     restart: always
     image: xayon/docker-kodi-beta:gbm 
     privileged: True
     ports:
      - 8080:8080
     volumes:
      - /dev/bus/usb:/dev/bus/usb
```

I'm exposing port 8080 because I use the web interface, but that's up to you.
Also, this mounts /dev/bus/usb as volume so you can use your keyboard and
peripherals.

```bash
docker run -P8080:8080 --restart=always --privileged xayon/docker-kodi-beta:gbm
 ```


## Why

Kodi 19 isn't stable enough to be properly packaged with libretro and all the
binary add-ons.

At first (July 2020) the packages were broken, and, after a first manual build,
I decided this had to be automated. Docker seems like the best option for that.

Note that some addons are not yet migrated to python3, wich is a requirement
for kodi 19. 

I have successfully tested this build with:

- Jellyfin addon
- Netflix addon
- Youtube addon
- RomCollectionBrowser addon


## Acknowledgments

- SicLuceatLux for his [docker-kodi][1] wich introduced me to
  [x11docker][2] and inspired part of this Readme

[1]: https://github.com/SicLuceatLux/docker-kodi
[2]: https://github.com/mviereck/x11docker
[3]: https://github.com/mviereck/x11docker#shortest-way-for-first-installation "guide"
[4]: https://github.com/xbmc/xbmc/commit/3f78d7e27055d337d28e2f8354f750d222952246 "3f78d7e"
[5]: https://github.com/xbmc/xbmc/blob/master/docs/README.Linux.md "oficially recommended way"
