Install the required packages:

```
sudo apt-get update
sudo apt-get install supervisor
```
Create a new Laravel project:

Create a new supervisor configuration file for the queue worker:

```
sudo nano /etc/supervisor/conf.d/laravel-worker.conf
```
Add the following configuration to the file and save it:

```
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/project/artisan queue:work --queue=high,low
autostart=true
autorestart=true
user=www-data
numprocs=1
redirect_stderr=true
stdout_logfile=/var/log/laravel-worker.log
```
Replace /path/to/artisan with the path to the artisan script in your Laravel project.

Create a new supervisor configuration file for the CRONS worker:

```
sudo nano /etc/supervisor/conf.d/laravel-crons.conf
```

Add Following configuration to the file:

```
[program:laravel-crons]
process_name=%(program_name)s_%(process_num)02d
directory=/var/www/project/
command=php artisan schedule:work
autostart=true
autorestart=true
user=root
numprocs=1
redirect_stderr=true
stdout_logfile=/var/log/laravel-crons.log
```

Reread the Supervisor configuration and start the queue worker:

```
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl restart laravel-worker:*
sudo supervisorctl restart laravel-crons:*
```
This will start the queue worker and it will listen for new jobs to process.

To dispatch a job to the queue, you can use Laravel's dispatch method:

```
dispatch(new ProcessJob($args));
```
