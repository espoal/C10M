# C10M
## Introduction
<p align="justify">
In this article we'll investigate how to solve the **C10M problem**, or how to handle 10 millions concurrent web users on commodity hardware. We'll try to constrain ourselves to using one or **two 1 gigabit/s dedicated servers** and eventually scaling out using the cloud, and with a **budget of 300 euros** per month, excluding personnel salary.

In order to achieve our goals we'll have to rethink how the clients will interact with the backend, exploiting what modern browsers offer us. We'll also make sure to deliver the fastest user experience possible, while forcing as few rules as possible to developers.
</p>

## Smart Client
### Fetch patching and HTTP 304
<p align="justify">
The traditional way to scale web services is to use load-balancers and caches. Typically once a single server can't handle anymore the peak load, the domain will be rerouted to a service whose sole purpose is to spread the load, locally or over the network. Common examples are Nginx in a reverse proxy configuration, HAproxy, or dedicated hardware solutions.  

My idea is to move the load-balancer inside the client, hence the *smart client* name, exploiting Service Worker capabilities to patch fetch requests and reroute them to cache, if possible, or to the best endpoint according to latency and load. Here's a flow diagram of how requests are handled:  
 
![Flow diagram of a fetch event](https://raw.githubusercontent.com/alberto-esposito/C10M/master/assets/fetch_flow.svg)
</p> 

### Pure functions and the cache
Functional programming has become popular in the Javascript world thanks to React, but is well suited to front end programming in general. 
```js
page = async* render(state)
newState = async eventHandler(oldState, event)
updates = async* conciliate(newState, oldState)
```

### Smart requests
Don't request everything, read as stream
### User segmentation

It's important 

 - Shared Worker:  Browsers that support sharing threads across tabs. Modern blink-based browsers, 
 - Service Worker: Browsers that support patching fetch requests inside a service worker.  Webkit powered browsers, older bbrowsers 
 - No Javascript:
 
 Other features useful to segment the user base:
 
 - ECMAScript support:
 - Compression support:
 - Media support:


## Backend Architecture
![Server Layout](https://raw.githubusercontent.com/alberto-esposito/C10M/master/assets/server.svg)
### Scaling
#### Hybrid Cloud Approach
hello
#### Scaling up
hello
#### Scaling out
hello
### Optimizations
#### Unix Domain sockets vs TCP/IP protocol
#### HTTP/3
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk1ODQ0MzA1MiwxNDYxMTk4MzIyLDEzMT
A5OTUxMzgsNTk0MDM5OTI0LDE0OTg5MjE2OTAsLTg0MDc5NTI4
NywxNjIwNzExNDc1LC0xMTg3NDExNjAxLC0zMzk4MzUzMjUsLT
IxMTA5NzAyMSw5MTcwOTgxMjMsLTYxMjEyNTk1LC0yMTE4NTYz
NjE4LC0xMjg1OTA2MDEwLC02MzgyMTY5MjUsLTIwMjMxMzUyMi
wtMTA3NDY1ODM1OSwtNDMwNzEwMDA2LDU5NjkyNDM2XX0=
-->