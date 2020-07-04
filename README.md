# C10M
## Introduction
In this article we'll investigate how to solve the **C10M problem**, or how to handle 10 millions concurrent web users on commodity hardware. We'll try to constrain ourselves to using one or **two 1 gigabit/s dedicated servers** and eventually scaling out using the cloud, and with a **budget of 300 euros** per month, excluding personnel salary.

In order to achieve our goals we'll have to rethink how the clients will interact with the backend, exploiting what modern browsers offer us. We'll also make sure to deliver the fastest user experience possible, while forcing as few rules as possible to developers.

## Smart Client
### Fetch patching and HTTP 304

The traditional way to scale web services is to use load balancers and caches. Typically once a single server can't handle anymore the peak load, the domain will be rerouted to a service whose sole purpose is to spread the load, locally or over the network. Common examples are Nginx in a reverse proxy configuration, HAproxy, or dedicated hardware solutions.
My idea is to move the load balancer inside the client, hence the *smart client* name, exploiting Service Worker capabilities to patch fetch requests and reroute them to cache, if possible, or to the first available endpoint.
![Flow diagram of a fe](https://raw.githubusercontent.com/alberto-esposito/C10M/master/assets/fetch_flow.svg)

### User segmentation

Hello

 - Shared Worker:  Browsers that support sharing threads across tabs. Modern blink-based browsers, 
 - Service Worker: Browsers that  Webkit powered browsers, older browsers 
 - No Javascript:
 
 Other features useful to segment the user base:
 - Compression support:
 - Media support:


## Backend Architecture
![Server Layout](https://raw.githubusercontent.com/alberto-esposito/C10M/master/assets/server.svg)
### Hybrid Cloud Approach
hello
### Optimizations
#### Unix Domain sockets vs TCP/IP protocol
#### HTTP/3
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5NjE3OTU4Niw5MTcwOTgxMjMsLTYxMj
EyNTk1LC0yMTE4NTYzNjE4LC0xMjg1OTA2MDEwLC02MzgyMTY5
MjUsLTIwMjMxMzUyMiwtMTA3NDY1ODM1OSwtNDMwNzEwMDA2LD
U5NjkyNDM2XX0=
-->