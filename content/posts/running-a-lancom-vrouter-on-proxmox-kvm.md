---
author: zoxvijawofijasodfij
category:
  - hypervisors
date: "2023-11-27T19:11:08+00:00"
guid: https://itty.nl/?p=109
tag:
  - kvm
  - lancom
  - proxmox
  - pve
  - vmware
  - vrouter
title: Running a LANCOM vRouter on Proxmox/KVM
url: /running-a-lancom-vrouter-on-proxmox-kvm/

---
Today I struggled for some time to get a [LANCOM vRouter](https://www.lancom-systems.com/products/routers-sd-wan/central-site-vpn-gateways/lancom-vrouter) appliance to work on [Proxmox](https://proxmox.com/), in the end I got there but the provided instructions weren't working.

Hence I write this small post to help that small group of people out there that might at some point come across the need to do the same.

According to the official installation guide for the KVM image we should use the following features:  
\- Import the provided .img as a VirtIO Disk;  
\- Provide some CPU and RAM;  
\- Use Standard VGA as Display;  
\- Provide two serial ports;  
\- Provide as many VirtIO network cards as needed.

Surprise, no bueno, the VM will continually bootloop.

So, after downloading the OVF for VMware and importing it, I extracted the following requirements:  
\- Import the provided .img as a SATA Disk;  
\- Use a LSI 53C895A SCSI controller;  
\- Provide some CPU and RAM;  
\- Use the i440fx machine type;  
\- Provide as many VirtIO network cards as needed.

Surprise, it works! One can now continue and configure the vRouter as needed.

\-\-\- UPDATE 04/11/2024 ---

Somehow the vRouter filesystem got corrupted, I tried everything to get it back up and running again, sadly no chance. It seems like they use a specialised filesystem for appliances, based on FAT32 and minifs, I was able to read the qcow2 file from a Linux desktop but repairing the filesystem wasn't successfull.

Upon reading the new vRouter installation guide, setting up a new vRouter was way quicker this time, they currently have included the steps to set it up on top of Proxmox VE, without a specific need for the above mentioned steps, it was mostly a next next finish approach this time, so we chose to restore from a backup.
