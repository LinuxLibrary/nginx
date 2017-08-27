# VHosts Files

- Till now we have seen how to configure a basic webserver for our local host.
- Let us now see the process of configuring a custom website.
- Either we should have our DNS configured for the site we are looking for or we can put an entry in the ***/etc/hosts*** file for the IP which we want to host from.
- In my case I want to name my website as ***www.lltest1.ll***, so I am adding an entry for that in the ***/etc/hosts*** file

```
# vi /etc/hosts

192.168.1.110	www.lltest1.ll	lltest1.ll
```

- Now I'll create a config file for this website. For this we need to create a config file in the ***vhost.d*** directory.
- If we name our custom website config files with the name of the site followed by an extension ***.conf*** would be easier for us to know which config file corresponds to which site.

```
# cd /etc/nginx/vhost.d/
# vi www.lltest1.ll.conf

server {
	listen 80;
	
	root /var/www/html/lltest1;
	index index.html index.htm index.php;

	server_name www.lltest1.ll lltest1;
}
```

- In the above case we are giving the alias name of our website. As in nginx we have ***server_name*** directive capable to handle both server name and server alias functions.
- After creating the config file check for any errors.

```
# nginx -t
```
- Now let us create the root directory for this site and an index file

```
# mkdir -p /var/www/html/lltest1
# cd /var/www/html/lltest1
# echo "WELCOME TO LINUX_LIBRARY_TESTING SITE" > index.html
```

- Reload the service and test the new site

```
# nginx -s reload
# elinks http://www.lltest1.ll
# elinks http://lltest1
```
