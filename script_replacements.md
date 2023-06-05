# Script Replacements

_This file contains replacements for content in bash scripts mentioned in [the guide](./guide.md)_

## `$STEAMEXEC`

The location of your steam executable entrypoint.

You can find this by running `which steam` in a terminal.

## `$STEAMLIBDIR`

The location of the steam library containing your SkyrimSE installation.

To find this, you can do the following;

1. Open steam
2. Click "steam" in the top-left corner
3. Click "settings"
4. Click "downloads" in the left sidebar
5. Click "steam library folders" in the main window (about halfway down)
6. Find the library containing Skyrim Special Edition
7. Use the path shown at the top of the window, above the colorful disk usage bar

## `$PROTONVERSION`

The version of Proton to use.

If following the guide exactly, this should read `.../Proton\ 8.0/proton`, i.e. `$PROTONVERSION` is
`8.0`.

## `$MO2EXE`

The location of your MO2 installer.

This is the file downloaded from Mod Organizer 2's Nexus page, it's most likely in your downloads
folder, though you can move and rename it as you wish.

If following the guide exactly, `$MO2EXE` is `~/Desktop/MO2.exe`.
