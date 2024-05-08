# setup wordpress
## install wp
```bash
# install wp-cli
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x wp-cli.phar
mv wp-cli.phar ~/../usr/bin/wp
mkdir wp
wp core download
php -S localhost:8080
```
## setup db
```bash
# start db
mysqld
# open db on cli
mysql -u root -p
```
> paste this sql to create db
```sql
CREATE DATABASE wordpress;
GRANT ALL PRIVILEGES ON wordpress.* TO "wp-user"@"localhost" IDENTIFIED BY "passwd123";
FLUSH PRIVILEGES;
EXIT
```
change :
- wordpress : name table for wordpress
- wp-user : to user name databases
- passwd123 : password untuk db user
- localhost : db ip

## setup wp
```bash
cp wp-config-sample.php wp-config.php
```
then change :
- `DB_NAME` : name table
- `DB_USER` : user name db
- `DB_PASSWORD` : password usr
- `DB_HOST` : db ip

> if you use termux use `127.0.0.1` instead `localhost`

example :

```php
<?php
define( 'DB_NAME', 'wordpress' );

/** Database username */
define( 'DB_USER', 'wp-user' );

/** Database password */
define( 'DB_PASSWORD', 'passwd123' );

/** Database hostname */
define( 'DB_HOST', '127.0.0.1' );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8' );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );
```

## git setup
```gitignore
# Wordpress - ignore core, configuration, examples, uploads and logs.
# https://github.com/github/gitignore/blob/main/WordPress.gitignore

# Core
#
# Note: if you want to stage/commit WP core files
# you can delete this whole section/until Configuration.
/wp-admin/
/wp-content/index.php
/wp-content/languages
/wp-content/plugins/index.php
/wp-content/themes/index.php
/wp-includes/
/index.php
/license.txt
/readme.html
/wp-*.php
/xmlrpc.php

# Configuration
wp-config.php

# Example themes
/wp-content/themes/twenty*/

# Example plugin
/wp-content/plugins/hello.php

# Uploads
/wp-content/uploads/

# Log files
*.log

# htaccess
/.htaccess

# All plugins
#
# Note: If you wish to whitelist plugins,
# uncomment the next line
#/wp-content/plugins

# All themes
#
# Note: If you wish to whitelist themes,
# uncomment the next line
#/wp-content/themes
```
