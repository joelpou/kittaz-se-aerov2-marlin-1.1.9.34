# KITTAZ as TAZ5 with SE AeroV2 and Marlin v1.1.9.34

This firmware modifies a Lulzbot KITTAZ to work as a TAZ5 using the [SE SingleExtruderAeroV2](https://lulzbot.com/store/lulzbot-se-tool-head-nickel-plated-copper-0-5-mm-kt-cp0136?ref=KT-CP0136#product-description) hotend with [Marlin v1.1.9.34](https://download.lulzbot.com/Software/Marlin/1.1.9.34/) which is last known version to work with KITTAZ (TAZ4) that features a [RAMBO v1.2g board](https://reprap.org/wiki/Rambo_v1.2).

# Resources

1. [How to mount SE AeroV2 toolhead?](https://ohai.lulzbot.com/project/mount-adapter-installation-instructions-taz56/)
2. [How to load filament to E3D Titan Aero Extruder?](https://www.youtube.com/watch?v=Etjmb84w3YU&ab_channel=IT-Works3D)
3. [How to update and flash firmware with Lulzbot Cura?](https://ohai.lulzbot.com/project/flashing-firmware-through-cura-3620/firmware-flashing/)
4. [Lulzbot Gitlab v1.1.9.34 repo](https://gitlab.com/lulzbot3d/marlin/-/tree/5f9c029d153c3cac2728ecbb04a5d45b27810733/)
5. [Lulzbot v1.1.9.34 configurations directory](https://download.lulzbot.com/Software/Marlin/1.1.9.34/)
6. [Great RAMBo review by Thomas Sanladerer](https://www.youtube.com/watch?v=6PHExxK8lLg&t=261s&ab_channel=ThomasSanladerer)


# LulzBot Marlin firmware

This is the development branch of Marlin for LulzBot printers.

The source on this branch can compile firmware for the TAZ and Mini series, as well as all the current toolheads. This firmware also supports some internal R&D prototypes and toolheads.

# Safety and warnings:

**My RAMBO v1.2g X-Axis driver was damaged by previous owner** and had to [modify the firmware header file pins_RAMBO.h](https://3dprinting.stackexchange.com/questions/3925/how-to-switch-motor-outputs-and-use-e1-as-x-in-marlin-firmware) to swap E1 pinouts with X pinouts since I didn't want to buy a new RAMBO board and didn't care about the dual extruder configuration. If you use this repo you probably should use default commented values.

**This repository may contain untested software.** It has not been extensively tested and may damage your printer and present other hazards. Use at your own risk. Do not operate your printer while unattended and be sure to power it off when leaving the room. Please consult the documentation that came with your printer for additional safety and warning information.

# Bash compilation on Linux using "avr-gcc"

Install [avrdude](https://web.engr.oregonstate.edu/~traylor/ece473/webpages/ubuntu_install.html). Run the "build-lulzbot-firmware.sh" from the top level directory. This will build the ".hex" files for every printer and toolhead combination. The ".hex" files will be saved in the "build" subdirectory. 

The script will only build for printer Juniper_TAZ5 and CecropiaSilk_SingleExtruderAeroV2 toolhead. Uncomment other printers/toolheads combos if using different.

Note that I could only build using avr-gcc and didn't really have time to make platformio build work. Building with platformio gives me some compilation errors.

# Compilation using Arduino IDE

To select what firmware to build, modify the lines starting with "//#define" towards the bottom of the "Marlin/Configuration_LulzBot.h" file. Remove the leading "//" and modify the text after "LULZBOT_" and "TOOLHEAD_" so that it specifies the desired printer model or the desired toolhead, as listed in the top of the file.

For example, to compile for the Mini 2, modify the lines such that they read:

  #define LULZBOT_Hibiscus_Mini2
  #define TOOLHEAD_Finch_AerostruderV2

To compile for a TAZ using a standard toolhead, modify the lines such that they read:

  #define LULZBOT_Oliveoil_TAZ6
  #define TOOLHEAD_Tilapia_SingleExtruder

Then, open the "Marlin.ino" file from the "Marlin" subdirectory in the Arduino IDE. Select the board "Arduino/Genuino Mega or Mega 2560" from the "Board" submenu menu of the "Tools" menu and the port to which your printer is connected from the "Port" submenu from the "Tools" menu.

To compile and upload the firmware to your printer, select "Upload" from the "Sketch" menu.
