# rTorrent + ruTorrent
 - `0.9.6`, `latest`

This is a container running rTorrent with ruTorrent as WebUI.

### Usage
Simply run
```
docker run --name rtorrent \
    -v /home/elraro/Downloads:/downloads \
    -p 8181:80 \
    -p 51001:51001 \
    -d elraro/rtorrent-lxc
```
**Change rtorrent port**

By default rtorrent uses port 51001-51001. You can change these ports with the `RTORRENT_PORT` environmental variable. Remember to publish the port(s) to. And yes, even if you specify only one port, you will have to write it as it was a range, 52002-52002. You can specify a range of ports, but its recommended to only use one. And remember that Docker will make as many iptables entries as there are ports in the range.
```
docker run --name rtorrent \
    -v /home/elraro/Downloads:/downloads \
    -e RTORRENT_PORT=52002-52002 \
    -p 52002:52002 \
    -p 8181:80  \
    -d elraro/rtorrent-lxc
```
**Authentication**

To get authentication use `HTUSER` and `HTPASS`.
```
docker run --name rtorrent \
    -v /home/elraro/Downloads:/downloads \
    -e HTUSER=Admin \
    -e HTPASS=Passw0rd \
    -p 8181:80 \
    -p 51001:51001 \
    -d elraro/rtorrent-lxc
```
**Rtorrent watch folder**

Rtorrent has a cool feature where it watches a folder for torrent files and starts them automatically. Just mount the volume `/watch`
```
docker run --name rtorrent \
    -v /home/elraro/Downloads:/downloads \
    -v /home/elraro/Watch:/watch \
    -p 8181:80 \
    -p 51001:51001 \
    -d elraro/rtorrent-lxc
```

**Consistent torrents**

If you want to make your torrents consistent (being able to create a new container with the same torrents), just mount the volume `/home/rtorrent/rtorrent-session`
Be sure to make the session directory on the host writable by uid/gid 1000 or by everyone. If rtorrent cannot write to the folder, rtorrent will not start.
When ever you recreate a new container with existing session files, make sure to delete `rtorrent.lock` in the host session directory before running the new one. Or else rtorrent will fail to start.
```
docker run --name rtorrent \
    -v /home/elraro/Downloads:/downloads \
    -v /home/elraro/rtorrent-sessions:/home/rtorrent/rtorrent-session \
    -p 8181:80 \
    -p 51001:51001 \
    -d kerwood/rtorrent-lxc
```


Patrick Kerwood @ [https://LinuxBloggen.dk](https://LinuxBloggen.dk)  
Original source code [https://github.com/Kerwood/Rtorrent-LXC](https://github.com/Kerwood/Rtorrent-LXC)
Elraro @ [https://www.elraro.eu](https://www.elraro.eu)
Fork it at Github [https://github.com/elraro/Rtorrent-LXC](https://github.com/elraro/Rtorrent-LXC)
