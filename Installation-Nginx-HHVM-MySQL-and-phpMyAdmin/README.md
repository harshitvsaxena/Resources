<a id="top"></a>

# Installing NGINX, HHVM, MySQL, phpMyAdmin in Ubuntu

Installation is pretty easy. I'm doing installation using Ubuntu 16.04 LTS.
If you have any other Ubuntu Version it is pretty much same and also I've added
info which will help you installing on other distros also.

First open the terminal using `Ctrl+Alt+t`.

---

<a id="table_of_content"></a>
## Table of Contents

- [Installing Nginx](#installing_nginx)
- [Installing MySQL](#installing_mysql)
- [Installing HHVM](#installing_hhvm)
- [Configuring Nginx and HHVM](#configuring_nginx_and_hhvm)
- [Installing phpMyAdmin](#installing_phpmyadmin)

---

<a id="installing_nginx"></a>

## Installing Nginx

```sh
sudo apt-get update && sudo apt-get install nginx nginx-common nginx-core
sudo service nginx start
```

Now open the browser and point it to `http://localhost`

If the above link shows `Welcome to nginx!`, Congrats! Nginx is working correctly.

<a href="#table-of-contents">Table Of Content</a> | <a href="#top">Top</a>

---

<a id="installing_mysql"></a>

## Installing MySQL

```sh
sudo apt-get update
sudo apt-get install mysql-server mysql-client
```
The above command will ask you to set up a password for MySQL.

After this is complete, run this command:

```sh
mysql_secure_installation
```

It will ask following question:

```sh
Change the root password? [Y/n] `--> N`

Remove anonymous users? [Y/n] `--> Y`

Disallow root login remotely? [Y/n] `--> Y`

Reload privilege tables now? [Y/n] `--> Y`
```
Now MySQL is installed. Great!

<a href="#table-of-contents">Table Of Content</a> | <a href="#top">Top</a>

---

<a id="installing_hhvm"></a>

## Installing HHVM

HHVM has not given official release for 16.04 LTS as of now. So I've installed
release for 15.10 Wily Werewolf and it is working perfect. But you need to check
for your release at this link: `https://docs.hhvm.com/hhvm/installation/linux`

Please visit the above link and only download the one for your Ubuntu version.

```sh
# installs add-apt-repository
sudo apt-get install software-properties-common

sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449
sudo add-apt-repository "deb http://dl.hhvm.com/ubuntu $(lsb_release -sc) main"
sudo apt-get update
sudo apt-get install hhvm
```

#### Setup hhvm FCGI
```sh
sudo /usr/share/hhvm/install_fastcgi.sh
```

<a href="#table-of-contents">Table Of Content</a> | <a href="#top">Top</a>

---

<a id="configuring_nginx_and_hhvm"></a>

## Configuring Nginx and HHVM

#### Steps to follow:

1 - Use this
```sh
cd /etc/nginx/sites-available/
sudo vim default
```
Make these changes:
* Find `server_name _;`
* Change it to `server_name localhost;`
* Check whether `include hhvm.conf` is there in the file if it's not there add it below the `server_name localhost;`.
* Also add `index.php` in the line `index index.html index.htm index.nginx-debian.html;` so that it will look like this `index index.html index.htm index.nginx-debian.html index.php;`.
* For making changes to the file, press `i` on your keyboard and start making changes.
* After you are done save it by pressing `esc` key and entering `:x` or `:wq`.
* Please be careful while using vim otherwise you can use nano: `sudo nano default`.
* You may have to install vim using `sudo apt-get install vim`.

2 - Now,
```sh
sudo vim /etc/nginx/hhvm.conf
```
* Comment the line `fastcgi_pass 127.0.0.1:9000;` by putting `#` in front of this line like this: `# fastcgi_pass 127.0.0.1:9000;`.
* Now add this `fastcgi_pass unix:/var/run/hhvm/hhvm.sock;` below the above line.
* Save it the same way as done above.

3 - Again,
```sh
sudo vim /etc/nginx/server.ini
```
* Comment the line `hhvm.server.socket = 9000` by putting `#` in front of this line like this: `# hhvm.server.socket = 9000`.
* Now add this `hhvm.server.file_socket=/var/run/hhvm/hhvm.sock` below the above line.
* Save it the same way as done above.

4 - One last thing, please check whether your html folder has correct ownership. If it's owner is root you might not be able to get result. Use these command
```sh
cd /var/www/
sudo chown www-data:www-data -R html
sudo chmod 777 -R html
```

5 - Restart all the services like this:
```sh
sudo service nginx restart
sudo service mysql restart
sudo service hhvm restart
```
Congrats, you have successfully installed and configure Nginx, HHVM and MySQL.

6 - Test, whether it is working or not by just creating index.php inside html folder and runing it in browser.

* Make a new file using:
```sh
sudo vim /var/www/html/index.php
```

* Write this inside the php file:
```php
<?php
echo phpinfo();
?>
```
* Now direct your browser to `localhost` or `localhost/index.php`.
* If the result is a blue box showing details of HHVM. Great `Mission Accomplished`.

<a href="#table-of-contents">Table Of Content</a> | <a href="#top">Top</a>

---

<a id="installing_phpmyadmin"></a>

## Installing phpMyAdmin

Hold on soldier, still one thing remaining:

Install it using:
```sh
sudo apt-get update
sudo apt-get install phpmyadmin
```

During the installation, a prompt will open for more information. It will ask which web server to automatically configure. Since Nginx is not one of the available options, just hit TAB to bypass this prompt.

The next prompt will ask if you would like dbconfig-common to configure a database for phpmyadmin to use. Select "Yes" to continue.

It will ask for the database administrative password that we configured during the MySQL installation to allow these changes. Afterward, it will ask to select and confirm a password for a new database that will hold phpMyAdmin's own data.

For the Nginx web server to find and serve the phpMyAdmin files correctly, we just need to create a symbolic link from the installation files to our Nginx document root directory by typing this:

```sh
sudo ln -s /usr/share/phpmyadmin /usr/share/nginx/html
```

Also make a symbolic link like this, it will make sure phpmyadmin is working:

```sh
sudo ln -s /usr/share/phpmyadmin /var/www/html/
```

Hold on some packet are missing in this installation, use this:
```sh 
sudo apt-get install php-mbstring php7.0-mbstring php-gettext
```

If you have phpMyAdmin already installed then you can reconfigure it using:

```sh
sudo dpkg-reconfigure phpmyadmin
```

Again restart all the services like this:

```sh
sudo service nginx restart
sudo service mysql restart
sudo service hhvm restart
```

Now go to browser and direct it to: `localhost/phpmyadmin/`. It will show phpmyadmin login which you can login through the username and password provided at the time of installation.

<a href="#table-of-contents">Table Of Content</a> | <a href="#top">Top</a>

---

Yes! Finally you are all set for a wonderful web development environment. Go on now, start coding.

## Happy Coding
# THE END 
