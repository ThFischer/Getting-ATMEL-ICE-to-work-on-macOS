# Getting ATMEL-ICE to work on macOS (verified with Catalina 10.15.7)

MacOS may grab the Atmel-ICE USB device and prevent access.
Folllow these instructions ([found here](https://www.avrfreaks.net/comment/2394561#comment-2394561)): 
1. `sudo chown -R root:wheel AtmelICE.kext`
2. `sudo mv AtmelICE.kext /Library/Extensions/AtmelICE.kext`
3. `sudo kextload /Library/Extensions/AtmelICE.kext`

If you get a permissions error:
1. `sudo rm -rf /Library/Extensions/AtmelICE.kext`
2. Restart the Mac and get into recovery mode (hold down CMD + R while booting)
3. Mount the OS drive by choosing the Disk Utility, select the drive and mount it from the menu.
4. Open a terminal by going to the Utilities menu at the top of the screen and then Terminal
5. Remove the driver from /Volumes/your volume/Library/StagedExtensions/Library/Extensions
   `rm -rf /Volumes/your volume/Library/StagedExtensions/Library/Extensions/AtmelICE.kext`
6. Close the terminal and restart the computer
7. Follow the steps (1…3) in the first part of this post and you should have a working driver

Test with avrdude (e.g. for ATmega2560):

`avrdude -c atmelice_isp -p ATmega2560`

Expected output is something similar to:

    avrdude: AVR device initialized and ready to accept instructions
    Reading | ################################################## | 100% 0.00s
    avrdude: Device signature = 0x1e9801 (probably m2560)
    avrdude: safemode: Fuses OK (E:FD, H:D8, L:FF)
    avrdude done.  Thank you.
