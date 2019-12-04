# MariaDB 
MariaDB Training Nurremburg 12.2019

## Possible collations MariaDB 
https://mariadb.com/kb/en/library/supported-character-sets-and-collations/

## Write logs (general and slow) in both TABLE and FILE 
```
set global log_output='TABLE,FILE';
```

## Show all errors 
```
[root@localhost mariadb]# cat mariadb.log | grep -i error
```

## Show all options of mysqld for galera on Centos 8 
```
/usr/libexec/mysqld --help --verbose | grep wsrep
```

## Mysqldump with best options for PIT (Point in Time Recovery) (ONLY WITHOUT REPLICATION) 
```
mysqldump --all-databases --delete-master-logs --master-data=2 --single-transaction -p > /usr/src/all-databases-master-data.sql
# with gtid 
mysqldump --all-databases --delete-master-logs --master-data=2 --single-transaction --gtid -p > /usr/src/all-databases-master-data-gtid.sql
```
## Purge manually 

https://mariadb.com/kb/en/library/purge-binary-logs/
PURGE BINARY LOGS BEFORE '2013-04-21';

## Mariabackup ##

```
mariabackup  -u root --backup --target-dir=/usr/src/$(date +"%Y-%m-%d")
# prepare 
mariabackup  --prepare --target-dir=/usr/src/backupdir 
# copy-back
systemctl stop mariadb 
mv /var/lib/mysql /var/lib/mysql.backup
mariabackup  --copy-back --target-dir=/usr/src/backupdir
cd /var/lib/
chown -R mysql:mysql mysql
# adjust context for selinux 
restorecon -Rv /var/lib/mysql
systemctl start mariadb 

## Mariabackup - Reference ##

https://mariadb.com/kb/en/library/full-backup-and-restore-with-mariabackup/


