# ES6

## Learning resources

### [You don't know JS series by Kyle Simpson](https://github.com/getify/You-Dont-Know-JS)
### [The Modern Javascript Tutorial](http://javascript.info/)
### [JavaScript. The Core: 2nd Edition](http://dmitrysoshnikov.com/ecmascript/javascript-the-core-2nd-edition/)
### [MDN docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
### [Secrets of the JavaScript Ninja: 2nd Edition](https://www.dropbox.com/s/pafbxnka2q2z893/Resig_D__Bibeault_B__Maras_J_-_Secrets_of_the_JavaScript_Ninja_Second_Edition_-_2016.pdf?raw=1)
### [Eloquent JavaScript](http://eloquentjavascript.net/)


## Const, Let

- with `var` we've only been able to create a scope inide a function
- with `let` anytime it's wrapped around a __curly bracket {}__ it creates a new scope - even __if statements__

```javascript
let wizardLevel = false;

if (experience = 90) {
    let wizardLevel = true;
    console.log('inside', wizardLevel);
}
console.log('outside', wizardLevel);
```
```
inside true
outside false
```
- &uarr; created it's own scope inside the if statement

- if used var:

```javascript
var wizardLevel = false;

if (experience = 90) {
    var wizardLevel = true;
    console.log('inside', wizardLevel);
}
console.log('outside', wizardLevel);
```
```
inside true
outside true
```

- __const__ = constant
- constants cannot be changed
- if we assign an object to a constant:

```javascript
const obj = {
    player: 'bobby',
    experience: 100,
    wizardLevel: false
}
// results in error
obj = 8;
// allows to change
obj.wizardLevel = true;
```
- properties of the object can be changed, we just can't reassign a const variable


## Destructuring

```javascript
 const obj = {
    player: 'bobby',
    experience: 100,
    wizardLevel: false
}

const player = obj.player;
const experience = obj.experience;
let wizardLevel = obj.wizardLevel;

// destructuring
const { player, experience  } = obj;
let { wizardlevel } = obj;
// now we can access player and experience
console.log( player );
console.log( experience );
```

## Declaring Object properties

- in ES6 we can have dynamic properties, property values

```javascript
const name = 'john snow';

const obj = {
    [name]: 'hello',
    ['ray' = 'smith']: 'hihi',
    [1+2]: 'heyhey'  
}
```
```
{3: "hihi", john snow: "hello"}
```
- very useful if we want to calculate something for the property value

- sometimes we want the property to match the value
```javascript
const a = 'Simon';
const b = 'true';
const c = {};

const obj = {
    a: a,
    b: b,
    c: c
}
```
- in ES6 we can remove the declaration if they're the same and do
- useful in REACT

```javascript
const a = 'Simon';
const b = 'true';
const c = {};

const obj = {
    a,
    b,
    c
}
```

## Template strings

- we can create a template string with backticks __``__
- we can dynamically add a value with __`${variable/value}`__
- we can do operation inside the dynamic __`${}`__ 

```javascript
// Annoying
const greeting = "Hello" + name + " you seem to be going " + greeting + "!";

// In ES6
const name = 'Sally';
const age = 34;
const pet = 'horse';

const greeting = `Hello ${name} you seem to be ${age-10}. What a lovely ${pet} you have.`;
```

## Default arguments

- we can give default arguments to parameters, so if no value is provided, they'll default to some values and not break the code

```javascript
function greet(name='', age=30, pet='cat') {
    return `Hello ${name} you seem to be ${age-10}. What a lovely ${pet} you have.`;
}
```

## Javascript type = Symbol

```javascript
let sym1 = Symbol();
let sym2 = Symbol('foo');
let sym3 = Symbol('foo');
```
```
sym1 --> Symbol()
sym2 --> Symbol(foo)
sym3 --> Symbol(foo)
sym2 === sym3 --> false
```
- even though 2 symbols look the same, they're distinct
- symbols are used because they create this completely unique type
- there's not going to be any conflict


