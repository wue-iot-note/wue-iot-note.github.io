---
title: VMWare Worksation setup (Ubuntu)
layout: default
---

# VMWare Worksation setup (Ubuntu)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## To Do's

sudo apt-get install open-vm-tools-desktop </br>
reboot </br>
Settings -> Options -> Shared Folders -> [add path] </br>
sudo vmhgfs-fuse .host:/ /mnt/ -o allow_other -o uid=1000 </br>

