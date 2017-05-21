# Websy Lamp with Docker

### Requirements

 - Docker - https://docs.docker.com/engine/installation/
 - Docker Compose 3 - https://docs.docker.com/compose/install/
 
### Usage

```bash
git clone https://github.com/marciocamello/websy_lamp.git
cd websy_lamp
docker-compose up -d
```

### Containers

- Nginx
- PHP-FPM
- MariaDB
- MongoDB
- PhpMyAdmin
- NodeJS 6

### Nginx
 
[NGINX official docker hub] - https://hub.docker.com/_/nginx/
  
- Config

```yml
nginx-server:
    image: nginx:latest
    container_name: websy-nginx-server
    restart: always
    volumes:
        - /home/developer:/home
        - /home/developer/docker/websy_lamp/nginx/conf:/etc/nginx/conf.d
    ports:
        - "80:80"
        - "443:443"
    links:
        - php-fpm
        - mariadb
```            

- Samples
  - laravel.conf
  - codeigniter2.conf
  - codeigniter3.conf
  - yii2-app-basic.conf
  - yii2-app-advanced.conf  
  
### PHP-FPM
 
[PHP official docker hub] - https://hub.docker.com/_/php/
  
- Config

```yml
php-fpm:
    #image: php:5.6-fpm -> uncomment this line to switch php version
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
 
[MariaDB official docker hub] - https://hub.docker.com/_/mariadb/
  
- Config

```yml
mariadb:
    image: mariadb:latest
    container_name: websy-mariadb
    restart: always
    ports:
        - "3306:3306"
    volumes:
        - /home/developer/docker/websy_lamp/mariadb/conf:/etc/mysql/conf.d
    environment:
      - MYSQL_ROOT_PASSWORD=root       
      - MYSQL_USER=root      
      - MYSQL_PASSWORD=root 
```

- Change env params
  - MYSQL_ROOT_PASSWORD=root       
  - MYSQL_USER=root      
  - MYSQL_PASSWORD=root
  
### MongoDB
 
[MongoDB official docker hub] - https://hub.docker.com/_/mongo/
  
- Config

```yml
mongodb:
    image: mongo:3
    command: mongod --noprealloc --smallfiles --replSet mongodb --dbpath /data/db --nojournal --oplogSize 16 --noauth
    container_name: websy-mongodb
    restart: always
    volumes:
        - /home/developer/docker/websy_lamp/mongodb/data:/data/db
    ports:
        - "27017:27017"  
    links:
        - nodejs   
```

### PhpMyAdmin 
 
[PhpMyAdmin official docker hub] - https://hub.docker.com/r/phpmyadmin/phpmyadmin/
  
- Config

```yml
phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: websy-phpmyadmin
    restart: always
    ports:
        - "8080:80"
    links:
        - mariadb:db 
```

### NodeJS

[NodeJS official docker hub] - https://hub.docker.com/_/node/
  
- Config

```yml
nodejs:
    image: node:6
    container_name: websy-nodejs
    restart: always
    build:
        context: .
        dockerfile: nodejs/Dockerfile
    ports:
        - "8009:8009"  
    volumes:
        - /home/developer:/home
    links:
        - mariadb
        - nginx-server
```
