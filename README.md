# SMD2000
A mini-DTX version of the Amiga 2000 (motherboard)

## SMD 2000 Motherboard
This is the motherboard for the SMD2000 "BUSHFIRE" project, a mini-DTX sized Amiga 2000.
Official project information can be found at Amiga Retro Brisbane projects page:
https://www.amigaretro.com/projects/


## Licensing
Design is open source hardware.
1. Any and all derivative designs must also be open source.
2. No person, business, or other entity associated with this design shall be liable for any damages incurred by anyone as a result of using this design.  If you do not accept this condition do not build the project.
3. Free for private use by anyone.
4. Free for anyone to make for sale, except people associated with A1200.net keycaps.  You guys suck.
5. CERN Open Hardware Licence Version 2 - Strongly Reciprocal CERN-OHL-S) license applies, subject to conditions 1-4 above.
6. Any portions of this design from other projects shall be licensed according to their respective licenses if their licenses are not compatible with CERN-OHL-S or the conditions above.
7. All Other Rights Reserved.


## Requirements
To make this project work you also need to build an Agnus card and a CPU card.  They are documented separately.

The SMD2000 project requires a donor Amiga, either an A500, A500+, A2000, or A600 plus a Gary.


## Useful Links
Bluster - in case you don't have a Buster IC (i.e. your donor machine is an A500):
https://github.com/LIV2/Bluster/tree/master
Bluster drop in replacement is not tested with the SMD2000 yet but there is no reason it will not work (the real Buster is confirmed working).

Open Video Hybrid - in case you don't have a Vidiot:
https://github.com/SukkoPera/OpenAmigaVideoHybrid

Latest RGB2HDMI software can be found at:
https://github.com/hoglet67/RGBtoHDMI/releases


## Notes and Eratta
Serial Port and Mouse Port are the same shape!  Now I know why Commodore used a 25 pin Serial port!  Be extra careful to not connect mouses to the serial port and serial devices to the mouse port otherwise there will be a release of magic smoke!  Recommend using DB9 protector for serial port e.g.: https://www.thingiverse.com/thing:2121877

### ROM
The SMD2000 has address lines for 1 MB or 2 MB ROMs.  Jumpers are present on the upper two address lines to switch between four 512 kb rom images (or two 1 MB images).

If using a Commodore rom or 27C400 eprom put it in the bottom of the socket, i.e. leave pins 1 and 42 on the socket empty (like on A500).  J519 & J520 do nothing in this scenario.

If using a 1 MB or 2 MB rom with multiple images you can switch between them using switches attached to CN519 & CN520; set J519 & J520 to 2-3.  Many users will want a switched Kickstart with KS1.3 and KS3.1/3.2; this can be achieved using a 27C800 with KS1.3 in the lower half and KS3.1 or 3.2 in the top half and connecting a switch to CN519.  You can switch up to four images (or a 1 MB image and two 512 kb images) using a 27C160 and CN520 as well.

If using a 1MB or 2MB custom rom set J519 & J520 to 1-2.

### LEDs
Extra LEDs have been added to the computer.  There are currently three ways to see the power LED, and two for the floppy drive LED (plus the LEDs on the floppy drives themselves).
Power LEDs:
Case: this is the same as in the A2000.  Populate Q302, R307, & C919.  If R308 is not populated the case LED will flash on and off instead of bright and dim when the Guru is about to meditate.  You can populate R308 if you want the LED to "dim" instead of switch off.  Commodore used a 200 ohm resistor in the A2000 and a 100 ohm resisitor on the A500 but optimal size will vary for your particular LED.
LED on motherboard: Populate Q360, R360, C360, & D360.  No "dim" option available.
LED on A500KBD port: fit Q361, R361, C361.  No "dim" option available.

### FDD LEDs
Floppy LEDs added same way as A500 (inverted _MTR0D).  Most users will not want to add a separate Floppy LED so these components are marked "Do Not Populate".
If using either of them populate the pull up resistor R363.
If using case floppy LED populate Q362, R362 & J360.
If using A500KBD port populate Q363 & R364.

NB the LEDs have changed since the final prototype.  The extra LED options (other than for the original case LED) are UNTESTED but there is no reason they will not work since it's simple copy paste.

### Other
Motherboard mounting holes had to be moved a little after the first prototype, and as a result the board was made 4 mm wider than "DTX" specification (on the slots side) but it still fits in the ML09 case.  Be careful if you intend to fit it in a tighter case.


