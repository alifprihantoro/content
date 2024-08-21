- apps :
  - [x] [neovim](https://neovim.io/) : `pkg install neovim`
  - [vscodium](https://vscodium.com/) :
```bash
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg |
  gpg --dearmor |
  dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg
echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' |
  tee /etc/apt/sources.list.d/vscodium.list
apt update && apt-get install codium
```
  - vscode
  - [nano](https://www.nano-editor.org/) : `pkg install nano`
- cloud :
  - [x] [github codespace](https://github.com/features/codespaces)
  - [gitpod](https://www.gitpod.io/)
  - [codesandbox](https://codesandbox.io/)
- online web based :
  - [stackblitz](https://stackblitz.com/)
  - [codepen](https://codepen.io/)
- offline web based :
  - [code-server](https://github.com/coder/code-server) : `pkg install code-server`