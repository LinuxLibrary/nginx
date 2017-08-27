# Optimizing the NGINX Configurations

- Location of the nginx main config file is ***/etc/nginx/nginx.conf***
- Let us know about this configuration file and its options first
- ***worker_processes***
	- This is responsible for machine to know how many workers are available to spawned after getting bounded to an IP / Port.

- ***worker_connections***	
	- By default this will be set to ***1*** but depending on the connections the host can accept we can change it.
	- Through ***ulimit -n*** we can know the max number of connections allowed to a host.

	```
	worker_connections 1024;
	```

- ***Buffers***
This section should be placed in the ***html*** section and before the ***include*** statement of the nginx config file.

	- ***client_body_buffer_size***
	
	```
	client_body_buffer_size	10k;
	```

	- ***client_header_buffer_size***

	```
	client_header_buffer_size 1k;
	```

	- ***client_max_body_size***

	```
	client_max_body_size 8m;
	```

	- ***large_client_header_buffers***

	```
	large_client_header_buffers 2 1k;
	```

- ***Timeouts***
This will tell the server to know the max time to wait after a request has been received from a client. There are 2 types of timeouts.
	- ***client_body_timeout***
	This can be set to a max of 12 seconds.

	```
	client_body_timeout 12;
	```

	- ***client_header_timeout***
	Maintaining the same as the timeout for the body

	```
	client_header_timeout 12;
	```

	- ***keep_alive_timeout***, ***send_timeout***
	These will let the system know till when a request can be waited and when to send the error if not able to serve the request. If you already have these then you can modify those as per your choice.

	```
	keep_alive_timeout 15;
	send_timeout 10;
	```
	
- Test your configurations
This would always be a good practice to verify your config before restarting the application as you can get to know where you have misconfigured.

```
# nginx -t

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

- Restart nginx

```
# systemctl restart nginx
```
