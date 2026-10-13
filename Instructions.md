# Instructions on Rebuilding Memnoch

## Configure Network
Check the IP address

```bash
ip addr
```

If the IP address is not 192.168.1.10, it need to be changed

Verify the Connection Name:

```bash
nmcli connection show
```

Changing the IP Address:

1. Change the IP address and Subnet (e.g., /24 for 255.255.255.0)

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.addresses 192.168.1.10/24
```

2. Set the Gateway IP

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.gateway 192.168.1.1
```

3. Set the DNS servers (separated by spaces if multiple)

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dns "192.168.1.1 8.8.8.8 8.8.4.4"
```

4. Switch the method from DHCP (Automatic) to Manual

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.method manual
```

5. Apply the Changes

```bash
sudo nmcli connection down "Wired connection 1" && sudo nmcli connection up "Wired connection 1"
```

6 Verify the IP Address change 

```bash
ip addr
```

## Install Files

### Development
- build-essential
- gh
- git
- jsonlint
- kate
- kdevelop
- kdevelop-python
- neovim
- pyflakes3
- pylama
- pylint
- python3-flake8-class-newline
- python3-flake8-class-newline
- python3-flake8-deprecated
- python3-flake8-import-order
- python3-flake8-quotes
- shellcheck
- vim
- vim-ale
- yamllint

```bash
sudo apt install -y build-essential gh git kate kdevelop kdevelop-python jsonlint neovim pyflakes3 pylama pylint python3-flake8-class-newline python3-flake8-deprecated python3-flake8-import-order python3-flake8-quotes shellcheck vim vim-ale yamllint
```

### Games
- 0 A.D.
- kigo
- kmahjongg
- kmines
- kpat
- ksudoku

```bash
sudo apt install -y 0ad kigo kmahjongg kmines kpat ksudoku
```

### AV
- fonts-crosextra-carlito
- fonts-crosextra-caladea
- gImageReader
- gimp
- gstreamer1.0-vaapi
- libdvd-pkg
- krita
- kubuntu-restricted-extras
- mediainfo
- picard
- shortwave
- shotwell
- vlc

```bash
sudo apt install -y fonts-crosextra-carlito fonts-crosextra-caladea gimagereader gimp gstreamer1.0-vaapi libdvd-pkg krita kubuntu-restricted-extras mediainfo picard shortwave shotwell  vlc
sudo dpkg-reconfigure libdvd-pkg
```


### System Tools
- bashtop
- bleachbit
- filelight (disk usage analyzer)
- dolphin
- elisa
- errands
- file-roller
- Fsearch
- gparted
- gprename
- htop
- simple-scan
- skanlite
- skanpage
- solaar
- system-config-printer
- variety
- xsane

```bash
sudo apt install -y bashtop bleachbit filelight  dolphin elisa errands file-roller fsearch gparted gprename htop simple-scan skanlite skanpage solaar system-config-printer variety xsane
```

### Internet
- curl
- evolution
- filezilla
- hexchat
- Konversation
- nfs-common
- remmina
- sabnzbdplus
- transmission
- wget

```bash
sudo apt install -y curl evolution filezilla hexchat konversation remmina sabnzbdplus transmission wget
```

### Security
- gufw
- keepass2
- keepass2-doc
- keepass2-plugin-hibpofflinecheck

```bash
sudo apt install -y gufw keepass2 keepass2-doc keepass2-plugin-hibpofflinecheck
```

### Office
- Libreoffice
- kmymoney
```bash
sudo apt install -y libreoffice kmymoney
```

### Enable Flatpak support
Flatpak is a popular package format runs in sandbox environment. Tons of applications support Linux through Flatpak package.

