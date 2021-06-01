# My dotfiles

Here are the configuration files for my Arch Linux build. I save this directory in "~/.dotfiles" and, when installing Arch to a new system, I just clone the repository and run the installation script after having my dependencies installed (see Dependencies section).

```shell
git clone https://github.com/marcosrdac/dotfiles ~/.dotfiles
# or, via SSH
git clone git@github.com:marcosrdac/dotfiles.git ~/.dotfiles

cd ~/.dotfiles
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

When using NVidia, I sometimes have to set udev rules for backlight controls to be manageable by the wheel group. I do that by editing the file "/etc/udev/rules.d/90-backlight.rules" and put the following there:
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

There are programs that I need Installed in order for my configs to work correctly. You can install them with

```sh
./install_dependencies
```

## To do

- [ ] [rename applications](https://developer.gnome.org/menu-spec/)
