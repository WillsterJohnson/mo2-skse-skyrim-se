# Files for Nerds

No nonsense, let's get to it.

## Install Stuff

We need Steam, Skyrim Special Edition, the Mod Organizer 2 installer (run via below command), and
SKSE.

Before running below command, configure Proton compatibility for Skyrim SE in Steam, then launch
Skyrim and get past the intro cutscene & character creation (not strictly needed, but may prevent
quirks & bugs).

```sh
STEAM_COMPAT_CLIENT_INSTALL_PATH=/usr/bin/steam \
STEAM_COMPAT_DATA_PATH=/PATH/TO/steamapps/compatdata/489830 \
/PATH/TO/steamapps/common/Proton\ <PROTON VERSION>/proton run \
/PATH/TO/mo2-installer.exe
```

Delete the installer exe after MO2 is installed.

SKSE should be installed after MO2 to ensure it's installed correctly.

## SKSE Shortcut

Use the same command use to run the installer to run the MO2 executable at
`/PATH/TO/steamapps/compatdata/489830/pfx/drive_c/Modding/MO2/ModOrganizer.exe`.

Over on the top-right, add SKSE as an option for running, then create a desktop shortcut.

This should create a file at
`/PATH/TO/steamapps/compatdata/489830/pfx/drive_c/users/steamuser/Desktop/<NAME>.lnk`, verify this.

## If Everything Above Was Done Correctly it's Time to Grab the Files in this Folder

`~/.local/share/applications`;

- `MO2.desktop` - a desktop shortcut to launch MO2
- `SKSE64.desktop` - a desktop shortcut to launch SKSE

`/usr/local/bin/` (these files need paths filled in)

- `mo2` - a bash script to launch MO2
- `skse64` - a bash script to launch SKSE
- `nxmhandler` - a bash script to register NXM URIs with MO2 (requires FireFox)
- `nxmhandler-all` - a bash script to read in a list of NXM URIs from a file and pass them to
  `nxmhandler`
