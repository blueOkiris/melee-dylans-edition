# Super Smash Bros. Melee: Dylan's Edition

## Description

A new experience for those who love Super Smash Bros melee (a mod)

Created using these fine tools:

- Crazy Hand
- DAT Texture Wizard
- Melee Code Manager
- The Melee Decompilation Effort

Engine changes from base game:

- Universal Wall Jump Mechanic
   + I.e. all characters can now wall jump
- Universal 4-Frame L-Cancelling:
   + Every L-cancelled aerial has a lag of 4 frame instead of the lag getting divided by some factor. Very similar to Smash 64's Z-cancelling
   + No longer feels like "negative when missed" but rather "positive when hit."
   + Also, bigger L-Cancel window (10 frames)
   + 4 Frames so you don't accidentally shield after (4-frames is typically base landing lag as well)
- Universal 4-Frame Jump Squat
   + Consequence of consistent wave dash as well
   + 4 Frames because that's the most common jump squat
   + Not really Nerf/Buff I think (except *maybe* Fox nerf bc he's so technical and a huge buff to G-dorf and Bowser), but potentially:
      * Buffs:
         - DK
         - Ganondorf
         - Falco
         - Bowser
         - Puff
         - Link
         - Mewtwo
         - Roy
         - Yoshi
         - Zelda
      * Nerfs:
         - Fox
         - ICs
         - Kirby
         - Pichu
         - Pikachu
         - Samus
- Default to tournament settings and characters and stages unlocked by default

Character-specific changes from base game:

- Game & Watch as a Functioning Character (ongoing):
   + Shield Size: 10.75 -> 18 (just enough to cover himself)
   + Weight: 60 -> 70 (same as Kirby but higher than Puff; still dies early, but not absurdly so since he doesn't have a kit to make up for it)
   + Wall Jump H Vel and V Vel: 1.3, 2.3 -> 1.0, 1.8 (makes it so he doesn't just die from using it now that he has one)
   + Up-B
      * Angle: .524 (30 degrees) -> 1.047 (60 degrees)
      * Landing Lag: 40 -> 30
      * Can face any direction
   + Down-Smash: (actually a kill move):
      * Angles: 20, 80 -> 361, 90 (kill top easier and down sdi causes off stage bad angle)
      * Knockback: 10, 60 -> 40, 60 (stronger edge hitbox)
      * Knockback Growth: 50, 90 -> 70, 90 (strong edge hitbox)
      * Swap X Offsets and to 3400, 1600 and size to 800, 1400 (bc it makes more sense; edge of hammer sends out, while meat of it sends up)
   + Spot Dodge: 2-12-20 -> 2-16-8 (based on Fox's; an actually useful spot dodge)
   + Bacon:
      * Angle: 70 -> 90 (Help in setting up follow ups for getting in)
      * Attribute: Normal -> Fire (It's hot bacon; makes sense)
      * Damage: 4 -> 6 (Indirectly increases hitstun)
      * Frame Rep Hit Starts On: 3 -> 1 (can shoot out the bacon quickly)
      * Count: 5 -> 3 (nerf to couteract speed buffs)
      * Hspeed, Vspeed: 1.0, 1.0 -> 2.5, 0.5 (more useful in neutral than slow up)
      * Duration stale rests on ground: 30 -> 60 (can be used to set traps)
      * Ground: 1, 18, 20, 22, 35 -> 1, 8, 1, 1, 13 (to make the 3 come out faster)
      * I would do Air: 1, 16, 30 -> 1, 6, 11 (same but air) BUT it messes up side-b for some reason, so it's left alone. Air is now slower than ground
   + TODO: Fix absurd down-b lag and incentivize use and make aerials actually aerials not special moves (allow L-cancelling)

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
- Melee Code Manager v4.4.1 (rename in your repo to `melee-code-mgr`)
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
12. Open up Melee Code Manager and open the iso in it
13. Go to "Default Game Settings," select set to Tournament Defaults and save
14. Go to "Mods Library" and add a path to "mcm-mods.txt"
15. Enable the Unlock mod
16. Create a patch via `xdelta3 -e -s vanilla-melee.iso dylans-edition.iso melee-dylans-edition-<version>.patch`

