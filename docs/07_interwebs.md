## About the internet and programming

There are a lot of topics to cover here, so we'll keep it thin and you can google terms you learn here if you want to know more.

## Web Protocols

__LAN__

LAN (Local Area Network) Protocols are used to transmit data locally, like between devices on Ethernet. LAN Protocols are lower level than Internet Protocol. This is important because IP relies on LAN Protocols to handle the complexity of hardware transmission details.

So a computer has drivers for writing to its WiFi chip, and your program makes system calls to talk via IP to some web service, the data you send is wrapped up in Internet Protocol formatting, and then that IP Packet is stuffed into a LAN Protocol data packet. This is important because it means when you send a message, the computer sends more data than you actually wanted to send, because of headers and metadata necessary for the protocols to work.

A LAN Protocol might be formatted in binary something like `|MAC Address|PayloadSize|PayloadSignature|<your IP payload>|` - lookup ethernet to learn more.

Those data formats vary depending if you are using Ethernet or WiFi, but the data that they carry almost invariably turns out to be packets of data for Internet Protocol.

__Internet Protocol__

IP Protocol is mostly a spec around routing and getting data to specific IP Addresses. For most intents and purposes you can think of IP addresses like post office addresses. A packet goes up the heriarchy until it finds an internet service provider router which knows what region to send the packet, then it gets sent in that direction until eventually it gets there.

You can watch how many "hops" your packets are making using the `tracert` command in linux. You can observe the latency on your connection to a destination using `ping`.

__TCP__

Transmission Control Protocol exists because packets get lost in Internet Protocol which is best-effort. Literally like missing frames from a video or a page from an email.

Missing data totally wrecks most binary formats, because they have headers about binary sizes and where to find data inside their file structure. (think: corrupted PDF files)

So that's no way to live! TCP solves that problem. You open a TCP socket and write data into it, and TCP sends all kinds of messages back and forth using Internet Protocol in order to verify data delivery and data ordering. If anything goes wrong, TCP times out or indicates the socket is broken, and then both parties know some data was missing. Typically you ignore anything recieved if there was a TCP error.

__DNS__

Domain Name System is a system where servers all around the world keep track of what domains point to what IP addresses. Your internet service provider gives your router an IP address that the world wide web can find, but you have to pay extra for this service that gives it a name.

Ahead of any request e.g. `curl google.com` is a preliminary request via UDP which is a protocol faster but less reliable than TCP, to a name server. Typically the name server is either provided by your internet service provider, or you can manually configure it in your phone/computer - you might do this because for example google provides a fast free nameserver.

You want DNS requests to be super fast because they get made before *every* other request. The operating system has a DNS cache where it keeps track of recent requests to DNS servers and tries to avoid duplicate requests.

> Note, whoever sees your DNS requests knows what sites you visit, even if you strictly use HTTPS for the actual communication later.

__TLS__

TCP solves reliable data transmission for us, we know when data was sent successfully. That does not mean it was sent *securely*

TLS (Transmission Layer Security) encrypts data sent via TCP using public key cryptography. Asymmetric cryptography (what public key crypto is) is like locking data in a box with two key holes. One key locks the box, one key unlocks the box. Neither key does both.

HTTP(S) uses asymmetric crypto with TLS to secure data, you will probably have to learn about getting an HTTPS certificate and generating the private key (and keeping it secure) if you stand up a web server that serves HTTPS traffic.

__HTTP__

HyperText Transfer Protocol is the protocol web pages use to send information to your browser.

Here's the request I made to wikipedia to get some details on IPv6
```
GET /wiki/IPv6 HTTP/1.1
Host: en.wikipedia.org
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:82.0) Gecko/20100101 Firefox/82.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
DNT: 1
Connection: keep-alive
Cookie: WMF-Last-Access=15-Nov-2020; WMF-Last-Access-Global=15-Nov-2020; GeoIP=US:MO:Saint_Charles:38.80:-90.50:v4; enwikimwuser-sessionId=70f707d82c0937438e76
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
TE: Trailers
```

At this point there is HTTP 1.1 and HTTP 2 which is becoming more popular. They are pretty similar but HTTP2 requires TLS

HTTP Status codes are pretty famous. HTTP Servers respond with a status code as part of the protocol, 200-299 means success, 300-399 means a reroute, 400-499 means something was wrong with the request, and 500-599 means the request failed.

Commonly you will see:
* 200 success
* 201 created
* 301 not modified
* 302 redirected
* 400 bad request
* 401 forbidden
* 403 unauthorized
* 404 not found
* 429 rate limited
* 500 unexpected error
* 503 bad gateway, server is down

If the codes seem ambiguous, they are, programmers mix them up all the time and sometimes return the wrong codes.

__Recap__

You want to send an HTTP request with `curl` from the command line?
that HTTP payload gets wrapped in TLS, then TCP, then IP, then LAN, and finally gets sent out into the world.

Sometimes folks refer to "Layers" in networking. Layer 7 is the "Application Layer" which is a pretty good description of how many layers exist to make our simple `curl` command code work.

## How do I use it?

From the command line if you want to listen on a port try `nc -l 3000` to listen on port 3000. Then in a different terminal try `curl localhost:3000` and you will see the HTTP request in your `nc` terminal.

In programming:
* If you want to make a web request look into an HTTP library,
* otherwise just look for a TCP library.

An example client library for HTTP in JavaScript is `axios` and in python there is `httplib`.

[Next: Web Servers](08_web_servers.html)