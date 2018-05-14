# README
## HATSTALL

This docker image runs a Hatstall service in order to simplify sortinghat database management.
This image is designed to be run next to a sortinghat database.

More information about [Hatstall](https://github.com/chaoss/grimoirelab-hatstall)  
More information about [Sortinghat](https://github.com/chaoss/grimoirelab-sortinghat)

## CONFIGURATION
They are two ways to configure and use this image, either by bind mounting a configuration files or by 
using env variables, the second option is the easiest one.

### ENVIRONMENT
#### HATSTALL_ADMIN_USER
Admin user used to access the default interface. Default set to 'admin'

#### HATSTALL_ADMIN_MAIL
Admin email used by admin user. Default set to admin@example.com

#### HATSTALL_ADMIN_PASS admin
Admin password used by admin user. Default set to admin

#### HATSTALL_ALLOWED_HOST
Allowed host to access the user interface. Default set to [*]

Example: '[localhost,127.0.0.1]

#### HATSTALL_DATABASE
Sqlite3 database used by hatstall
! This is not the sortinghat database.

#### HATSTALL_DEBUG
Hatstall debug mode enable. Default set to false

#### SHDB_USER
Sortinghat database username. Default set to sortinghat

__! This setting is not taken into account if shdb.cfg is present__

#### SHDB_PASSWORD
Sortinghat database password. Default set to password

__! This setting is not taken into account if shdb.cfg is present__

#### SHDB_NAME
Sortinghat database name. Default set to sortinghat

__! This setting is not taken into account if shdb.cfg is present__

#### SHDB_HOST
Sortinghat database hostname. default set to sortinghatdb

__! This setting is not taken into account if shdb.cfg is present__


### FILE
#### SHDB
Mount shdb.cfg at /var/www/django-hatstall/shdb.cfg with following content
```
[SHDB_Settings]
use=root
password=password
name=hatstall_sh
host=localhost
```

#### HTTP/HTTPS
By default this image only listen on port 80.
In order to use HTTPS, you must handle it by yourself with following informations:
* Mount ssl files at the place defined in you apache conf file
* Override '/etc/apache2/sites-available/000-default.conf'
* Override '/etc/apache2/sites-enabled/000-default.conf'

#### SQLITE3
The sqlite3 database is located at /var/www/hatstall.sqlite3

## Example

```
docker run \
  -i -t --rm \
  -p 80:80 \
  --name hatstall \
  -e "HATSTALL_DEBUG=True" \
  -e "HATSTALL_ALLOWED_HOST=['*']" \
  -e "SHDB_USER=sortinghat" \
  -e "SHDB_PASSWORD=password" \
  -e "SHDB_NAME=sortinghat" \
  -e "SHDB_HOST=sortinghatdb" \
  grimoirelab/hatstall:latest \

```
