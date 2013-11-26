RPNES-configs
=============

Configuration files for RetroPie software, for the hardware in the RPNES-1 console.  The files in this repo belong on the SD card of the Raspberry Pi after a RetroPie installation.

RetroPie can be found here: http://blog.petrockblock.com/retropie/  (project page and SD card image).  RetroPie's github repo and installation script live at https://github.com/petrockblog/RetroPie-Setup.

The root of this repo is a mirror of the root of the SD card, so you can just copy to the SD card and run a few post-copy steps to install.  See **Installation** below for details.

This repo is maintained by Mike Turley (mturley on github, /u/yooman on reddit).  Direct all inquiry to mike@miketurley.com, or post an issue on this repo if you have a problem.

#### This revision of the repository is compatible with RetroPie version 1.9.1.


A note about the USB ROM copy service
-------------------------------------

IMPORTANT: Do not connect any USB devices containing game ROMs to the Raspberry Pi until after following these installation instructions.  The default RetroPie USB copy service actually copies all your games onto the tiny SD card at USB storage connection time, which I for one do not want.  The replacement script instead maintains symbolic links in the proper place for emulationstation to just find the games right on the USB storage.  No need to copy to SD to play!  Just plug in your game drive and go.


Installation
------------

1. First, install RetroPie on your SD card.  The easiest way to do this is by [downloading the RetroPie SD card image from the project's download page](http://blog.petrockblock.com/retropie/retropie-downloads/), and then using a standard Raspbian-compatible technique to copy that image to an SD card.  [See here for guides on this process](http://elinux.org/RPi_Easy_SD_Card_Setup).  Personally, I use a little tool called [PiFiller](http://ivanx.com/raspberrypi/) for Mac OSX.  People on Windows have had success with [Win32DiskImager](http://sourceforge.net/projects/win32diskimager/).

2. Connect the Raspberry Pi to a USB keyboard and to the internet, and then boot it up.  It takes a good several minutes sometimes, wait for the RetroPie Project splash screen, and then a little later you'll get either an input configuration screen or an emulator menu.

3. When the machine is fully booted, press F4 on the keyboard to exit and reach a bash terminal.

4. Install dependencies from apt (the default sudo password is "raspberry"):

    `sudo apt-get install git xutils-dev symlinks`
    
5. Clone this repository somewhere and then copy its contents into the home directory:

    `git clone https://github.com/mturley/RPNES-configs.git`
   
    `cp -rv ~/RPNES-configs/* ~/`
    
    Note: this `cp -rv` step will eventually be replaced by integration with the RetroPie-Setup tool or a custom post-install script.

6. **YOU ARE NOT DONE**, do not connect game storage yet.  Make sure you have expanded your filesystem with `sudo raspi-config` before proceeding.

7. Reinstall the replacement USB ROM copy script by running `sudo ~/RetroPie-Setup/retropie-setup.sh` and selecting `3. Setup`, then scrolling down and choosing to install the USB ROM copy service.  DO NOT use the main options, which will reinstall the whole operating system.

8. Reboot the system (IMPORTANT). This activates the changes to the USB ROM link service.  After rebooting, you can connect a USB storage drive and the link service will create a directory called roms/ on your drive for you, which will contain empty directories for each platform.  These directories are where you should put your game ROM files, extracted from any archives they came in.

9. If you're using a [Mausberry Circuits shutdown switch](http://mausberrycircuits.com/) on the Raspberry Pi, as I am in my builds, set it up to properly shut down the machine:

    `wget http://www.mausberrycircuits.com/setup.sh`
    `sudo bash setup.sh`

10. Plug your game USB storage back into the Pi, and restart emulationstation or reboot.  Your system is now playable!

11. Note that the default configuration is for 1 to 4 of [these specific SNES-style 3rd party controllers from RetroLink](http://www.lukiegames.com/New-SNES-Retro-PC-USB-Controller_p_11155.html).  To use the system with different controllers, you'll need to replace the file at `RetroPie/configs/all/retroarch.cfg`.  There is an alternate file [in that directory](https://github.com/mturley/RPNES-configs/tree/master/RetroPie/configs/all) suffixed -xbox which works with Xbox 360 controllers (wireless), although there's a lag issue there.  To generate your own controller mapping for this file, use the `retroarch-joyconfig` command-line tool, [documented here](https://github.com/petrockblog/RetroPie-Setup/wiki/Is-there-another-way-to-set-up-the-gamepad-for-use,-e.g.,-withing-the-snes-emulator%3F).

12. Enjoy!  Use [the issue tracker here on github](https://github.com/mturley/RPNES-configs/issues) for suggestions and bugs, and feel free to contact me [by email](mailto:mike@miketurley.com) or [on reddit](http://www.reddit.com/message/compose/?to=yooman).


Want me to do all this for you?
-------------------------------

I do take custom orders for building and configuring machines with this setup, see my [Parts List and Pricing Rubric here](https://docs.google.com/document/d/1rLLHG-VLm9iHEIwyDLYxpoxHrP2LZxCx-SFpLb31xx0/edit).

NOTE: build orders are currently suspended so I have time to study (I'm a senior in a CompSci BS program).  New orders will be back-orders (think months), and I'll take normal orders again some day soon.
