# install nginx php on ubuntu
## Update the package list on your Ubuntu server:

```
sudo apt update
```

## Install Nginx:
```
sudo apt install nginx
```

## Install PHP and required modules:
```
sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc
```

## Configure Nginx to work with PHP:
```
sudo nano /etc/nginx/sites-available/default
```

## Add the following lines to the server block:
```
location / {
    try_files $uri $uri/ /index.php?$query_string;
}

location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
}
```
Save and exit the file.

## Test the configuration and restart Nginx:
```
sudo nginx -t
sudo systemctl restart nginx
```

# Nginx Configuration:

## In the /etc/nginx/nginx.conf file, you can modify the worker_processes and worker_connections values to optimize the use of system resources:

```
user www-data;
worker_processes 1;
worker_rlimit_nofile 8192;

events {
    worker_connections 512;
    multi_accept on;
}
```

This configuration sets Nginx to use only one worker process, limit the number of open file descriptors, and limit the number of connections per worker process.

## PHP Configuration:

## In the /etc/php/7.4/fpm/pool.d/www.conf file, you can modify the following PHP-FPM pool settings:

```
[www]
user = www-data
group = www-data
listen = /run/php/php7.4-fpm.sock
listen.backlog = 65535
listen.owner = www-data
listen.group = www-data
listen.mode = 0660
pm = dynamic
pm.max_children = 10
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
pm.max_requests = 500
```
These settings set PHP-FPM to use a Unix socket, limit the number of child processes, and adjust the number of processes according to demand.

## Other Optimizations:

You can also optimize the PHP opcache to reduce the load on the PHP interpreter and speed up script execution. In the /etc/php/7.4/fpm/php.ini file, you can modify the following opcache settings:

```
opcache.enable=1
opcache.enable_cli=0
opcache.memory_consumption=64
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=4000
opcache.revalidate_freq=2
opcache.fast_shutdown=1
```

These settings enable the opcache, allocate a limited amount of memory for caching, and set limits on the number of scripts that can be stored in the cache.

## PERMISSIONS FOR LARAVEL APP

Ensure that the file and directory ownership is correctly set: The first step is to ensure that the files and directories are owned by the user that Nginx is running as. On Ubuntu, the user is typically www-data. You can use the following command to set the ownership:

```
sudo chown -R www-data:www-data /var/www/project
```
Ensure that the file and directory permissions are correctly set: The second step is to ensure that the file and directory permissions are set correctly. You can use the following commands to set the correct permissions:

```
sudo find /var/www/project -type f -exec chmod 644 {} \;
sudo find /var/www/project -type d -exec chmod 755 {} \;
sudo chmod -R 775 /var/www/project/storage
sudo chmod -R 775 /var/www/project/bootstrap/cache
```


