- [Basics](#basics)
- [Async/Await](#Async/Await)
- [Fetch API](#fetch-api)
- [Promises](#promises)
- [Callbacks](#callbacks)
- [AJAX](#ajax)

# Basics

Asynchronous Javascript is based on events. Every promise and observable library is based on them.

Synchronous code uses a `call stack`, a data structure keeping track of the program execution.

Asynchronous code uses an `event queue`, a list of functions handled in a FIFO manner, which is checked repeatedly by the `event loop`.

The event loop is a programming construct that waits for and dispatches functions in the `event queue` to the `call stack`.

```javascript
setTimeout(() => {
    console.log("I will happen later...");
}, 5000);
```

This doesn't execute after 5 seconds... It gets added to the `event queue` after 5 seconds.

In reality, **Javascript is not asynchronous at all**. It comes from the environment i.e. browsers and nodejs, specifically the Behavior Object Model (BOM).

window

-   Document Object Model (DOM)
    -   getElementById
-   Behavior Object Model (BOM)
    -   setTimeout
    -   XMLHttpRequest
    -   fetch
    -   history
-   ECMAScript
    -   Object
    -   Array
    -   Function

# Async/Await

Async/Await enables us to write asynchronous code in a synchronous fashion. Under the hood, it’s just syntactic sugar using generators and yield statements to “pause” execution. 

In other words, async functions can “pull out” the value of a Promise even though it’s nested inside a callback function, giving us the ability to assign it to a variable.

```javascript
const posts = [
{title: "Post One", body: "This is post one"}, 
{title: "Post two", body: "This is post two"}
];

function getPosts(){
settimeout(() => {      //Arrow Function
let output = "";
post.forEach((post,index) => {output += `<li>${post}.title</li>`;
document.body.innerHTML = outpout;
},1000);
}

function createPost(post) {
return new Promise (resolve, reject= => {
settimeout( () => {
posts.push(post);

const error = false;

if(!error) {
resolve();}

else{
reject("Error: Something went wrong");
}
}, 2000);
});
}

asycn function innit(post: any){
await createPost({title: "Post three", body: "This is post three"});
//Wait until the first function is done to pass to the other
getPosts();
}

init();
```
### Await with Fetch
```javascript
async function fetchUsers() {
const res = await fetch("https://jsonplaceholder.typicode.com/users").then(res => res.json());

const data = await res.json();
console.log(data);
fetchUsers();
```

Under the hood it looks like...

```javascript
const request = url => {
    ajax("GET", url).then(response => it.next(JSON.parse(response)));
};

function* main() {
    const result = yield fetch("http://api.com/users/1");
    const data = yield result.json();
    console.log(data);
}

const it = main();
it.next();
```

### Combination Example
```javascript
async function getDataOne() {
    let res = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    let data = await res.json()
    return data;
}

async function getDataTwo() {
    let res = await fetch("https://jsonplaceholder.typicode.com/todos/2");
    let data = await res.json()
    return data;
}

async function getBoth() {
    var resultOne = await getDataOne();
    var resultTwo = await getDataTwo();
    console.log(resultOne, resultTwo)
}

getBoth();

// Compared to this
function foo() {
    fetch("https://jsonplaceholder.typicode.com/todos/1")
    .then(res => res.json())
    .then(resultOne => {

        fetch("https://jsonplaceholder.typicode.com/todos/2")
        .then(res => res.json())
        .then(resultTwo => {

            console.log(resultOne, resultTwo)
            
        })
        .catch(err => console.log(err));

    })
    .catch(err => console.log(err));
}

foo()
```

# Fetch API

An AJAX library using promises, available by default in all modern browsers. A promise is like a placeholder for a response we are going to get in the future.

Fetch always returns a promise. Promise resolves to the response object. This response object has different helper methods like response.json(), response.text(), response.blob() etc.

Fetch also takes a second parameter, which is a configuration object.

## GET INFO FROM API

```javascript
// ES6
fetch("http://www.api.com/data")
    .then(res => res.json())
    .then(data => data)
    .catch(err => err);
```

## POST

```javascript
// ES6
fetch("http://www.api.com/data", {
    method: "POST",
    headers: {
        Accept: "application/json",
        "Content-type": "application/json"
    },
    body: JSON.stringify({ title: title, body: body })
}) 
    .then(res => res.json())
    .then(data => {
        console.log(data)
    })
    .catch(err => err);

// Async Await
async function postData(){
    let response = await fetch("http://www.api.com/data", {
        method: "POST",
        headers: {
            Accept: "application/json",
            "Content-type": "application/json"
        },
        body: JSON.stringify({ title: title, body: body })
    }) 

    let data = await response.json()

    if (response.status !== 2000){
        throw Error(data.message)
    }
    
    console.log(data)
}
```

# Promises

The `Promise()` constructor takes a function, which takes the `resolve` and `reject` functions.

```javascript
new Promise((resolve, reject) => {
    if (goodThingsHappen) {
        resolve(goodThings); // passed to .then()
    } else {
        reject(reasonsForFailing);
    }
});
```

The promise object is used for deferred and asynchronous computations and it represents and operation that hasn't completed yet, but is expected in the future.

Promises are obtained with `.then()`.

```javascript
// Immediately resolved.
let myPromise = Promise.resolve("Foo");
myPromise.then((res) => console.log(res);) // Foo

// Delayed
var myPromise = new Promise(function(resolve, reject){
    setTimeout(() => resolve(4), 2000); // Return 4 after 2 seconds.
});

myPromise.then((res) => {
    res += 3; // Wait for the 4 and add 3 to it.
    console.log(res); // 7 after 2 seconds.
});
```

## Fetch under the hood with Promises

```javascript
const posts = [
{title: "Post One", body: "This is post one"}, 
{title: "Post two", body: "This is post two"}
];

function getPosts(){
settimeout(() => {      //Arrow Function
let output = "";
post.forEach((post,index) => {output += `<li>${post}.title</li>`;
document.body.innerHTML = outpout;
},1000);
}

function createPost(post) {
return new Promise (resolve, reject= => {
settimeout( () => {
posts.push(post);

const error = false;

if(!error) {
resolve();}

else{
reject("Error: Something went wrong");
}
}, 2000);
});
}
createPost({title: "Post three", body: "This is post three"})
.then(getPosts)     //Calls the function get posts after creating at posts
.catch(err => console.log(err));    //If there's an error it console.logs the error
```

## Promise All

Takes an array of promises and executes if they are all successful.
```javascript
const posts = [
{title: "Post One", body: "This is post one"}, 
{title: "Post two", body: "This is post two"}
];

function getPosts(){
settimeout(() => {      //Arrow Function
let output = "";
post.forEach((post,index) => {output += `<li>${post}.title</li>`;
document.body.innerHTML = outpout;
},1000);
}

function createPost(post) {
return new Promise (resolve, reject= => {
settimeout( () => {
posts.push(post);

const error = false;

if(!error) {
resolve();}

else{
reject("Error: Something went wrong");
}
}, 2000);
});
}
const promise1 = Promise.revolve ("Hello World");
const promise2 = 10;
const promise3 = New Promise(resolve, reject) => setTimeout(resolve, 2000, "Goodbye"));
Promise.all([promise1, promise2, promise3]).then((values) => console.log(values)); //values == "Hello World", 10, Goodbye |it returns it in 2s
```
### Fetch promises
```javascript
const promise4 = fetch("https://jsonplaceholder.typicode.com/users").then(res => res.json());
// With fetch we need to use 2 .then because if not it gives us a lot of data
Promise.all([promise1, promise2, promise4]).then((values) => console.log(values));  
```

## Chaining

```javascript
let futureNumber = Promise.resolve(2); // 2

futureNumber
    .then(n => n + 1) // 3
    .then(n => n * 2) // 6
    .then(n => Math.pow(n, 2)) // 36
    .then(n => console.log(n)); // 36

futureNumber.then(n => console.log(n)); //2
```

# Callbacks

A callback is a function that is to be executed after another function has finished executing — hence the name ‘call back’.

In JavaScript, functions are objects. Because of this, functions can take functions as arguments, and can be returned by other functions. Functions that do this are called **higher-order functions**. Any function that is passed as an argument is called a **callback function**.

```javascript
# Callbacks
```javascript
const posts = [
{title: "Post One", body: "This is post one"}, 
{title: "Post two", body: "This is post two"}
];

function getPosts(){
settimeout(() => {      //Arrow Function
let output = "";
post.forEach((post,index) => {output += `<li>${post}.title</li>`;
document.body.innerHTML = outpout;
},1000);
}

function createPost(post) {
settimeout( () => {
posts.push(post);
},2000);
}
getPosts();
createPost({title: "Post three", body: "This is post three"});
});
```
If you see the page at this moment there's only post1&2 because getPosts function executed faster than create post. to fix this we use asynchronis programming
```javascript
function createPost(post, callback) { //the same of above but with function as a parameter
settimeout( () => {
posts.push(post);
callback();     //We want pur callback function to be getPosts so it show all of the posts
},2000);
}
getPosts();
createPost({title: "Post three", body: "This is post three"}, getPosts;
```

Passing named functions.

```javascript
function baz(input) {
    console.log(input);
}

// This executes the baz function immediately.
// Logs Baz Foo and "TypeError: callback is not a function
foo("Foo", baz("Baz"));

// Named callback. Logs Foo Baz.
foo("Foo", function() {
    baz("Baz");
});

// Works fine because it doesn't execute immediately.
// Must have no arguments. Logs Foo Qux.
foo("Foo", logQux);

function logQux() {
    console.log("Qux");
}
```

Another example...

```javascript
function callbackSandwich(callbackFunction) {
    console.log("Top piece of bread.");
    callbackFunction();
    console.log("Bottom piece of bread.");
}

// We pass in an anonymous function, to be called inside.
callbackSandwich(function() {
    console.log("Slice of cheese.");
});
```

## AJAX with callback

```javascript
var request = new XMLHttpRequest();

request.addEventListener("load", event => {
    console.log(event.target.responseText);
});

request.open("GET", "http://www.api.com/data");
request.send();
```

Can be refactored into...

```javascript
function ajax(method, url, callback) {
    var request = new XMLHttpRequest();
    request.addEventListener("load", callback);
    request.open(method, url);
    request.send();
}

ajax("GET", "http://www.api.com/data", event => {
    console.log("SUCCESS", event.target.responseText);
});
```

Which is pretty much what the ajax libraries do.

# AJAX
- Asynchronous JavaScript & XML
This is all done via vanilla Javascript, but it can be done via libraries such as JQuery, Axios, Superagent, Fetch API, Node HTTP...

```javascript
var xhr = new XMLHttpRequest();     // Create the XHR object | XML HTTP Request Object => xhr 

xhr.open("GET", "http://www.api.com/data", true);   // xhr.type, url/file, is it async?
console.log("readyState: ", xhr.readyState);    // readyState: 1

    xhr.onprogress = function() {   // OPTIONAL Used for loader
  console.log("readyState: ", xhr.readyState);    // readyState: 3

xhr.onload = function() {   // When the xhr object loads 
    if (this.status == 200) {   // Check the status
      console.log("readyState: ", xhr.readyState);    // readyState: 4
        return JSON.parse(this.responseText);    //this.responseText => brings the text
        //If you want to access an specific part of the JSON object, you have to use JSON.parse (JSON.parse(this.responseText).name) => Rick 
        document.querySelector().innetHTML = this.responseText;
    }
};

 // Not necessary xhr.onerror = function() {
     console.log("error");
};

xhr.send();     //Sends Request
```
 **HTTP Status**
```
200: "OK"
403: "Forbidden"
404: "Not Found"
```

Can also be done like this.

```javascript
var request = new XMLHttpRequest();

request.addEventListener("load", event => {
    console.log(event.target.responseText);
});

request.addEventListener("error", event => {
    console.error(event.target.responseText);
});

request.open("GET", "http://www.api.com/data");
request.send();
```

**Regular HTTP request**  
`Client` --- Request ---> `Server`  
`Client` <--- Response --- `Server`

**Ajax**  
`Client` --- JS Call ---> `Ajax Engine` --- XMLHttpRequest (XHR) ---> `Server`  
`Client` <--- HTML --- `Ajax Engine` <--- JSON --- `Server`

## XMLHttpRequest (XHR) Object

This API in the form of an object is provided by the browser's Javascript environment, and it has its own properties and methods which transfer data between the browser and a server.

```html
<button id="button">Get data</button>
```

```javascript
document.getElementById("button").addEventListener("click", loadData);
```

### Old way

We have to make sure we are on the `readyState 4`.

```javascript
// Create XHR Object
var xhr = new XMLHttpRequest(); // Can be named req

// Establish server connection - type, url/file, async
xhr.open("GET", "http://www.api.com/data", true); 

console.log("readyState: ", xhr.readyState);    // readyState: 1

xhr.onreadystatechange = function() {
    console.log("readyState: ", xhr.readyState); // readyState: 1, readyState: 2, readyState: 3, readyState: 4
    
    if (this.readyState == 4 && this.status == 200) {   // When we use on readystatechange we have to use 4 so it runs
        return JSON.parse(this.responseText);
    }
};

// If it fails
xhr.onerror = function() {
    console.log("error");
};

// Send request
xhr.send();
```

**readyState values**

```
0. Request not initialized.
1. Server connection established.
2. Request received.
3. Processing request.
4. Request finished and response ready.
```

### New way

The difference from the old way is that `onload` will not run unless we are on `readyState 4`

```javascript
// Create XHR Object
var xhr = new XMLHttpRequest(); // Can be named req

// Establish server connection - type, url/file, async
xhr.open("GET", "http://www.api.com/data", true); // readyState 1

xhr.onload = function() {
    // readyState 1, 4
    if (this.status == 200) {
        return JSON.parse(this.responseText);
    }
};

// If it fails
xhr.onerror = function() {
    console.log("error");
};

// Send request
xhr.send();
```

### Loading

```javascript
xhr.onprogress = function() {
    // readyState 3
    // Show loading...
};
```

### POST

```html
<form method="POST" id="form">
    <input type="text" id="input">
    <input type="submit" value="submit">
</form>
```

```javascript
document.getElementById("form").addEventListener("submit", submitForm);

function submitForm(e) {
    e.preventDefault();

    var input = document.getElementById("input").value;
    var params = "input=" + input;

    var xhr = new XMLHttpRequest();

    xhr.open("POST", "http://www.api.com/data", true);

    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

    xhr.onload = function() {
        // readyState 1, 4
        if (this.status == 200) {
            return JSON.parse(this.responseText);
        }
    };

    xhr.onerror = function() {
        console.log("error");
    };

    xhr.send(params);
}
```
