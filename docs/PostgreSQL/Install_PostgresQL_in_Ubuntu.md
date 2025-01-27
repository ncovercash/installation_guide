# Install PostgreSQL in Ubuntu

## Enable PostgreSQL Apt Repository


```
sudo apt-get install wget ca-certificates

wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
```


### Install PostgreSQL on Ubuntu

```
sudo apt-get update

sudo apt-get install postgresql postgresql-contrib

sudo  apt-get install postgresql-client

```


### Connect to PostgreSQL

```
sudo -u postgres psql
```

### Alter PostgreSQL password

```
ALTER USER postgres PASSWORD 'NEWPASSWORD';
```

## Access PostgreSQL over network

### Change listen_address `localhost to *` in  file  `/etc/postgresql/{version_number}/main/postgresql.conf`
```
# - Connection Settings -
listen_addresses = '*'      # what IP address(es) to listen on;     
```

### Changes in `pg_hba.conf`

Add the following line in `# IPv4 local connections`:

```
host   all             all          0.0.0.0/0                   md5
```

and comment

```
#host   all          all        127.0.0.1/32                     md5
```

#### Restart PostgreSQL to take effect

```
sudo systemctl restart postgresql
```

We have configured everything required for remote host connection. Verify that the service is listening on port 5432.
```
db1@1:~$ ss -tunelp | grep 5432
tcp   LISTEN 0      244          0.0.0.0:5432      0.0.0.0:*    uid:113 ino:90438 sk:4 cgroup:/system.slice/system-postgresql.slice/postgresql@14-main.service <->
tcp   LISTEN 0      244             [::]:5432         [::]:*    uid:113 ino:90439 sk:6 cgroup:/system.slice/system-postgresql.slice/postgresql@14-main.service v6only:1 <->
```

Allow the port through the firewall if you have ufw enabled.

```
sudo ufw allow 5432/tcp
```

Now use the syntax below to connect to your instance from a remote machine.

```
psql 'postgres://<username>:<password>@<host>:<port>/<db>?sslmode=disable'
```

For example, I will try and connect to my instance with the superuser account created. Note that the remote machine should have PostgreSQL installed.

```
psql 'postgres://admin:Passw0rd@192.168.205.10:5432/postgres?sslmode=disable'
```

## Known Problem

* Check the permission problem in `/var` directory to create folder for `data` and `log`.
