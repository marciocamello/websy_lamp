# Websy Lamp with Docker

### Containers

- Nginx
- PHP-FPM
- MariaDB
- MongoDB
- PhpMyAdmin
- NodeJS 6

### Nginx
 
[NGINX official docker hub] https://hub.docker.com/_/nginx/

- Samples
  - laravel.conf
  - codeigniter2.conf
  - codeigniter3.conf
  - yii2-app-basic.conf
  - yii2-app-advanced.conf  
  
### PHP-FPM
 
[PHP official docker hub] https://hub.docker.com/_/php/

- Switch php version

```yml
php-fpm:
        #image: php:5.6-fpm -> uncomment this line
        image: php:fpm -> comment or remove this line
        container_name: websy-php-fpm
        restart: always
        build:
            context: .
            dockerfile: php-fpm/Dockerfile
        volumes:
            - /home/developer:/home
            - /home/developer/docker/websy_lamp/php-fpm/php.ini:/etc/php/7.1/fpm/conf.d/99-overrides.ini
        links:
            - mariadb
```        

### MariaDB
 
[MariaDB official docker hub] https://hub.docker.com/_/mariadb/

- Change env params
  - 
