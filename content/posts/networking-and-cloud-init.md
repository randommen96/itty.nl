---
author: zoxvijawofijasodfij
category:
  - automation
  - cloud-init
  - hypervisors
  - networking
date: "2022-11-13T20:28:20+00:00"
guid: https://itty.nl/?p=76
tag:
  - api
  - cloud-init
  - expert
  - hetzner
  - myloc
  - netplan
  - networking
  - provisioning
  - proxmox
  - pve
  - ubuntu
title: Networking and cloud-init
url: /networking-and-cloud-init/

---
Sometimes cloud providers or maybe in your own infrastructure you might find the need to have your default gateway outside of your subnet, for example this is sometimes done by [Hetzner](https://www.hetzner.com/) and [Myloc](https://www.myloc.de/).

The problem with [cloud-init](https://cloud-init.io/) is that it doesn't like it when your gateway is outside your subnet, well, it works with for example 1.1.1.100/32 and 1.1.1.1 but when you try 1.1.1.100/32 and 9.9.9.9 as gateway you will find out that cloud-init happily provisions your VM with the address, but that there are no routes.

Now you can easily create your own (non-persistent) routes to see if it works:

```
# ip route add <gateway IP> dev <interface name>

# ip route add default via <gateway ip>
```

In our example the gateway ip would be 9.9.9.9 and the interface name eth0.

In this example we're working with [Ubuntu](https://ubuntu.com/), which uses [netplan](https://netplan.io/) nowadays, cloud-init will write a netplan file for you, every time it applies the settings, so anytime you change something within cloud-init settings, which is hard because that means you cannot just edit the .yaml file and be done with it.

Now there is a solution for that, within your template you can add a file, for example /etc/netplan/60-routes.yaml, in which case it is important that the number 60 is higher than the number of the file that cloud-init writes, because it gets applied last that way. The contents of the file should look something like this:

```
network:
  version: 2
  ethernets:
    eth0:
      routes:
        - to: default
          via: 9.9.9.9
          on-link: true
```

You can now try it via the command "netplan try" and see if it works for you. If it does you can template the VM for use with this specific gateway/route for all IP's to use and still be flexible with the Proxmox API / cloud-init in provisioning your VM's.

This works because the file isn't touched by cloud-init and so it stays always the same. So you can still use cloud-init to provide different IP's as long as the gateway needed stays the same.

Enjoy!
