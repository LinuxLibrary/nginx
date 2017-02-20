# Standard NGINX Configuration

- For NGINX the base and main configuration file is ***/etc/nginx/nginx.conf*** as it contains all the main and mandatory configs.
- Let us add an include statement to pull our customized configs.
- We can see the ***ngin.conf*** file has an ***include*** directive in the ***http*** section which will tell the main config to pull the configs from.
- By default it will pull the configs from ***/etc/nginx/conf.d*** directory.
- We'll add an additional ***include*** directive to pull our configs from ***/etc/nginx/vhost.conf*** in which we are going to have our custom configs. Here we'll remove the ***server*** directive and have that in our custom config file.

```
# cp -prv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.`date +"%Y%m%d"`
# vi /etc/nginx/nginx.conf

include /etc/nginx/vhost.d/*.conf;
```

- If we are hosting multiple websites then we can have our ***SITE_NAME.d*** directory in place of ***vhost.d***. This will help us in hosting multiple websites to avoid confusion.
- Now let us create a directory named ***vhost.d*** and prepare our custom config.

```
# cd /etc/nginx
# mkdir vhost.d
# cp -prv conf.d/default.conf vhost.d/
```

- If you are unable to find the default.conf file in conf.d directory then you can copy from below

```
#
# The default server
#
server {
    listen       80;
    server_name  _;

    #charset koi8-r;

    #access_log  logs/host.access.log  main;

    # Load configuration files for the default server block
    # include /etc/nginx/default.d/*.conf;

    location / {
        root   /var/www/html;
        index  index.php index.html index.htm;
    }

    error_page  404              /404.html;
    location = /404.html {
        root   /usr/share/nginx/html;
    }

    error_page  500 502 503 504 /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # redirect server error pages to the static page /50x.html
    #
}
```

- Comment the ***include*** directive which points to load the default configs from the ***/etc/nginx/default.d***
- Change the document root to ***/var/www/html*** from ***/usr/share/nginx/html*** in the ***location*** section.
- Create the document root and create and index file.

```
# mkdir /var/www/html
# echo -e "WELCOME TO LINUX-LIBRARY NGINX WEBSERVER\nThis site is under development" > /var/www/html/index.html
```

- Once you are done with your customizations then restart the nginx service.
