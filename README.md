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
<p align="justify">
Functional programming has become popular in the Javascript world thanks to React, but is well suited to front end programming in general. Pure functions are functions that will always have the same output given an input, i.e. they do not depend and do not have an internal state, thus allowing us to build easily testable components.  <br> 
Another advantage of pure functions is that they pair very well with caches. Given a cached state, I can easily hydrate it by running a render function, compared to having to OOP where you have to patch the internal state of Objects, leading to many mistakes. <br>
At a high level one could imagine such a flow: 
</p>

```js
page = async* render(state)
newState = async* eventHandler(oldState, event)
updates = async* conciliate(newState, oldState)
```
<p align="justify">
Since `render` 
</p>

### Entry point and subsequent requests

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

hello

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
eyJoaXN0b3J5IjpbLTE1NzY4NDE4NDcsMTQ2MTE5ODMyMiwxMz
EwOTk1MTM4LDU5NDAzOTkyNCwxNDk4OTIxNjkwLC04NDA3OTUy
ODcsMTYyMDcxMTQ3NSwtMTE4NzQxMTYwMSwtMzM5ODM1MzI1LC
0yMTEwOTcwMjEsOTE3MDk4MTIzLC02MTIxMjU5NSwtMjExODU2
MzYxOCwtMTI4NTkwNjAxMCwtNjM4MjE2OTI1LC0yMDIzMTM1Mj
IsLTEwNzQ2NTgzNTksLTQzMDcxMDAwNiw1OTY5MjQzNl19
-->