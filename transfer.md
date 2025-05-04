# transfer

- [transfer](#transfer)
  - [syncthing](#syncthing)
  - [goproxy](#goproxy)
  - [rustdesk](#rustdesk)
  - [ssh](#ssh)
    - [win10 prevent ssh from disconnecting](#win10-prevent-ssh-from-disconnecting)

## syncthing

[Syncthing](https://github.com/syncthing/syncthing/releases) is a continuous file synchronization program. It synchronizes files between two or more computers.

```bash
# in fedora
sudo dnf install syncthing

# enable and start
sudo systemctl enable syncthing@gewei.service
sudo systemctl restart syncthing@gewei.service

# change from 127.0.0.1:8384 -> 0.0.0.0:8384
vi ~/.local/state/syncthing/config.xml

# go to browser visit
http://your_server_host:8384/
# set password and sync directory
# copy the Device ID

# firewall port
22000/TCP
22000/UDP
21027/UDP # 
8384/TCP # for webui
```

```bash
# in windows
# download from https://github.com/syncthing/syncthing/releases

# make syncthing run in background and portable
# write a start.ps1
Start-Process -WindowStyle Hidden -FilePath D:\Dev\syncthing\syncthing.exe --home=D:\Dev\syncthing\data
# run
& D:\Dev\syncthing\start.ps1

# write a stop.ps1
Get-Process -Name "syncthing" | Stop-Process
& D:\Dev\syncthing\stop.ps1

# visit 127.0.0.1:8384
# set password and sync directory
# add device by fedora Device ID
```

## goproxy

download [proxy_admin_free](https://github.com/snail007/proxy_admin_free/blob/master/README_ZH.md) by bash

```bash
# in server
curl -L https://mirrors.host900.com/https://github.com/snail007/proxy_admin_free/blob/master/install_auto.sh | bash 

# install path /usr/local/bin/proxy-admin
# configuration path /etc/gpa, change port of webui
# uninstall just exec : /usr/local/bin/proxy-admin uninstall && rm /etc/gpa
# please visit : http://YOUR_IP:32080/ username: root, password: 123

# change pwd in webui, all kinds of configuration in webui
# config YOUR_PORT for client
# download proxy.crt and proxy.key from webui for client
```

```bash
# in client
# download proxy from https://github.com/snail007/goproxy/releases
./proxy client -P YOUR_IP:YOUR_PORT -T tls -C proxy.crt -K proxy.key --k default
```

## rustdesk

deploy rustdesk-server in aliyun, [tutorial](https://rustdesk.com/docs/en/self-host/rustdesk-server-oss/install/)

```bash
# recommended
wget https://raw.githubusercontent.com/techahold/rustdeskinstall/master/install.sh
chmod +x install.sh
./install.sh
# no need to install HTTP server
# it will show public key xxxxxxxxxxxxxxxxxxxxxx, note it

# open firewall ports
21114:21119/tcp
21116/udp
```

```bash
# uninstall rustdesk-serer completely
sudo systemctl stop rustdeskrelay.service rustdesksignal.service
sudo systemctl disable rustdeskrelay.service rustdesksignal.service
sudo rm -rf /var/log/rustdesk/
sudo rm -rf /opt/rustdesk/
sudo rm -rf /etc/systemd/system/rustdesksignal.service
sudo rm -rf /etc/systemd/system/rustdeskrelay.service

# if you want to uninstall gohttpserver
sudo systemctl stop gohttpserver.service
sudo systemctl disable gohttpserver.service
sudo rm -rf /var/log/gohttp/
sudo rm -rf /opt/gohttp/
sudo rm -rf /etc/systemd/system/gohttpserver.service
```

how to use in client

```bash
# go to settings/Network
paste ID/Relay Server with your ip
# paste the public key
xxxxxxxxxxxxxxxxxxxxxx
```

## ssh

### win10 prevent ssh from disconnecting

method1: edit `~/.ssh/config`
- `ServerAliveInterval 30`: Sends a keepalive message every 30 seconds
- `ServerAliveCountMax 120`: (Optional)If no response is received after 120 keepalive messages (i.e., 1 hours), the client will terminate the connection.

```bash
# ~/.ssh/config
Host *
    ServerAliveInterval 20
    ServerAliveCountMax 120
```

method2: run in console

```bash
# in windows terminal
# keep ssh alive: https://github.com/microsoft/terminal/issues/7291
ssh -o ServerAliveInterval=30 your_name@your_host
```