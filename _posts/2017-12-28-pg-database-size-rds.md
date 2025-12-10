---
layout: post
title: "Getting the pg_database_size with postgres_exporter on RDS"
date: 2017-12-28 06:00:00
---

I've been working on getting the `pg_database_size` so that I can get it
displayed on my grafana dashboard, but I ran into an issue getting it to work
on an AWS RDS database even though it worked just fine on a self hosted
postgresql database.

I'm using this [postgres_exporter][1] docker image that comes with [this
`pg_database_size` query][2] by default:

```
pg_database:
  query: " SELECT pg_database.datname, pg_database_size(pg_database.datname) as size FROM pg_database" 
```

If you connect to your rds pg database and run that query yourself you will run
into an error something along the lines of not having access to the rdsadmin
db. We really don't need access to the rdsadmin db anyways so we can modify
this query to exclude this db so that pg doesn't return an error and we can
easily get the db sizes of all the other dbs that we do have access to. Here is
the modified query:

```
pg_database:
  query: " SELECT pg_database.datname, pg_database_size(pg_database.datname) as size FROM pg_database WHERE datname != 'rdsadmin'" 
```

[1]: https://github.com/wrouesnel/postgres_exporter
[2]: https://github.com/wrouesnel/postgres_exporter/blob/master/queries.yaml
