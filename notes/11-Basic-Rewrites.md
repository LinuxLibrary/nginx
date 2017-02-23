# Basic Rewrites

- Before using the reqrite directive let us know something about when to use that.
- If we have FAQ under the blog in our website which has been moved as FAQs then everyone who accesses through the old links to anything under /blog/FAQ will now be server as we have FAQs in place of FAQ.
- In such case we can serve those requests with a ***reqrite*** directive with regular expressions.

```
location /blog/FAQ {
	rewrite ^/blog/FAQ/(.*)$ http://www.lltest1.ll/blog/FAQs/$1 permanent;
}
```

- Here we are taking anyting which comes under /blog/FAQ into a variable and service those at /blog/FAQs/ with that same name as a permanent rewrite.
