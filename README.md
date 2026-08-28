**What**

I have a set of changes that could be applied to the current version 1.0d of 
Aotta's PiColeco project, which should resolve a few issues.
https://github.com/aotta/PiCOLECO

**Why**

In my development process, I needed a PiColeco but I found it wasn't working 
on a heavily modified ColecoVision that I use for fine-tuning timing.  I needed
to redesign the PCB so it has a solid ground to eliminate ground-bounce for my
instrumentation to be most effective.  Code refinement was tested on the HMCVS.

**The heavily-modified CVS (HMCVS)**

This CVS has no LS components or original memory and runs at 3.1 watts without 
a cartridge with a custom power supply.  CVS turned off uses 0.2W.  With the 
PiColeco, I measured 3.6W.  Most of the components are AHCT and HCT, with a
62c256 for system memory and another for video memory. All of the logic signals 
have fast edges and faster propagation.  Standard cartridges, as well as my 
flash-chip cartridges (29c160, 39SF040, etc) with AND-gate logic combining the 
block enable lines, all work well with it when hardware is directly on the bus.

**The 1.0d PiColeco code (SDK 2.2)**

Cartridge would not start up at all.  I started recompiling with a delay on the
gpio call that gets all the pins, wrapping the call in an inline function and
applying it to most of the pin reads.  This allowed the menu to come up on my
HMCVS and select a game.  I found a timing range that worked well, using 
assembly NOP's, but it was always quirky.  Menu lines wouldn't de-highlight
and mess up the menu, games would have their own quirks or crash, some games
wouldn't work at all.  Then I discovered the bug causing the game not to start 
without a manual reset was related to the issues I was having. So I've 
re-written a few blocks of code, and resolved some or most issues.

**The new PCB**

You can take these gerbers and produce them yourselves, they are an overall
upgrade over the original PCB and recommended for all further use.

**Why Here**

I'd like some feedback from those who can test this on a fully original CVS.
The ones here are all modified to some degree and this code is now working on
all of them.  Also I needed a place to link for Aotta to review the work.