```bash
sudo apt install flatpak
sudo flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

### Manual Install
- Warzone 2100 - Requires Flatpak
```bash
flatpak install -y flathub net.wz2100.wz2100
flatpak run net.wz2100.wz2100
```
- Veracrypt
```bash
wget https://github.com/veracrypt/VeraCrypt/releases/download/VeraCrypt_1.26.29/veracrypt-1.26.29-Ubuntu-26.04-amd64.deb
sudo apt install ./veracrypt-1.26.29-Ubuntu-26.04-amd64.deb
```
- gLabels-qt 4.0
```bash
#https://github.com/j-evins/glabels-qt
sudo add-apt-repository -y ppa:krisives/glabels-qt
sudo apt update
sudo apt install -y glabels-qt
```
- Calibre
```bash
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin
```

- Google Chrome
```bash
#Download the latest stable Google Chrome package
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
#Install the package and automatically set up the official repository
sudo apt install ./google-chrome-stable_current_amd64.deb
```

- Install VS Code
```bash
wget -O vscode.deb "https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64"
sudo apt install -y ./vscode.deb
```

- Install M4B-tool (https://github.com/sandreas/m4b-tool)

  Install dependencies
  ```bash
  sudo apt install -y ffmpeg fdkaac php-cli php-intl php-json php-mbstring php-xml php-curl php-zip
  ```

  Install mp4v2-utils (https://github.com/enzo1982/mp4v2/ or https://mp4v2.org/)
  ```bash
  wget https://github.com/enzo1982/mp4v2/releases/download/v2.1.3/mp4v2-2.1.3.tar.bz2
  bunzip2 mp4v2-2.1.3.tar.bz2
  tar xvf mp4v2-2.1.3.tar
  cd mp4v2-2.1.3
  ./configure && make && sudo make install
  ```
  Install / upgrade m4b-tool
  ```bash
  sudo wget https://github.com/sandreas/m4b-tool/releases/download/v0.5.2/m4b-tool.phar -O /usr/local/bin/m4b-tool && sudo chmod +x /usr/local/bin/m4b-tool
  ```

  Check installed m4b-tool version
  ```bash
  m4b-tool --version
  ```

  Install Tone
  ```bash
  wget https://github.com/sandreas/tone/releases/download/v0.2.5/tone-0.2.5-linux-x64.tar.gz
  tar xzf tone-*.tar.gz
  sudo mv tone*/tone /usr/local/bin/
  tone --help
  ```
- GitHub Desktop

  Download and add the GPG security key
  ```bash
  wget -qO - https://mirror.mwt.me/shiftkey-desktop/gpgkey | gpg --dearmor | sudo tee /etc/apt/keyrings/mwt-desktop.gpg > /dev/null
  ```
  Add the software repository source
  ```bash
  sudo sh -c 'echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/mwt-desktop.gpg] https://mirror.mwt.me/shiftkey-desktop/deb/ any main" > /etc/apt/sources.list.d/mwt-desktop.list'
  ```
  Update package lists and install GitHub Desktop
  ```bash
  sudo apt update
  sudo apt install github-desktop
  ```

- Thunderbird

  Add the PPA
  ```Bash
  sudo add-apt-repository ppa:mozillateam/ppa
  ```
  Setup PPA Priority
  `sudo nano /etc/apt/preferences.d/mozillateamppa'
  
  ```bash
  Package: thunderbird*
  Pin: release o=LP-PPA-mozillateam
  Pin-Priority: 1001
  
  Package: thunderbird*
  Pin: release o=Ubuntu
  Pin-Priority: -1
  ```
  Install Thunderbird Deb package
  ```bash
  sudo apt update
  sudo apt install thunderbird
  ```
- NordVPN
```bash
sh <(wget -qO - https://downloads.nordcdn.com/apps/linux/install.sh) -p nordvpn-gui
```

- Enable Restricted and Multiverse Repositories
```bash
sudo add-apt-repository restricted
sudo add-apt-repository multiverse
```

- Clean Up Unused Packages and Cache
After setting up your system and installing all necessary apps, tidy up system repositories and free up disk space by removing leftover dependencies:
```bash
sudo apt autoremove -y
sudo apt clean
sudo apt autopurge
sudo apt autoclean
flatpak uninstall --unused -y
```

## After Install Changes



