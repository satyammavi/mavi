## Nmap

```
nmap -sV -Pn -vv --script=mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql-variables,mysql-vuln-cve2012-2122 $ip -p 3306

nmap -sV -Pn -vv -script=mysql* $ip -p 3306
```

## Local Access

if you gain access to target box and see mysql running , you can try to connect with it from target locally

```
mysql -u root 
# Connect to root without password

mysql -u root -p 
# A password will be asked

# Always test root:root credential
```

## Remote Access

```
mysql -h <Hostname> -u root

mysql -h <Hostname> -u root@localhost
```

## If running as root
If Mysql is running as root and you have acces, you can run commands:

```
mysql> select do_system('id');

mysql> \! sh
```

## Getting all the information from inside the database

```
mysqldump -u admin -p admin --all-databases --skip-lock-tables 
```

## Post Enumeration
Here are list of some files to check after shell on target system to get some credentials or some juicy information that help to get root easily

### MySQL server configuration file

- Unix
    ```
    my.cnf
    /etc/mysql
    /etc/my.cnf
    /etc/mysql/my.cnf
    /var/lib/mysql/my.cnf
    ~/.my.cnf
    /etc/my.cnf
    ```
    
- Windows
 
    ```
    config.ini
    my.ini
    windows\my.ini
    winnt\my.ini
    <InstDir>/mysql/data/
    ```
    

### Command History

```
~/.mysql.history
```

### Log Files

```
connections.log
update.log
common.log
```

### Finding passwords to MySQL
- You might gain access to a shell by uploading a reverse-shell. And then you need to escalate your privilege.
    
- Look into the database and see what users and passwords that are available.

    ```
    /var/www/html/configuration.php
    ```