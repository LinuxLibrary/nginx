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
