# Location Block Syntax

Before we cover how Nginx decides which location block to use to handle requests, let's go over some of the syntax you might see in location block definitions. Location blocks live within server blocks (or other location blocks) and are used to decide how to process the request URI (the part of the request that comes after the domain name or IP address/port).

- Location blocks generally take the following form:

```
location optional_modifier location_match {
    ....
}
```

The location_match in the above defines what Nginx should check the request URI against. The existence or nonexistence of the modifier in the above example affects the way that the Nginx attempts to match the location block. The modifiers below will cause the associated location block to be interpreted as follows:

- ***(none):*** If no modifiers are present, the location is interpreted as a prefix match. This means that the location given will be matched against the beginning of the request URI to determine a match.
	
	```
	location /site {
	    ....
	}
	```

- ***=:*** If an equal sign is used, this block will be considered a match if the request URI exactly matches the location given.

	```
	location = /page1 {
	    ....
	}
	```

- ***~:*** If a tilde modifier is present, this location will be interpreted as a case-sensitive regular expression match.

	```
	location ~ \.(jpe?g|png|gif|ico)$ {
	    ....
	}
	```

- ***~*:*** If a tilde and asterisk modifier is used, the location block will be interpreted as a case-insensitive regular expression match.

	```
	location ~* \.(jpe?g|png|gif|ico)$ {
	    ....
	}
	```

- ***^~:*** If a carat and tilde modifier is present, and if this block is selected as the best non-regular expression match, regular expression matching will not take place.

	```
	location ^~ /costumes {
	    ....
	}
	```
