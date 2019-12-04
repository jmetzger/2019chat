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
