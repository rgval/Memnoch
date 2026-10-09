# Instructions on Rebuilding Memnoch

## Install Files

### Development
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
- gprename
- htop
- solaar
- system-config-printer
- variety

### Internet
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

`PPA: `
`sudo add-apt-repository ppa:mozillateam/ppa`

2. Setup PPA Priority
The Thunderbird DEB package in Ubuntu repository is a wrapper for the SNAP, which has higher version number! You need to setup a higher priority for the PPA package.
To do so, run command to create & edit config file:

`sudo nano /etc/apt/preferences.d/mozillateamppa`

Here I user nano text editor works in most desktops. You may replace it with gnome-text-editor for default GNOME, or other editor depends on your desktop environment.
When file opens, paste following lines and save it:

`Package: thunderbird*`
`Pin: release o=LP-PPA-mozillateam`
`Pin-Priority: 1001`

For choice, you may add 3 more lines below:

`Package: thunderbird*`
`Pin: release o=Ubuntu`
`Pin-Priority: -1`

It sets the  priority of thunderbird packages from PPA to 1001, and the one from system repository to -1 which will prevent it from being installed.

3. Install Thunderbird Deb package
Now, you need to run the command below to manually refresh system package cache:

`sudo apt update`

Finally, run apt install command to install the .deb package from PPA:

`sudo apt install thunderbird`

If you everything goes well, it should output that’s getting package from ppa.launchpadcontent.net
