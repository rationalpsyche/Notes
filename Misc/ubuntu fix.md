# Ubuntu fixes

## DNS after suspend

Comment `dns=dnsmasq` in `/etc/NetworkManager/NetworkManager.conf`

## Dell XPS keyboard light

`echo "blacklist dell_laptop" > /etc/modprobe.d/dell_backlight.conf`

## Color in the shell

Uncomment `force_color_promp=yes` in `.bashrc`
