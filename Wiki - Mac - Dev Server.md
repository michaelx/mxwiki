# Install Apache, MySQL and PHP

## 1. Activate PHP

File: `/etc/apache2/httpd.conf`
Uncomment: `LoadModule php5_module libexec/apache2/libphp5.so`

## 2. Install MySQL

### Get Homebrew

Homebrew is the missing package manager for Mac OS and makes installing MySQL super easy.

```
ruby <(curl -fsSkL raw.github.com/mxcl/homebrew/go)
```

### Install MySQL via Homebrew

```
brew install mysql
unset TMPDIR
mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp
```

## 3. Secure MySQL

```
mysql_secure_installation
```


# Apache + MySQL Control Script

```
#! /bin/sh

# ------------------------------------------------------------------------- #
# Apache + MySQL Control Script V. 1.0
# by @michael_xander > http://michaelxander.com
# ------------------------------------------------------------------------- #

command=$1

if [ $# -eq 0 ]
then
    echo "Please provide a command: start, restart, stop"
    read command
fi

if [ $command = "start" -o $command = "restart" -o $command = "stop" ]
then
    mysql.server $command
    sudo apachectl $command
else
    echo "Unkown command provided."
fi
```


# Create VirtualHosts

File: `/etc/apache2/httpd.conf`
Uncomment: `Include /private/etc/apache2/extra/httpd-vhosts.conf`

Now Apache will load `httpd-vhosts.conf`.

## My VirtualHosts

File: `/etc/apache2/extra/httpd-vhosts.conf`

```
# My Settings
<VirtualHost *:80>
    ServerName localhost
    DocumentRoot "/Library/WebServer/Documents/"
</VirtualHost>

<VirtualHost *:80>
    ServerName local
    ServerAlias local.io
    DocumentRoot "/Users/Michael/Projects/_local.io"
    ErrorLog "/private/var/log/apache2/local.io-error_log"
    CustomLog "/private/var/log/apache2/local.io-access_log" common

        <Directory "/Users/Michael/Projects/_local.io">
            Options Indexes FollowSymLinks
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
</VirtualHost>
```

## Edit Hosts File

File: `/etc/hosts`

Add your server aliases at the bottom of the file.

```
# Custom
127.0.0.1	local.io
```


# Optional

## Start MySQL at Login

```
ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents
```

## Apache Config

File: `/etc/apache2/httpd.conf`

### My Low RAM Config

```
# Low Memory Settings

StartServers 1
MinSpareServers 1
MaxSpareServers 3
MaxClients 3
MaxRequestsPerChild 300
```

## MySQL Config

File: `~/.my.cnf`

### My Low RAM Config

```
[mysql]

# CLIENT #
port                           = 3306
skip-locking

[mysqld]

# GENERAL #
default-storage-engine         = InnoDB

# MyISAM #
key-buffer-size                = 8M
sort-buffer-size 			   = 256K
read-buffer-size 			   = 256K
read-rnd-buffer-size 		   = 512K
myisam-sort-buffer-size 	   = 1M
join-buffer-size 			   = 1M
myisam-recover                 = FORCE,BACKUP

# SAFETY #
max-allowed-packet             = 16M
max-connect-errors             = 100

# BINARY LOGGING #
expire-logs-days               = 7
sync-binlog                    = 1

# CACHES AND LIMITS #
tmp-table-size                 = 8M
max-heap-table-size            = 4M
query-cache-type               = 0
query-cache-size               = 0
max-connections                = 10
thread-cache-size              = 10
open-files-limit               = 65535
table-definition-cache         = 128
table-open-cache               = 256

# INNODB #
innodb-flush-method            = O_DIRECT
innodb-log-files-in-group      = 3
innodb-log-file-size           = 4M
innodb-flush-log-at-trx-commit = 1
innodb-file-per-table          = 1
innodb-buffer-pool-size        = 16
```