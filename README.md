# Install Hass.io on Raspberry 4
- https://community.home-assistant.io/t/installing-home-assistant-supervised-on-a-raspberry-pi-with-debian-10/247116
- https://github.com/scstraus/home-assistant-config

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

## Add Zigbee to MQTT
- Add official Add-on: `Mosquitto broker`
  - Update config
```yml
logins:
  - username: plinh
    password: passwd
customize:
  active: false
  folder: mosquitto
certfile: fullchain.pem
keyfile: privkey.pem
require_certificate: false

```
- Add: `https://github.com/zigbee2mqtt/hassio-zigbee2mqtt`

![image](https://user-images.githubusercontent.com/11713395/133923949-2de714ec-0beb-45f8-b091-d6c451f719a5.png)

## Home assistant Config
```yml

# Configure a default setup of Home Assistant (frontend, api, etc)
default_config:

# Text to speech
tts:
  - platform: google_translate

http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.30.32.0/24
    - 192.168.1.0/24

group: !include groups.yaml
automation: !include automations.yaml
script: !include scripts.yaml
scene: !include scenes.yaml
```
### AutoSSH config
```yml
hostname: ha.pnlinh.me
ssh_port: '2223'
username: root
remote_forwarding:
  - ':80:172.17.0.1:8123'
local_forwarding:
  - ''
other_ssh_options: '-o ExitOnForwardFailure=yes -v'
monitor_port: '0'
gatetime: '30'
```
# Blog
- https://www.troyhunt.com/iot-unravelled-part-1-its-a-mess-but-then-theres-home-assistant/

