#install nginx php on ubuntu.md
##Update the package list on your Ubuntu server:

´´´
sudo apt update
´´´

Install Nginx:
´´´
sudo apt install nginx
´´´
Install PHP and required modules:

Copy code
sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc
Configure Nginx to work with PHP:

javascript
Copy code
sudo nano /etc/nginx/sites-available/default
Add the following lines to the server block:

javascript
Copy code
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
}
Save and exit the file.

Test the configuration and restart Nginx:

Copy code
sudo nginx -t
sudo systemctl restart nginx
Now you have PHP and Nginx installed and configured together on your Ubuntu server. You can create PHP files and serve them using Nginx.
