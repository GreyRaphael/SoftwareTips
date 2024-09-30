# transfer

- [transfer](#transfer)
  - [syncthing](#syncthing)
  - [goproxy](#goproxy)

## syncthing

[Syncthing](https://github.com/syncthing/syncthing/releases) is a continuous file synchronization program. It synchronizes files between two or more computers.

```bash
# in fedora
sudo dnf install syncthing

# enable and start
sudo systemctl enable syncthing@gewei.service
sudo systemctl restart syncthing@gewei.service

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
````