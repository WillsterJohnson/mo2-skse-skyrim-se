# Guide

_This guide looks really long but at least half of it is just warnings and idiot-proofing. If you're
somewhat familiar with Linux, this should take about 10 minutes to complete._

This guide will go through every step to take you from not having Steam installed to having a
handful of useful terminal commands and `.desktop` files to use Mod Organizer 2 to modify and launch
Skyrim Special Edition.

It also assumes you're a novice Linux user, each step will be carefully detailed, and there will be
constant reminders to [practice good safety habits (seriously, read `terminal_safety.md`)](./terminal_safety.md).

## Install Steam

Head over to [Steam's website](https://store.steampowered.com/) and click "install steam" at the top
of the page.

Run the installer, log in with your credentials, and launch the Steam application.

## Install Skyrim Special Edition

You probably own Skyrim SE if you're reading this, so head over to your library and install it.

If you don't already own it, you can buy it in the store. Pirated copies (probably) won't work with
this guide.

## Configure Proton Compatibility

On the library page for Skyrim SE, click the cog icon and select "properties".

In the properties window, click the "compatibility" tab.

Check the box that says "force the use of a specific Steam Play compatibility tool" and select the
version of Proton you want to use.

I recommend using version 8.0 or higher, however version 7.X
should work without issue. Version 6.X and below are known to cause some issues, so avoid older
versions of Proton.

## Run Skyrim Special Edition

Ensure that you can run vanilla Skyrim SE without issue before continuing.

You should also create at least one character, and reach the point where you can move around freely.

## Download the Mod Organizer 2 Installer

You can download the installer from [Mod Organizer 2's Nexus page](https://www.nexusmods.com/skyrimspecialedition/mods/6194?tab=files).

You should get an `.exe` file with a fairly long name, I recommend moving this to your desktop, and
renaming it `mo2.exe` - we only need this for the next step before we can safely delete it.

## Install Mod Organizer 2

This can be done in a variety of ways, however I've found this method to be the most reliable.
There are linux install scripts available, but due to them being 3rd-party tools with a relatively
small audience, the maintainers understandably have higher priorities.

You should copy the following script into a text file, and make the [relevant replacements](./script_replacements.md),
then copy it into your terminal and run it.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
STEAM_COMPAT_CLIENT_INSTALL_PATH=$STEAMEXEC \
STEAM_COMPAT_DATA_PATH=$STEAMDIR/steamapps/compatdata/489830 \
$STEAMDIR/steamapps/common/Proton\ $PROTONVERSION/proton run \
$MO2EXE
```

> You should keep a copy of this command with the replacements made, as it will be useful in later
> steps. You can drop the last line (the `$MO2EXE` part), as this will not be used.

After running this, the installer window should appear.

1. select "accept" then "next"
2. use the default path `C:\Modding\MO2` then "next" (yes - the Windows path is correct)
3. scroll down and uncheck "add windows defender exclusions" then "next"
4. check "don't create a start menu folder" then "next"
5. **do not** check "create a desktop shortcut" then "next"
6. click "install", allow the installer to run, then "finish"

## Create a `.desktop` file for Mod Organizer 2

The first part of this step is to create the executable script which the `.desktop` file will point
to. This script will launch Mod Organizer 2 using the correct environment variables, and will be
accessible from anywhere in your terminal by typing `mo2`.

### Create `mo2` Script

The following command will open a text editor in your terminal ready to write to the file
`/usr/local/bin/mo2`.

In Nano, you use the arrow keys to move the cursor, `Ctrl+Shift+V` to paste, `Ctrl+O` to save, and
`Ctrl+X` to exit.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo nano /usr/local/bin/mo2
```

In this file, paste the following script. Make the necessary [replacements](./script_replacements.md),
then save and exit. You may find it easier to copy the script into a text editor, make the
replacements, then paste it into Nano.

Be absolutely certain that there is **nothing**, not even a space or a blank line, before
`#!/bin/bash`, it is an essential piece of syntax known as a "shebang" which tells the terminal how
to interpret the script.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
#!/bin/bash
STEAM_COMPAT_CLIENT_INSTALL_PATH=$STEAMEXEC \
STEAM_COMPAT_DATA_PATH=$STEAMDIR/steamapps/compatdata/489830 \
$STEAMDIR/steamapps/common/Proton\ $PROTONVERSION/proton run \
$STEAMDIR/steamapps/compatdata/489830/pfx/drive_c/Modding/MO2/ModOrganizer.exe
```

Next give the file appropriate permissions to allow it to be executed.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo chmod 755 /usr/local/bin/mo2
```

### Create `mo2.desktop`

Finally, the `.desktop` file needs to be created. The following command will again use Nano to open
a text editor in the terminal.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo nano ~/.local/share/applications/mo2.desktop
```

Paste the following configuration into this file, then save and exit.

You may change the `Name` to anything you like, this is the name that will appear in your
application menu. You can also change the `Icon` if you wish, however this guide will **not** cover
how to do this.

Be absolutely certain that the `Exec` is the name of the file you created above, if following this
guide exactly, it should be `mo2`. You should not include the leading path, for example
`/usr/local/bin/mo2` should be `mo2`.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
[Desktop Entry]
Name=ModOrganizer2
Comment=Launch ModOrganizer2
Exec=mo2
Icon=steam
Terminal=true
Type=Application
Categories=Game;
```

Now check your applications list. You should see an entry for Mod Organizer 2, and clicking it
should launch Mod Organizer 2 (close MO2 for now, there are other things to do first).

## Set Up `nxm://` Protocol Handling

At the time of writing, this is only possible in the FireFox browser due to arbitrary limitations
within Chrome (you used to be able to do this in Chrome, not anymore!).
Head over to [FireFox.com](https://firefox.com/) to install FireFox, or use your distro's store or
package management tool.

### Configure FireFox

In FireFox, paste `aboute:config` in the address bar.

Once there, enter `network.protocol-handler.expose.nxm` in the search bar on the page.

Check the "Boolean" option, then click the "+" icon to the right. Ensure that the text in the centre
reads "false".

### Create `nxmhandler` Script

Similarly to creating the `mo2` file, the next step is to create an `nxmhandler` file.

Run the command below, then copy-paste the script into the file. Make the necessary
[replacements](./script_replacements.md), then save and exit.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo nano /usr/local/bin/nxmhandler
```

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
#!/bin/bash
STEAM_COMPAT_CLIENT_INSTALL_PATH=$STEAMEXEC \
STEAM_COMPAT_DATA_PATH=$STEAMDIR/steamapps/compatdata/489830 \
$STEAMDIR/steamapps/common/Proton\ $PROTONVERSION/proton run \
$STEAMDIR/steamapps/compatdata/489830/pfx/drive_c/Modding/MO2/nxmhandler.exe "$1"
```

Next give the file appropriate permissions to allow it to be executed.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo chmod 755 /usr/local/bin/nxmhandler
```

### Create `nxmhandler-all` Script

`nxmhandler-all` will take in a text file which contains a list of `nxm://` URIs, and will launch
`nxmhandler` for each one, installing multiple mods at once. This can be used to share mod lists,
such as the ones described in [my recommendations](./recommendations.md).

Run the command below, then copy-paste the script into the file. Make the necessary
[replacements](./script_replacements.md), then save and exit.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo nano /usr/local/bin/nxmhandler-all
```

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
#!/bin/bash
file=$1
if [[ -z $file ]]; then
    echo "Usage: $0 <filepath>.nxmuri"
    exit 1
fi
file_content=$(cat "$file")
list=$(echo "$file_content" | sed -e 's/#.*$//' | sed -e '/^$/d')
total=$(echo "$list" | wc -l)
echo "Total: $total"
echo "List:"
echo "$list"
count=1
while IFS= read -r nxmuri; do
        echo "$count/$total ($nxmuri)"
        count=$((count+1))
        nxmhandler "$nxmuri"
done <<< "$list"
```

Next give the file appropriate permissions to allow it to be executed.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo chmod 755 /usr/local/bin/nxmhandler-all
```

## Launch Mod Organizer 2

If you have done everything correctly up to this point, you will be able to launch MO2 from your
applications list.

If you're unable to do this, you may have missed a step, or your distro may not automatically
refresh it's `.desktop` file listings. Try logging out an back in to your user account, or
restarting your computer.
If this does not work, be sure that you have run the `sudo chmod` commands, and that you have
created the `mo2` file and `mo2.desktop` file in the correct locations.

Any further issues may be discussed in the [discussions tab](https://github.com/WillsterJohnson/mo2-skse-skyrim-se/discussions).

## Install SKSE

**Manually** install SKSE from the [Silverlock website](https://skse.silverlock.org/).

You likely need the "Current Anniversary Edition build".

As instructed on SKSE's website, you should watch this
[video tutorial on how to install SKSE](https://www.youtube.com/watch?v=xTGnQIiNVqA). The video
shows the use of some files which are no longer used, don't panic if you appear to be missing files,
you can safely ignore them.

## Create a Windows `.lnk` Shortcut for SKSE

Launch MO2 if you don't already have it open.

Over on the top-right next to the "run" button there is a dropdown menu. Click it, then select
"edit".

In the popup window on the top-left next to "executables" there is a "+" icon. Click it, then select
"add from file".

Select the `skse64_loader.exe` file, then click "Open".

If you don't see it immediately, navigate to `desktop`, `my computer`, then your real computer's
drive should be located at `Z:`. If there is no drive labelled `Z:`, simply select the drive which
is _not_ `C:`.

From here, navigate to `$STEAMDIR/steamapps/common/Skyrim Special Edition` (see
[replacements](./script_replacements.md)), then select the `skse64_loader.exe` file, then click
"Open".

On the right in the box labelled "title", rename this to "SKSE".

On the left in the box labelled "executables", click and drag "SKSE" to be at the top. This ensures
that when you open MO2, SKSE will be the default program to run.

Click "apply", then "okay".

Below the "run" button in MO2, there is a dropdown labelled "shortcut". Click this, then select
"desktop". This appears to do nothing, however by clicking "shortcut" again the icon on the
"desktop" option will have changed to a delete icon.

To verify for certain, run the following command (see [replacements](./script_replacements.md)). It
will output the contents of the virtual Windows desktop folder, which will contain a `.lnk` file for
SKSE.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
ll /media/will/NVMe250/steam/steamapps/compatdata/489830/pfx/drive_c/users/steamuser/Desktop/
```

Make a note of the name of this file, if following this guide exactly it should be `SKSE.lnk`.

## Map a `.desktop` file to the Windows `.lnk`

In this step, you should refer back to
[the same instructions for MO2's `.desktop` file](#create-a-desktop-file-for-mod-organizer-2).

### Create `skse64` Script

Open Nano

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo nano /usr/local/bin/skse64
```

Paste the script

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
#!/bin/bash
STEAM_COMPAT_CLIENT_INSTALL_PATH=$STEAMEXEC \
STEAM_COMPAT_DATA_PATH=$STEAMDIR/steamapps/compatdata/489830 \
$STEAMDIR/steamapps/common/Proton\ $PROTONVERSION/proton run \
$STEAMDIR/steamapps/compatdata/489830/pfx/drive_c/users/steamuser/Desktop/SKSE.lnk
```

Make the necessary [replacements](./script_replacements.md), then save and exit.

Give the file appropriate permissions to allow it to be executed.

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo chmod 755 /usr/local/bin/skse64
```

### Create `skse64.desktop` File

Open Nano

_[IMPORTANT WARNING - READ BEFORE YOU RUN ANY COMMANDS](./terminal_safety.md)_

```sh
sudo nano ~/.local/share/applications/skse64.desktop
```

Paste the script

```sh
[Desktop Entry]
Name=SKSE64
Comment=Launch SKSE64 TESV SSE with MO2
Exec=skse64
Icon=steam
Terminal=false
Type=Application
Categories=Game;
```

Now check your applications list. You should see an entry for SKSE64, and clicking it should launch
Skyrim SKSE64 via MO2. Until mods are installed however, it can be difficult to verify.

## Complete

You now have instant access to both Mod Organizer 2 and your Modded Skyrim via SKSE from your
applications menu, and you can now automatically download mods from Nexus using the `nxmhandler`
script we created.

## Next Steps

Head over to [the Skyrim Special Edition Nexus mods page](https://www.nexusmods.com/skyrimspecialedition/)
and install some mods.

If you're new to modding, I have some [recommendations](./recommendations.md), as well as the
following short guide to modding Skyrim SE.

You will find an incredible amount of NSFW content on the Skyrim SE Nexus. I don't mean mods which
add revealing clothing to the game (those certainly exist), I mean mods who's thumbnail image is
full nudity or sexual imagery. Don't browse Nexus in public, or in view of others who might have
something to say about what you're viewing online. If this is what you want from modded Skyrim, more
power to you I suppose, but if you're looking for worldbuilding and immersion, you might have to
trawl through a lot of NSFW content to find what you're looking for. Go to the
[mods search page](https://www.nexusmods.com/skyrimspecialedition/mods/) and use the "refine
results" menu to filter for what you want.

When installing a mod, you may be prompted to install some dependencies. Make sure you _always_
install _all_ required dependencies, and when possible seek out first-party and third-party
compatibility patches for mods, especially if you find that some content is broken or interacts in
strange or immersion-breaking ways.

You'll almost certainly need
[USSEP, the Unofficial Skyrim Special Edition Patch](https://www.nexusmods.com/skyrimspecialedition/mods/266),
so go ahead and install this now. You'll find that certain bugs are removed by SKSE and USSEP, such
as the Dawnstar chest and other similar chests, so be aware that in most cases your game will be
more lore-friendly and prevent the use of exploits and glitches.
