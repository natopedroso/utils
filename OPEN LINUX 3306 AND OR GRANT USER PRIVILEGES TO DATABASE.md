# To open port 3306 in Ubuntu and grant remote access to the sos user on the sos database, you can follow these steps:

# Open the MySQL configuration file:

```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
Find the bind-address line and comment it out by adding a # character at the beginning:

```
#bind-address           = 127.0.0.1
```
This will allow MySQL to listen for connections from any IP address, not just localhost.

Save the file and exit the editor.

Restart the MySQL service to apply the changes:
```
sudo systemctl restart mysql
```
Log in to the MySQL server as the root user:

```
mysql -u root -p
```
Create a new user sos with a password and grant it all privileges on the sos database:

```sql
CREATE USER 'sos'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON sos.* TO 'sos'@'%';
```
Replace 'password' with a strong password for the sos user.

Flush the privileges to apply the changes:

```sql
FLUSH PRIVILEGES;
```
Exit the MySQL server:

```
exit;
```
Allow incoming traffic on port 3306 in the Ubuntu firewall:

```
sudo ufw allow 3306/tcp
```
