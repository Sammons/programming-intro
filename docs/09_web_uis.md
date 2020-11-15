## Web UIs

Web interfaces are built with three main technologies typically:
* HTML5 (Hyper Text Markup Language)
* CSS (Cascading Style Sheets)
* JavaScript

Sometimes called "HTML5 and friends"

CSS gives web pages color and shapes. HTML defines the elements. JS makes it interactive.

Part of being interactive means that JS can modify HTML and CSS on the fly while running, so many modern projects actually just use JS to build the whole web page.

__HTML__

A basic outline for an html page is like this:
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>What you see for the tab title</title>
</head>
<body>
  <!-- custom page code -->
</body>
</html>
```

You can find lots of resources on HTML online, I recommend inspecting pages with the chrome inspector (right click -> inspect) if you want to see what their HTML code is.

Parsing HTML pages lets you write web-scrapers which can extract data from web pages automatically.

__CSS__

I skipped this section, I think the [Mozilla docs are the best on web technology](https://developer.mozilla.org/en-US/docs/Web/CSS) so read those instead.

__JS__

Again JS is a deep topic. Keep in mind that learning browser JS will not necessarily translate immediately to backend Node.js code because the libraries are often different.

[MDN Docs on JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

__TypeScript__

JavaScript is a little hard to manage when you get thousands of lines of code. Most big businesses today actually write [TypeScript instead](https://www.typescriptlang.org/)

I think TypeScript is easier to aproach if you are new to programming altough the very first steps may be a bit more challenging than with regular JavaScript.


## How it runs

This sequence is pretty important, make sure to remember what is running on your web server, and what is running in the browser. Mixing these up is a big pain point for some beginners.

1. Browser requests e.g. google.com
2. DNS request resolves an IP, HTTPS request goes to the server
3. Server processes the request and performs backend logic. Responds.
4. Browser parses and presents HTML page returned by the server.
   * note post-parsing the HTML page can refer to other HTML, JS, CSS, Images etc. which are fetched in additional HTTP requests. They can refer to more resources... and it goes on.
5. CSS is processed to render the page pretty-like.
6. JS is processed to apply interactivity to the page. 
   * changes to html or css will be picked up as they happen
7. User interacts with the page, JS may make additional requests to the backend to fetch more data and run more backend code.


## Static Websites vs Websites with a backend

Why not do everything in the UI? Well some websites do!

Such websites are called serverless or static, you fetch the index.html and then almost everything works with no further interactions.

Many free content delivery networks (CDNs) exist for publishing static content. github.com provides this service for free, for example.

The limitation is that all the source code in a website is public, it is hard to have a serverless website process login and payment or write to a database securely. It can be done, but it is difficult.

Since server code is not running in the browser of some person out in the world, it is much more secure.

## Should I learn to build a web ui? 

I recommend it. Many languages, like python, offer ways to generate interfaces easily on your desktop from data you have locally - but you cannot share that UI very easily.

Companies most definitely still use custom Web UIs, but it is true that small businesses and individuals are increasingly using automated tools to generate their websites. It used to be common to make some easy cash setting up websites for local businesses, you can still do that but usually you are setting up a tool for them instead of building it from scratch. These tools require less knowledge of the web but still need some technical knowledge.

Additionally mobile applications have increasing support for building their interfaces using HTML, CSS, and JavaScript.

So you learn one way to build UIs and it can be at least somewhat re-used in lots of ways.

> If you want to build a UI just for yourself you can write an index.html file and drag it into chromium to see how it looks.

