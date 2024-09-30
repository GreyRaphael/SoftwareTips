# transfer

- [transfer](#transfer)
  - [syncthing](#syncthing)

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
```

```bash
# in windows
# download from https://github.com/syncthing/syncthing/releases

# make syncthing run in background and portable
Start-Process -WindowStyle Hidden -FilePath D:\Dev\syncthing\syncthing.exe --home=D:\Dev\syncthing\data

# visit 127.0.0.1:8384
# set password and sync directory
# add device by fedora Device ID
```