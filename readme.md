# Callbacks Review

## Lesson Objectives

  - Define and use a callback function
  - Use a callbacks with JavaScript timing functions
  - Use a callback to handle an event
  - Use a callback to an array method

## Callbacks

  - What are callbacks?
  - Why does function signature matter?

```js
function callFunctionPassedIn (fnPassedIn) {
  fnPassedIn()
}
```

## Event Listeners

```js
$(document).ready(function(){
  //code
})
```

```js
$(document).ready(initDoc)

function initDoc () {
  
}
```

### We Do: $ jQuery Hijink$ 

https://www.microsoft.com/

```js
//first run this...
jQuery('body').html('') // $ is an alias for jQuery! they refer to the same thing

//then run these
$('body').html('<h1>MICHAELSOFT</h1>')
$('body').click(function(){
  console.log(this, ' was clicked!')
  $(this).css('background', 'red')
})
```
## Array Methods: Higher-Order Functions

### Callback Function Signature & Composition

Array methods like `.map`, `.sort`, and `.reduce` each take callback functions that have unique **function signature**.

#### Map

[.map(*callback*)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

> function (currentValue, index, array)
> this function acts upon each item that map is iterating over and **must have a return in order for `.map` to return a changed array**. 

#### Filter

[.filter(*callback*)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

> function (currentValue, index, array)
> this function also acts upon each item that filter is iterating over **returning a boolean expression**, which determine whether or not the item will be included in the array returned by `.filter`. 

#### Sort

[.sort(*callback*)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

> function (a, b) //comparison function which compares a & b

```js
const numbers = [11, 42, 39, 14, 25]

numbers.sort(compare)

function compare (a, b) {
  // return a - b
  // how is the return above working?
  // see the breakdown below from MDN

  // a should come before b
  if (a is less than b by some ordering criterion) {
    return -1 // => a, b
  }

  // b should come before a
  if (a is greater than b, or comes after, by the ordering criterion) {
    return 1 // => b, a
  }

  // a must be equal to b
  return 0 //remain in place
}
```

#### Reduce

[.reduce(*callback*)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

> function (accumulator, currentValue, index, array)

```js
const numbers = [11, 42, 39, 14, 25]

numbers.reduce((total, current) => total + current)
//we're not providing an accumulator here, so reduce will take the first item from the array and use that as the starting value of the accumulator
//as a consequence, currentValue will be the item at index 1 in the array that .reduce() is being called on
```

```js
function add (firstNum, secondNum) {
  return firstNum + secondNum
}

const numbers = [11, 42, 39, 14, 25]

const sum = numbers.reduce(add)
```


```js
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

var countedNames = names.reduce(function (allNames, name) { 
  if (name in allNames) {
    allNames[name]++;
  }
  else {
    allNames[name] = 1;
  }
  return allNames;
}, {});
// countedNames is:
// { 'Alice': 2, 'Bob': 1, 'Tiff': 1, 'Bruce': 1 }
```

## Timing Functions

### setTimeout

Timeouts run functions after a delay, specified in milliseconds.

```js
function alertPopUp () {
  alert("Pop Up")
}

const numberOfMilliseconds = 1000 // 1 second

setTimeout(alertPopUp, numberOfMilliseconds)
```

### setInterval

`setInterval` does a couple things: it calls the function passed in every so often, depending on the number of milliseconds specified. It works just like setTimeout, but the action happens repeatedly. Since the function is going run indefinitely, we will want to have a means of stopping that function from running. We have a function that can do this, `clearInterval`, but we also need a way of identify which recurring process we want to end. Luckily, setInterval returns a whole number which function as that recurring action's id.

```js
// anonymous callback function
const timerId = setInterval(function () {
  console.log('One second has just passed.')
}, 1000)

//wait a bit and then run...
clearInterval(timerId)
```
