---
author: David der Nederlanden
category:
  - backups
date: "2022-02-20T20:16:47+00:00"
guid: https://itty.nl/?p=17
tag:
  - backblaze
  - backups
  - hetzner
title: Offsite backups
url: /offsite-backups/

---
I use a [NAS](https://en.wikipedia.org/wiki/Network-attached_storage) to host my own files, using a [RAID](https://en.wikipedia.org/wiki/RAID) and [snapshots](https://en.wikipedia.org/wiki/Snapshot_(computer_storage)), productivity is somewhat ensured, however, immutable backups is also one of my needs, what if ransomware happens or my house burns down?

For that I use [Backblaze](https://www.backblaze.com/) B2, directly from my [QNAP](https://www.qnap.com/) with HBS3, but also trough [rclone](https://rclone.org/) inside a VM, as HBS3 doesn't support hiding files and thus the data would be ever growing.
