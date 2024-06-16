# my gui apps

```sh
apt update -y
apt upgrade -y
apt thunar chromium firefox kitty -y

# install postman
apt install nodejs -y
aria2c -x5 https://dl.pstmn.io/download/latest/linux_arm64 --out=postman.tar.gz
tar -xvzf postman.tar.gz
mv Postman .postman
```
