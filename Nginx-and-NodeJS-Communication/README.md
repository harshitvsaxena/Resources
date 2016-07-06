<a id="top"></a>

# Nginx and Node.js Communication

Getting Nginx as front-end web server and node.js to work as the back-end server is the best combination to have for any node.js application.

In this document we are going to see how we can setup such an environment.

I am here assuming that you have already installed Nginx and NodeJS in your system. If not please go through these installation. You can use these links for help:

- Nginx Installation: [Installation-Nginx-HHVM-MySQL-and-phpMyAdmin](../Installation-Nginx-HHVM-MySQL-and-phpMyAdmin/README.md)
- NodeJS Installation: https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-an-ubuntu-14-04-server

Please complete these installation before starting this. Also I assume you are having a node.js app running to know if the setup is working or not.

If you do not have an app in node.js, please go through this link to create your first app: http://socket.io/get-started/chat/

It is pretty easy and you will get to learn a lot about node.js

Also before getting start use this so that you don't have to do sudo everytime:

```sh
$ sudo su
# cd ~
```
or you can directly do

```sh
$ sudo -s
```

Now let's get started:

#### Step 1. Create a directory

Create a directory from where the node.js app will be served. I have created inside `\var\www` folder.

You can create this directory anywhere,

```sh
# mkdir /var/www/node
```

#### Step 1. Copy-Paste

We need to copy the `default` file at this location `/etc/nginx/sites-available/`:

```sh
# cp /etc/nginx/sites-available/default /etc/nginx/sites-available/node
```

#### Step 2. Change The Content

Now open this file at `/etc/nginx/sites-available/node`

```sh
# vim /etc/nginx/sites-available/node
```

and change the structure of server block in this file like this:

```
server {
        listen 80;
        listen [::]:80;

        server_name node.localhost;

        root /var/www/node;
        #index index.html index.htm;

        location / {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;
                proxy_set_header X-NginX-Proxy true;
                proxy_pass http://127.0.0.1:8124/;
                proxy_redirect off;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";

                proxy_redirect off;
                proxy_set_header   X-Forwarded-Proto $scheme;
                #proxy_cache $my_cache;
                proxy_cache_key sfs$request_uri$scheme;
                #try_files $uri $uri/ =404;
        }
}
```

You can edit the file by hitting `i` key.

So in the above code make sure to give port in line `proxy_pass http://127.0.0.1:8124/;` which you are using for node.js app. I'am using port `8124` so I have added this.

Also in the line `root /var/www/node;` give the address of the directory where you have the node.js application.

Now save this by using `esc` key and entering `:x` or `:wq` and hitting `Enter` key.

#### Step 3. Make Symbolic link

Now we need to create a symbolic link in `sites-enabled` folder so as this can be actually served by the nginx server.

```sh
# ln -s /etc/nginx/sites-available/node /etc/nginx/sites-enabled/
```

#### Step 4. Change /etc/hosts file

This step is not necessary, but for being on the safe side.

Open `/etc/hosts` file:

```sh
# vim /etc/hosts
```

Now add this line in the above file:

```
127.0.0.1   node.localhost
```

#### Step 5. Testing the Setup

Restart the Nginx Server:

```sh
# service nginx restart
```

Now start your node.js app:

```sh
# node index.js
```

Now redirect your browser to `http://node.localhost`, you will be able to see the node.js app running there.

---

Resource: http://blog.danyll.com/setting-up-express-with-nginx-and-pm2/

[Top](#top)

---

## The End
