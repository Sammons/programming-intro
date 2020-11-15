### About high level programs

High level languages care less about the details of resources, and typically trust their language writers to handle that complexity for the programmer.

My opinion is that the highest level language widely available is JavaScript.

If you have chrome nearby, open a tab, right click anywhere and select "Inspect". Then in the window at the bottom of the page click "Console".

This Console has a JavaScript interpreter! Most web pages today use JavaScript to do ... well everything you see.

Try running a program for fun:

```js
const replacement = document.createElement('div')
replacement.innerHTML = "Hello World"
document.body.replaceChildren(replacement)
setTimeout(() => {
  window.alert('I did it!');
}, 100)
```

Your tab content will be replaced with "Hello World" and an alert will pop up. Fun right?

You may have noticed though, that code sample used lots of stuff that seems mysterious without explanation. That's the downside of high level languages.

They use lots of libraries, and you have to read the API (Application Program Interface) documentation to get stuff done. 

High level programmers spend as much time figuring out what to write, as writing the actual code.



