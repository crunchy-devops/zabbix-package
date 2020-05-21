# Install PostgreSQL and TimescaleDB

## Install all packages
Switch to sudo user   
```sudo -s```

```yum install -y https://download.postgresql.org/pub/repos/yum/12/redhat/rhel-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm```

add a repo ,copy and paste the following snippet
```shell script
# Add our repo
sudo tee /etc/yum.repos.d/timescale_timescaledb.repo <<EOL
[timescale_timescaledb]
name=timescale_timescaledb
baseurl=https://packagecloud.io/timescale/timescaledb/el/7/\$basearch
repo_gpgcheck=1
gpgcheck=0
enabled=1
gpgkey=https://packagecloud.io/timescale/timescaledb/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
EOL
```
Hit enter  
Type   
```yum -y update ```  
``` yum install -y timescaledb-postgresql-12```

## Initdb 
as a sudo user 
```shell script
 mkdir -p /var/lib/pgsql/12/data
 chown -R postgres:postgres /var/lib/pgsql
```
as a postgres user
```
  su - postgres
  /usr/pgsql-12/bin/initdb -D /var/lib/pgsql/12/data  
```
## Change pg_hba.conf and postgresql.conf
Get your public ip address  
https://www.whatismyip-address.com/?check  
open in /var/lib/pgsql/12/data/pg_hba.conf add the following line  
```shell script
host    postgres        postgres        <your_ip>/32          md5  
```
Change these lines in /var/lib/pgsql/12/data/postgresql.conf
``` 
listen_addresses = '*'   
shared_preload_libraries = 'timescaledb'
```
## set a postgres password
as a postgres user  
type psql 
and ```ALTER USER postgres WITH PASSWORD 'password' ```

## Start postgresql service 
as a root user 
```shell script
systemctl start postgresql-12 
systemctl enable postgresql-12
```
