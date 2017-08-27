# Working with ROOT and ALIAS Directives

- In this case I am trying to host a static file server to serve my files in the file system.
- And I want this happen without affecting the current running webserver.
- For this I am commenting the root and index directives and providing 2 seperate location directives.

```
#        root /var/www/html/lltest1;
#        index index.html index.htm index.php;
```

- In the first location section I am specifying the directory root of the webserver.

```
        location / {
                root /var/www/html/lltest1/;
                index index.html index.htm index.php;
        }
```

- In the second location I am specifying my aliaas for hosting the file server.

```
        location /rhel7/ {
                alias /u01/yum/rhel7/;
                index index.html index.htm index.php;
                autoindex on;
                try_files $uri $uri/ =404;
        }
```


