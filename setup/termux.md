# setup termux

## setup termux

- delete/custom text output if first open

```sh
rm ~/../usr/etc/motd
```

- add startup (every first open o4 new session)
  > example

```sh
echo "tmux attach \; send-keys tmuxl C-m" >~/../usr/etc/termux-login.sh
```

- custom keyboard goto [here](https://wiki.termux.com/wiki/Touch_Keyboard)
- custom color :
  - goto `~/.termux/colors.properties`
  - reaplace color on that file
    > [!IMPORTANT]
    > you can find best colorscheme to you terminal. example i use [Tokyo Night](https://raw.githubusercontent.com/folke/tokyonight.nvim/main/extras/kitty/tokyonight_moon.conf), but you must delete some color (you just only use `color<num>` exaple `color0 #1b1d2b`)
- change your font :
  - download your best font, i recomended use this [link](https://www.nerdfonts.com/font-downloads)
  - find your best font in that website
  - extract reaplace to `~/.termux/font.ttf`
- make zsh to default :
  > if you change package manager, do this again

```sh
chsh -s zsh          # set default to zsh
```

## change package manager

> official docs : https://wiki.termux.com/wiki/Switching_package_manager

- install zip => `pkg install zip -y`
- check arsitektur => `uname -m`
- download bootstrap pacman in [here](https://github.com/termux-pacman/termux-packages/releases)

> [!WARNING]
> change filename.zip ke file yang kalian download

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
