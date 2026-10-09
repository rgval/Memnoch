# Instructions on Rebuilding Memnoch

## Install Files

### Development
- build-essential
- gh
- git
- gvim
- Kate
- kdevelop
- kdevelop python support
- lint
- pylint
- vim
- VS Code

### Games
- 0 A.D.
- kigo
- kmahjongg
- kmines
- kpatience
- ksudoku
- Warzone

### AV
- gImageReader
- gimp
- libdvd-pkg
- krita
- kubuntu-restricted-extras
- mediainfo
- MusicBrainz Picard
- shortwave
- shotwell
- SkanLite
- Skanpage
- vlc
- Xsane

### System Tools
- bashtop
- bleachbit
- bulk rename
- disk usage analyzer
- Document Scanner
- dolphin
- elisa
- errands
- file-roller
- Fsearch
- gparted
- gprename
- htop
- solaar
- system-config-printer
- variety

### Internet
- curl
- evolution
- filezilla
- Google Chrome
- hexchat
- Konversation
- remmina
- sabnzbd+
- transmission

### Security
- gufw
- keepassxc
- kmymoney

### Manual Install
- Warzone 2100
- Veracrypt
- QT Label 

### Office
- Libreoffice



## After Install Changes

### Enable Flatpak support
Flatpak is a popular package format runs in sandbox environment. Tons of applications support Linux through Flatpak package.

`sudo apt install flatpak`

Next, you may install local flatpak files by running command:

`flatpak install drag-and-drop-flatpak-file-here`

Or, add the Flathub repository into system:

`flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo`

For choice, add --user flag for current user only. Then, use the command in a Flathub app page to install (click down arrow besides “Install” button).

**NOTE:** After enabled Flatpak support, you need a log out and back in to apply the variable changes.

### Install Thunderbird via PPA
The Ubuntu Team members have been maintaining the “Mozilla Team” PPA for many years. The PPA contains the Thunderbird ESR (v140 so far), Firefox ESR, and Firefox stable as .deb packages.
The PPA is “official” but maintained by Ubuntu Team. So far, it supports Ubuntu 26.04, Ubuntu 25.10, Ubuntu 24.04, Ubuntu 22.04, and Ubuntu 20.04.

1. Add the PPA

```
PPA: 
sudo add-apt-repository ppa:mozillateam/ppa
```

2. Setup PPA Priority
The Thunderbird DEB package in Ubuntu repository is a wrapper for the SNAP, which has higher version number! You need to setup a higher priority for the PPA package.
To do so, run command to create & edit config file:

`sudo nano /etc/apt/preferences.d/mozillateamppa`

Here I user nano text editor works in most desktops. You may replace it with gnome-text-editor for default GNOME, or other editor depends on your desktop environment.
When file opens, paste following lines and save it:

```
Package: thunderbird*
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1001
```

For choice, you may add 3 more lines below:

```
Package: thunderbird*
Pin: release o=Ubuntu
Pin-Priority: -1
```

It sets the  priority of thunderbird packages from PPA to 1001, and the one from system repository to -1 which will prevent it from being installed.

3. Install Thunderbird Deb package
Now, you need to run the command below to manually refresh system package cache:

`sudo apt update`

Finally, run apt install command to install the .deb package from PPA:

`sudo apt install thunderbird`

If you everything goes well, it should output that’s getting package from ppa.launchpadcontent.net

### Enable Restricted and Multiverse Repositories

```
sudo add-apt-repository restricted
sudo add-apt-repository multiverse
```

### Setup Firewall and Security Hardening
Security should be a priority. Ubuntu comes with a built-in firewall manager called ufw (Uncomplicated Firewall), but it is disabled by default.
To enable the firewall and block unauthorized incoming connections:

```sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```
To verify the status of your firewall rules:

`sudo ufw status verbose`

10. Clean Up Unused Packages and Cache
After setting up your system and installing all necessary apps, tidy up system repositories and free up disk space by removing leftover dependencies:

```
sudo apt autoremove -y
sudo apt clean
flatpak uninstall --unused -y
```

## System Updates

1. Reduce swappiness for desktop installations like it is suggested for Ubuntu
(= the system will prioritize freeing up parts of physical memory a bit more over using the swap file or partition).

If you are curious you can check the setting before and after the reboot with sudo sysctl vm.swappiness.
`echo -e "# Reduce swappiness for desktop installation (default = 60)\nvm.swappiness=10" | sudo tee /etc/sysctl.d/99-sysswappiness.conf`

(this writes the modified value to your system)
The change will only be applied after a reboot


2. Reduce systemd timeouts for desktop installations like KDE suggests for Plasma in their Distribution/Packaging Recommendations
(= the system will not "hang" for 90 seconds - which is the default value - from time to time when logging out, rebooting or shutting down).

I am still quite conservative here and use 15 seconds because on older machines it has seldom taken as long as 10–14 seconds for certain processes to quit gracefully by themselves (for example: KDE neon uses 16 seconds, TUXEDO OS and Garuda KDE use 10 seconds).
`sudo mkdir -p /etc/systemd/system.conf.d && echo -e "# Reduce timeout (default = 90s)\n\n[Manager]\nDefaultTimeoutStopSec=15s" | sudo tee /etc/systemd/system.conf.d/99-systemtimeout.conf`