### Setup Firewall and Security Hardening
Security should be a priority. Ubuntu comes with a built-in firewall manager called ufw (Uncomplicated Firewall), but it is disabled by default.
To enable the firewall and block unauthorized incoming connections:

```sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```
To verify the status of your firewall rules:

`sudo ufw status verbose`



## System Updates

1. Reduce swappiness for desktop installations like it is suggested for Ubuntu
If you are curious you can check the setting before and after the reboot with `sudo sysctl vm.swappiness`.
The change will only be applied after a reboot

```bash
echo -e "# Reduce swappiness for desktop installation (default = 60)\nvm.swappiness=10" | sudo tee /etc/sysctl.d/99-sysswappiness.conf
```

2. Reduce systemd timeouts for desktop installations
The change will only be applied after a reboot

```bash
sudo mkdir -p /etc/systemd/system.conf.d && echo -e "# Reduce timeout (default = 90s)\n\n[Manager]\nDefaultTimeoutStopSec=15s" | sudo tee /etc/systemd/system.conf.d/99-systemtimeout.conf
sudo mkdir -p /etc/systemd/user.conf.d && echo -e "# Reduce timeout (default = 90s)\n\n[Manager]\nDefaultTimeoutStopSec=15s" | sudo tee /etc/systemd/user.conf.d/99-usertimeout.conf
```

3. Change GRUB (the boot loader) to show the boot menu for 5s second in single-boot setups
Makes a backup of your /etc/default/grub​ file first

```bash
sudo cp /etc/default/grub /etc/default/grub.orig
```

Make GRUB show the boot menu
    
```bash
sudo sed -i 's/GRUB_TIMEOUT_STYLE=hidden/GRUB_TIMEOUT_STYLE=menu/' /etc/default/grub
```

Write the timeout value to your system

```bash 
sudo sed -i 's/GRUB_TIMEOUT=0/GRUB_TIMEOUT=5/' /etc/default/grub
```

Keeps the timeout value if GRUB has "problems" with a partition - could be e.g. Btrfs or LVM)

```bash
echo -e "\n# Match RECORDFAIL_TIMEOUT to TIMEOUT\nGRUB_RECORDFAIL_TIMEOUT=​\$GRUB_TIMEOUT" | sudo tee -a /etc/default/grub
```

Update your GRUB boot loader with the new values

```bash
sudo update-grub
```

4. Enable the X11 session additionally to Wayland
Will not take affect until reboot

```bash
sudo apt install -y plasma-session-x11
```



## Mount Drives
Create the mount points for the Second Hard Drive and the NAS
NOTE: The IP address on Memnoch must be set correctly or the NAS will reject the connection.

```bash
sudo mkdir /media/shared
sudo mkdir /mnt/audiobooks
sudo mkdir /mnt/calibre-libraries
sudo mkdir /mnt/home
sudo mkdir /mnt/movies
sudo mkdir /mnt/music
sudo mkdir /mnt/photo
sudo mkdir /mnt/tv
sudo mkdir /mnt/video
```

Edit /etc/fstab

```bash
UUID=2023c085-62fa-4219-884f-e5e215a0c15f /media/shared	ext4	defaults	0 1
192.168.1.50:volume1/audiobooks /mnt/audiobooks nfs defaults 0
192.168.1.50:volume1/calibre-libraries /mnt/calibre-libraries nfs defaults 0
192.168.1.50:volume1/homes/rgval /mnt/home nfs defaults 0
192.168.1.50:volume1/movies /mnt/movies nfs defaults 0
192.168.1.50:volume1/music /mnt/music nfs defaults 0
192.168.1.50:volume1/photo /mnt/photo nfs defaults 0
192.168.1.50:volume1/tv /mnt/tv nfs defaults 0
192.168.1.50:volume1/video /mnt/video nfs defaults 0
```
Reload the systemctl so that machine recognizes the new drives

```bash
sudo systemctl daemon-reload
```

Mount the new Drives and Folders

```bash
mount -a
```
