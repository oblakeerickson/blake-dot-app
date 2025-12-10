---
layout: post
title:  "Connect to pg from remote server"
date:   2016-10-30 01:00:00 -0600
---

For development I have a separate vm for my postgres database, but by default
connections to postgres can only come from localhost.

To allow connections to postgres other than from localhost you need to do two
things: (1) Modify `pg_hba.conf` and (2) modify the `postgresql.conf`
file. **NOTE: these settings are for local development only and should not be
used in production**.

These files can be found in `/etc/postgresql/9.5/main/`.

For `pg_hba.conf` change the IPv4 address from `127.0.0.1` to:

```
# IPv4 local connections:
host    all             all             0.0.0.0/0               md5
```

And for `postgresql.conf` file set the `listen_addresses` to `'*'`:

```
listen_addresses = '*'
```

Also I didn't have a password set for the user I was using. To set the password
for a pg user you can use this command:

```
ALTER USER username WITH PASSWORD 'password';
```

To connect to the database from node:

```
var pg = require('pg');
var connectionString = "postgres://username:password@192.168.0.10:5432/dbname";
```
