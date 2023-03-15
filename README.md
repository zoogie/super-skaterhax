# super-skaterhax

## Thanks 
- webkit test cases 
- MrNbaYoh for his blogs
- Yellows8 for the hbmenu loader code: https://github.com/yellows8/3ds_browserhax_common

## Intro

Super-skaterhax is yet another primary userland exploit for the new3ds browser, Skater. It's the successor to [new-browserhax-XL](https://github.com/zoogie/new-browserhax-XL), which was coldly murdered in its sleep by firmware 11.15. RIP.

## What's needed

A new3ds (or new2ds) on firmware:<br>
```
11.15 - 11.16 on all 4 new3ds regions US,EU,JP,KR
```

## Directions (userland)

IMPORTANT: Follow these instructions EXACTLY as this exploit is sensitive to any variance.

0) Make sure the following 3 files are on the sd card root of your 3ds. Go to the release page to find these files and download them. Open the file go inside the correct region folder of your 3ds to find the below files.
```
sdmc:/arm11code.bin
sdmc:/browserhax_hblauncher_ropbin_payload.bin
sdmc:/boot.3dsx
```
1) Start the browser and type in one of the following URLs:
```
https://zoogie.github.io/web/super (USA,EUROPE,JAPAN)
https://zoogie.github.io/web/korea (KOREA)
```
2) After reaching the site, it should say "GO GO!" at the top left but press the star on the bottom left instead.
3) Press "Bookmark this page" then press the bottom-left star again.
4) Tap the icon on the bottom RIGHT of the screen with 3 horizontal dashes.
5) Press Settings then tap Delete Cookies.
6) Press the HOME button on the 3ds to exit the browser. 6.5) OPTIONAL, but recommended if exploit keeps crashing: before next step, power system off, then back on
7) Immediately hit the A button to relaunch the browser (this exit/relaunch thing saves your data in case you're wondering).
8) Tap the GO GO! link on top screen, then approve any prompts that show up. Hbmenu should launch! Retry if you get a yellow screen freeze.

How to RETRY:

0) Relaunch the browser. You should automatically land on the exploit page again (the one with GO GO! link).
1) Start on step 4 above and continue.

NOTE: 
- If for any reason you don't land on the "GO GO!" page after after relaunching the browser, use the bookmark you saved to get back there. Then continue on step 4.
- Some regions may give you an SSL warning before landing on the exploit page on github, just press A to pass these prompts. If you get these, your date/time may be set incorrectly and you should fix it if so.

## Exploit details

This is a Use-After-Free that occures when an svg mask paints a text selection in a certain test case. The webkit test demo this is based on can be found [here](https://github.com/WebKit/WebKit/blob/main/LayoutTests/svg/masking/mask-should-not-paint-selection.html). Implementation details can be found in comments inside this repo, starting with super/index.html. The repo code is not intended for production, since all of the added comments and stuff have likely uncalibrated my offsets.

## Troubleshooting (hbmenu)

- Problem: The 3ds freezes on a yellow screen.<br>
Solution: Try again. Boot rate is about 75-80%. This has always been an issue with *hax homebrew and not specific to this implementation.* If this keeps occurring over and over, it's likely being caused by running browserhax while cfw (luma3ds + boot9strap) is already installed -- don't do this! Follow https://3ds.hacks.guide for proper instructions on how to launch .3dsx homebrew under cfw. Hard freezing with regular screens (ie no solid colored screen) can also indicate running under cfw.

- Problem: I get a "An exception occured" black screen with white text on both screens.<br>
Solution: You already have cfw and there's no reason to run browserhax. Consult [this](https://3ds.hacks.guide/finalizing-setup.html) for instructions on how to run homebrew properly under cfw.

- Problem: The 3ds freezes on some other color screen or "An error has occured" prompt shows up.<br>
Solution: Make sure you have *all* the correct files. Check your region is correct.<br>
At minimum, make sure to have the below 3 files in the sd root as shown.

```
sdmc:/arm11code.bin
sdmc:/browserhax_hblauncher_ropbin_payload.bin
sdmc:/boot.3dsx
```
Note that these are the same files used as in the previous new-browserhax, so no need to change them if they're already there.

- Problem: I still can't get the exploit to work and all the solutions above didn't help.<br>
Solution: Power 3ds off, then on, then go the the Settings sections and select "Reset Save", and then go through the steps again from step 1. (choose Google as your search engine if it asks).

## FAQ

Q: What is SKATER?<br>
A: It's Nintendo's codename for the new3ds browser. It's significantly different from the old3ds browser, Spider, and it thus requires different exploits.

Q: Will you support Spider (old3ds, old2ds)?<br>
A: Not for a long while, at least not from me. I'm done with "double patched" browser exploits with a single firmware update. But who knows, there could be others working on old3ds/Spider!

Q: Why is this exploit "sensitive"?<br>
A: The heap shifts around with even the smallest source or runtime change. Comments, 1 byte url length changes, a simple unexpected tap on the screen -- all of this can shift the heap addresses around a few bytes and stop the exploit. This is a big reason why I didn't use my nice "nbhax" menu I used for the previous browser exploits.

Q: What is that image below GO GO! link?<br>
A: That is a normal .bmp image with nopslide and payload code inserted! Don't touch it -- for office use only!

Q: Where did this browser exploit come from originally?<br>
A: https://github.com/WebKit/WebKit/blob/main/LayoutTests/svg/masking/mask-should-not-paint-selection.html

Q: Why did you name it super-skaterhax instead of super-new-browserhax-XXL?<br>
A: Nintendo's meme naming scheme mockery has run its course, mostly.

Q: Will this exploit be fixed in a firmware update?<br>
A: All I can say is the my 4 previous ones were, but, who knows, the 3ds is 12 years old now.