## Arrow functions

```javascript
// Old way
function add(a, b) {
    return a + b;
}

// New way - arrow function
const add = (a, b) => a + b;

// Or we can also do
const add = (a, b) => {
    return a + b;
}
```
- __`=>`__ represents __`return`__
- with arrow function if I've got a single return, I can put it on one line and it assumes that it will be returned after the `=>`


## Advanced Functions

```javascript
// Old
function first() {
    var greet = 'Hi',
    function second() {
        alert(greet);
    }
    return second;
}

var newFunc = first();
newFunc();

// New
const first = () => {
    const greet = 'Hi';
    const second = () => {
        alert(greet);
    }
    return second;
}

const NewFunc = first();
newFunc();
```
- &uarr; the above ran will show an alert with text 'Hi'

### Closures

- child scope has always access to parent scope
    - e.g. function in a function
    - a function ran. the function executed. it's never going to execute again, BUT, it's going to remember that there are references to those variables, so the child scope always has access to the parent scope
    - children have access to their parent scope, but parent's don't have access to children scope


### Currying

- [Link to Medium article](https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983)
-  the process of converting a function that takes multiple arguments into a function that takes them one at a time

```javascript
const multiply = (a, b) => a + b;
const curriedMultiply = (a) => (b) => a + b;
const multiplyBy5 = curriedMultiply(5);
```
- now, everytime we pass a number into `multiplyBy5()`, it is going to be multiplied by 5

```javascript
multiplyBy5(5);
// 25
multiplyBy5(10);
// 50
multiplyBy5(11);
// 55
```

### Compose

