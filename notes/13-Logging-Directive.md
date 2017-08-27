# Logging Directive

- By default while our webpage get some hits then the actions will be logged to either access/error log files based on the scenario.
- In default case the settings of these logs are configured in our nginx base config file.
- We can modify those as per our choice like for a domain level or some thing else.
- If we have multiple domains then we can do that for a domain level.
- In such case we need to add those log directives to our nginx domain based config file located in our ***vhost.d*** directory.
- We need to add the log directives under the ***server_name*** directives.

```
# vi /etc/nginx/vhost.d/www.lltest1.ll.conf

access_log /var/log/nginx/lltest1.access.http.log;
error_log /var/log/nginx/lltest1.error.http.log;
```

- In the same way we can have separate log files to log our https traffic.
- Add the following lines under the server_name directive in the server section for https block.

```
access_log /var/log/nginx/lltest1.access.https.log;
error_log /var/log/nginx/lltest1.error.https.log;
```

- One more thing about logging we need to keep in mind is that is our webserver is getting more traffic then as the logs will being constantly being written then we'll have to face issue with the machine as we'll have lot of I/O happening on the server.
- To overcome this situation we need to use buffers for the logs we have lot of I/O on.
- Means we will be having more I/O for the access log. Then we need to use buffer for that.
- To do this we just need to add the ***buffer*** and its size at the end of the access_log line.

```
access_log /var/log/nginx/lltest1.access.https.log combined buffer=32k;
```

- The contents of the buffer will be written to the log file only when it is filled up and once the contents of the buffer written to the log then the contents of the buffer will be flushed.


