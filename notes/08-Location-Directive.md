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

Nginx evaluates the possible location contexts by comparing the request URI to each of the locations. It does this using the following algorithm:

	- Nginx begins by checking all prefix-based location matches (all location types not involving a regular expression). It checks each location against the complete request URI.
	- First, Nginx looks for an exact match. If a location block using the = modifier is found to match the request URI exactly, this location block is immediately selected to serve the request.
	- If no exact (with the = modifier) location block matches are found, Nginx then moves on to evaluating non-exact prefixes. It discovers the longest matching prefix location for the given request URI, which it then evaluates as follows:
		- If the longest matching prefix location has the ^~ modifier, then Nginx will immediately end its search and select this location to serve the request.
		- If the longest matching prefix location does not use the ^~ modifier, the match is stored by Nginx for the moment so that the focus of the search can be shifted.
	- After the longest matching prefix location is determined and stored, Nginx moves on to evaluating the regular expression locations (both case sensitive and insensitive). If there are any regular expression locations within the longest matching prefix location, Nginx will move those to the top of its list of regex locations to check. Nginx then tries to match against the regular expression locations sequentially. The first regular expression location that matches the request URI is immediately selected to serve the request.
	- If no regular expression locations are found that match the request URI, the previously stored prefix location is selected to serve the request.

It is important to understand that, by default, Nginx will serve regular expression matches in preference to prefix matches. However, it evaluates prefix locations first, allowing for the administer to override this tendency by specifying locations using the = and ^~ modifiers.

It is also important to note that, while prefix locations generally select based on the longest, most specific match, regular expression evaluation is stopped when the first matching location is found. This means that positioning within the configuration has vast implications for regular expression locations.
