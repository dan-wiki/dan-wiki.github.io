---
title: PostgreSQL: Set Up
date: 2015-12-22 01:18:00 -500
categories: ['postgresql', 'set up']
tags: ['tech']
---

1.  apt-get install posgresql

2.  passwd postgres

3.  sudo -i -u postgres

4.  mkdir data

5.  initdb -D /var/lib/postgresql/data

6.  postgres -D /var/lib/postgresql/data

7.  nano /var/lib/postgresql/data/pg_hba.conf

    1.  host all all 0.0.0.0/0 trust

8.  nano /var/lib/postgresql/data/postgresql.conf

    1.  listen_addresses=\'\*\'

9.  pg_ctl -D /var/lib/postgresql/data start

10. \\list or \\l: list all databases

11. \\dt: list all tables in the current database

12. ctrl+d to exit

13. locale -a

14. createdb db1 \--encoding=\'utf-8\' \--locale=C.UTF-8

    \--template=template0;

15. psql

16. CREATE USER dan WITH PASSWORD \'passwordhere\';

17. GRANT ALL PRIVILEGES ON DATABASE db1 TO dan;

18. CREATE SCHEMA scoreboard;

19. GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA scoreboard TO dan;

20. ctrl+d

21. sudo apt-get install phpmyadmin apache2-utils

22. <https://company_name_here.com:12321/>

23. In Webmin, Servers -\> Apache Webserver

24. Set port 12322 for access. Alternatively, dan.wiki/phppgadmin per

    the below.

25. cd /usr/share/mediawiki

26. ln -s /usr/share/phppgadmin phppgadmin



```{=html}

<!-- -->

```

1.  To stop:

2.  pg_ctl -D /var/lib/postgresql/9.1/main stop

3.  To start:

4.  pg_ctl -D /var/lib/postgresql/data start

5.  Ctrl+c when you see Autovacuum started

6.  Possibly to just use:

7.  postgres -D /var/lib/postgresql/data

