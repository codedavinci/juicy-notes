# ECMAScript2015 (ES6)
### Idiotic notes for idiot people, like me 🤤 🤤

---
> "All this "open-sourceness" evolves way too quickly and read long books, video tutorials can get very tiring, isn't it ? so I just felt the necessecity of having these quick tips handy."
---

The rule is very simple, I write a code example and then "idiotically" I'll say **what** it is, **when** to apply it, and **why** this way because honestly, I can't rely on my brain, can you ? 


## New Feautures ES6 & Tips

- [Arrow funtions](#arrow-functions)
- [Let keyword](#let-keyword)
   * [Set Variables](#set-variables)
   * [Loops](#loops)
- [Paramenters](#parameters)
   * [Default Arguments](#default-arguments)
- [Const declaration](#const-declaration)
- [ShortHand properties](#shorthand-properties)
- [Object enhancement](#object-enhancement)
- [Spread operators](#spread-operators)
- [String templates](#string-templates)
- [Destructuring assignment](#destructuring-assignment)
- [Import and Export](#import-and-export)
- [Arrays Conversion](#array-conversion)
- [Promises](#promises)
- [Generators](#generators)


## Arrow Functions

```js
//ES5
var sendMessage = function (message, sender) {
    return message + sender;
}
//ES6
var sendMessage = (message, sender) =>  {
    return message + sender; 
}
//ES6 Short-Hand (More than one parameter)
var rectangle = (length, width) => length * width;

//ES6 Short-Hand (One parament)
var square = x => x * x; 

//Handling Actions Inside an Object
//ES5 
var sendMessage = {
  name: "Eddie",
  handleMessage: function(message, handlerCb){
    handlerCb(message);
  }, 
  sayIt: function () {
    var that = this; // Make a copy of the whole scope, so we can access "name" inside of the callback function.
    this.handleMessage("Good morning ", function (message){
        that.name;
        console.log(message + that.name);
    }) 
  }
}


var sendMessage ={
  name: "John",
  
  handleMessage: function (message, handler){
    handler(message);
  },
  
  sayIt: function () {
    this.handleMessage("Hello, ", message => console.log(message +       this.name)) // The arrow functions leave an open door, to access the scope using "this".
  }
}

deliveryBoy.receive();


```
**What it is:** This is a new feature called "Arrow Functions" from the new update on *ECMAScript2015* or *ES6* Version. 

**When to apply it:** There's no specification saying when to apply it, but it's always good to keep the code consistent, by following the main web standards such as: If you have a function with more than one parameter and have error, data and a callback, please always folow the order `someFunction(err,  data, callback)`. 

**Why:** Because all *Web Developers* will love you forever for not making their life harder 😬  


## Let Keyword
#### Set variables

```js
//Case where you Reasign a variable
var animal = "panda";
{ var animal = "koala"; }
console.log(animal); //koala
//The majority people think that it would display "panda" because it's out of the curly braces 😜, but in this case because the variable has the same name, it's simply reassigning its value. 

//Solution for it (using "let")
let animal = "panda";
{ let animal = "koala"; }
console.log(animal); //panda

//Solution #2 using "var" (locking it in a function)
var animal = "panda"
function setAnimal(){
    var animal = "koala"; //blocked by the scope
}
console.log(animal) //panda
```

#### Loops

```js
//ES5 - Example
var array = []
for(var index; index < 10; index++){
    array.push(function(){
        console.log(index);
    });
}
array.forEach(function(f){
    f();
});


//ES6
var array = [];
for(var index = 0; index < 10; index++ ){
    array.push(() => console.log(index));
}
array.forEach((f) => f()); // 10, 10, 10, 10, 10, 10, 10.  Because the last time the loop iterate, the ten (10) copies of the variable index is reassigned with the last value, because it's declared with "var" 

//Solution Using let
var array = [];
for(let index = 0; index < 10; index++ ){
    //Each time it iterates, a new copy of index (with a new  reference) is created with the keyword "let", rather than just create a copies of the same reference with "var" 
    array.push(() => console.log(index));
}
array.forEach((f) => f());

```

**What it is:** This is a new keyword called `let`,  from the new update on *ECMAScript2015* or *ES6* Version. The `let` allows us to use block scopping

**When to apply it:** Whenever you come up with a situation where you need to assign a variable with the same and doesn't want it to be affected by changing it's reference, for instance in loops.

**Why:** Because if you don't you'll just over-perform the system with your code, overthink on your logic and face lots of problems such as reassignments 🙅 🙅

## Parameters

#### Default Arguments
```js
//No Arguments
function sayIt(message, name){
    console.log(message + ", " + name);
} 
sayIt(); //undefined, undefined

//Defining default Arguments
function sayIt(message, name ="Eddie"){
    console.log(message + ", " + name);
} 
sayIt("Good morning"); // Good morning, Eddie

//Overwriting Default Arguments
function sayIt(message, name="Eddie"){
    console.log(message + ", " + name);
} 
sayIt("Good morning", "Panda"); // Good morning, Panda

//Function as an argument (No default)
function apply(done){
    done();
}
apply(); //Error - undefined is not a function.

//Function as an argument (No default - ES5)
function apply(done){
    done();
}
apply(function(){
    console.log("done!");
}); //done !

//Function as an argument with default param (ES5)
function apply(done = function(){
    console.log("done!");
}){
    done();
}
apply(); //done!

//ES6
function apply(done = () => console.log("done!")){
    done();
}
apply(); //done!

//ES6 Short-hand using let
let apply = (done = () = console.log("done!")) => done(); //done!
```


**What it is:** Very cool feature that allows us set *default arguments in our functions*

**When to apply it:** Whenever you come up with a situation where you need to assign with a default value. 

**Why:** Sometimes, there are cases that we want to return something to the client, even though it has receveid nothing 😎😎


## Const Declaration

```js
//ES5 Standards for constants
var PI = 3.14; //All in uppercase to represent that it's a constant.
var PORT = 8080;// but still, it could easily be reassigned. 
PORT = 3000;
console.log(PORT); //3000


//ES6 new feature "const"
const PI = 3.14;
const PORT = 8080;
PORT = 3000;
console.log(PORT); //Error:  the variable PORT is read-only and can't be reassigned.

//ES6 assign properties to a const variable.
const OBJ = {};
OBJ.name = "Eddie";
OBJ.age = 26;
console.log(OBJ); //{ name: "Eddie",  age: 26 }

//ES6 Reassign a const variable. 
const OBJ = {};
OBJ = "Eddie";
console.log(OBJ); //Error, OBJ is read-only and can't be reassigned.
//
```

**What it is:** the keyword `const` allows us to create a constant of a variable reference, this is very importa: **just of a variable reference**, It means that you can change its reference, for instance, if you we assign a variable with a string, I can't change this string, but if I assign a variable with an empty object, I can add properties to it 😱 😱. Cool, right ??

**When to apply it:** Whenever you need to create a variable that must not be changed its reference, such as PORT's, Static values, Server IP and etc.. 

**Why:** Because as said earlier, we want to proctect our variables against being overwritten /changed 💪 💪

## ShortHand Properties
```js
let firstName = "Eddie";
let lastName = "Henrique";
let person = {firstName, lastName}
console.log(person) // {firstName: "Eddie",  lastName: "Henrique"}
let department = "IT";
let employee = {person, deparment}   //{ department: "IT", person:{ firstName: "Eddie", lastName: "Henrique" } }
```

**What it is:** We can easily construct objects and its properties with this new sintaxe.

**When to apply it:** Whenever we face some requirements where need to create new properties into our new object. This way we don't have the necessary of creating multiples models. 

**Why:** Because we need to be cautious when to extend our objects, use with moderation. 👀 

## Object Enhancement

```js
let gender = "male";
let legs = 4;
function walk(){ 
console.log("Walking..");
}

let healthAnimal = {gender, legs, walk} //because the properties are the same name, the object treats as if it was  {color: color, doors: doors}(ES5 way !)
console.log(house.color);
console.log(house.doors);
healthAnimal.walk(); // "male", 4, "Walking.."


//Different ways of constructing Objects.
let healthAnimal = { gender, 
                    legs, 
                    walk(){   //In ES5 would be  walk: function() { }
                    console.log("Walking..");
                    } 
console.log(house.color);
console.log(house.doors);
healthAnimal.walk(); // "male", 4, "Walking.."

//Another way, through computed properties ["property"]

let healthAnimal = { gender, 
                    legs, 
                     ["walk"]: function {
                    console.log("Walking..");
                    } 
console.log(house.color);
console.log(house.doors);
healthAnimal.walk(); // "male", 4, "Walking.."

```

**What it is:** That's the new and beautiful several ways of construct an object in the new ECMAScript2015(ES6)

**When to apply it:** It'll depend on your requirements. One thing we know, it facilitates very much on how to design our application with ES6 .

**Why:** Because It's just awesome 😂 😂

## Spread Operators
```js

//Merging two arrays without Spread Operators
let array = [1, 2, 3, 4, 5];
let array2 = [6, 7, 8, 9, 10];
array.push(array2);
console.log(array); // [1, 2, 3, 4, 5, [6, 7, 8, 9, 10]]

//Console log With Spread Operators 
let array = [1, 2, 3, 4, 5];
let array2 = [6, 7, 8, 9, 10];
array.push(...array2); //Adding the Spread sign "..."
console.log(array); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] (It merges without any problem)
console.log(...array); // 1 2 3 4 5 6 7 8 9 10 (Just the values of the array)

//Spread into parameters 

let measuraments = [4, 2, 5];
function getVolumeRetangularPrism(length, width, height){
    let result =  length * width * height;
    console.log(result);
}
getVolumeRetangularPrism(...measuraments); //40 

```

**What it is:** Spread Operators allow us to easily manipulate the values of an Array, by freeing it. 

**When to apply it:** Whenever you need to use the data of an array you can easily free it, by using the 3 dots, for instance, merging 2 arrays with spread operators is very easy !

**Why:** I wouldn't want to complicate this process  😂 😂

## String Templates
```js
//Simple string building
var k3 = "I love you <3";
var lovemessage = ` I just wanna say ${k3}`; //PS: It takes all space you define, even paragraphs.
console.log(lovemessage); //I Just wanna say I love you <3

//Doing Expressions
var x = 4;
var area = `the area is ${ x * x }`;
console.log(area);

//Executing function with String Templates.
var date = new Date;
function check(strings, ...values){ //all strings are casted into array strings, and all values are spread into values array.
    if( values[0] < 9){
      values[2] = "I am getting ready to go to work";
    }else if( values[0] > 17 && values[1] > 30){
     values[2] = ",I am already off work";
    }else{
    values[2] = "and I am still working. :)";
    }
    return `${strings[0]}${values[0]}:${values[1]}${strings[1]} ${values[2]}`
}

var workerstatus = check`It's ${date.getHours()}${date.getMinutes()}${""}`
console.log(workerstatus);
```

**What it is:** This is a very powerful feature that allows us build our own string using logic, operations and even run functions to determine its content. 🤓 🤓 

**When to apply it:** Whenever you come up with a requirement where you need to display a string wiith some values of variables or properties. PS: We can also use *Regex* (Regular expressions into it). 🤑 🤑

**Why:**  Because, It's extremly powerful, specially in some cases where you need some live update on the client side, without send a request back to the server 👌 👌

## Destructuring Assignment
```js
//ES5 - Log out a property of an object
var obj = { type: "A" }
console.log(obj.type); //"A"

//ES6 - Log out a property with Destructuring Assignement (One property)
var { type } = { type: "Class A"}
console.log(type) //"Class A"

// Multiple properties
var { type, color } = { type : "Class A", owner : "Frank Martinez", color : "blue" make : "Honda" }
console.log(type, color); //Class A  blue

// Destructuring an Array
var [first,,,,last] = [1, 2, 3, 4, 5]; //Note that because there are empty spaces in between the comas the other values are innacessible.
console.log(first, last) //1 5

//Getting just the "Make" from an array  of cars with "Destructuring Assignment, and Arrow Functions (Callback)
var cars = [
    {
        type: "Classe A",
        color: "green",
        make: "Honda"
    },
    {
        type: "Classe B",
        color: "blue",
        make: "Mercedes"
    },
    {
        type: "Classe D",
        color: "yellow",
        make: "Subaru"
    },
    {
        type: "Classe F",
        color: "white",
        make: "Volvo"
    }
]
cars.forEach(({make}) => console.log(make)); // "Honda" "Mercedes" "Subaru" "Volvo". It literally checks if there's any property in the object with the same "Make" and make it available externally.


//Abstract Function receiving Destructured Parameters.
var [, Mercedes] = cars; 

function getColor({color}){ //I am passing the Destructured field  I want from the distructure object tha i'm gonna be passing.
    console.log(color);
}
getColor(Mercedes); //blue
```

**What it is:** This is a very simplified way to manipulate the values of  properties of objects, if you know what I mean.. 🤓 🤓 

**When to apply it:** Whenever you feel like manipulating the object and its proerty. 🤤 🤤

**Why:**  Because abstraction is the key !! 🔑 🔑

## Import and Export
```js
//main.js 
import { getSquareArea,
        getVolumeRetangularPrism
        }  from  ' math/formulas ';

//math/formulas.js (First way)
function getSquareArea( x, y ){  return x  * y }
function getVolumeRetangularPrism(length, width, height){
    return  length * width * height;
}
export { getSquareArea, getVolumeRetangularPrism };

//Second way (Exporting the function right on the signature. Both ways will be importerd the same way.)
export function getSquareArea( x, y ){  return x  * y }
export function getVolumeRetangularPrism(length, width, height){
    return  length * width * height;
}

//Import with aliases 
    import { getSquareArea as getArea,
            getVolumeRetangularPrism as getVolume
        }  from  ' math/formulas ';
        
        
//Import everything from the file
import * as formulas from ' math/formulas ';

//Import some data the same way. (data/cars.js)
export var cars = [
    { type: "Classe A", color: "green", make: "Honda" },
    { type: "Classe B", color: "blue", make: "Mercedes"}
    ];

//Importing this data/cars.js 
import { cars } from 'data/cars';
console.log(cars.filter(({color}) => color == "blue")); //{ type: "Classe B", color: "blue", make: "Mercedes"}
```

## Array Conversion

#### NodeList to Array
```js
const cars = Array.from(document.querySelectorAll('.car')); // considering the class that's being passed is car. 

```

**What it is:** `Array.from` is the most effective way to convert  lists that come from the server side (usually defined as a `NodeList`). 
*PS: Note tha `Array.from` is a new feauture that allows us to do this convertion **natively**.*  🙏🙏

**When to apply it:** Whenever you need to do some changes values of any list and you don't have access to the server side code. 

**Why:** Because the type `NodeList` **does not**  have all typical methods such as `Array.filter`, `Array.forEach`, `Array.reduce` and etc..  Simple as that 😑 😑

## Promises
```js
//ES6 Common Standards 
 var p = new Promise((resolve, reject) => {
    if(true){
        resolve("It was resolved");
    }else{
        reject("It was rejected");
    }
 });
 
 p.then((data) => console.log("success: ", data)); //success: It was resolved
 p.catch((error) => console.log("error :", error));
 
//Passing p.catch as a callback nested in p.then 
p.then((data) => console.log("success :", data), p.catch((error) => {
    console.log("Error: ", error);
});

//Chaining multiples "then's 
p.then((data) =>  {
    console.log("success: ", data);
    return data //Note that we need to explictly return the data, in order to be accessed by the second "then" 
}). 
then(data => console.log("accomplised: ", data)); 
p.catch((error) => console.log("error :", error));
// 
```
**What it is:** It's a feature that allows us execute some layerd process, based on `resolve` and `reject`. 

**When to apply it:** When yu have some layerd process and need to test out applying some logic into it. 

**Why:** Because gives you function structure to deal with logic and cases in multiple blocks. Better than you `try` `catch`. Also it is standand across develop teams. 

## Generators 
```js
// Generators are not *Functions*
function* sayIt(){ /
    console.log('Saying hello !');
    yield "Execute this now"
}
let speak = sayIt();
console.log(speak); //{ next: [Function], throw: [Function }
let next = speak.next();
console.log(next); //{ value: "Execute this now", done: false }
console.log(next);// {value: undefined, done: true }
```

**What it is:** Generators are **Iterators Functions** that process it's statements based on `yield`.  That means that each time we run `next()` it will check the last `yield` assignement and then execute it. 

**When to apply it:** Whevever there's a situation you need to create a store and make it publicly available, like when it's applied on `redux` for instance.

**Why:** Because it's a great way to invoke an execution of a method manually.



 



 