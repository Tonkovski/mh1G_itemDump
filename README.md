# mh1G_itemDump
Monster hunter 1j&amp;G's memory values for inventory items &amp; equipment, and more.

(God knows if I'm expressing myself clearly in English, let me know if I am being vague or having typos.)

## Introduction

Monster Hunter 1j&G, journey in such a typical old-school game reminds us of the good old times right? Not until you accidentally lost your data in a "virtual *fire* accident" and all those precious *memories* -  whether they are physical *memcards* or not - all suddenly become *CloudFlare*d...

Sorry for those really bad puns. Especially when these things really happened. So instead of starting over with the game again bare-handed, "Spawning items from nowhere" using CheatEngine or other means seems like a better choice.

So this is how the repository helps: **Quick gears & items value lookup, while locating the exact memory address to fit them in.**

## Disclaimer

* Some comrades in the Discord channel argues that *cheating* in such a classical game is sort of a *sin*, and I partially agree with that. **The tutorial here is for "save rebuild" purposes.**
* As a newcomer myself (whose first MH being *Monster hunter World*), I advise every newcomer to **take the lessons** - whether taught by *Prof. Yian Kut-ku* or by *Mr. Diablos* - **before trying out those "clever" thoughts**.
* ***Warning:* Everything in this tutorial goes untested - and will never be tested - in online sessions, only do it offline!** Cheating online may have unpredictable effects on the server, let along saying that it can possibly be an insult to other players and all the contributors in this community.
* **Tampering with memory can ruin the game save, make sure regular backups are made.**
* ~~No monsters were harmed during the developing period of this tutorial.~~ OK, I admit killing an *Aptonoth* or two for testing purposes, sorry about that.

## Tutorial: How to locate the addresses?

Sorry for those who actually owns a PS2, this method is intended for PCSX2 users, but you can always copy the simulation data into a physical MC, can you?

The basic knowledge to use CheatEngine is required, if not, just Google it out.

### Preliminaries

* Money, items (whether in storage or in poach) and equipment are stored in fixed locations each time the game is loaded. That is to say, the offset from the base address of EEmem is fixed. 
* Money is stored as a 4-byte integer.
* Item takes up 4-byte memory. The lower 2 bytes store the hex value of certain item, and the higher 2 bytes store the quantity of it.
  * E.g., for 10 `Potion` (0x0001) in MH1j, it looks like `01 00 0A 00`, while for 100 `Monster Fluid` (0x011D) it will be `1D 01 64 00`, notice how Little-endian works when tackling multi-byte data.
  * The quantity of each item can be "overcharged" by memory-tampering, exceeding the maximum stack number. **This feature goes untested, use at own risks**.
* Equipment takes up 6-byte memory. The 1st byte is always 0x01, the 2nd byte indicates the variety of equipment, the 3rd & 4th bytes indicates the hex value of certain equipment of that variety, and the last 2 bytes goes `00 00`.
  * E.g., for `Iron Katana  "Grace"` in MH1j it will be `01 06 0B 00 00 00`, while for `Origin Knife G` in MHG it will be `01 06 50 01 00 00`.

### Methods for PCSX2 v1.6.0

The basic address of EEmem is always at `0x20000000`. Based on this info, a few examples are given using offsets provided by spreadsheets...

* Money address for MH1j is `0x20000000 + 0x3C6FE0 = 0x203C6FE0`.
* Slot No.**m** of item box for MH1j begins in address `0x20000000 + 0x3C7184 + (m - 1)*4`.
* Slot No.**n** of equipment box for MHG begins in address `0x20000000 + 0x32C254 + (n - 1)*6`.

### Methods for PCSX2 v1.7+

The basic address of EEmem changes every time the program restarts. Thankfully, we can always use the `eemem` pointer in CheatEngine to locate the basic address. More info is available at [this page]([PCSX2 1.7+ Cheat Engine Script Compatibility](https://forums.pcsx2.net/Thread-PCSX2-1-7-Cheat-Engine-Script-Compatibility)).

Based on such info, a few examples are given using offsets provided by spreadsheets...

* Money address for MH1j is `eemem + 0x3C6FE0`.
* Slot No.**m** of item box for MH1j begins in address `eemem + 0x3C7184 + (m - 1)*4`.
* Slot No.**n** of equipment box for MHG begins in address `eemem + 0x32C254 + (n - 1)*6`.

## What's next

This harshly scrached tutorial is written during the gaps of my heavy school work, without warranties of any kind. If more time is devoted in the future (which is not very possible), certain things can be achieved:

* Fix typo & mistakes, if there exists any.
* More information added in the spreadsheet.
* A brand new CheatSheet for the game.

Feel free to fork & submit issues. And huge thanks for starring this repository, it will encourage me a lot.

## Acknowledgments

* MH1j in-game English text data from *viciousShadow*.
* MHG in-game English text data from *Yuzu*, and from joint efforts of *amaillo* and *pepesito1* respectively.
* Reference data from MH1j/G wiki pages.
* Commendations to every pioneers in **MH Oldschool** site for contributing to the perfect retro-style forum & platform.
