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


# Creating VirtualHosts

File: `/etc/apache2/httpd.conf`
Uncomment: `Include /private/etc/apache2/extra/httpd-vhosts.conf`

Now Apache will load `httpd-vhosts.conf`.

## My VirtualHosts

```
# My Settings
<VirtualHost *:80>
    ServerName localhost
    DocumentRoot "/Library/WebServer/Documents/"
</VirtualHost>

<VirtualHost *:80>
    ServerName local
    ServerAlias local.io
    DocumentRoot "/Users/Michael/Projects/Webdevelopment/Local_dev"
    ErrorLog "/private/var/log/apache2/local.io-error_log"
    CustomLog "/private/var/log/apache2/local.io-access_log" common

        <Directory "/Users/Michael/Projects/Webdevelopment/Local_dev">
            Options Indexes FollowSymLinks
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
</VirtualHost>
```

## Edit hosts file

File: `/etc/hosts`

Add your server aliases at the bottom of the file.

```
# Custom
127.0.0.1	local.io
```