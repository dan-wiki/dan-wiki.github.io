---
title: NextCloud
date: 2021-03-28 18:04:00 -500
categories: []
tags: ['Setting up an AWS instance of NextCloud using Wasabi S3, AWS Glacier backup, and local backup', 'Set up micro EC2 Ubuntu instance and save the applicable keys for SSH access', 'SSH into instance.  I chose to use a virtual Ubuntu instance in Windows, but PuTTy works fine as well.  AWS provides connection strings', 'Create a new S3 bucket and a policy for its use', 'Create a IAM user with the S3 bucket policy and note the key and secret for later', '{"Version": "2012-10-17","Statement": [{"Effect": "Allow","Action": ["s3:GetBucketLocation","s3:ListAllMyBuckets"],"Resource": "arn:aws:s3:::*"},{"Effect": "Allow","Action": ["s3:*"],"Resource": ["arn:aws:s3:::YOUR-BUCKET-NAME"]},{"Effect": "Allow","Action": ["s3:PutObject","s3:GetObject","s3:DeleteObject"],"Resource": ["arn:aws:s3:::YOUR-BUCKET-NAME/*"]}] }', 'Assign an elastic IP to the EC2 instance', 'Get a domain name', 'Configure the domain name through Route 53 to hit
---

## Setting up an AWS instance of NextCloud using Wasabi S3, AWS Glacier backup, and local backup {#setting_up_an_aws_instance_of_nextcloud_using_wasabi_s3_aws_glacier_backup_and_local_backup}

1.  Set up micro EC2 Ubuntu instance and save the applicable keys for
    SSH access
2.  SSH into instance. I chose to use a virtual Ubuntu instance in
    Windows, but PuTTy works fine as well. AWS provides connection
    strings
3.  Create a new S3 bucket and a policy for its use
4.  Create a IAM user with the S3 bucket policy and note the key and
    secret for later
    -   {\"Version\": \"2012-10-17\",\"Statement\": \[{\"Effect\":
        \"Allow\",\"Action\":
        \[\"s3:GetBucketLocation\",\"s3:ListAllMyBuckets\"\],\"Resource\":
        \"arn:aws:s3:::\*\"},{\"Effect\": \"Allow\",\"Action\":
        \[\"s3:\*\"\],\"Resource\":
        \[\"arn:aws:s3:::YOUR-BUCKET-NAME\"\]},{\"Effect\":
        \"Allow\",\"Action\":
        \[\"s3:PutObject\",\"s3:GetObject\",\"s3:DeleteObject\"\],\"Resource\":
        \[\"arn:aws:s3:::YOUR-BUCKET-NAME/\*\"\]}\] }
5.  Assign an elastic IP to the EC2 instance
6.  Get a domain name
7.  Configure the domain name through Route 53 to hit the elastic IP

### Installing Database and Web Server {#installing_database_and_web_server}

1.  Login to Linux command line using SSH tool like PuTTy
2.  sudo -i -u root
3.  sudo apt update
4.  sudo apt install nginx -y
5.  systemctl start nginx
6.  systemctl enable nginx
7.  systemctl status nginx
8.  sudo apt install php-fpm php-curl php-cli php-mysql php-gd
    php-common php-xml php-json php-intl php-pear php-imagick php-dev
    php-common php-mbstring php-zip php-soap php-bz2 -y
9.  cd /etc/php/7.4/
10. nano fpm/php.ini
    -   Uncomment the \'date.timezone\' line and change the value with
        your own timezone.
        -   date.timezone = America/New_York
    -   Uncomment the \'cgi.fix_pathinfo\' line and change the value to
        \'0\'.
        -   cgi.fix_pathinfo=0
    -   Save and Exit
11. nano cli/php.ini
    -   Uncomment the \'date.timezone\' line and change the value with
        your own timezone.
        -   date.timezone = America/New_York
    -   Uncomment the \'cgi.fix_pathinfo\' line and change the value to
        \'0\'.
        -   cgi.fix_pathinfo=0
    -   Save and Exit
12. nano fpm/pool.d/www.conf
13. Uncomment
    -   env\[HOSTNAME\] = \$HOSTNAME
    -   env\[PATH\] = /usr/local/bin:/usr/bin:/bin
    -   env\[TMP\] = /tmp
    -   env\[TMPDIR\] = /tmp
    -   env\[TEMP\] = /tmp
    -   Save and Exit
14. systemctl restart php7.4-fpm
15. systemctl enable php7.4-fpm
16. ss -xa \| grep php
17. systemctl status php7.4-fpm
18. sudo apt install mariadb-server -y
19. systemctl start mariadb
20. systemctl enable mariadb
21. systemctl status mariadb
22. mysql_secure_installation
    -   Enter current password for root (enter for none): Press Enter
    -   Set root password? \[Y/n\] Y
    -   Remove anonymous users? \[Y/n\] Y
    -   Disallow root login remotely? \[Y/n\] Y
    -   Remove test database and access to it? \[Y/n\] Y
    -   Reload privilege tables now? \[Y/n\] Y
23. mysql -u root -p
    -   TYPE THE MYSQL ROOT PASSWORD
    -   create database nextcloud_db;
    -   create user nextclouduser\@localhost identified by
        \'Nextclouduser421@\';
    -   grant all privileges on nextcloud_db.\* to
        nextclouduser\@localhost identified by \'Nextclouduser421@\';
    -   flush privileges;
24. In NextCloud Settings within the web interface under
    Administration\>Security, enable all server-side encryption

### Enabling SSL Encryption {#enabling_ssl_encryption}

1.  sudo -i -u root
2.  sudo apt install certbot -y
3.  systemctl stop nginx
4.  certbot certonly \--standalone -d backup.coffee
5.  sudo service nginx reload

### Renewing SSL Encryption (only if needed) {#renewing_ssl_encryption_only_if_needed}

1.  sudo -i -u root
2.  sudo apt-get install python3-certbot-nginx
3.  systemctl stop nginx
4.  certbot certificates
5.  certbot certonly \--nginx \--cert-name backup.coffee \--dry-run
6.  sudo service nginx reload

### Installing NextCloud {#installing_nextcloud}

1.  sudo apt install wget unzip zip -y
2.  cd /var/www/
3.  wget -q <https://download.nextcloud.com/server/releases/latest.zip>
4.  unzip -qq latest.zip
5.  sudo chown -R www-data:www-data /var/www/nextcloud
6.  cd /etc/nginx/sites-available/
7.  nano nextcloud

`   upstream php-handler {`\
`       #server 127.0.0.1:9000;`\
`       server unix:/var/run/php/php7.4-fpm.sock;`\
`   }`

`   server {`\
`       listen 80;`\
`       listen [::]:80;`\
`       server_name cloud.hakase-labs.io;`\
`       # enforce https`\
`       return 301 `[`https://$server_name:443$request_uri`](https://$server_name:443$request_uri)`;`\
`   }`

`   server {`\
`       listen 443 ssl http2;`\
`       listen [::]:443 ssl http2;`\
`       server_name cloud.hakase-labs.io;`

`       # Use Mozilla's guidelines for SSL/TLS settings`\
`       # `[`https://mozilla.github.io/server-side-tls/ssl-config-generator/`](https://mozilla.github.io/server-side-tls/ssl-config-generator/)\
`       # NOTE: some settings below might be redundant`\
`       ssl_certificate /etc/letsencrypt/live/cloud.hakase-labs.io/fullchain.pem;`\
`       ssl_certificate_key /etc/letsencrypt/live/cloud.hakase-labs.io/privkey.pem;`

`       # Add headers to serve security related headers`\
`       # Before enabling Strict-Transport-Security headers please read into this`\
`       # topic first.`\
`       #add_header Strict-Transport-Security "max-age=15768000; includeSubDomains; preload;" always;`\
`       #`\
`       # WARNING: Only add the preload option once you read about`\
`       # the consequences in `[`https://hstspreload.org/`](https://hstspreload.org/)`. This option`\
`       # will add the domain to a hardcoded list that is shipped`\
`       # in all major browsers and getting removed from this list`\
`       # could take several months.`\
`       add_header Referrer-Policy "no-referrer" always;`\
`       add_header X-Content-Type-Options "nosniff" always;`\
`       add_header X-Download-Options "noopen" always;`\
`       add_header X-Frame-Options "SAMEORIGIN" always;`\
`       add_header X-Permitted-Cross-Domain-Policies "none" always;`\
`       add_header X-Robots-Tag "none" always;`\
`       add_header X-XSS-Protection "1; mode=block" always;`

`       # Remove X-Powered-By, which is an information leak`\
`       fastcgi_hide_header X-Powered-By;`

`       # Path to the root of your installation`\
`       root /var/www/nextcloud;`

`       location = /robots.txt {`\
`           allow all;`\
`           log_not_found off;`\
`           access_log off;`\
`       }`

`       # The following 2 rules are only needed for the user_webfinger app.`\
`       # Uncomment it if you're planning to use this app.`\
`       #rewrite ^/.well-known/host-meta /public.php?service=host-meta last;`\
`       #rewrite ^/.well-known/host-meta.json /public.php?service=host-meta-json last;`

`       # The following rule is only needed for the Social app.`\
`       # Uncomment it if you're planning to use this app.`\
`       #rewrite ^/.well-known/webfinger /public.php?service=webfinger last;`

`       location = /.well-known/carddav {`\
`         return 301 $scheme://$host:$server_port/remote.php/dav;`\
`       }`\
`       location = /.well-known/caldav {`\
`         return 301 $scheme://$host:$server_port/remote.php/dav;`\
`       }`

`       # set max upload size`\
`       client_max_body_size 512M;`\
`       fastcgi_buffers 64 4K;`

`       # Enable gzip but do not remove ETag headers`\
`       gzip on;`\
`       gzip_vary on;`\
`       gzip_comp_level 4;`\
`       gzip_min_length 256;`\
`       gzip_proxied expired no-cache no-store private no_last_modified no_etag auth;`\
`       gzip_types application/atom+xml application/javascript application/json application/ld+json application/manifest+json application/rss+xml application/vnd.geo+json application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/bmp image/svg+xml image/x-icon text/cache-manifest text/css text/plain text/vcard text/vnd.rim.location.xloc text/vtt text/x-component text/x-cross-domain-policy;`

`       # Uncomment if your server is build with the ngx_pagespeed module`\
`       # This module is currently not supported.`\
`       #pagespeed off;`

`       location / {`\
`           rewrite ^ /index.php;`\
`       }`

`       location ~ ^\/(?:build|tests|config|lib|3rdparty|templates|data)\/ {`\
`           deny all;`\
`       }`\
`       location ~ ^\/(?:\.|autotest|occ|issue|indie|db_|console) {`\
`           deny all;`\
`       }`

`       location ~ ^\/(?:index|remote|public|cron|core\/ajax\/update|status|ocs\/v[12]|updater\/.+|oc[ms]-provider\/.+)\.php(?:$|\/) {`\
`           fastcgi_split_path_info ^(.+?\.php)(\/.*|)$;`\
`           set $path_info $fastcgi_path_info;`\
`           try_files $fastcgi_script_name =404;`\
`           include fastcgi_params;`\
`           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;`\
`           fastcgi_param PATH_INFO $path_info;`\
`           fastcgi_param HTTPS on;`\
`           # Avoid sending the security headers twice`\
`           fastcgi_param modHeadersAvailable true;`\
`           # Enable pretty urls`\
`           fastcgi_param front_controller_active true;`\
`           fastcgi_pass php-handler;`\
`           fastcgi_intercept_errors on;`\
`           fastcgi_request_buffering off;`\
`       }`

`       location ~ ^\/(?:updater|oc[ms]-provider)(?:$|\/) {`\
`           try_files $uri/ =404;`\
`           index index.php;`\
`       }`

`       # Adding the cache control header for js, css and map files`\
`       # Make sure it is BELOW the PHP block`\
`       location ~ \.(?:css|js|woff2?|svg|gif|map)$ {`\
`           try_files $uri /index.php$request_uri;`\
`           add_header Cache-Control "public, max-age=15778463";`\
`           # Add headers to serve security related headers (It is intended to`\
`           # have those duplicated to the ones above)`\
`           # Before enabling Strict-Transport-Security headers please read into`\
`           # this topic first.`\
`           #add_header Strict-Transport-Security "max-age=15768000; includeSubDomains; preload;" always;`\
`           #`\
`           # WARNING: Only add the preload option once you read about`\
`           # the consequences in `[`https://hstspreload.org/`](https://hstspreload.org/)`. This option`\
`           # will add the domain to a hardcoded list that is shipped`\
`           # in all major browsers and getting removed from this list`\
`           # could take several months.`\
`           add_header Referrer-Policy "no-referrer" always;`\
`           add_header X-Content-Type-Options "nosniff" always;`\
`           add_header X-Download-Options "noopen" always;`\
`           add_header X-Frame-Options "SAMEORIGIN" always;`\
`           add_header X-Permitted-Cross-Domain-Policies "none" always;`\
`           add_header X-Robots-Tag "none" always;`\
`           add_header X-XSS-Protection "1; mode=block" always;`

`           # Optional: Don't log access to assets`\
`           access_log off;`\
`       }`

`       location ~ \.(?:png|html|ttf|ico|jpg|jpeg|bcmap)$ {`\
`           try_files $uri /index.php$request_uri;`\
`           # Optional: Don't log access to other assets`\
`           access_log off;`\
`       }`\
`   }`

1.  ln -s /etc/nginx/sites-available/nextcloud /etc/nginx/sites-enabled/

nginx -t

1.  systemctl restart nginx
2.  systemctl restart php7.4-fpm
3.  for svc in ssh http https
4.  do
5.  ufw allow \$svc
6.  done
7.  ufw enable
8.  ufw status numbered

### Enabling Wasabi storage {#enabling_wasabi_storage}

1.  In the Linux command prompt
    -   Login to domain name through NextCloud interface and add the
        external storage app
    -   Sign up at wasabi.com
    -   Create and store root access key
    -   Create bucket for NextCloud
    -   Configure NextCloud per
        <https://wasabi-support.zendesk.com/hc/en-us/articles/360029643411-How-do-I-use-NextCloud-with-Wasabi->

=== Adding Database Backup ==

1.  The database is required to be able to decrypt any filesystem
    backups
2.  Pushing database contents to S3 bucket

### Retrieving NextCloud File Encryption Keys {#retrieving_nextcloud_file_encryption_keys}

1.  Edit /etc/sudoers to have the lines:
2.  ubuntu ALL=(root) NOPASSWD: ALL
3.  Then run the following:
    1.  cat /etc/ssh/sshd_config \|grep -i sftp-server Copy the
        sftp-server full path
4.  Get WinSCP and add a new connection with the same login and target
    as the SSH connection the private key in the advanced settings of
    the new connection. The latest version will automatically user
    PuTTyGen to create the .ppk version
5.  Go to Advanced \> SFTP \> SFTP Server and type in sudo su -c
    /usr/lib/openssh/sftp-server
6.  In WinSCP, download the contents of the following paths to a secure
    place offline (mine are going into a safe and someplace offsite):
7.  /var/www/nextcloud/data/files_encryption/OC_DEFAULT_MODULE
8.  Comment out the added line from /etc/sudoers
9.  NOTE: had to get some help from Libera.Chat IRC \#ubuntu. This was a
    neat way to share output: cat /etc/os-release \| nc termbin.com 9999

### Testing Decryption {#testing_decryption}

1.  In case NextCloud stops working and we need to recover our encrypted
    data from Wasabi or elsewhere, we need to prove that the encryption
    keys that NextCloud is using to encrypt the files before they land
    in Wasabi or other external storage can be used to decrypt the raw
    files
2.  In NextCloud, upload a file named test.txt with a sentence in it.
    Use the Wasabi external storage folder
3.  Log into Wasabi and download the now encrypted text.txt
4.  Place the file on a Linux host. Using Windows 10 virtual Ubuntu, I
    grabbed the file from the C drive mount and copied it to a local
    temp folder i.e.:
    1.  mkdir \~/temp/
    2.  mkdir \~/temp/keys/
    3.  cd \~/temp/keys/
    4.  cp /mnt/f/Keys/NextCloud/Encryption_Keys/\* .
    5.  cd ..
    6.  cp \"/mnt/d/Downloads/test (1).txt\" .
    7.  

### Ultimately did not use the snap install method, but keeping those steps for reference {#ultimately_did_not_use_the_snap_install_method_but_keeping_those_steps_for_reference}

1.  Find the snap
    -   sudo snap find nextcloud
2.  Install the Nextcloud application
    -   sudo snap install nextcloud
3.  Create the Nextcloud administrator account
    -   sudo nextcloud.manual-install USERNAME PASSWORD
4.  List Trusted Domain(s)
    -   sudo nextcloud.occ config:system:get trusted_domains
5.  Add your domain to the list of domains Nextcloud
    -   sudo nextcloud.occ config:system:set trusted_domains 1
        \--value=YOURDOMAINNAME
6.  Check php memory limit
    -   sudo snap get nextcloud php.memory-limit
7.  Setup / Update PHP memory limits
    -   snap set nextcloud php.memory-limit=512M
8.  Setup SSL
    -   sudo ufw allow 80,443/tcp
    -   sudo nextcloud.enable-https lets-encrypt
