# js101-guvi-assignment-day1

## HTTP/1.1 and HTTP/2 Differences
The Hypertext Transfer Protocol, or HTTP, is an application protocol that has been the de facto standard for communication on the World Wide Web since its invention in 1989. 
HTTP 1.1 came out in 1997 and in 2015 HTTP 2 was released which offered several methods to decrease latency, especially when dealing with mobile platforms and server-intensive graphics and videos, it does it by compression of HTTP header fields, and add support for stream prioritization to minimize page load latency. 

**HTTP/2 does not modify the application semantics of HTTP in any way. All the core concepts, such as HTTP methods, status codes, URIs, and header fields, remain in place. Instead, HTTP/2 modifies how the data is formatted (framed) and transported between the client and server.**

### Below are the key differences b/w both the protocol version: 

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

### 2. Predicting Resource Requests
The client receives an HTML page on sending a GET request. While examining the page contents, the client determines that it needs additional resources for rendering the page and makes further requests to fetch these resources. As a consequence of these requests, the connection load time increases. Since the server already knows that the client needs additional files, it can save the client time by sending these resources before requesting; thus, offering a great solution to the problem.

- **HTTP/1.1**
  - HTTP/1.1 has a different technique called resource inlining, wherein the server includes the required source within the HTML page in response to the initial GET request.         Though this technique reduces the number of requests that the client must send, the larger, non-text format files increase the size of the page.
  - As a result, the connection speed decreases, and the primary benefit obtained from it also nullifies. Another drawback is the client cannot separate the inlined resources       from the HTML page.
 
 - **HTTP/2**
   - HTTP/2 supports multiple simultaneous responses to the client’s initial GET request, the server provides the required resource along with the requested HTML page. This is        called the server push process, which performs the resource inlining like its precursor while keeping the page and the pushed resource separate.
   - This process fixes the main drawback of resource inlining by enabling the client machine to decide to cache/decline the pushed resource separate from the HTML page.

### 3. Buffer Overflow
Server and client machine TCP connection requires both of these to have certain buffer space for holding incoming requests. Though these buffers can hold numerous or large requests, they may also lack space due to small or limited buffer size. It causes buffer overflow at receiver’s end, resulting in data packet loss. For example, packets received after the buffer is full, will be lost.

- **HTTP/1.1**
  - The flow control mechanism in HTTP/1.1 relies on the basic TCP connection. In beginning itself, both the machines set their buffer sizes automatically. 
  - If the receiver’s buffer is full, it shares the receive window details, telling how much available space is left. The receiver acknowledges the same and sends an opening         signal. 
  - Note that flow control can only be implemented on either end of the connection. Moreover, since HTTP/1.1 uses a TCP connection, each connection demands an individual flow       control mechanism.

- **HTTP/2**
  - It multiplexes data streams utilizing the same (one) TCP connection. So, in this case, both machines can implement their flow controls instead of using the transport layer.
  - The application layer shares the available buffer size data, after which, both machines set their receive window details on the multiplexed streams level
  - In addition, the flow control mechanism does not need to wait for the signal to reach its destination before modifying the receive window.

### 4. Compression
Every HTTP transfer contains headers that describe the sent resource and its properties. This metadata can add up to 1KB or more of overhead per transfer, impacting the overall performance. For minimizing this overhead and boosting performance, compressions algorithms must be used to reduce the size of HTTP messages that travels between the machines.

- **HTTP/1.1**
  - HTTP/1.x uses formats like gzip to compress the data transferred in the messages. However, the header component of the message is always sent as plain text.
  - Though the header itself is small, it gets larger due to the use of cookies or an increased number of requests.
- **HTTP/2**
  - To deal with this bottleneck, HTTP/2 uses HPACK compression to decrease the average size of the header. This compression program encodes the header metadata using Huffman       coding, which significantly reduces its size as a result.
  - In addition, HPACK keeps track of previously transferred header values and further compresses them as per a dynamically modified index shared between client and server.

<br />
<br />
<hr />
<br />
<br />

# Object's internal representation in Javascript
An object, is a reference data type. Objects are quite different from JavaScript’s primitive data-types(Number, String, Boolean, null, undefined and symbol) in the sense that while these primitive data-types all store a single value each (depending on their types).

Loosely speaking, objects in JavaScript may be defined as an unordered collection of related data, of primitive or reference types, in the form of “key: value” pairs. These keys can be variables or functions and are called properties and methods, respectively, in the context of an object.

For Eg. If your object is a student, it will have properties like name, age, address, id, etc and methods like updateAddress, updateName, etc.

## 1. Syntax
   - Objects are variables too. But objects can contain many values. The following code assigns many values (Mercedes, C-class, White and soo on) to a variable named Car:
     > var car = {Make: “Mercedes”, Model: “C-Class”, Color: “White”, Fuel: Diesel, Weight: “850kg”, Mileage: “8Kmpl”, Rating: 4.5};
     
## 2. Properties
   - The __name:value__ pair in an object are called properties.
   - The object properties can be different primitive values, other objects and functions.
   - Properties can usually be changed, added, and deleted, but some are read only.
      - Adding property
        >  ObjectName.ObjectProperty = propertyValue;
      - Deleting property
        >  delete ObjectName.ObjectProperty;
      - Access a property from an object is:
        - > objectName.property       -------->  Car.Make
        - > objectName["property”]    -------->  Car["Make"]
        - > objectName[expression]    -------->  x = "Make"; Car[x]
      
## 3. Object methods
  - An object method is an object property containing a function definition.
  - Let’s assume to start the car there will be a mechanical functionality.
      > function(){ return ignition.on  }
  - And similarly to stop/brake/headlights on & off, etc.
  - So, simple definition for Javascript __Object Methods__ is “Methods are actions that can be performed on objects.”.
   





