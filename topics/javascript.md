# JavaScript
- [Variables](#Variables)
- [Data Type](#Data-Type)
- [Arrays](#Arrays)
- [Objects](#Objects)
- [Loops](#Loops)
- [Conditionals](#Coditionals)
- [Functions](#Functions)
- [Classes](#Classes)
- [DOM](#Document-Object-Model-(DOM))
- [Events](#Events)
- [Hoisting](#Hoisting)
- [Useful](#Useful)
- [Debugging](#Debugging)
## Variables

```javascript
var a;     // Not used anymore
let c = 1;     // changes
console.log(c);  // =>1
c = 2; // => 2
const b = 2;   // Immutable
b = 1;    // Error
```
## Data Type

```javascript
const name = "John";    // String
let age = 30;     // Number 
const IsCool = true;  // Boolean
const x = null ;    // Null
const y = undefined;   // Undefined
```
With typeof we get the data type of a variable

```javascript
console.log(typeof name);    //String
```
-   length
```javascript
console.log(name.lenght;    //4
```
-   Change Case
```javascript
console.log(name.toUpperCase();    // JOHN
console.log(name.toLowerCase();    // john
```
-   substring 
```javascript
console.log(name.substring(0,3);    //Jo
```
-   split a string into an array
```javascript
console.log(name.split("");    // ["J" "O" "H" "N"] 

const s = "technology, computers, it ,code";
console.log(name.split(" ");    // ["technology" "computers" "it" "code"] 
```

## Arrays
Variables that hold multiple values
```javascript
const fruits = ["apples", "oranges", "pears"];
```
-   Push => Adds a value to the beginning of the Array
 ```javascript
fruits.push(mangos); //["apples", "oranges", "pears", "mangos"];
```
-   unshift => Adds a value to the beginning of the Array
```javascript
fruits.unshift(mangos);
fruits.push(mangos); //["mangos", "apples", "oranges", "pears"];
```
-   isArray => Is this an Array
```javascript
console.log(Array.isArray(fruits));   //true
console.log(Array.isArray(fruits));   //false
```
-   indexOf => Position of a value inside an Array
 ```javascript
console.log(fruits.indexOf(oranges); //2
```

## Objects
```javascript
const person = {
firstName: "John",
lastName: "Doe",
age: 30,
hobbies: ["music", "movies", "sports"],
adress: {
 street: "50 main st",
 city: "Boston",
 state: "MA"
 }
}

consolelog(person.hobbies[1]; //movies
```
- ES6 allows you to get the values of an object out and asing them to a new variable for easier access. 
 ```javascript
const {firstName, lastName, adress{city}} = person;
console.log(firstName);  //John
console.log(city);  //Boston
```
## Loops
### For

```javascript
for(let i = 0; i<10; i++) {
console.log(i);}
```
### While
```javascript
let i =0;
while(i<10) {
console.log(i);
i++;}
```
### Loop through Arrays
Get every value of an Array
```javascript
for( let X of arrayName){}
```
### ForEach
```javascript
let arr = [
{
id:1,
text: Hi
},
{
id:2,
text: How are you?
}
]
arr.forEach(function(variable){
console.log.variable.text}
```

### Map
```javascript
let arrText = arr.map(function(variable){
return variable.text;
}
```
## Conditionals
```javascript
const x = 10;
if (x == 10){console.log("X es un 10!")}
else if (x>10) {console.log("X es mayor a 10")}
else {console.log("X es menor a 10")}
```
- SHORTHAND
```
const x = 10;
const color = x > 10 ? "red" : "blue";  // blue
```
### Switch
```javascript
switch(color) {
case "red";
console.log("color is red");
break;

case "blue";
console.log("color is blue");
break;

default;
console.log("color isn't red or blue");
break;
}
```
## Functions

Functions are first class objects - a function is a regular object of type `function`. The function object type has a constructor: `Function`.

There are several ways to declare a function.

The difference is how the function interacts with the external components (the outer scope, the enclosing context, object that owns the method, etc) and the invocation type (regular function invocation, method invocation, constructor call, etc).


```javascript
function addNums(num1 = 1, num2 = 1){  //Le puedo asignar valores predefinidos a una función
return num1 + num2;
}
cosole.log(addNums(5,5));  //10
cosole.log(addNums());  //2
```
### Arrow Function
Crea una variable con el nombre de tu función y los parametros y después le dices lo que hace con una flecha
```javascript
const addNums (num1, num2) => num1+num2  //Si es solo una expreción lo que hay dentro de la función no hace falta que pongas {} ni return
cosole.log(addNums(5,5));  //10
```

## Classes
```
class Person {
constructor(firstName, lastName, dob){
  this.firstName = firstName;
  this.lastName = lastName;
  this.dob = new Date(dob);
  }
function getBirthYear () {
return this.dob.getFullYear();}

function getFullName() {
return `${this.firstName} ${this.lastName}`;}
}
```
- Befor ES6 Classes didn't exits, they used functions instead
```javascript
function Person(firstName, lastName, dob) {
this.firstName = firstName;  //this allow us to use the info that is passed later
this.lastName = lastName;
this.dob = new Date(dob);
}

Person.prototype.getBirthYear = function() {  //they are inside the proto so they don't show when we call the function
return this.dob.getFullYear();}

Person.prototype.getFullName = function() {
return `${this.firstName} ${this.lastName}`;}
```

## Document Object Model (DOM)

The Document Object Model (DOM) maps out an entire page as a document composed of a hierarchy of nodes like a tree structure and using the DOMAPI nodes can be removed, added, and replaced.

```javascript
document.getElementById();
document.getElementsByClassName();
ocument.getElementsByTAgName();

document.querySelector();  //Can select by Id's Class and tags
document.querySelectorAll();  //Select all of the items
```
### Make changes in the page
```javascript
document.querySelector(.items).remove();
document.querySelector(.items).style.background = "#ccc";
document.querySelector(body).classList.add = ".bgColor"

document.querySelector(.items).textContent = "Hello";
document.querySelector(.items).innerText = "Hi";
document.querySelector(.items).innerHTML = '<h1>Hey</h1>';
```

## Events
```
const btn = document.querySelector(button);
btn.addEventListener("click", (e) => {   //If it is a form we should put e.preventDefault(); so the page doesn't recharged after clicked.
console.log("click"); 
```

# Hoisting

Both variable and function declarations are hoisted to the top on code execution, meaning that their order is irrelevant i.e functions can be called before they are declared.

# Useful

## Truthy / Falsy

Strings with at least one letter and numbers larger than zero are `truthy`.

```javascript
console.log(true && "foo"); // foo
console.log(true && "foo" && 1); // 1
```

# Debugging

```javascript
// Write to console
console.log();

// Show DOM element
console.dir();

// Display the call stack of a function
console.trace();

// Track execution time
console.time("point"); // undefined
console.timeEnd("point"); // point: 1337.42 ms

// Count the number of executions
console.count("foo"); // foo: 1
console.count("foo"); // foo: 2
console.countReset("foo"); // undefined
console.count("foo"); // foo: 1

// Avoid if-else statements
function greaterThan(a, b) {
    console.assert(a > b, { message: "a is not greater than b", a: a, b: b });
}
greaterThan(2, 1); // a is not greater than b, a: 2, b: 1

// Heap size
console.memory;

// Display a table. Takes an array of objects.
console.table(array);
```
