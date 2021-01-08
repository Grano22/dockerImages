# Docker Images Repository
Cheers to my Docker Images repository, you can use this images to deploy target solutions. Have a fun!

1. dockerfile.mysqlready | PHP 7.3
* build with command: docker build -f ./dockerfile.mysqlready -t php7.3-fpm/mysqlready .
* build with compose:
```yml
version: '1'
services:
  web:
    image: php7.3-fpm/mysqlready
    links:
      - mysql:db
    volumes:
      - '{specify_your}'
    ports:
      - "8000:8080"
    command: "php -S 0.0.0.0:8080"
    working_dir: {specify_your}
    container_name: phpServer
  mysql:
    image: mysql
    ports:
      - "3306:3306"
    command: mysqld --user=root --default-authentication-plugin=mysql_native_password
    environment:
      - MYSQL_ROOT_PASSWORD={your_mysql_root_password}
    container_name: mysqlServer
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    links:
      - mysql:db
    depends_on: 
      - mysql
    ports:
      - "8082:80"
    environment:
      - PMA_USER=root
      - PMA_PASSWORD={your_mysql_root_password}
      - PHP_UPLOAD_MAX_FILESIZE=100MB
    container_name: phpAdminSQLHost
```

