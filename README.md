<!--

---
lang: american
---
-->

[![Build Status](https://travis-ci.org/cw-ansible/cw.interfaces.svg?branch=master)](https://travis-ci.org/cw-ansible/cw.interfaces)
[![Tweet this](http://img.shields.io/badge/Tweet-it00aced.svg)](https://twitter.com/intent/tweet?tw_p=tweetbutton&via=renard_0&url=https%3A%2F%2Fgithub.com%2Fcw-ansible%2Fcw.interfaces&text=Configure%20network%20interfaces%20with%20%23ansible.)
[![Follow me on twitter](http://img.shields.io/badge/Twitter-Follow-00aced.svg)](https://twitter.com/intent/follow?region=follow_link&screen_name=renard_0&tw_p=followbutton)


# interfaces

This roles configures the `/etc/network/interfaces` file on
[Debian](http://debian.org) and [Ubuntu](http://ubuntu.com) like
distributions.
 
## Usage

Include the `cw.interfaces` module to your playbook.

## Configuration

See specific documentation in `defaults/main.yml`

## Examples

### Simple DHCP on `eth0`

    interfaces_network_interfaces:
      interfaces_network_interfaces:
       - file: /etc/network/interfaces
         data:
         - iface: lo
         - iface: eth0

### Advanced static IP on `eth0`

    interfaces_network_interfaces:
      - file: /etc/network/interfaces
        data:
          - iface: lo
          - iface: eth0
            hostname: server.example.com
            comment: private interface (admin)
            address: 172.18.0.1
            netmask: 255.255.128.0
            gateway: 172.18.127.1
            dns-nameservers:
              - 192.168.1.1
              - 192.168.8.8
            dns-search: example.com
            routes:
              - { network: 172.12.0.0/17, gateway: 172.18.127.254 } 
              - { network: 192.168.0.0/16, gateway: 172.18.127.254 }
              - { network: 10.0.0.0/8, gateway: 172.18.127.254 }


Default gateway is `172.18.127.1` and all RFC1915 are routed via
`172.18.127.254`.

### Example from `interfaces(5)` man page


    interfaces_network_interfaces:
      - file: /etc/network/interfaces
        data:
        - iface: eth0
        - source: interfaces.d/machine-dependent
        - source-directory: interfaces.d
        - mapping: eth0
          script: /usr/local/sbin/map-scheme
          map:
            - HOME eth0-home
            - WORK eth0-work
        - iface: eth0-home
          address: 192.168.1.1
          netmask: 255.255.255.0
          up: flush-mail
        - iface: eth0-work
        - iface: eth1
          type: allow-hotplug
      # Other examples
      - file: /etc/network/interfaces.d/extra
        data:
        - iface: lo
        - iface: lo:1
          address: 127.10.10.1
          netmask: 255.255.255.255
        - iface: eth2
          method: manual
          auto vmbr0
        - iface: vmbr2
          bridge_ports: eth2
          bridge_stp: 'off'
          bridge_fd: 0
          routes:
            - { network: 172.19.0.0/17, gateway: 172.18.127.254 }
            - { network: 172.19.192.0/22 gateway: 172.18.127.1 }



## Copyright

Author: Sébastien Gross `<seb•ɑƬ•chezwam•ɖɵʈ•org>` [@renard_0](https://twitter.com/renard_0)

License: WTFPL, grab your copy here: http://www.wtfpl.net
