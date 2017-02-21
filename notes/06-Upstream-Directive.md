# Upstream Directive and Load Balancing

- We have did this exercise for proxying and load balancing Apache-Tomcat with Nginx.
- [Proxy with NGINX](https://github.com/LinuxLibrary/tomcat/blob/master/notes/09-Proxy-Connection.md)
- [Load Balancing with NGINX](https://github.com/LinuxLibrary/tomcat/blob/master/notes/10-Basic-Clustering.md)

- Here while using the default function of loadbalancing with Nginx Upstream directive it uses round-robin method.
- Means if we have configured LoadBalancing between 2 nodes then the Nginx will forward traffic to 1 hit to 1 server and the 2nd hit to another and goes on.
- If we are clear that one of the 2 machines can handle more load then we can prioritize that host to have the number of consicutive connections through the ***weight*** function used along with the ***server*** in the ***upstream*** directive.
- Let us try this for the above Load Balancing concept of Tomcat

- ***OLD***
```
upstream myTomcat {
    server dev01.linux-library.ll:8080;
    server dev02.linux-library.ll:8081;
}
```

- ***NEW***
```
upstream myTomcat {
    server dev01.linux-library.ll:8080 weight=1;
    server dev02.linux-library.ll:8081 weight=2;
}
```

- Means 1 connection will be forwarded to dev01 and 2 connections will be forwarded to dev02.
- We are going to have 2 times the load of dev01 coming in dev02
