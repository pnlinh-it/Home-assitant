# Install Hass.io on Raspberry 4
- https://community.home-assistant.io/t/installing-home-assistant-supervised-on-a-raspberry-pi-with-debian-10/247116

## Add ssh remote
Generate ssh key-pair
```sh
pnlinh@Linhs-MacBook-Pro  ~  ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/pnlinh/.ssh/id_rsa): homeassistant
pnlinh@Linhs-MacBook-Pro  ~  cat homeassistant.pub
```
Open `sysconf.txt` at root directory of debian image uncomment line `root_authorized_key`
```
root_pw=password
root_authorized_key=<entire_homeassistant.pub_content>
```
```
ssh root@<pi_ip_address> -i homeassistant
```


```sh
apt update && apt upgrade -y
apt install sudo -y
apt-get install -y software-properties-common apparmor-utils apt-transport-https ca-certificates curl dbus jq network-manager

systemctl disable ModemManager

systemctl stop ModemManager

curl -fsSL get.docker.com | sh

curl -sL "https://raw.githubusercontent.com/Kanga-Who/home-assistant/master/supervised-installer.sh" | bash -s -- -m raspberrypi4
```

# Blog
- https://www.troyhunt.com/iot-unravelled-part-1-its-a-mess-but-then-theres-home-assistant/
