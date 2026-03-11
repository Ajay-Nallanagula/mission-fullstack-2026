**process.env variables are not read during runtime you get an error how do we resolve them**

- The issue is that Webpack doesn't automatically provide process.env in the browser. You need to configure Webpack to inject environment variables. Let me fix your setup:

1. Install dotenv-webpack:

```bashnpm install dotenv --save-dev

```

2. Update your webpack.config.js:

```javascript
const webpack = require("webpack");
require("dotenv").config();  //This will read your .env file

new webpack.DefinePlugin({
  "process.env.REACT_APP_RTK_API_URL": JSON.stringify(
    process.env.REACT_APP_RTK_API_URL || "http://localhost:3000/api"
  ),
}),
```

3. Now you can access your environment variables in your code using process.env.VARIABLE_NAME

**dotenv Vs dotenv-webpack**

- dotenv is a zero-dependency module that loads environment variables from a .env file into process.env. It is typically used in Node.js applications to manage configuration settings.
- dotenv-webpack is a plugin for Webpack that integrates dotenv functionality into the Webpack build process. It allows you to use environment variables defined in a .env file within your client-side code during the build process.

### GENERAL

What is Engineering manager: https://videoportal.epam.com/video/NYOOGxY4

Ravi Yelluripati

GitHub Copilot:
Username: Ajay-Nallanagula1_epam
NOTE: Please note that you should log in using your EPAM-provided GitHub username, which is in the following format: firstname-lastname_epam. After the end user name is specified on the sign in form, you will be suggested to sign in via SSO

## EPAM FULLSTACK TOPICS

1. JavaScript
2. TypeScript
3. React.js
4. Next.js
5. Node.js
6. Nest.js
7. Cloud(AWS/Azure/GCP)
8. Database(SQL/NoSql)
9. Design Pattern
10. DSA
11. Problem Solving
12. Product Engineering
13. GraphQL
14. Docker
15. Accessibility
16. Performance Optimisation
17. Security
18. Knowledge of CI/CD

React:
https://react.dev/learn/you-might-not-need-an-effect // See the links in that page gold mine!!

Atomics
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics
https://aditya003-ay.medium.com/atomics-in-node-js-34aa4b5a76ee

Proxy and Reflect:
https://javascript.info/proxy

Javascript:
Learn about IndexedDB: https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB,
Learn on HTML Canvas, Video,Audio, drag drop, geolocation.
#region Webstorage : localstorage, sessionstorage, document.cookie

//Before accessing storage check if it exists
if (typeof(Storage) !== "undefined") {
// Code for localStorage/sessionStorage.
} else {
// Sorry! No Web Storage support..
}

localstorage:
// Store
localStorage.setItem("lastname", "Smith");
// Retrieve
document.getElementById("result").innerHTML = localStorage.getItem("lastname");
localStorage.removeItem("lastname");

sessionStorage:
sessionStorage.setItem("lastname", "Smith");
// Retrieve
document.getElementById("result").innerHTML = sessionStorage.getItem("lastname");
sessionStorage.removeItem("lastname");

document.cookie examples:
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";
document.cookie = "username=John Doe";
#endregion Webstorage : localstorage, sessionstorage, document.cookie
Module Patterns AMD/UMD/CJS/ES : Covered.
#region Transpiler Vs Compiler
======================
Compiler:
A compiler takes the source code of a program as input and translates it into machine language (binary code) which can be directly executed by a machine.
Compilation is a one-way process.
The output is generally at a much lower level of abstraction than the source code.
Examples include the Java compiler (javac), GCC for C/C++, etc.
Transpiler (also known as source-to-source compiler):

A transpiler takes the source code written in one programming language and produces the equivalent source code in another programming language.
The process can go both ways, meaning you can convert back the output code into the input language.
The output is typically at approximately the same level of abstraction as the input.
Examples include Babel (transpiles from ES6+ to ES5 JavaScript), TypeScript to JavaScript etc.

#endregion Transpiler Vs Compiler
#region Intersection Observer
The Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport. Essentially, it allows developers to execute code based on whether an element is in view or not. This is particularly useful for lazy loading images or implementing infinite scrolling without relying on event listeners, which can improve performance and user experience.

