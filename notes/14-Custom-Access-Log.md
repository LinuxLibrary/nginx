# Customizing Access Log Format

- We can customize the Nginx logging format as per our choice.
- For customizing we need to use the ***log_format*** directive.
- Under the ***server_name*** directive we need to add a ***log_format*** directive followed by a name for this format.


```
log_format LLAccessFormat 'Remote IP: $remote_addr - Time Request: $time_local - User/Browser Agent: $http_user_agent';
```

- We can find most of the tags explained below. The log format can contain common variables, and variables that exist only at the time of a log write:

	- ***$bytes_sent***   
	The number of bytes sent to a client

	- ***$connection***   
	Connection serial number

	- ***$connection_requests***   
	The current number of requests made through a connection

	- ***$msec***   
	Time in seconds with a milliseconds resolution at the time of the log write

	- ***$pipe***   
	'p" if request was pipelined, "." otherwise

	- ***$request_length***   
	Request length (including request line, header, and request body)

	- ***$request_time***   
	Request processing time in seconds with a milliseconds resolution; time elapsed between the first bytes were read from the client and the log write after the last bytes were sent to the client.

	- ***$status***   
	Response status

	- ***$time_iso8601***   
	Local time in the ISO 8601 standard format

	- ***$time_local***   
	Local time in the Common Log Format

- Header lines sent to a client have the prefix “sent_http_”, for example, $sent_http_content_range.
- The configuration always includes the predefined “combined” format:

	> log_format combined '$remote_addr - $remote_user [$time_local] '
	>                   '"$request" $status $body_bytes_sent '
	>                   '"$http_referer" "$http_user_agent"';

```
Syntax:	open_log_file_cache max=N [inactive=time] [min_uses=N] [valid=time];
open_log_file_cache off;
Default:	
open_log_file_cache off;
Context:	http, server, location
```

- Defines a cache that stores the file descriptors of frequently used logs whose names contain variables. The directive has the following parameters:

	- `max`  sets the maximum number of descriptors in a cache; if the cache becomes full the least recently used (LRU) descriptors are closed

	- `inactive`  sets the time after which the cached descriptor is closed if there were no access during this time; by default, 10 seconds

	- `min_uses`  sets the minimum number of file uses during the time defined by the inactive parameter to let the descriptor stay open in a cache; by default, 1

	- `valid`  sets the time after which it should be checked that the file still exists with the same name; by default, 60 seconds

	- `off`  disables caching

	- Usage example:
	
	```
	open_log_file_cache max=1000 inactive=20s valid=1m min_uses=2;
	```
