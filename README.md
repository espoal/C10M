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

Additionally, with this flow offline functionality is trivial.
</p> 

### User segmentation

<p align="justify">
It's important to segment our user base according to their capabilities, optimally by sniffing the request headers or by using conditional imports:

 - Shared Worker:  Browsers that support sharing threads across tabs. Roughly 33% of the market.
 - Service Worker: Browsers that support patching fetch requests inside a service worker.  Cross-tab communication resource sharing can be achieved using IndexedDB. Roughly 60% of the market.
 - No Javascript: In case a browser doesn't fall in the previous two categories, we can provide a JS-less experience. This might be considered too much work for such a small user base, but this work can be used to bootstrap a Google AMP implementation. A lot of functionalities usually achieved through JS can be done in [CSS instead](https://github.com/you-dont-need/You-Dont-Need-JavaScript), making the page much faster for every user. 
 
 Other features useful to segment the user base:
 
 - ECMAScript support: Usually developers use Babel to compile the code to the minimum common denominator, thus creating huge and bloated Javascript files.
 - Compression support: Brotli is a new compression algorithm, which is much better. 
 - Media support: Even though the web seems to be converging toward WebP, it's useful the differentiate media support and serve only the best format.

</p>

### Entry point and subsequent requests
<p align="justify">

The first time
</p>

### Bonus: Pure functions and the cache
<p align="justify">
Functional programming has become popular in the Javascript world thanks to React, but is well suited to front end programming in general. Pure functions are functions that will always have the same output given an input, i.e. they do not depend and do not have an internal state, thus allowing us to build easily testable components.  <br> 
Another advantage of pure functions is that they pair very well with caches. Given a cached state, I can easily hydrate it by running a render function, compared to having to OOP where you have to patch the internal state of Objects, leading to many mistakes. <br>
At a high level one the render loop could be: 
</p>

```js 
const render = async* state => {...}
const eventHandler = async* (oldState, event) => {...}
const conciliate = async* (oldState, newState) => {...}

render(initialState) // this should be skipped by using SSR

document.on('event', async () => {
	render(
		conciliate(state, 
			eventHandler(state, event)
		))
})
```
<p align="justify">
Since render is a pure function that depends only on the state, we can bootstrap the DOM by using a default and then stream the result. We are using an async iterator so that we don't have to wait for the function to complete, instead we can serve the content as soon as it's ready, for example by loading the head tag as soon as possible we can start prefetching scripts, CSS and images. <br>
In case of an event (URL change, form submission, ....) a new state is generated using an event handler. Again we are using an async iterator because there might be multiple long requests, and we don't want to wait for all of them to complete before we can start rendering. The conciliate function is responsible for updating the state, maybe using a diffing algorithm, and then pass the result to the render function that can surgically update the changed components.
The render is itself an async iterator, so it can yield to the main thread between updates, even if they are the result of a single event, allowing for a 60 fps experience even on resource constrained devices. 
</p>

## Backend Architecture
![Server Layout](https://raw.githubusercontent.com/alberto-esposito/C10M/master/assets/server.svg)
### Load considerations

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
eyJoaXN0b3J5IjpbODM0NDAwMTkxLDEyMDc0NDg3NTksMTIzOD
c3NTgxOCwtMTUxMjg0NjI4Miw1NzMzNTY2NzcsMTQ2MTE5ODMy
MiwxMzEwOTk1MTM4LDU5NDAzOTkyNCwxNDk4OTIxNjkwLC04ND
A3OTUyODcsMTYyMDcxMTQ3NSwtMTE4NzQxMTYwMSwtMzM5ODM1
MzI1LC0yMTEwOTcwMjEsOTE3MDk4MTIzLC02MTIxMjU5NSwtMj
ExODU2MzYxOCwtMTI4NTkwNjAxMCwtNjM4MjE2OTI1LC0yMDIz
MTM1MjJdfQ==
-->