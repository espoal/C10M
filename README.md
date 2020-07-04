# C10M
## Introduction
In this article we'll investigate how to solve the **C10M problem**, or how to handle 10 millions concurrent web users on commodity hardware. We'll try to constrain ourselves to using one or **two 1 gigabit/s dedicated servers** and eventually scaling out using the cloud, and with a **budget of 300 euros** per month, excluding personnel salary.

In order to achieve our goals we'll have to rethink how the clients will interact with the backend, exploiting what modern browsers offer us. We'll also make sure to deliver the fastest user experience possible, while letting developers use the too

## Smart Client
### User segmentation

Hello

 - Shared Worker:  Modern blink-based browsers, 
 - Service Worker: Webkit powered browsers, older browsers 
 - No Javascript:
 
 Other features useful to segment the user base:
 - Compression support:
 - Media support:

### Fetch patching and HTTP 304
## Backend Architecture
![Server Layout](https://raw.githubusercontent.com/alberto-esposito/C10M/master/assets/server.svg)
### Hybrid Cloud Approach
hello
### Optimizations
#### Unix Domain sockets vs TCP/IP protocol
#### HTTP/3
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc5NDU4ODkxMCwtMTI4NTkwNjAxMCwtNj
M4MjE2OTI1LC0yMDIzMTM1MjIsLTEwNzQ2NTgzNTksLTQzMDcx
MDAwNiw1OTY5MjQzNl19
-->