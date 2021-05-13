# My dotfiles

Here are the configuration files for my Arch Linux build. I save this directory in "~/.dotfiles" and, when installing Arch to a new system, I just clone the repository and run the installation script after having my dependencies installed (see Dependencies section).

```shell
git clone https://github.com/marcosrdac/dotfiles $HOME/.dotfiles
# or, via SSH
git clone git@github.com:marcosrdac/dotfiles.git $HOME/.dotfiles

cd $HOME/.dotfiles
./install
```

Then I set *zsh* as my user's default interactive shell:

```shell
chsh -s `which zsh`
```

I also give permissions for me to shutdown my PC and mount drives without password, putting the next line in "/etc/sudoers":

```
%wheel ALL=(ALL) NOPASSWD: /sbin/shutdown, /sbin/poweroff, /sbin/halt, /bin/systemctl suspend, /sbin/mount, /sbin/umount
```

When using NVidia, I sometimes have to set udev rules for backlight controls to work. So I edit the file "/etc/udev/rules.d/90-backlight.rules" and put the following there:
```shell
SUBSYSTEM==“backlight”, ACTION==“add”,
ACTION=="change", SUBSYSTEM=="backlight", RUN+="/usr/bin/chgrp wheel /sys/class/backlight/%k/brightness"
ACTION=="change", SUBSYSTEM=="backlight", RUN+="/usr/bin/chmod g+w /sys/class/backlight/%k/brightness"
```

If you want external drives automounting, use:
```shell
systemctl enable devmon@$USER
systemctl start devmon@$USER
```


## Dependencies

There are programs that I need Installed in order for my configs to work correctly. Here is the list:

### From Arch Oficial Repositories

```
# terminal multiplexer
tmux
# getting locate
mlocate
# mounting drives
udevil
# gettinh zsh
zsh zsh-syntax-highlighting
# alsa and pulse (pulse is on AUR bellow)
alsa alsa-utils alsa-tools pulseaudio-alsa
# X
xorg xorg-server xorg-xinit xorg-apps
# window manager
bspwm polybar yad networkmanager-dmenu
compton sox unclutter redshift scrot acpi brightnessctl mpv
# wallpaper setting
xwallpaper
# file managers
vifm thunar
# browsers
qutebrowser firefox
# music
mpd mpc ncmpcpp
# neomutt
neomutt urlscan
libnotify dunst
# web downloaders
wget curl git youtube-dl
# ssh client
openssh
# dealing with clipboard
xclip xsel xdotool
# file compression
zip unzip unrar
# latex
texlive
# making mouse cursor disappear
unclutter
# screenshot
scrot
# e-reader
zathura zathura-cb zathura-djvu zathura-pdf-mupdf zathura-ps
# torrents
transmission-cli
# lightdm: needed for using teamviewer
lightdm lightdm-gtk-greeter lightdm-gtk-greeter-settings
```


### From AUR

```
yay
# getting pulseaudio
pulseaudio pamixer
# view images from inside terminals
python-ueberzug
# making lightdm use xinit
xinit-xsession
# dropbox
dropbox dropbox-cli
# security
keepassx2 python-keepmenu
# making themes from pictures
wpgtk
# torrent visualizer
tremc
```


## To-do

- [ ] Review dependencies
