OpenRC README
=============

OpenRC is a dependency-based init system that works with the
system-provided init program, normally `/sbin/init`.

## Debian Packaging for OpenRC 0.43.5 Metztli build hack

Please make sure to fulfill software dependencies listed in debian/control file.

Subsequently...

Once inside metztli-openrc-0.43.5 directory:

`ln -s debian/patches`

`quilt push -a --fuzz=0`

`dpkg-buildpackage [-d] -F -us -uc -jX -T binary-arch,binary-indep`

 where option -d implies ignore dependencies listed in debian/control file
 (only if you absolutely know those dependencies are fulfilled, else build fails)

 and X stands for number of CPUs/cores assigned to the build procedure.
 please see man dpkg-buildpackage for more elaborate explanation(s).

When build finishes, generated .deb files will be found at parent directory.

OpenRC builds under Metztli Reiser4 / Debian Buster GCC8/Bullseye GCC10 AMD64

[Metztli IT OpenRC] (https://tenochtitlan.city/@metztli/108531009118817304)

## Metztli Reiser4 / Debian backports Installation

Use dpkg -i to install .deb files generated in the above procedure. 

## NOTE: if OpenRC (other software) is built and installed as original instructions below,
   the user will have dependency issues installing related .deb software packages in future.

## Installation 

OpenRC requires GNU make.

Once you have GNU Make installed, the default OpenRC installation can be
executed using this command:

`make install`

## Configuration

You may wish to configure the installation by passing one or more of the
below arguments to the make command

```
PROGLDFLAGS=-static
LIBNAME=lib64
DESTDIR=/tmp/openrc-image
MKBASHCOMP=no
MKNET=no
MKPAM=pam
MKPREFIX=yes
MKPKGCONFIG=no
MKSELINUX=yes
MKSTATICLIBS=no
MKSYSVINIT=yes
MKTERMCAP=ncurses
MKTERMCAP=termcap
MKZSHCOMP=no
PKG_PREFIX=/usr/pkg
LOCAL_PREFIX=/usr/local
PREFIX=/usr/local
BRANDING=\"Gentoo/$(uname -s)\"
SH=/bin/sh
```

## Notes

We don't support building a static OpenRC with PAM.

You may need to use `PROGLDFLAGS=-Wl,-Bstatic` on glibc instead of just `-static`.

If you are building OpenRC for a Gentoo Prefix installation, add `MKPREFIX=yes`.

`PKG_PREFIX` should be set to where packages install to by default.

`LOCAL_PREFIX` should be set to where user maintained packages are.
Only set `LOCAL_PREFIX` if different from `PKG_PREFIX`.

`PREFIX` should be set when OpenRC is not installed to /.

If any of the following files exist then we do not overwrite them

```
/etc/devd.conf
/etc/rc
/etc/rc.shutdown
/etc/conf.d/*
```

`rc` and `rc.shutdown` are the hooks from the BSD init into OpenRC.

`devd.conf` is modified from FreeBSD to call `/etc/rc.devd` which is a
generic hook into OpenRC.

`inittab` is the same, but for SysVInit as used by most Linux distributions.
This can be found in the support folder.

Obviously, if you're installing this onto a system that does not use
OpenRC by default then you may wish to backup the above listed files,
remove them and then install so that the OS hooks into OpenRC.

## Reporting Bugs

Please report bugs on our [bug tracker](http://github.com/OpenRC/openrc/issues).

If you can contribute code , please feel free to do so by opening
[pull requests](https://github.com/OpenRC/openrc/pulls).

## IRC Channel

We have an official irc channel, #openrc on the libera network.
Please connect your irc client to irc.libera.chat and join #openrc on
that network.

