# Super Smash Bros. Melee: Dylan's Edition

## Description

A new experience for those who love Super Smash Bros melee (a mod)

Created using these fine tools:

- Crazy Hand
- DAT Texture Wizard
- The Melee Decompilation Effort

Engine changes from base game:

- Universal Wall Jump Mechanic
   + I.e. all characters can now wall jump
- Universal 4-Frame L-Cancelling:
   + Every L-cancelled aerial has a lag of 4 frame instead of the lag getting divided by some factor. Very similar to Smash 64's Z-cancelling
   + No longer feels like "negative when missed" but rather "positive when hit."
   + Also, bigger L-Cancel window (10 frames)
   + 4 Frames so you don't accidentally shield after (4-frames is typically base landing lag as well)

## Patching an ISO

Dependencies:
 
- A legally obtained copy of Super Smash Bros. Melee. Why?
   1) The decomp is not complete
   2) The art assets are not owned by you or I and cannot under any circumstances be distributed
- xdelta3

1. Create a copy of your Melee iso in the repo (since you probably don't want to alter your main one)
2. Download the patch from the Releases section
3. Run the command `xdelta3 -d -s vanilla-melee.iso melee-dylans-edition-<version>.patch SSBMDE.iso`

## Building (To Create a Patch)

This should only be done if developing new changes to the mod.

Dependencies:

- Clone the repo then do: `git submodule update --init --recursive`
- Crazy Hand v1.31 (rename in your repo to `crazy-hand`)
- DAT Texture Wizard v6.1.4 (rename in your repo to `dat-tex-wiz`)
- A legally obtained copy of Super Smash Bros. Melee. Why?
   1) The decomp is not complete
   2) The art assets are not owned by you or I and cannot under any circumstances be distributed
- Python
- Ninja
- Java (only need runtime)
- Wine (if on Linux)
- xdelta3

1. Create a copy of your Melee iso in the repo (since you probably don't want to alter your main one).
2. Open up DAT Texture Wizard (on Linux do `WINEARCH=win64 WINEPREFIX=$(pwd)/.wine wine dat-tex-wiz/DAT\ Texture\ Wizard.exe`) and then load your (copy) iso
3. Optionally, go to Disc Details and do the following steps:
   1. Import banner.png as the iso image
   2. Change the Image Name to "Super Smash Bros. Melee: Dylan's Edition" and press enter
   3. Change the Short Title to "SSBM: DE" and press enter
   4. Change the Short Maker to "Melee DE" and press enter
   5. Change the Long Title to "SUPER SMASH BROS. Melee: Dylan's Edition" and press enter
   6. Change the Long Maker to add "/Dylan Turner" and press enter
   7. Hit Ctrl+S to save
4. In the Disc File Tree, under GALE01/System Files/, select "Start.dol," hit "Export" and save it as "main.dol" under `<repo>/code/orig/GALE01/sys/main.dol`
5. Open a terminal and navigate to `<repo>/code/`
6. Run `python configure.py` then `ninja` to build a new main.dol in `<repo>/code/build/main.dol`
7. Go back to GALE01/System Files/ and select "Start.dol" again, but this time import the new `<repo>/code/build/main.dol` and save
8. Close D.T.W
9. Open a terminal and navigate to the `<repo>/crazy-hand/` folder you created. Start crazy hand with the command `java -jar Crazy\ Hand\ v1.31.jar`
10. Select each of the changed characters and load their patch from `<repo>/char-mods/<character>.dat`
11. Save your changes and close Crazy Hand
12. Create a patch via `xdelta3 -e -s vanilla-melee.iso dylans-edition.iso melee-dylans-edition-<version>.patch`

