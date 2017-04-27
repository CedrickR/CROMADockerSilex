1 : Create Docker images
-----------------------------

In Docker directory, run the commands : 
```bash
docker build -t croman/apache:2.4 ./apache2.4/
docker build -t croman/php-fpm:7.0 ./php-fpm7.0/
docker build -t croman/mysql:5.7 ./mysql5.7/
docker build -t croman/phpmyadmin:4.6 ./phpmyadmin4.6/
```

2 : Modify docker-compose.yml
-----------------------------
You must modify volumes for `croman_database` , `croman_php` and `croman_web` containers with your own directory, for example :
```yaml
    croman_database:
        container_name: croman_database
        environment:
            MYSQL_ROOT_PASSWORD: password_root
            MYSQL_DATABASE: database_name
            MYSQL_USER: user_name
            MYSQL_PASSWORD: password_name
		...
        volumes:
            - "/xxx/xxx/CROMADockerSilex/Data:/var/lib/mysql"
    croman_php:
        container_name: croman_php
        ...
        volumes:
            - "/xxx/xxx/CROMADockerSilex/Silex:/var/www/html"
    croman_web:
        container_name: croman_web
        ...
        volumes:
            - "/xxx/xxx/CROMADockerSilex/Logs/Apache2:/var/log/apache2"
```

3 : Run the application
-----------------------------

In Silex directory, run the command :
```bash
$ docker-compose up -d
```

4 : Test the application
-----------------------------

Add virtual host in file `/etc/hosts`. Open it and add this line :
```bash
127.0.0.1     app.local
```

Silex application : [app.local:60000/index.php](http://app.local:60000/index.php)

PHPMyAdmin : [app.local:60002](http://app.local:60002)

MySQL : [app.local:3306](http://app.local:3306) and hostname : croman_database

5 : Stop the application
-----------------------------
In Symfony directory, run the command :
```bash
$ docker-compose stop
```