---
author: David der Nederlanden
category:
  - hypervisors
  - uncategorized
date: "2023-11-29T19:47:50+00:00"
guid: https://itty.nl/?p=121
tag:
  - experience
  - kvm
  - proxmox
  - pve
  - vmware
title: The interesting future of Hypervisors
url: /the-interesting-future-of-hypervisors/

---
In the landscape of hypervisors there are a couple of big names that always come up when engineers are talking about virtualisation, a couple can be, [VMware](https://www.vmware.com/), [Hyper-V](https://nl.wikipedia.org/wiki/Hyper-V), [Nutanix](https://www.nutanix.com/), you name them.

The reason for that is that they've been around for so long that most people have seen or touched it at some point in their career, in 2008 [Proxmox](https://www.proxmox.com/) came around, as a newcomer it was always the special kid in class that used it.

My first glance at Proxmox was in March 2018, the company I then started working at exclusively used Proxmox, at the time still version 5.x, since then a lot has improved and changed, to name a few milestones:  
\- [Proxmox Backup Server](https://www.proxmox.com/en/proxmox-backup-server/overview), this improved full backups of VM's a lot as they're now incremental for the most part;  
\- [SDN](https://pve.proxmox.com/pve-docs/chapter-pvesdn.html) (Software Defined Networking) is currently growing hard, with full [EVPN/VXLAN](https://www.juniper.net/us/en/research-topics/what-is-evpn-vxlan.html) support;  
\- [SDS](https://pve.proxmox.com/wiki/Storage) (Software Defines Storage) has always been improving and the integration of [CEPH](https://ceph.io/) and [ZFS](https://zfsonlinux.org/) has been going really nice.

The nice part about this is that as the development cycle is still very fast paced, it feels as if you're part of a revolution, you're not stuck in a settled enterprise solution as-is, Proxmox is still pioneering its way down the road.

If you ever want to talk or have questions about Proxmox and one of their products, feel free to contact me as I'd love to tell you all about them from a business user perspective.
