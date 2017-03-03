# Custom Error Pages

- To have custom error pages we need to have our custom pages first. Let us create a custom error page.
- Go to your domain directory under ***/var/www/html***

```
# cd /var/www/html/lltest1/
# echo "###  404 - Page doesn't exist  ###" > 404.html
```

- Now we need to config this in our config file of this domain. We need to add it under server_name directive.

```
# vi /etc/nginx/vhost.d/www.lltest1.ll.conf

error_page 404 = /404.html;
location = /403.html {
	root /var/www/html/lltest1;
	internal;
}
```
