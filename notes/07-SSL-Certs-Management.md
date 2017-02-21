# SSL Certificate Management

- Create a directory for SSL certificates in ***/etc/nginx***

```
# mkdir -p /etc/nginx/ssl
cd /etc/nginx/ssl
```

- Generate a certificate

```
# openssl genrsa -des3 -out server.key 1024
```

> NOTE : You need to give a pass phrase to generate your key between 4 to 8191 characters

- Now let us use this key to create a signin certificate request

```
# openssl req -new -key server.key -out server.csr
Enter pass phrase for server.key:
Country Name (2 letter code) [XX]:IN
State or Province Name (full name) []:AP
Locality Name (eg, city) [Default City]:Hyderabad
Organization Name (eg, company) [Default Company Ltd]:Linux-Library
Organizational Unit Name (eg, section) []:IT
Common Name (eg, your name or your server's hostname) []:dev02
Email Address []:vmsnivas@gmail.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```

> NOTE: Leave the extra attributes blank

- Now we need to remove the pass phrase for the ***server.key*** or else NGINX will prompt for the pass phrase every time you restart it.
- Backup your ***server.key*** file

```
# cp -prv server.key server.key.`date +"%Y%m%d"`.bak
```

- Now we can use the backup key file as input and the main file as the output with an empty phrase to remove the pass phrase.

```
# openssl rsa -in server.key.`date +"%Y%m%d"`.bak -out server.key
```

> NOTE: We need to give the passphrase here but it will rewrite the server.key file without a pass phrase

- Now we need to sign and create our certificate

```
# openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

- We have our certificate ready and all we need to do now is to prepare our server to answer the requests over ***https*** on ***443*** port
- For this we need to add a new server section to serve the requests to listen on 443 in our custom config file in /etc/nginx/vhost.d

```
# vi www.lltest1.ll.conf

server {
        listen 443;

        root /var/www/html/lltest1;
        index index.html index.htm index.php;

        server_name www.lltest1.ll lltest1;

        ssl on;
        ssl_certificate /etc/nginx/ssl/server.crt;
        ssl_certificate_key /etc/nginx/ssl/server.key
}
```

- Here we are saying NGINX to turn on SSL function for this site and use the certificate and the key provided below.
- Verify the configuration

```
# nginx -t
```

- Reload the NGINX service

```
# nginx -s reload
```

- Now you can verify your website from any browser. It will shows an error as you are not registered your certificate with neither of the third party certificate providers. But there is no issue as yours is a self signed certificate. You can use proceed unsafe option to go ahead and use your site.
