
Debian
====================
This directory contains files used to package manod/mano-qt
for Debian-based Linux systems. If you compile manod/mano-qt yourself, there are some useful files here.

## mano: URI support ##


mano-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install mano-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your mano-qt binary to `/usr/bin`
and the `../../share/pixmaps/mano128.png` to `/usr/share/pixmaps`

mano-qt.protocol (KDE)

