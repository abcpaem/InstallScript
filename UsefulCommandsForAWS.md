# Useful Commands for AWS

The following list of commands are quite useful when installing or troubleshooting Odoo in AWS using RDS, EC2, ALB and EFS.

## RDS Database

##### Install Postgres client:
```
sudo apt-get install postgresql-client
```
##### Get Postgres version:
```
pg_config --version

psql --version
```
##### Connect to RDS:
```
psql --host=odoo.xxxxxxxxxxxx.us-east-1.rds.amazonaws.com --port=5432 -U master -d postgres --password
```
##### Create Odoo user:
```
CREATE USER odoo WITH PASSWORD 'odoo' CREATEDB;
```
##### List DB users:
```
\du
```

## EFS and Files

##### Mount EFS:
```
sudo mount -t efs -o tls fs-xxxxxxxxxxxxxxxxx.efs.us-east-1.amazonaws.com /odoo/.local/share/Odoo/filestore/efs
```
##### View mounted EFS:
```
df -T
```
##### View Odoo logs:
```
tail -100 /var/log/odoo/odoo-server.log
```
##### Delete all files not named "a" and excluding current directory:
```
find -maxdepth 1 ! -name a ! -name . -exec rm -rv {} \;
```
##### List files in Megas:
```
ls -l --block-size=M
```
##### Copy all files and directories:
```
cp -a /source_folder/. /destination_folder/

cp -a /odoo/.local/share/Odoo/sessions/. /odoo/.local/share/Odoo/filestore/efs/sessions
```
##### Find file:
```
find / -iname 'file_name' 2>/dev/null
```
##### Zip and unzip files:
```
sudo apt-get install zip gzip tar

zip -r my_arch.zip my_folder

unzip my_arch.zip
```
##### View Odoo configuration file:
```
sudo cat /etc/odoo-server.conf
```

## Services

##### List services running:
```
sudo systemctl list-units --state running
```
##### Start / Stop / Restart Odoo service:
```
sudo service odoo-server start

sudo service odoo-server stop

sudo service odoo-server restart
```
