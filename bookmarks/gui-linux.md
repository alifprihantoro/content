- Browser :
  - [chromium](https://www.chromium.org/chromium-projects/) => `apt install chromium`
  - [firefox-esr](https://www.mozilla.org/en-US/firefox/enterprise/) => `apt install firefox-esr`
- [postman](https://www.postman.com/) =>
change `aria2c -x` to curl/other download manager
```sh
# install postman
aria2c -x5 https://dl.pstmn.io/download/latest/linux_arm64 --out=postman.tar.gz
tar -xvzf postman.tar.gz
mv Postman .postman
cat > /usr/share/applications/postman.desktop << EOF
[Desktop Entry]
Version=1.0
Name=Postman
Exec=~/.postman/app/Postman %U
Icon=/root/.postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
StartupWMClass=Postman
StartupNotify=true
Keywords=decelopment
EOF
```
- terminal :
  - [kitty](https://github.com/kovidgoyal/kitty) => `apt install kitty`
- file manager :
  - [thunar](https://docs.xfce.org/xfce/thunar/start) => `apt install thunar`
- app finder :
  - [jgmenu](https://github.com/jgmenu/jgmenu) => `apt install jgmenu`
- themes manager :
  - [lxappearance](https://github.com/lxde/lxappearance) (for gtk) => `apt install lxappearance`