---
title: Installing PrivateInternetAccess
date: 2016-11-30 02:47:00 -500
categories: [article,technology,instructions]
tags: ['vpn','tech']
---

1.  rm -rf .pia_manager

2.  sudo mkdir /pia

3.  chown -R dan:dan /pia

4.  cd /pia

5.  wget

    <https://www.privateinternetaccess.com/installer/download_installer_linux>

6.  tar -xvf download_installer_linux

7.  chmod x+ pia-v65-installer.sh

8.  mkdir .pia_manager

9.  ln -s /pia/.pia_manager \~/.pia_manager

10. ./pia-v65-installer.sh

11. rm \~/pia.sh

12. echo \'\#!/bin/sh\' \> \~/pia.sh

13. echo \'/pia/.pia_manager/pia_manager/run.sh \> /dev/null 2\>&1

    &\' \>\> \~/pia.sh

14. Input username, password, save

15. Right click tray icon, connect



[Category:Category Linux]

