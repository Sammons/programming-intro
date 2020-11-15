## Web Servers

Every website you visit, every network-enabled mobile app, is backed by web servers.

The term `server` can refer to a machine that runs a program which serves internet traffic, but it can also refer to the program itself.

An HTTP(S) webserver is a program which is listening on port 80 for non-TLS requests and 443 for TLS requests. Usually it uses a framework like `django` in python or `expressjs` in node.js to process these requests.

> Note a program like `nginx` often proxies requests and handles serving traffic on 443 and 80, it forwards requests to a custom port where `django` or `expressjs` are listening like 3000.

> Linux requres sudo to listen on ports below 1000

So the HTTP Framework reads the payload, something like 

```
GET / HTTP/1.1
Host: localhost:3000
```

and reads the `/` data from disk or a database, and writes that data to the Socket the client has opened with the web server.

Not that a server can have lots, sometimes thousands, of inbound connections on one port.

In express.js, a javascript web framework, a simple web server can look like this ([from their docs](https://expressjs.com/en/5x/api.html#app)):
```js
const express = require('express')
const app = express()

app.get('/', function (req, res) {
  res.send('hello world')
})

app.listen(3000)

```

The code above would respond with "hello world" to that HTTP request, and the response would be wrapped appropriately for the HTTP protocol by the expressjs framework.

> Note the web path `/` typically serves an `index.html` file by convention

### What else do web servers do?

* They have to handle security, this is a deep topic but I recommend https://auth0.com/ documentation for developers just wanting to use something that works.
* They can handle more protocols than HTTP! For example proprietary servers at Netflix talk to eachother over regular TCP connections using protocols other than HTTP.
* They can call other servers, sometimes many other services.
* Whatever you want, it is custom code after all.

[Next: Web UIs](09_web_uis.html)