# How to install rEFInd

by Freebird54

**rEFInd**  is a boot manager, forked and reworked from the EFI boot control program
called  **rEFIt** . It allows the easy control of multi-boot systems, regardless of what
those systems might be.

Note: It will simplify your life, and the setup, if SECURE BOOT has been disabled
in your UEFI BIOS.

These are the steps you need to install it:

#### 1. Install the Program

`yay refind`

It will probably show you several packages - number 1 from the extras repository should
be your choice. It may even already be installed. When it is installed,

#### 2. run the install script

`refind-install`

The chances are excellent that you now have the capability to boot with rEFInd in control.
If you try it right away, you will most likely see 2 entries for each bootable system on your
computer. If you have only 2, for instance Ubuntu and EndeavourOS, there should be 4
choices on the screen. If you see a lot more than that, did you remember to remove the USB
stick you installed from? Reset and try without it plugged in! OK, you're back (or never left).
As you use the arrow keys to highlight each of your choices, you will notice that a description
of the file that will be booted shows up underneath the row of logos. One entry for each will
be for grubx64.efi and the other will be similar to vmlinuz-linux as EndeavourOS uses. Either
will work. There are other easy things you can do to simplify, or beautify it from here.

* **Give it a customized logo to display for EndeavourOS**

* **Hide the alternative boot choices you won't be using**
* <strong>Add special boot options (such as microcode) to direct boot</strong>

#### 3. Customize your displayed logo (optional)

Because  **EndeavourOS**  is relatively new, the displayed logo for your system is likely to be
Tux - the Linux penguin. If you would rather have the EndeavourOS logo, then you need to have
a copy of it. You can easily find it on the internet with a search. When you have it, it is best to resize
it to 128x128 with the following.

`convert logo-iconname.png -resize 128x128 os_endeavouros.png`
The name shown above  **[os_endeavouros.png]**  as the final outcome is a special name to  **rEFInd**  for displaying a boot choice. To 'activate' that choice,

`sudo cp os_endeavourOS.png /boot/efi/EFI/refind/icons`

When that has been done, The icon you copied will be shown as one of the choices for a boot.

#### 4. Hide the extra entries (optional)

If you want to simplify your visible boot options, you should decide which method of booting
suits you better - either by starting up the grub that was created on the original installation (or
on subsequent updates) or by directly booting the OS. As you highlight each choice, under it is a description of the boot file it will use. If it says the file /EFI/endeavouros/grub64.efi, it will select
and boot the grub entry, from which you can choose the item you wish. If it says that it will boot
from /boot/vmlinuz-linux, it will do a direct boot.  Highlight your choice for hiding, and hit <delete>
and you won't see it again. To UNhide an entry (perhaps to select a fallback kernel), choose the
recycle tool on the lower line.

#### 5.  **Add special boot options (optional) to direct boot**

To do this you will need to edit the refind.conf file. This is usually found (at least on EndeavourOS)
in the  **/boot/efi/EFI/refind**  directory. You will need add a menuentry as below for ensuring your
microcode image is included:

`menuentry "EndeavourOS" {` `` `volume root-endvr` `` `loader /boot/vmlinuz-linux` `` `initrd /boot//amd-ucode.img /boot/initramfs-linux.img}`

Of course, you should specify the correct microcode file for your system instead (intel-ucode.img if you are running an Intel system for example) and you need a label on the partition where boot files
are located.

#### Notes / Troubleshooting:

There are a LOT of other capabilities of  **rEFInd**  that I haven't touched on here. Everything about its
theming can be changed, for example. An example shown in the documentation puts your contact
information on the boot screen, should you be running a laptop and want it back. Many other things
are built in for handling special cases as well.

One of the things I appreciate is that it can pick up and display boot options for USB sticks that have
ISO's on them - whether you are distro hopping, or just needing a live environment for troubleshooting. No need to enter the BIOS for that!

One problem, however, that you may run into is what the program's author calls a 'boot coup', where the installation procedure or a change that causes grub to be updated can replace rEFInd as the boot manager first in the boot order. This can be repaired by efibootmgr - or even more easily by going into the BIOS and reselecting rEFInd as the first boot method in the list in NVRAM. It certainly simplifies keeping things separate and up-to-date on a system like mine with 5 distros on it!

More can be found in the Arch Wiki - and of course, the comprehensive information from the original source of it all:

https://www.rodsbooks.com/refind/

