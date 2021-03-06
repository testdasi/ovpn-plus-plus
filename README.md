# openvpn-plus-plus
OpenVPN client with http proxy, socks proxy, dns-over-tls and a random ovpn picker.

## High-level instructions
* Run docker - first run will stop itself due to missing ovpn file
* Copy / extract your ovpn files in the host path that is mapped to */config/ovpn_files* (at least 1 file is required, must have .ovpn extension)
* If there are separate cert files (crt + pem), place them in host location path that is mapped to */config/ovpn*
* Start docker again

## Credit
Based on [binhex/arch-privoxyvpn](https://hub.docker.com/r/binhex/arch-privoxyvpn).

## Key features
1. OpenVPN client to connect to your favourite VPN provider
1. Privoxy for http proxy (ip:8118)
1. Microsocks for socks proxy (ip:9118)
1. Stubby for dns-over-tls client (ip:53 or 127.2.2.2:53 or 127.2.2.2:5253)
1. A new IP every docker start (i.e. random ovpn picker, multiple ovpn files required e.g. [PIA ovpn files](https://www.privateinternetaccess.com/openvpn/openvpn.zip))
1. Minor / cosmetic fixes

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
        testdasi/openvpn-plus-plus

## Unraid + PIA Example
    docker run -d\
        --cap-add=NET_ADMIN \
        --name='openvpn-plus-plus'\
        --net='bridge'\
        -e TZ="Europe/London"\
        -e 'VPN_ENABLED'='yes'\
        -e 'ENABLE_SOCKS'='yes'\
        -e 'ENABLE_PRIVOXY'='yes'\
        -e 'VPN_USER'='user'\
        -e 'VPN_PASS'='password'\
        -e 'VPN_PROV'='pia'\
        -e 'VPN_OPTIONS'=''\
        -e 'LAN_NETWORK'='192.168.0.1/24'\
        -e 'NAME_SERVERS'='127.2.2.2'\
        -e 'SOCKS_USER'='user'\
        -e 'SOCKS_PASS'='password'\
        -e 'ADDITIONAL_PORTS'=''\
        -e 'DEBUG'='false'\
        -e 'UMASK'='000'\
        -e 'PUID'='99'\
        -e 'PGID'='100'\
        -p '8118:8118/tcp'\
        -p '9118:9118/tcp'\
        -p '53:53/tcp'\
        -p '53:53/udp'\
        -v '/mnt/user/appdata/openvpn-plus-plus':'/config':'rw'\
        'testdasi/openvpn-plus-plus'

## Notes
* I code for fun and my personal uses; hence, these niche functionalties that nobody asks for. ;)
* Tested exclusively with [PIA ovpn files](https://www.privateinternetaccess.com/openvpn/openvpn.zip)
* Intended to be used with Unraid but would work in other x86/amd64 environments too.
* If you like my work, [a donation to my burger fund](https://paypal.me/mersenne) is very much appreciated.

[![Donate](https://raw.githubusercontent.com/testdasi/testdasi-unraid-repo/master/donate-button-small.png)](https://paypal.me/mersenne). 

