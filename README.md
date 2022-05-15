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
| 14. |[Create hello world app?](#q-create-hello-world-app)|
| 15. |[How to compare two nodejs?](#q-how-to-compare-two-nodejs)|
| 16. |[Why let and var bindings behave differently using setTimeout function?](#q-Why-let-and-var-bindings-behave-differently-using-setTimeout-function)|
| 17. |[What is event loop in nodejs?](#q-what-is-event-loop-in-nodejs)|
| 18. |[What is middleware?](#q-what-is-middleware)|
| 19. |[What is features of ES6?](#q-what-is-features-of-es6)|
| 20. |[What is use-strict?](#q-what-is-use-strict)|
| 21. |[What is object destructuring?](#q-what-is-destructuring)|
| 22. |[Does alias is supported in object destructuring?](#q-does-alias-is-supported-in-object-destructuring)|
| 23. |[What is promises?](#q-what-is-promises)|
| 24. |[What is promise all?](#q-what-is-promise-all)|
| 25. |[What is promise race method?](#q-what-is-promise-race-method)|
| 26. |[What if throw new Error in promise, is it resolved or reject?](#q-what-if-throw-new-error-in-promise-is-it-resolved-or-rejected)|
| 27. |[How to call five promises in loop sequentially?](#q-how-to-call-five-promises-in-loop-sequentially)|
| 28. |[How to complete promises if one promise fails?](#q-how-to-complete-promises-if-one-promise-fails)|
| 29. |[What is prop drilling in reactjs?](#q-what-is-prop-drilling-in-reactjs)|
| 30. |[What is hoc in reactjs?](#q-what-is-hoc-in-reactjs)|
| 31. |[What is pure component in reactjs?](#q-what-is-pure-component-in-react-js)|
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
for (var i=0; i<3;i++){
  setTimeout(()=>{
    console.log(i)
  },1000)
} // this logs 3 three times.

for (let i=0; i<3;i++){
  setTimeout(()=>{
    console.log(i)
  },1000)
}// this logs 0,1,2 

let j;
for (j = 0; j < 3; j++) {
  const log = () => {
    console.log(j);
  }
  setTimeout(log, 100); // 3,3,3
}
```
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***How to call five promises in loop sequentially?***

```js

const delays = [1000, 2000, 5000, 3000, 500, 12000];
const startTime = Date.now();

const delay = (timeDelay) => {
    console.log(`Waiting: ${timeDelay / 1000} seconds.`);
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(timeDelay)
        }, timeDelay)
    })
}

// solution 1
(async () => {
    for await (const d of delays) {
        await delay(d).then(sec => {
            console.log(`Waited: ${sec / 1000} seconds\n`);
        })
    }
})()

// solution 2: recursive
const doNextPromise = (d) => {
    delay(delays[d]).then(sec => {
        console.log(`Waited: ${sec / 1000} seconds\n`);
        d++;

        if (d < delays.length) {
            doNextPromise(d)
        } else {
            console.log(`Total: ${(Date.now() - startTime) / 1000} seconds.`);
        }
    })
}

// doNextPromise(0)
```
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>