(this writes the modified value for the system processes to your system)

`sudo mkdir -p /etc/systemd/user.conf.d && echo -e "# Reduce timeout (default = 90s)\n\n[Manager]\nDefaultTimeoutStopSec=15s" | sudo tee /etc/systemd/user.conf.d/99-usertimeout.conf`

(this writes the modified value for the user processes to your system)
The change will only be applied after a reboot


3. Change GRUB (the boot loader) to show the boot menu for 1 second in single-boot setups
(= only Kubuntu is installed - this makes the boot menu much easier to access whenever you might need it).

Makes a backup of your /etc/default/grub​ file first

`sudo cp /etc/default/grub /etc/default/grub.orig`

Make GRUB show the boot menu
    
`sudo sed -i 's/GRUB_TIMEOUT_STYLE=hidden/GRUB_TIMEOUT_STYLE=menu/' /etc/default/grub`

Write the timeout value to your system

`sudo sed -i 's/GRUB_TIMEOUT=0/GRUB_TIMEOUT=5/' /etc/default/grub`

Keeps the timeout value if GRUB has "problems" with a partition - could be e.g. Btrfs or LVM)

`echo -e "\n# Match RECORDFAIL_TIMEOUT to TIMEOUT\nGRUB_RECORDFAIL_TIMEOUT=​\$GRUB_TIMEOUT" | sudo tee -a /etc/default/grub`

Update your GRUB boot loader with the new values

`sudo update-grub`

4. Update your system and your programs for the first time

This is generally one of the first things you should do after installing any operating system.
This updates your installation

```
sudo apt update && sudo apt full-upgrade
sudo apt autopurge && sudo apt autoclean
```


6. Install missing essential software for desktop installations like
    • multimedia codecs etc.
    • Microsoft Web and replacement fonts.

    sudo apt install kubuntu-restricted-extras gstreamer1.0-vaapi fonts-crosextra-carlito fonts-crosextra-caladea


7. If you have a DVD or Blu-ray drive, install libdvdcss to be able to play back e.g. encrypted video DVDs.

    • sudo apt install libdvd-pkg
(this installs the play back for encrypted media)
    • sudo dpkg-reconfigure libdvd-pkg
(this activates the play back for encrypted media)

    

Bonus - 6 individual and potentially less important things to do:

Everything with a grey background behind a single "⦁" is a whole command and has to be copied into Konsole as a whole - even if it is longer than one line.


c. Enable the X11 session additionally to Wayland - like openSUSE Tumbleweed does and like TUXEDO OS offers during installation
(e.g. because you encounter problems in Wayland or use certain programs that require a “real” X11 session).
sudo apt update && sudo apt install plasma-session-x11

(this installs the X11 session)

Next be sure that “Automatically log in:” is off
in -> System Settings -> Colours & Themes (section: Appearance & Style) -> Login Screen (SDDM) -> [Behaviour…] (this is a button at the top).
Now
• reboot
and click on "Desktop Session: Plasma (Wayland)" and choose "Plasma (X11)" in the lower left corner of the log in screen to use X11 instead of Wayland.

From now on you can always switch back and forth between X11 and Wayland simply by logging out and choosing the desired session.
Note: Occasionally switching directly between X11 and Wayland sessions does not work reliably - instead a system restart is required.​


d. Always start with an empty session
(e.g. for stability, performance or security reasons).

Go to -> System Settings -> Session (section: System) -> Desktop Session -> Session Restore
and set “On login, launch apps that were open:”
to “Start with an empty session”.
Click [Apply].

You will have to log out and in again or reboot to apply the change.


e. Disable fast user switching
(e.g. for security or performance reasons in multi-user setups).
    • echo -e "\n[KDE Action Restrictions] [\$i]\naction/switch_user=false\naction/start_new_session=false" | sudo tee -a /etc/xdg/kdeglobals
(this writes the modified values for all users to your system)
You will have to log out and in again or reboot to apply the change.


f. Enable a local firewall
(e.g. if you don't connect to the internet via a modern router with an integrated firewall - please check with your router's manufacturer - or if you connect to the internet in a different way).

Go to -> System Settings -> Wi-Fi & Internet (section: Networking) -> Firewall
enter your password
and change the slider at the top from "Disabled" to "Enabled".
Finally, you must enter your password two more times.

The local ufw firewall is now enabled with default settings.

Last edited by Schwarzer Kater; Jun 01, 2026, 06:54 AM. Reason: added claydoh's suggestion to step



2. Reduce swappiness for desktop installations like it is suggested for *Ubuntu and like e.g. TUXEDO OS also does it
(= the system will prioritize freeing up parts of physical memory a bit more over using the swap file or partition).
If you are curious you can check the setting before and after the reboot with sudo sysctl vm.swappiness.
    • echo -e "# Reduce swappiness for desktop installation (default = 60)\nvm.swappiness=10" | sudo tee /etc/sysctl.d/99-sysswappiness.conf
(this writes the modified value to your system)
The change will be applied with the reboot after step 6. (7.)

Google Chrome
# 1. Download the latest stable Google Chrome package
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

# 2. Install the package and automatically set up the official repository
sudo apt install ./google-chrome-stable_current_amd64.deb
