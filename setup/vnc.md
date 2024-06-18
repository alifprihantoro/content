## install
```bash
apt update -y
apt upgrade -y
apt install tigervnc-standalone-server tigervnc-common -y
```
## Setup
### startup
```bash
echo "i3" > ~/.vnc/xstartup
chmod +x ~/.vnc/xstartup
```

### My Alias
> [!IMPORTANT]
> this for start and kill
```bash
# start in view 1 or 2 or more and resolution 520x260
alias sta='
rm -r .vnc/:*
rm -r .vnc/loc*
rm -r /tmp/.*
vncserver -geometry 520x260'
# kill view 1
alias sto='
vncserver -kill :1
'
# kill view with args
# example : stoo 1
stoo() {
  vncserver -kill :$1
}
```