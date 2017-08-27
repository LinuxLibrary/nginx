# Basic Rewrites

- Before using the reqrite directive let us know something about when to use that.
- If we have blog in our website which has been moved as blogs then everyone who accesses through the old links to anything under /blog will now be server as we have blogs.
- In such case we can serve those requests with a ***reqrite*** directive with regular expressions.

```
location /blog {
	root /var/www/html/lltest1;
	rewrite ^/blog/(.*)$ http://www.lltest1.ll/blogs/$1 permanent;
}
```

```
location /FAQ {
	root /var/www/html/lltest1/blogs;
	rewrite ^/FAQ/(.*)$ http://www.lltest1.ll/FAQs/$1 permanent;
}
```

- Here we are taking anyting which comes under /blog/FAQ into a variable and service those at /blog/FAQs/ with that same name as a permanent rewrite.
