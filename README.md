# js101-guvi-assignment-day1

## HTTP/1.1 and HTTP/2 Differences
The Hypertext Transfer Protocol, or HTTP, is an application protocol that has been the de facto standard for communication on the World Wide Web since its invention in 1989. 
HTTP 1.1 came out in 1997 and in 2015 HTTP 2 was released which offered several methods to decrease latency, especially when dealing with mobile platforms and server-intensive graphics and videos, it does it by compression of HTTP header fields, and add support for stream prioritization to minimize page load latency. 

**HTTP/2 does not modify the application semantics of HTTP in any way. All the core concepts, such as HTTP methods, status codes, URIs, and header fields, remain in place. Instead, HTTP/2 modifies how the data is formatted (framed) and transported between the client and server.**

Below are the key differences b/w both the protocol version: 

### 1. Delivery Model:
HTTP/1.1 sends messages as plain text, and HTTP/2 encodes them into binary data and arranged them carefully. This implies that HTTP/2 can have various delivery models.
Most of the time, a client's initial response in return for an HTTP GET request is not the fully-loaded page. Fetching additional resources from the server requires that the client send repeated requests, break or form the TCP connection repeatedly for them.

- **HTTP/1.1**
  - Addresses this problem by creating a persistent connection between server and client. Until explicitly closed, this connection will remain open. So, the client can use one TCP     connection throughout the communication w/o interrupting it again and again.
    This approach surely ensures good performance, but it also is problematic.
  - For example – If a request at the queue head cannot retrieve its required resources, it can block all requests behind it. This phenomenon is called head-of-line blocking (HOL     blocking).

- **HTTP/2**
  - HTTP/2 developers introduced a binary framing layer. This layer partitions requests and responses in tiny data packets and encodes them. Due to this, multiple requests and         responses becomes able to run parallelly with HTTP/2 and chances of HOL blocking are bleak.
  - Not only has it solved HOL blocking problem in HTTP/1.1, but it also concurrent message exchange between the client and the server. However, at times, multiple data streams       demanding the same resource can hinder HTTP/2’s performance. 
  - To achieve better performance, HTTP/2 has another way. It has the capability of stream prioritization. When sending streams in parallel, the client can assign weights (1-256)     to its stream to prioritize the responses it demands. Here, the higher the weight, the higher the priority. The serve sets the data retrieval order as per the request’s           weight. Programmers can enjoy better control on page rendering process with stream prioritization ability.
