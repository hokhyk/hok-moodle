####################Congratulations########################
Total OneinStack Install Time: 3032 minutes

Apache install dir:             /usr/local/apache

Database install dir:           /usr/local/mariadb
Database data dir:              /data/mariadb
Database user:                  root
Database password:              moodle

PHP install dir:                /usr/local/php

phpMyAdmin dir:                 /data/wwwroot/default/phpMyAdmin
phpMyAdmin Control Panel URL:   http://192.168.0.37/phpMyAdmin

redis install dir:              /usr/local/redis

Index URL:                      http://192.168.0.37/

install fileinfo:
./addons.sh
  option: 4


注意： 添加用户到某一个组 可以使用 usermod -G group_name user_name 这个命令可以添加一个用户到指定的组，但是以前添加的组就会清空掉。

所以想要添加一个用户到一个组，同时保留以前添加的组时，请使用 gpasswd 这个命令来添加操作用户：

gpasswd -a user_name group_name
gpasswd -a vagrant www
  
