---
title: Setting up finger print scanner
date: 2016-11-30 03:00:00 -500
categories: [articles,technology,linux,hardware,instructions]
tags: ['tech','scanner']
---

`   1  sudo apt-get install fingerprint-gui`\

`   2  lsusb`\

`   3  su`\

`   4  sudo add-apt-repository ppa:fingerprint/fingerprint-gui`\

`   5  sudo apt-get update`\

`   6  sudo apt-get install libbsapi policykit-1-fingerprint-gui fingerprint-gui`\

`   7  sudo apt-get update`\

`   8  sudo apt-get autoclean`\

`   9  sudo apt-get clean`\

`  10  sudo nano /etc/hosts`\

`  11  sudo apt-get autoclean`\

`  12  sudo apt-get clean`\

`  13  sudo apt-get autoremove`\

`  14  sudo dpkg --remove -force --force-remove-reinstreq package name`\

`  15  pavucontrol`\

`  16  sudo apt install pavucontrol`\

`  17  pactl load-module module-loopback latency_msec=1`\

`  18  pavucontrol`\

`  19  pactl load-module module-loopback latency_msec=0`

