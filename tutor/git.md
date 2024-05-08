# tutorial git
## setup
```bash
# setup git
git config --global user.email "alifprihantoro@gmail.com"
git config --global user.name "alifprihantoro"
git config --global core.editor nvim
```
## use ssh
## allow ssh in wifi
```sshconfig
Host github.com
  Hostname ssh.github.com
  Port 443
```

## hooks
> [!NOTE]
> cara kerja hook adalah ketika kita commit/push atau hal lain menggunakan git, akan mentriger script yang sudah diconfigurasi sebelumnya. hook dibagi menjadi dua, yaitu global (berlaku di setiap project) dan local (hanya berlaku di projek yang di setup). 
- remove `.example` di folder `.git/hook`
- atau gunakan cmd `ln -s ../path/yoour/file`
