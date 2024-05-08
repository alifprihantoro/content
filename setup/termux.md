# setup termux

## change package manager

> official docs : https://wiki.termux.com/wiki/Switching_package_manager

- pkg install zip
- `uname -m`
- download zip in [here](https://github.com/termux-pacman/termux-packages/releases)
```bash
mkdir ~/../usr-n
cd ~/../usr-n
mv /path/fileName.zip ./
unzip fileName.zip
cat SYMLINKS.txt | awk -F "←" '{system("ln -s '"'"'"$1"'"'"' '"'"'"$2"'"'"'")}'
```
- go to fail safe (hold new session then press failsafe) or see [here](https://wiki.termux.com/wiki/Recover_a_broken_environment)
```bash
cd ..
rm -fr usr/
mv usr-n/ usr/
```
- exit/new session
- then type here :
```bash
pacman-key --init
pacman-key --populate
```
- then try some install app with `pacman -S` or like normal `pkg install`

## setup with myconf
> [!warning]
> maybe you not use all of my install. check file `termuxInstall.sh` and remove if not you use. change email and username git.
```bash
git clone --depth=1 https://github.com/alifprihantoro/dotconf ~/.myconf
bash .myconf/termuxInstall.sh
```
## setup proot distro

```bash
pkg install proot proot-distro -y
proot-distro list # get list
proot-distro install ubuntu-lts
proot-distro login ubuntu-lts
apt update -y
apt upgrade -y
apt install chromium firefox-esr tigervnc-standalone-server tigervnc-common xfce4-terminal openbox
mkdir .config
cd .config
ln -s /data/data/com.termux/files/home/.myconf/openbox/
```

create text `.bashrc` :

```bash
alias sta='
rm -r .vnc/:*
rm -r .vnc/loc*
rm -r /tmp/.*
vncserver -geometry 1561x720'
```

if use `.myconf` :

```bash
ln -s /data/data/com.termux/files/home/.myconf/bash/.bashrc
```

### fonts

- download font : https://www.nerdfonts.com/font-downloads
- unzip to `~/.fonts/nameFont`
- reload font `fc-cache -fv` or exit then open again

### themes

> pastikan tidak ada folder `.themes`

- clone this `git clone https://github.com/addy-dclxvi/openbox-theme-collections --depth=1 ~/.themes`
- change with objconf

### xfce4-terminal

buat file di `~/.config/xfce4/terminal/terminalrc` yang ada di folder `.myconfig/xfce4/terminal/terminalrc`

atau :

```bash
cd ~/.config
ln -s $dc/xfce4
```

### openbox

- lihat pada folder `.myconf/openbox/rc.xml`
- taruh di folder `.config/openbox/rc.xml`
  atau

```bash
cd ~/.config
ln -s $dc/openbox
```

### browser

- chrome : `chromium --no-sandbox --force-dark-mode`
- firefox : `firefox --display=:1`
- terminal : `xfce4-terminal`
