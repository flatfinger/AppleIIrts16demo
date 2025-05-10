# AppleIIrts16demo
Demo of code to read DOS 3.3-format sectors

This is a slightly cleaned up demo of some code I wrote to scatter-load Apple II DOS3.3 sectors in a single-pass read without need for extra buffering.  The preboot code uses extra buffering and relies upon the nybble table created by the boot PROM, since it needs to fit within 256 bytes.  This application is a simple slide show that will display 16 pictures stored on a disk in in DOS 3.3 sector order, stored two per track.  For this project, I've included some miscellaneous pictures I threw in for testing purposes; no copyright on the images is claimed.

This demo is hard-coded for a floppy controller in slot 6, but will boot off either drive #1 or #2.  It will use the drive it booted from until a user hits "1" or "2" to select a disk.  For testing, it's probably most convenient to have a floppy which contains a sector-copy of the disk image, but then use a drive emulator to boot off test versions of the code and switch drives to read data from the floppy.

The code is written for the CC65 tool set, though at present it doesn't use the C compiler.  The a.batSample shows how to build the code with that toolset.

Feedback is welcome.  Anyone who wants to use the code elsewhere is free to do so; credit back to the flatfinger github repository would be appreciated.

Points of interest:

1. I don't really like the head movement code, but for my projects I need a head movement code that operates on 1/4-track steps.

2. At present I don't have any timeout logic, but reads will abort if Esc is hit.  This is far from elegant, but this is merely proof of concept.

3. The worst-case time between byte reads at one spot going between read loops is 32 cycles.  This occasionally causes hiccups on reads, but they get detected and work successfully on the retry.  A production-worthy loader should unroll the last loop iteration of the previous loop to fix this, but at the moment, the occasional errors show that the error detection and retry logic is working.
