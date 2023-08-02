---
title: Installing Fujitsu ScanSnap S300
date: 2016-11-30 02:42:00 -500
categories: ['linux']
tags: ['tech','scanner']
---

1.  sudo apt-get install sane

2.  ls -la /etc/sane.d/epjitsu.conf

3.  nano /etc/sane.d/epjitsu.conf

4.  ls -la /usr/share/sane/epjitsu/300_0C00.nal

5.  cd /usr/share/sane/

6.  ls

7.  mkdir epjitsu

8.  sudo mkdir epjitsu

9.  cd epjitsu/

10. ls

11. cp /home/dan/Downloads/300_0C00.nal .

12. sudo cp /home/dan/Downloads/300_0C00.nal .

13. lsblk

14. lsusb



[Category:Category Linux]

