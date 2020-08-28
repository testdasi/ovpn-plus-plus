# ovpn-plus-plus
OpenVPN client with http proxy, socks proxy, dns-over-tls and a random ovpn picker.

## Credit
Based on [binhex/arch-privoxyvpn](https://hub.docker.com/r/binhex/arch-privoxyvpn).

## Key features
1. OpenVPN client to connect to your favourite VPN provider
1. Privoxy for http proxy (<ip>:8118)
1. Microsocks for socks proxy (<ip>:9118)
1. Stubby for dns-over-tls client (<ip>:53 or 127.2.2.2:53 or 127.2.2.2:5253)
1. A script to randomly pick an ovpn file from a set
1. Minor fixes

## Usage
    docker run -d \
        --cap-add=NET_ADMIN \
        -p 8118:8118 \
        -p 9118:9118 \
        -p 53:53 \
        --name=<container name> \
        -v <path for config files>:/config \
        -v /etc/localtime:/etc/localtime:ro \
        -e VPN_ENABLED=<yes|no> \
        -e VPN_USER=<vpn username> \
        -e VPN_PASS=<vpn password> \
        -e VPN_PROV=<pia|airvpn|custom> \
        -e VPN_OPTIONS=<additional openvpn cli options> \
        -e LAN_NETWORK=<lan ipv4 network>/<cidr notation> \
        -e NAME_SERVERS=<name server ip(s)> \
        -e SOCKS_USER=<socks username> \
        -e SOCKS_PASS=<socks password> \
        -e ENABLE_SOCKS=<yes|no> \
        -e ENABLE_PRIVOXY=<yes|no> \
        -e ADDITIONAL_PORTS=<port number(s)> \
        -e DEBUG=<true|false> \
        -e UMASK=<umask for created files> \
        -e PUID=<uid for user> \
        -e PGID=<gid for user> \
        testdasi/ovpn-plus-plus

## Notes
I code for fun and my personal uses; hence, these niche functionalties that nobody asks for. ;)
Tested exclusively with [PIA ovpn files](https://www.privateinternetaccess.com/openvpn/openvpn.zip)
