# Return Directive

- If we are to develop some page navigations and if those doesn't exist then we can return some custom pages like 404. For this we can go with the location directive.

```
location /blog {
	return 404;
}
```

- We'll get a 404 error even if we have a proper location for blog exists. Because we are intentionally returning a 404 for /blog.
- We can also give a permanent redirect.

```
location /blog {
        return 301 http://linux-library.blogspot.in;
}
```
