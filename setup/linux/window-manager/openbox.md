# Setup Debian with I3 Window Manager

## Setup

### window manager

#### install

```sh
apt update -y
apt upgrade -y
apt install openbox lxappearance -y
```

> [!IMPORTANT]
> check my apps gui in [here](./gui-apps-install.md)

#### setup wm

- if complete and you cannot klick anything, be calm. Right klick for find apps.
- open terminal
- change/create configs 8n `~/.config/openbox/rc.xml`
> [!IMPORTANT]
> you can see my configs in [here](https://github.com/alifprihantoro/dotconf/blob/master/.config/openbox/rc.xml)

### themes

#### gtk themes :

- open [here](https://store.kde.org/)
- find theme you like, download (find in file tab), decompress into `$HOME/.themes`
- example my theme is [ojave](https://store.kde.org/p/1275087/)
- to decompress themes is `tar -xv /path/to/file.tar.xz ~/.themes`
- type `lxappearance` then change themes on that gui

#### font

- install

```sh
aria2c -x5 https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/FiraCode.zip --out=./FiraCode
unzip FiraCode ~/.fonts/firacode
fc-cache -fv
```

- goto `~/.config/i3/config` and change `font pango:` with your font, example : `font pango:Fira Code Bold Nerd Font Complete Mono Windows Compatible 10`

## Link
- [My GUI APP](../../../bookmarks/gui-linux.md)
- [My CLI APP](../../../bookmarks/cli.md)
- [My Configs](https://github.com/alifprihantoro/dotconf/)