function useOnScreen(ref) {
const [isIntersecting, setIntersecting] = useState(false);

const observer = new IntersectionObserver(
([entry]) => {
setIntersecting(entry.isIntersecting);
}
);
useEffect(() => {
observer.observe(ref.current);
return () => {
observer.disconnect();
};

}, []);
return isIntersecting;
}
#endregion Intersection Observer
#region AbortController
AbortController is a JavaScript built-in class that provides an interface to signal a fetch or a promise to be terminated prematurely. This allows you to have more control over your fetch or promise requests.

Here's an example of how you could use it with the fetch API:

const controller = new AbortController();
const { signal } = controller;

fetch('/api/some-endpoint', { signal })
.then(response => response.json())
.then(data => console.log(data))
.catch(error => {
if (error.name === 'AbortError') {
console.log('Fetch aborted');
} else {
console.error('Another error', error);
}
});

// Call this method to abort the fetch request
controller.abort();

#endregion AbortController
#region requestAnimationFrame
requestAnimationFrame is a JavaScript method that tells the browser you wish to perform an animation and requests that the browser calls a specified function to update an animation before the next repaint. The method takes as an argument a callback function that will be executed before the repaint. The beauty of requestAnimationFrame is that it's designed to sync animations to the browser's refresh rate, leading to smoother animations and reducing the likelihood of jank, especially in web animations and games.

let start;

function step(timestamp) {
if (start === undefined)
start = timestamp;
const elapsed = timestamp - start;

// Your drawing or animation code here

// Stop the animation after 2 seconds
if (elapsed < 2000) {
window.requestAnimationFrame(step);
}
}

window.requestAnimationFrame(step);

In this example, window.requestAnimationFrame(step) call tells the browser that you wish to perform an animation and requests that the browser schedule a repaint of the window for the next animation frame. When the repaint happens, the step function will be called with the time at which the repaint is occurring as a parameter.

You can also see that requestAnimationFrame(step) is called recursively within the step function. This creates an animation loop that continues running until we stop it after 2 seconds (2000 milliseconds) have passed.

This method allows more efficient animations by matching the animation frame rate with the browser's painting rate. It also automatically stops running when the tab is not active, which helps in saving CPU/GPU power.

Example 2:
[2:34 PM] Nikhil Jain
let elem = document.getElementById('animateMe'); // The element to be animated

let startPos = 0; // Starting position

let endPos = 300; // End position (pixels)

function animate() {

// Update the position

startPos++;

// Move the element right by 1px

elem.style.left = startPos + 'px';

// Continue the animation as long as startPos doesn't exceed endPos

if (startPos < endPos) {

    requestAnimationFrame(animate); // Call animate again before the next repaint

}else{
CancelAnimationFrame(animate); // Call animate again before the next repaint
}

}

// Start the animation

requestAnimationFrame(animate);

#endregion requestAnimationFrame
#region Server Sent event

Noifications , push updates to client, uni-directional , Facebook notifications , Cricket scores

#endregion Server Sent event
#region getBoundingClientRect()
getBoundingClientRect() will be useful to get top, right, bottom, and left: The top, right, bottom, and left boundaries of the element relative to the viewport.
For drag and drop functionality we will have to use this.

is a method in JavaScript used to get the size of an element and its position relative to the viewport. It returns a DOMRect object representing the size of the element, as well as its position relative to the top-left corner of the viewport.

let element = document.querySelector("#myElement");
let rect = element.getBoundingClientRect();
console.log(rect.top, rect.right, rect.bottom, rect.left);

#endregion getBoundingClientRect()

#region How does NPM, NPM-Registry , Node_Modules work?
Find the answer
#endregion How does NPM, NPM-Registry , Node_Modules work?

#region streams in native Javascript
https://developer.mozilla.org/en-US/docs/Web/API/Streams_API

#endregion streams in native Javascript

#region Redux Toolkit Query RTK Query

#endregion Redux Toolkit Query RTK Query

#region ArrayBuffers , SharedArrayBuffers

#endregion ArrayBuffers , SharedArrayBuffers

#region RaceConditions, DeadLock, Atomic Operations

#endrgion RaceConditions, DeadLock, Atomic Operations

# CMS and CMS headless :

Wordpress, Umbraco, Telerik, Sitecore,

Custom Logger Implementation:
https://innostax.com/implementing-a-custom-logger-with-winston-in-node-js/

Shadow Vs Virtual Dom
Example of ShadowDom: https://developer.mozilla.org/en-US/play

https://excalidraw.com/

https://kb.epam.com/display/GDOKB/FE-Interview+Standards
