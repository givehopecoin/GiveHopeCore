
Debian
====================
This directory contains files used to package givehoped/givehope-qt
for Debian-based Linux systems. If you compile givehoped/givehope-qt yourself, there are some useful files here.

## givehope: URI support ##


givehope-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install givehope-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your givehopeqt binary to `/usr/bin`
and the `../../share/pixmaps/givehope128.png` to `/usr/share/pixmaps`

givehope-qt.protocol (KDE)

