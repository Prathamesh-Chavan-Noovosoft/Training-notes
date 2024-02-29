# Notes

## What is HTTP - Taken from [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#http_is_simple)

### Client - Server protocol used to fetch data. 
HTTP is a protocol for fetching resources such as HTML documents.
It is the foundation of any data exchange on the Web and it is a client-server protocol,
which means requests are initiated by the recipient, usually the Web browser.
A complete document is reconstructed from the different sub-documents fetched,
for instance, text, layout description, images, videos, scripts, and more.

![image](https://github.com/Prathamesh-Chavan-Noovosoft/Training-notes/assets/159108395/724f1ab0-36ec-4c22-ac7b-53f8fb0b2c8c)

### HTTP follows a request response structure
Clients and servers communicate by exchanging individual messages (as opposed to a stream of data). The messages sent by the client, usually a Web browser, are called requests and the messages sent by the server as an answer are called responses.

## Where does HTTP lie in the network communication model
![image](https://github.com/Prathamesh-Chavan-Noovosoft/Training-notes/assets/159108395/aea96120-c7ce-4a41-88c5-a04585d4881a)

HTTP was designed in the early 1990s, but has become more extensible. It is an application layer protocol sent over [TCP](https://developer.mozilla.org/en-US/docs/Glossary/TCP) or [TLS](https://developer.mozilla.org/en-US/docs/Glossary/TLS)-encrypted TCP, though any reliable transport protocol could theoretically be used. It can fetch hypertext documents, images & videos and also post content to servers, like with HTML form results. HTTP can also be used to fetch parts of documents to update Web pages on demand.

## Components of HTTP

![image](https://github.com/Prathamesh-Chavan-Noovosoft/Training-notes/assets/159108395/ff71ceae-9aae-4d99-aced-6fa53c42a7e1)

Requests are sent by one entity, the user-agent (or a proxy on behalf of it). Most of the time the user-agent is a Web browser, but it can be anything, for example, a robot that crawls the Web to populate and maintain a search engine index.

Each individual request is sent to a server, which handles it and provides an answer called the response. Between the client and the server there are numerous entities, collectively called [proxies](https://developer.mozilla.org/en-US/docs/Glossary/Proxy_server), which perform different operations and act as gateways or [caches](https://developer.mozilla.org/en-US/docs/Glossary/Cache), for example.

In reality, there are more computers between a browser and the server handling the request: there are routers, modems, and more. Thanks to the layered design of the Web, these are hidden in the network and transport layers. HTTP is on top, at the application layer. Although important for diagnosing network problems, the underlying layers are mostly irrelevant to the description of HTTP.

## Client: User-agent
The user-agent is any tool that acts on behalf of the user. This role is primarily performed by the Web browser, but it may also be performed by programs used by engineers and Web developers to debug their applications.

The browser is always the entity initiating the request. It is never the server (though some mechanisms have been added over the years to simulate server-initiated messages).

To display a Web page, the browser sends an original request to fetch the HTML document that represents the page. It then parses this file, making additional requests corresponding to execution scripts, layout information (CSS) to display, and sub-resources contained within the page (usually images and videos). The Web browser then combines these resources to present the complete document, the Web page. Scripts executed by the browser can fetch more resources in later phases and the browser updates the Web page accordingly.

A Web page is a hypertext document. This means some parts of the displayed content are links, which can be activated (usually by a click of the mouse) to fetch a new Web page, allowing the user to direct their user-agent and navigate through the Web. The browser translates these directions into HTTP requests, and further interprets the HTTP responses to present the user with a clear response.

## Web Server
On the opposite side of the communication channel is the server, which serves the document as requested by the client. A server appears as only a single machine virtually; but it may actually be a collection of servers sharing the load (load balancing), or other software (such as caches, a database server, or e-commerce servers), totally or partially generating the document on demand.

A server is not necessarily a single machine, but several server software instances can be hosted on the same machine. With HTTP/1.1 and the Host header, they may even share the same IP address.

## [Basic aspects of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#basic_aspects_of_http)
- ### HTTP is simple
- ### HTTP is extensible
- ### HTTP is stateless but not sessionless
- ### Requires a reliable connection protocol

## [Things controlled by HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#what_can_be_controlled_by_http)

- ### Authentication
- ### Caching
- ### Relaxing the origin constraints
- ### Proxy and tunneling
- ### Sessions

## HTTP Messages
### Requests
![image](https://github.com/Prathamesh-Chavan-Noovosoft/Training-notes/assets/159108395/3709d855-3b00-401b-9895-6746e338f2bd)
### Responses
![image](https://github.com/Prathamesh-Chavan-Noovosoft/Training-notes/assets/159108395/bc531d7d-c5df-46c5-bc4b-4c29ebb4d767)

