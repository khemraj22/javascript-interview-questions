# javascript-interview-questions
javascript questions and answers

<br/>

| Sr.No|  Questions       |
|------|------------------|
| 01. |[What is Node.js?](#q-what-is-nodejs)|
| 02. |[What are the benefits of using Node.js?](#q-what-are-the-benefits-of-using-nodejs)|
| 03. |[What is default scope of application in Node.js?](#q-what-is-the-default-scope-of-application-in-nodejs)|
| 04. |[How to create package.json?](#q-how-to-create-package-json)|
| 05. |[What is typeof?](#q-what-is-typeof)|
| 06. |[What is typeof null?](#q-what-is-typeof-null)|
| 07. |[What is typeof undefined?](#q-what-is-typeof-undefined)|
| 08. |[What is difference between call and apply?](#q-what-is-difference-between-call-and-apply)|
| 09. |[What is fork method?](#q-what-is-fork-method)|
| 10. |[What is assert?](#q-what-is-assert)|
| 11. |[How do you debug nodejs app?](#q-how-do-you-debug-nodejs-app)|
| 12. |[What is difference between var and let?](#q-what-is-difference-between-var-let)|
| 13. |[Create hello world app?](#q-create-hello-world-app)|
| 13. |[How to compare two nodes?](#q-how-to-compare-two-nodes)|
| 13. |[Why let and var bindings behave differently using setTimeout function?](#q-Why-let-and-var-bindings-behave-differently-using-setTimeout-function)|
<br/>


## Q. ***What is Node.js?***

Node.js is an open-source server side runtime environment built on Chrome\'s V8 JavaScript engine. It provides an event driven, non-blocking (asynchronous) I/O and cross-platform runtime environment for building highly scalable server-side applications using JavaScript.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***What are the benefits of using Node.js?***

From a web server development perspective Node has a number of benefits:

  * Great performance! Node was designed to optimize throughput and scalability in web applications and is a good solution for many common web-development problems (e.g. real-time web applications).

  * Code is written in "plain old JavaScript", which means that less time is spent dealing with "context shift" between languages when you're writing both client-side and server-side code. 

  * JavaScript is a relatively new programming languages and benefits from improvements in language design when compared to other traditional web-server languages (e.g. Python, PHP,  etc.) Many other new and pouplar languages compile/convert into JavaScript so you can use TypeScript, CoffeeScript, ClojureScript, Scala, LiveScript, etc.

  * The node package manager (NPM) provides access to hundres of thousands of resuable packages. It also has best-in-class dependency resolution and can also be used to automate most of the build toolchain.

  * Node.js is portable. It is available on Microsoft Windows, macOS, Linux, Solaris, FreeBSD, OpenBSD, WebOS, and NonStop OS. Furthermore, it is well-supported by many web hosting providers, that often provide specific infrastrucutre and documentation for hosting 
    Node sites.

  * It has a very active third party ecosystem and developer community, with lots of people who are willing to help. 
    
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***Create hello world app?***
```js
const express = require('express')

const app = express()

const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***Why let and var bindings behave differently using setTimeout function?***

With var you have a function scope, and only one shared binding for all of your loop iterations - i.e. the i in every setTimeout callback means the same variable that finally is equal to 6 after the loop iteration ends.

With let you have a block scope and when used in the for loop you get a new binding for each iteration - i.e. the i in every setTimeout callback means a different variable, each of which has a different value: the first one is 0, the next one is 1 etc.
```js
(function timer() {
  for (var i=0; i<=5; i++) {
    setTimeout(function clog() {console.log(i)}, i*1000);
  }
})(); // this logs 6 six times.

(function timer() {
  for (let i=0; i<=5; i++) {
    setTimeout(function clog() {console.log(i)}, i*1000);
  }
})(); // this logs 0,1,2,3,4,5 
```
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>