## Fabrication Notes
Mouser part numbers for all components you can buy there are in the metadata for the symbols.  This has been exported as a CSV file, note this CSV file does not state which are Do Not Populate.

Use the interactive Bill of Materials for placing components, ibom.html.

The motherboard is expensive to make, being four layers.  I used JLCPCB, the cost was about $170 AUD for the minimum order of five boards, or a bit under $35 per board.  I chose green because it was the cheapest, they will do other colours for extra cost.  This includes an extra fee of $40 AUD due to the requirement for a 4-Wire Kelvin Test, due to the small size of the vias (this was mandatory from JLC).   Given the board is close to the limitations of JLCPCB I'm OK with that.  Don't specify the Kelvin test at initial checkout, they will add it later.  Even if you do specify it at checkout they will add it later again and you will pay for it twice (you can guess how I know this).  Even with the paying for two Kelvin tests it's way cheaper than PCBWaaaaaaay at USD 187 (about $280 AUD).

Assembly of the motherboard is a lot of work.  You can get JLC to partially assemble the board, I paid $284 AUD for partial assembly of two boards for the first prototype and $450 to partially assemble all five of the second prototype - that's most of the 0805 sized "birdseed" passives, about half the SMD ICs, and most of the headers.  That cost includes $30-40 worth of components on each board which you have to buy anyway, so it's actually a bargain if you consider it in relation to your hourly rate.  Get some mates together to share the upfront cost.  I think it's worthwhile unless you really, really like soldering birdseed.
I've added JLC's part number as a field in Kicad for many of the components so it shows up in their BOM tool, but it's not there for every component, and you will have to do some substitutions since the project was set up to be predominantly purchased from Mouser (I was going to hand solder it), some stuff is out of stock at JLC, and some stuff simply isn't available like the edge connectors.  When you use JLC's tool make sure you save a PDF copy of the BOM page so you know what not to buy from Mouser.  Also be aware if you want two sided assembly they will want you to add rails to the board, make sure they add a v cut so you can break them off after.  It's easier to specify this at the time of order.

This is a self-funded project and none of the companies mentioned have paid me anything.  This information is simply for your information, you can buy your PCB and component from whoever you like.

Finally, I had dramas with the tiny resistor packs every time I had to install them.  They're a real pain in the bum to solder by hand, and because JLC didn't have most of them in stock so I had to do it myself.  If your board doesn't work straight away, try reflowing all the resisitor packs.  If your mouse doesn't move check the resistor packs.  If you're cracking the shits it's probably because of the resistor packs.  You get the picture.  If you have a microscope it's really useful to check each one as you go.

## References
Commodore Amiga References:
Commodore Amiga A500/A2000 Technical Reference Manual.
Commodore schematics for A2000 Rev 4 & Rev 6.2, A500 Rev 6 & Rev 8 (A500+), and A1200 R1D4 schematics.  Scanned originals and amigawiki.org rebuilds referenced.
Coprocessor Expansion and 86 Pin Signals on Amiga Computers by Dave Haynie; this is presumably a Commodore document.

Other References:
DTX Mechanical Interface Specification rev 1.0.
ATX Specification v2.1 & v2.2.
Intel ISA Bus Specification and Application Notes.
Silverstone (r) ML109 case datasheet, www.silverstonetek.com.

Other Projects incorporated into this one:
RGB2HDMI:
https://github.com/c0pperdragon/Amiga-Digital-Video
https://github.com/Bloodmosher/Amiga-VideoSlot-RGBtoHDMI
Video Output:
https://www.pcbway.com/project/shareproject/Commodore_Amiga_DB23_RGB_External_Video
  _Buffer_V6_Compatible_with_GBS_8200_822_00cf763f.html

Symbols:
Symbols and footprints for most parts were downloaded from Mouser/Samacsys, and most were modified to make the schematics more readable.  Samacsys parts probably aren't covered by the Open Source license.  Footprints and symbols for generic parts e.g. jumpers/headers use Kicad libraries. 

Datasheets:
Links to datasheets are in the symbol metadata.
VGA Pinout Guide, https://pinoutguide.com/Video/VGA15_pinout.shtml.
M27C400 & M27C800 EPROM data sheets.
SPC Multicomp DSub9 to DSub25 adapter, http://www.farnell.com.

Technical Guides:
CTS Corporation Application Note: Crystal Basics, CTS Corporation.
A Guide to Debouncing by Jack G. Ganssle © 2004 The Ganssle Group.
555 timer in monostable mode https://todbot.com/blog/2010/01/02/momentary-button-as-onoff-toggle-using-555/.