- [Function composition](https://www.codementor.io/michelre/use-function-composition-in-javascript-gkmxos5mj)
- [10 ways to write Pipe/Compose](https://medium.com/front-end-weekly/10-ways-to-write-pipe-compose-in-javascript-f6d54c575616)
- [Pipe/Compose](https://medium.freecodecamp.org/pipe-and-compose-in-javascript-5b04004ac937)

- act of putting 2 functions together to form a 3rd function where the output of one function is the input of the other

```javascript
const compose = (f, g) => (a) => f(g(a));

// example
const sum = (num) => num + 1;

compose(sum, sum)(5);
// returns 7
```

#### Avoiding(Minimizing) Side Effects / Functional purity
- [Deterministic algorithm](https://en.wikipedia.org/wiki/Deterministic_algorithm)
- [Pure functions](https://medium.com/@halistechnology/functional-programming-pure-functions-2cd3b6804ebe)


- we want to think of functions as their own universe --> they should NOT affect the outside world
- __functional purity__ concept = in order for us to write really good programs, we want to avoid side effects and we always want to return something
    - by eliminating side effects and always returning something, we create sth called __Deterministic/Determinism__ => If we pass whatever arguments, it will always return the same value 

- What are the two elements of a pure function?
    - __Deterministic__ --> always produces the same results given the same inputs
    - __No Side Effects__ -->  It does not depend on any state, or data, change during a program’s execution. It must only depend on its input elements.


## Advanced Arrays

- [Arrays tips and tricks](https://www.codingame.com/playgrounds/6181/javascript-arrays---tips-tricks-and-examples)
- [Map, filter and reduce in JS](https://medium.com/@joomiguelcunha/learn-map-filter-and-reduce-in-javascript-ea59009593c4)
- [Functional programming - map, filter, reduce](https://medium.com/jsguru/javascript-functional-programming-map-filter-and-reduce-846ff9ba492d)
- [Map, filter, reduce JavaScript](https://hackernoon.com/map-filter-reduce-ebbed4be4201)
- [Simplify JS with map, filter and reduce](https://medium.com/poka-techblog/simplify-your-javascript-use-map-reduce-and-filter-bd02c593cc2d)
- [Map, filter,reduce in Python](http://book.pythontips.com/en/latest/map_filter.html)
- [__Array explorer__](https://sdras.github.io/array-explorer/)

- __for, forEach__

```javascript
// forEach
const array = [1, 2, 10, 16];
const double = [];
const newArray = array.forEach((num) => {
   double.push(num * 2);
});
console.log(double);
// returns [2, 4, 20, 32]
```

- __map, filter, reduce__
    - one of the most important methods used for day-to-day JS development
    - everytime I think of doing a loop - most probably I will need/end up using one of the 3(map, filter, reduce)

### map()
- the way `map()` works --> we always need to return something
```javascript
// longer way
const mapArray = array.map((num) => {
    return num * 2; 
})

// shorter way
// is we have a single parameter, we can omit the paranthesis
const mapArray = array.map(num => num * 2)
```
- everytime we want to loop through an array and take some actions on the elements - USE `map()` over a `forEach()`
    - all `forEach()` cares about is to iterate through the collection
    - `map()` loops through each element applying the operation on each elementa and finally storing each invocation of the operation into another collection
        - `map()` transforms the array

- change array inside an array:

```javascript
const array = [
	{
		username: "john",
		team: "red",
		score: 5,
		items: ["ball", "book", "pen"]
	},
	{
		username: "becky",
		team: "blue",
		score: 10,
		items: ["tape", "backpack", "pen"]
	},
	{
		username: "susy",
		team: "red",
		score: 55,
		items: ["ball", "eraser", "pen"]
	},
	{
		username: "tyson",
		team: "green",
		score: 1,
		items: ["book", "pen"]
	},
];

// create a new list with all user information, but add "!" to the end of each items they own
const newList = array.map(el => {
    el.items = el.items.map(item => {
      return item + '!';
    });
    return el;
});
```

### filter()

- we can filter our array with a condition

```javascript
// return elements that are greater than 5
const filterArray = array.filter(num => {
   return num > 5; 
});
```
- &uarr; the `filterArray` will only contain the elements that meet the condition
    - if it return true - it will go to the array
    - if it return false - it will NOT go to the array


### reduce()

- powerful method - we can actually do `map()` and `filter()` with `reduce()`

```javascript
// return the sum of the array
const reduceArray = array.reduce((accumulator, num) => {
    return accumulator + num;
}, 0);
```
- _num_ is the iterated element of the array
- _accumulator_ is something where we can store the information that happens in the body of the function
- we define the accumulator starting number as the 2nd argument


## Advanced Objects

- [JavaScript Object Explorer](https://sdras.github.io/object-explorer/)

### Reference type
- [How to compare 2 arrays in JS](https://codeburst.io/comparison-of-two-arrays-using-javascript-3251d03877fe)

```javascript
// in JavaScript
[] == []
// returns false
[] === []
// returns false
[1, 2] === [1, 2]
// returns false
```

```python
# in Python
[] == []
# returns true
[1, 2] == [1, 2]
# return true
[1, 2] == [2, 1]
# returns false
```
- let's try with objects

```javascript
var object1 = { value: 10 };
var object2 = object1;
var object3 = { value:  10 };

object1 === object2
true
object1 === object3
false
object2 === object3
false
object1.value === object2.value;
true
object1.value === object3.value;
true
object1 == object3;
false
object1.value = 15;
15
object1.value;
15
object2.value;
15
object3.value;
10
```
- __objects__ are __reference types__
- strings, integers, booleans, null, undefined are all __primitive types__, meaning the programming language defined them
- non-primitive types are not defined by the programming languages
    - meaning, they're created by the programmer

![Primitive vs reference](https://www.dropbox.com/s/4vv6i3r8un3ltnb/types_in_js.png?raw=1 "Primitives vs reference types")

```javascript
var object1 = { value: 1 };
// object2 holds a reference to object1
var object2 = object1;
```
- with object2, we're essentially storing a reference to object1
- the __address__ of object1 is assigned to object2
- __arrays__ are __objects__
    - when we create an array, we're basically creating a data structure

### Context

__context vs scope__

- context tells us where we're withing the object
- __this__ means what is the object environment we're in right now
    - what is to the left of the dot
    - e.g. `window.alert('Hello')` can also be written as `this.alert('Hello')` when inside the window object(in console)
- __this__ refers to the object it's inside of

```javascript
function a() {
    console.log(this);
}
```
- &uarr; returns `window` because we're still in the window object
- we can do `window.a()`

```javascript
const myObj = {
    a: function() {
        console.log(this);
    }
}
```
- &uarr; now if we run `myObj.a()` __this__ will be the 'myObj'

### Instantiation

- [Why you should use Prototype to create Class Methods in JavaScript](https://medium.com/the-andela-way/why-you-should-use-prototype-to-create-class-methods-in-javascript-ffaf82996977)
- [Javascript : Prototype vs Class](https://medium.com/@parsyval/javascript-prototype-vs-class-a7015d5473b)
- [Details of the object model - class-based vs prototype-based languages](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model)
- 

- instantiation is when we make a copy of an object and reuse the code
    - OOP - making instances/multiple copies of the object


```javascript
// the new way
class Player {
    constructor (name, type) {
        this.name = name;
        this.type = type;
    }
    introduce() {
        console.log(`Hi I am ${this.name}, I'm ${this.type}`);
    }
}

// everytime we extend, we need to call the constructor
// of the Player too
class Wizard extends Player {
    constructor (name, type) {
        super(name, type)
    }
}
```
- everytime we extend a class, we need to use __`super()`__


## Pass by reference VS Pass by value

- primitive types are immutable
    - we cannot change them, in order for us to change it, we need to remove it and create new 


![Pass by reference vs Pass by value visualization](https://www.dropbox.com/s/0qhqz60xz0u0wje/pass_by_reference_value.png?raw=1 "Pass by reference vs Pass by value")

```javascript
var a = 5;
var b = 10;

b++;
// a is 5
// b is 6 
```
- __a__ and __b__ has the address where the primitive value 5 and 10 sits in the memory
- pass by value means we copy the value and we create that value elsewhere in the memory

```javascript
let obj1 = { name: 'John', password: '123' }
let obj2 = obj1;
// obj1, obj2 are pointers to one location in memory
```
- as arrays are also objects

```javascript
var c = [1, 2, 3, 4, 5];
var d = c;
d.push(10);
// will modify d and also c
```
- we can change the behaviour by doing &darr;

```javascript
var c = [1, 2, 3];
var d = [].concat(c);
d.push(10);
// now d is [1, 2, 3, 10]
// but c is [1, 2, 3]
```

- with Objects it's more complicated --> we can __clone__ an object

```javascript
let obj = {a: 'a', b: 'b', c:'c'};
let clone = Object.assign({}, obj)
```
```javascript
Object.assign(target, source)`
```
- bear in mind it only clones the first layer
    - __shallow clone__
    - if we have an object inside an object, it's still going to reference to same place in memory

```javascript
let myObj = {
    a: 'a',
    b: 'b',
    c: {
        deep: 'try and copy me'
    }
};

let clone = Object.assign({}, myObj);
// {...obj} clones the obj
let clone2 = {...myObj}

obj.c.deep = 'hahaha';
console.log(myObj);
console.log(clone);
console.log(clone2);
```
```
{ a: 'a', b: 'b', c: { deep: 'hahaha'} }
{ a: 'a', b: 'b', c: { deep: 'hahaha'} }
{ a: 'a', b: 'b', c: { deep: 'hahaha'} }
```

- __spread__ operator clones the obj:
    - `{...obj}`

- to superclone --> we use JSON

```javascript
let superClone = JSON.parse(JSON.stringify(myObj));
```
- with JSON we can do a __deep clone__ of the object


## Type coercion

- [Type coercion table](https://dorey.github.io/JavaScript-Equality-Table/)
- [MDN Equality comparison](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
- [The Abstract Equality Comparison Algorithm](https://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3)

- the language converting one type to another type
- all languages have type coercion

```javascript
1 == '1'
true
```
- in JavaScript type coercion happens when we use `==` (double equals) sign.
    - compare the 2 values and if they are different types, try to coerce one into the same type

- `===` (3 equals) is strict comparison -> do NOT convert to other type
- always use `===` for comparing values

- coercion happens with IFs, too.

```javascript
// 0 is coerced to false
if (0) {
    // code
}
```

## ES7

### includes() method
- includes() method on strings and arrays

```javascript
'Heloooo'.includes('o');
// returns true
```

```javascript
const pets = ['cat', 'dig', 'bat'];
pets.includes('dog');
// returns false
```

- examples:
1. Check if this array includes the name "John".

```javascript
const dragons = ['Tim', 'Johnathan', 'Sandy', 'Sarah'];

dragons.includes('John');
```

2. Check if this array includes any name that has "John" inside of it. If it does, return true.

```javascript
const val = dragons.reduce((acc, curr) => {
    if (curr.includes('John')) {
      acc = true;
    }
    return acc;
}, false);
```
OR
```javascript
dragons.filter(name => name.includes('John')) 
// ['Johnathan']
```

3. Check if this array includes any name that has "John" inside of it. If it does, return that name or names in an array.

```javascript
const val = dragons.reduce((acc, curr) => {
  if (curr.includes('John')) {
	acc.push(curr);
  }
  return acc;
}, []);
```


### exponential operator **

```javascript
const square = (x) => x**2;
const cube = (y) => y**3;
```

## ES8

### String padding - string methods

- [String padding - padStart & padEnd](https://codeburst.io/learn-javascript-es-2017-string-padding-padstart-padend-88e90783e7de)

```javascript
.padStart()
.padEnd()
'Turtle'.padStart(10);
"    Turtle"
'Turtle.padEnd(10)';
"Turtle    ";
```
```javascript
const str1 = 'Breaded Mushrooms';

console.log(str1.padEnd(25, '.'));
// expected output: "Breaded Mushrooms........"
```
- makes the whole string 10 characters long including the string
- the 2nd parameter in `padStart()` and `padEnd()` provides the character to fill with

- __trim()__ removes any whitespaces from the string

```javascript
var greeting = '   Hello world!   ';

console.log(greeting);
// expected output: "   Hello world!   ";

console.log(greeting.trim());
// expected output: "Hello world!";
```

### Trailing commas in function's parameter lists and calls

```javascript
const fun = (a, b, c, d,) => {
    console.log(a);
}

fun(1, 2, 3, 4,);
```
- ending comma is now valid and won't give out any error
- useful when we have longer parameter list

```javascript
const fun = (
    a, 
    b, 
    c,
    d,
    e,
    ) => {
    console.log(a)
};
```

 ### Object.values() & Object.entries()
 
 - before we had `Object.keys`
     - it allowed us to work with them like an array
     - often when we work with servers we don't get nice looking objects, but still want to iterate through them

```javascript
let obj = {
    username0: 'Santa',
    username1: 'Rudolf',
    username2: 'Mr. Grinch'
}

// Object.keys(obj) iterates throught the object

Object.keys(obj).forEach((key, index) => {
    console.log(key, obj[key]);
})
```
```
username0 Santa
username1 Rudolf
username2 Mr. Grinch
```

- `Object.keys` is the 1st way to iterate through objects
- with __`Object.values(obj)`__ --> easier
#### `Object.values(obj)`

```javascript
Object.values(obj).forEach(value => {
    console.log(value);
})
```
```
Santa
Rudolf
Mr. Grinch
```
#### `Object.entries(obj)`

```javascript
Object.entries(obj).forEach(value => {
    console.log(value)
})
```
```
(2) ["username0", "Santa"]
(2) ["username1", "Rudolf"]
(2) ["username2", "Mr. Grinch"]
```
- now we can use __map, filter, reduce__ on objects

```javascript
console.log(Object.entries(obj));
```
```
(3) [Array(2), Array(2), Array(2)]
(2) ["username0", "Santa"]
(2) ["username1", "Rudolf"]
(2) ["username2", "Mr. Grinch"]
```
- example with __map__ we can iterate through key, value of objects

```javascript
Object.entries(obj).map(value => {
    return value[1] + value[0].replace('username', '');
})
```
```
(3) ["Santa0", "Rudolf1", "Mr. Grinch2"]
```

## Looping

- for, while, do while, forEach

```javascript
const basket = ['apples', 'oranges', 'grapes'];

// for loop
for ( let i = 0; i < basket. ) {
    console.log(basket[i]);
}

// forEach loop
basket.forEach( item => {
    console.log(item) ;
});
```
- iterating = looping through arrays or strings one by one
    - both arrays and strings are iterable
- additional 2 are __`for of`__ and __`for in`__


[For...of vs for...in](https://alligator.io/js/for-of-for-in-loops/)

### for of (ES6)

```javascript
for (item of basket) {
    console.log(item);
}
```

### for in (ES6)

- [Why is using "for...in" with array iteration a bad idea?](https://stackoverflow.com/questions/500504/why-is-using-for-in-with-array-iteration-a-bad-idea)

- `for in` works with objects
- `for in` allows us to loop over an object and take a look at __object properties__ --> (so that I can check what I need to go grocery shopping for)
- with object we are NOT iterating
- what we're doing with `for in`, we're __enumerating__ because properties of an object are what we call __enumerable__

- we iterate through arrays and strings but enumerate objects
- javascript object is enumerable when it allows us to see it's properties

```javascript
const detailedBasket = {
    apples: 5,
    oranges: 10,
    grapes: 1000
}

// for in
for (item in detailedBasket) {
    console.log(item);
}
```
```
apples
oranges
grapes
```

- `for...of` --> iterating --> arrays+strings
- `for...in` --> enumerating --> objects

- we get an error if we try to do `for...of` on an objects
    - Error: object is not iterable


- enumerating through arrays, objects etc.
    - for, forEach
    - Object.keys(), Object.values(), Object.entries()
    - for...in, for...of
    - map(), filter(), reduce()


1. Write a function checkBasket() that lets you know if the item is in the basket or not

```javascript
amazonBasket = {
  glasses: 1,
  books: 2,
  floss: 100
}

function checkBasket(basket, lookingFor) {
  for (item in basket) {
    if (item === lookingFor) {
      return true;
    }
  }
  return false;
}
```
- the above &uarr; will break the function and return true if found, if not, it will return false


## Debugging in JavaScript

1. Use `console.log()`
2. User `debugger;`

```javascript
// short
const flattened = [[0, 1], [2, 3], [4, 5]].reduce((a, b) => a.concat(b), []);

//long
const flattened = [[0, 1], [2, 3], [4, 5]].reduce(
    (acc, curr) => {
        debugger;
        return acc.concat(curr)
}, []);

```
- debugger allows us to step through a function
- it also shows:
    - variables in __scope__
    - context: __this__ value


## [How does JavaScript work?](https://www.udemy.com/the-complete-web-developer-zero-to-mastery/learn/v4/t/lecture/9427570?start=0)

- [Udemy video - How javascript works?](https://www.udemy.com/the-complete-web-developer-zero-to-mastery/learn/v4/t/lecture/9427570?start=0) --> watch the video several times

- __Explain the difference between synchronous and asynchronous__
- Explain: __Javascript is a single threaded language that can be non-blocking.__

1. What is a program?
- allocate memory
- parse and execute


## Modules

- [Brief History of Modules in Javascript](https://medium.com/@sungyeol.choi/javascript-module-module-loader-module-bundler-es6-module-confused-yet-6343510e7bde)

- [ES modules: A cartoon deep-dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)
