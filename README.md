# lenovo t470 hackintosh
![obligatory neofetch](https://a.iliyan.me/kzydto.png)

### specs
cpu: i5-6300U

gfx: hd 520

this guide **will not work** with other models of t470!

### what's working
- iGPU
- audio with voodooHDA
- ethernet
- usb 3.0
- sd reader
- wifi (i'm using a usb dongle but BCM94325Z should work)
- trackpad, trackpoint, and 3 buttons
- battery display
- nvme ssd
- sleep 

### what's not working
two brightness-related patches i took from [tluck's repo](https://github.com/tluck/Lenovo-T460-Clover) didn't work with my machine so the brightness can't be changed.

also, the touchscreen on my model doesn't work. working on getting that to work soon.

## instructions
### what you'll need
- 8gb+ usb stick
- a working mac/hackintosh (or, use muh_vanilla.md guide on win/linux)

### making the installer
1. find your volume name using `diskutil list` in terminal or Disk Utility.
2. once you know your volume name, make the installer. i'm assuming your installer app is in /Applications. run `sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume` where MyVolume is the name of your volume. if your volume has spaces in it, represent a space as such: `a\ b` so the space is `\ `.
3. hit enter, type your password, and it will make the installer. once it's done, install clover by clicking [here](https://sourceforge.net/projects/cloverefiboot/files/latest/download) to download the latest version.
4. open the pkg and for the destination select choose "Install macOS Mojave", go to the next page and customize per these options, then click install:

![clover](https://a.iliyan.me/hkwzzx.png)

### installing the efi folder
1. open terminal and type `diskutil list`. find your usb drive and find the efi partition. normally it's `diskXs1` where X is a number. once you know it, do `diskutil mount diskXs1` and you will see an EFI partition mounted into Finder. 
2. clone this repo / download it as a zip, and copy the efi folder from here into the efi partition. if there are any conflicts, just click replace. 

### installing macOS
1. take out your usb from your mac/working hack, and go to your t470. plug in the usb, and enter the boot menu by spamming the f12 key.
2. select the usb, hit enter, wait for clover to load, and in clover select the installer.
3. once it boots up, open Disk Utility, partition your ssd (do t470 machines have hdd?) and quit. then, open the installer, select your ssd, and install.
4. on the first restart, go back into the boot menu and select the usb. boot into "macOS Install" on your ssd. it will now complete installation.
5. when it restarts again, go back into the boot menu, select the usb, and boot into "macOS" on your ssd. you can set up your hackintosh now!

### setting up your hackintosh
once you've got everything installed, you need to set up the hackintosh.

follow the setup wizard and select "my computer does not connect to the Internet" if prompted. once you get into the main macOS screen, unplug the usb and plug it back into your mac or working hack.

download the following:
- [clover configurator](https://mackie100projects.altervista.org/download-clover-configurator/)
- any drivers you need for a usb wifi dongle if you use one

copy what you downloaded to the "Install macOS Mojave" partition on your usb.

after that, plug it back into your t470 and open clover configurator. if it does not open, right-click it and select open.

in clover configurator, select "Mount EFI" on the sidebar and find the partition with identifier `disk0s1`. that is your efi partition aka esp. 

![esp](https://a.iliyan.me/mdwol.png)

in the "Efi Partitions" section of Mount EFI, find `disk0s1` and click Mount Partition. enter your password if prompted.

now, select whatever other efi partition is in your Efi Partitions section. this is your USB's efi partition. mount it as well.

open the usb efi partition in finder. copy the EFI folder, and then open your ssd's efi partition and paste it. replace anything that may need to be replaced.

you've set up your efi partition!

### end / credits
that should be it. if you're having any issues with the repo or your hack feel free to contact me.

shoutout to:
- [rehabman](https://github.com/RehabMan) for his iGPU config.plist that i used
- [tluck](https://github.com/tluck/Lenovo-T460-Clover) for the ssdt's and other patches/config
- [maemo](https://gitlab.com/maemo8086/thinkintosh_t480/tree/master) for the theme and other misc kexts and help
- [r/hackintosh discord](https://discord.gg/u8V7N5C) for helping me out

### contact
email: introvert@riseup.net

or, just make a github issue and i'll respond.

thanks!
