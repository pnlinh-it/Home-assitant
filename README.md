# Install Hass.io on Raspberry 4
- https://community.home-assistant.io/t/installing-home-assistant-supervised-on-a-raspberry-pi-with-debian-10/247116

```sh
sudo -i

apt-get install -y software-properties-common apparmor-utils apt-transport-https ca-certificates curl dbus jq network-manager

systemctl disable ModemManager

systemctl stop ModemManager

curl -fsSL get.docker.com | sh

curl -sL "https://raw.githubusercontent.com/Kanga-Who/home-assistant/master/supervised-installer.sh" | bash -s -- -m raspberrypi4
```

# Blog
- https://www.troyhunt.com/iot-unravelled-part-1-its-a-mess-but-then-theres-home-assistant/
