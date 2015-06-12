<!--

---
lang: american
---
-->

[![Build Status](https://travis-ci.org/cw-ansible/cw.interfaces.svg?branch=master)](https://travis-ci.org/cw-ansible/cw.interfaces)
[![Tweet this](http://img.shields.io/badge/%20-Tweet-00aced.svg)](https://twitter.com/intent/tweet?tw_p=tweetbutton&via=renard_0&url=https%3A%2F%2Fgithub.com%2Fcw-ansible%2Fcw.interfaces&text=Configure%20network%20interfaces%20with%20%23ansible.)
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
     - file: /etc/network/interfaces
       data:
       - iface: lo
       - iface: eth0

### Advanced static IP on `eth0`

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



## Copyright

Author: Sébastien Gross `<seb•ɑƬ•chezwam•ɖɵʈ•org>` [@renard_0](https://twitter.com/renard_0)

License: WTFPL, grab your copy here: http://www.wtfpl.net
