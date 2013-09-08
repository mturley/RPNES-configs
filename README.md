RPNES-configs
=============

Configuration files for RetroPie software, for the hardware in the RPNES-1 console.

The files in this repo belong on the SD card of the Raspberry Pi after a RetroPie installation.

RetroPie can be found here: http://blog.petrockblock.com/retropie/  (project page and SD card image)

RetroPie's github repo and installation script live at https://github.com/petrockblog/RetroPie-Setup.

The root of this repo is a mirror of the root of the SD card, so you can just copy to the SD card and run a few post-copy steps to install.

The default version of each file is for 4 RetroLink SNES-style USB controllers.  Alternate files have extra extensions for -xbox and -ps3, etc.

The default is also a 4-player setup, since you can just deploy it with 2 controllers and it works as a 2-player setup.

This repo is maintained by Mike Turley (/u/yooman on reddit).  Direct all inquiry to mike@miketurley.com.

A note about the USB ROM copy service
-------------------------------------

IMPORTANT: Do not connect any USB devices containing game ROMs to the Raspberry Pi until after following these installation instructions.  The default RetroPie USB copy service actually copies all your games onto the tiny SD card at USB storage connection time, which I for one do not want.  The replacement script instead maintains symbolic links in the proper place for emulationstation to just find the games right on the USB storage.  No need to copy to SD to play!  Just plug in your game drive and go.

Installation
------------

# Copy the contents of the repo to the root of the SD card you've already installed RetroPie on.

    cp -rv ~/RPNES-configs/* /media/RPI-SD-CARD/

# **YOU ARE NOT DONE**, do not connect game storage yet.  Make sure you have expanded your filesystem with `sudo raspi-config` before proceeding.

# Reinstall the replacement USB ROM copy script by running `sudo ~/RetroPie-Setup/retropie-setup.sh` and selecting `3. Setup`, then scrolling down and choosing to install the USB ROM copy service.  DO NOT use the main options, which will reinstall the whole operating system.  Reboot after this step.

# After rebooting, you can connect a USB storage drive and the link service will create a directory called roms/ on your drive for you, which will contain empty directories for each platform.  These directories are where you should put your game ROM files, extracted from any archives they came in.

# Plug your game USB storage back into the Pi, and restart emulationstation or reboot.  Your system is now playable, enjoy!

# Note that the default configuration is for 1 to 4 of [these specific SNES-style 3rd party controllers from RetroLink](http://www.lukiegames.com/New-SNES-Retro-PC-USB-Controller_p_11155.html).  To use the system with different controllers, you'll need to replace this file: RetroPie/configs/all/retroarch.cfg.  There is an alternate file in that directory suffixed -xbox which works with Xbox 360 controllers (wireless), although there's a lag issue there.
