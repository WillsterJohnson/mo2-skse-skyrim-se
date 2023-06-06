# Extra Info

More information for users who have followed [the guide](./guide.md).

## Steam Input

Unfortunately it seems that Steam Input doesn't work correctly when launching Skyrim SE SKSE through
MO2 or the SKSE shortcut.

I have attempted the following combinations, with my test being the use of the paddles on my Xbox
Elite Series 2 controller for ABXY inputs.

- Steam Input enabled for vanilla Skyrim, launch via SKSE shortcut
- Steam Input enabled for SKSE shortcut, launch via SKSE shortcut
- Steam Input enabled for SKSE shortcut and vanilla Skyrim, launch via SKSE shortcut
- Xpadneo installed, Steam Input enabled for vanilla Skyrim, launch via SKSE shortcut
- Xpadneo installed, Steam Input enabled for SKSE shortcut, launch via SKSE shortcut
- Xpadneo installed, Steam Input enabled for SKSE shortcut and vanilla Skyrim, launch via SKSE
  shortcut

To conduct each test, I set up one of the above configurations and launch as described. I then allow
MO2, SKSE, and Skyrim SE to load. Once reaching the main menu in Skyrim, I ensure "continue" is
selected, then press the paddle mapped to "A". To be certain, I then press the other three paddles,
allowing a second or two between inputs. If the game does not respond to the inputs, I consider the
test a failure.

I also repeated the tests twice, the first time using bluetooth connection, the second using a wired
connection over USB. In all cases, I ensure the controller is operating correctly by navigating
Steam big picture using only the DPad and paddles, this confirms that the controller is connected
and that the paddles are functioning correctly outside of SKSE Skyrim SE.

If anyone is able to get Steam Input working correctly in a setup not dissimilar to the one
described in [the guide](./guide.md), please
[open an issue](https://github.com/WillsterJohnson/mo2-skse-skyrim-se/issues) detailing the steps
you took to get it working. You don't need to have used an Xbox Elite Series 2 controller, nor a
controller with paddles, so long as you have successfully used Steam Input to map one or more
buttons to another, and shown that it works, the steps you took will be a valid way to get Steam
Input working.
