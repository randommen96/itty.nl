---
author: David der Nederlanden
category:
  - recap
date: "2025-01-01T22:01:13+00:00"
guid: https://itty.nl/?p=183
tag:
  - experience
  - it
  - lifestyle
  - tech-recap
title: 2024 Tech recap
url: /2024-tech-recap/

---
This year was a busy year with bigger long running projects, which take quite a toll but are in the end very rewarding. In a small list the following activities are the most notable:

- Migrated a Nagios Core monitored environment to a Zabbix environment, based on the Zabbix agent 2 and Active checks;
  - Previously we built the Nagios config files with Python from our CMDB, in Zabbix we use Autoregistration rules based on metadata.
- Consolidated 3 datacenters, consisting of 10 racks into 2 datacenters with 8 racks, doing so decommisioning older servers and rebuilding the entire network infrastructure, transistioning from traditional copper to fully fiber, standardized on Singlemode, fully multihomed, built with Juniper Apstra;
- Upgraded two PowerDNS nameservers to up-to-date versions;
- Upgraded multiple Proxmox clusters from 6.x to 8.x;
- Upgraded multiple Ceph clusters from Nautilus to Reef;
- Deployed and implemented multiple MariaDB Galera clusters;
- Migrated servers from one Fortigate VDOM to another with minimal impact;
- Expanded Ceph clusters and replaced nodes with live workloads;
- Cleaned up two RIPE ORGS and handled the audit of one;
- Built a campus network based on Fortiswitches managed by Fortigates.
- Worked together with Juniper on a Case Study about Juniper Apstra;
- Handled multiple CentOS 6 to AlmaLinux upgrades;
- Upgraded Zabbix 6.4 to 7.0 LTS;
- Gave multiple presentations and trainings about networking and Proxmox;
- Attended AlmaLinux Day, CloudFest, Juniper NL Tech club, Dutch Proxmox day, NLNOG Day 2024 and Cephalocon which sparked my interest and got me more involved in opensource communities and trying to bring my relevant input;
