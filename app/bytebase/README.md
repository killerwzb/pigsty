# Bytebase

Schema Migrator for PostgreSQL

```bash
cd app/bytebase; docker-compose up -d
```

Visit [http://ddl.pigsty](http://ddl.pigsty) or http://10.10.10.10:8887


```bash
make up         # pull up bytebase with docker-compose in minimal mode
make run        # launch bytebase with docker , local data dir and external PostgreSQL
make view       # print bytebase access point
make log        # tail -f bytebase logs
make info       # introspect bytebase with jq
make stop       # stop bytebase container
make clean      # remove bytebase container
make pull       # pull latest bytebase image
make rmi        # remove bytebase image
make save       # save bytebase image to /tmp/bytebase.tgz
make load       # load bytebase image from /tmp
```



## Use External PostgreSQL

Bytebase use its internal PostgreSQL database by default, You can use external PostgreSQL for higher durability.

```yaml
# postgres://dbuser_bytebase:DBUser.Bytebase@10.10.10.10:5432/bytebase
db:   { name: bytebase, owner: dbuser_bytebase, comment: bytebase primary database }
user: { name: dbuser_bytebase , password: DBUser.Bytebase, roles: [ dbrole_admin ] }
```

if you wish to user an external PostgreSQL, drop monitor extensions and views & pg_repack

```bash
DROP SCHEMA monitor CASCADE;
DROP EXTENSION pg_repack;
```

After bytebase initialized, you can create them back with `/pg/tmp/pg-init-template.sql`

```bash
psql bytebase < /pg/tmp/pg-init-template.sql
```