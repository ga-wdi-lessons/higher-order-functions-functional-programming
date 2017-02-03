# Functional Programming & Higher-Order Functions

## Learning Objectives

- Explain the idea of programming paradigms
- Highlight advantages of functional programming
- Identify the benefits of pure functions and avoiding side effects
- Define the concepts of state and immutability
- Explain the benefits of higher order functions
- Implement `filter`, `map`, `reduce`, `sort` and other higher order functions

## Framing (5 minutes)

Programming at it's most basic level is the process developers undergo to instruct a computer to perform a task. But there are a number of programmatic approaches that can be taken to enable your computer to solve a specific problem. We call these approaches **programming paradigms.**

So far in WDI, we've largely relied on the *procedural programming* paradigm, which is the notion of writing a series of step-by-step instructions for your computer to carry out. For example, we wrote out every `console.log()` or `alert()` message we wanted to appear based on what our user would input as a response in "Choose You Own Adventure".

Most recently, we dipped our toes into the **object-oriented programming** paradigm. This design pattern allows us to considerably DRY up our code to achieve *abstraction*, *encapsulation* and *modularity*.

Let's look at another programming paradigm...

## Why Functional Programming? (10 minutes)

Functional programming has been called the [mustachioed hipster](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/) of the programming paradigms. But it's far from being a new concept. Lisp, one of the first programming languages ever created -- back in the 1950s -- had already embraced the paradigm.

[Ardent fans](https://www.youtube.com/watch?v=BMUiFMZr7vk&t=1s) have lauded functional programming for its emphasis on writing programs that will result in fewer bugs and more reusable code. The paradigm has historically been used with high-scale systems spanning thousands of networked computers, where it's critical that the program do exactly what's expected every time in the interest of performance and integrity. Many shied away from it, however, because "pure" functional languages are challenging to grasp and the paradigm was perceived as too "computer science-y" and academic.

*So why is functional programming seeing a resurgence?*

[Javascript is cool now.](http://blog.salsitasoft.com/why-now/)

When [Brendan Eich](http://blog.salsitasoft.com/why-now/) created Javascript for his then-employer Netscape, he was ordered by management to make the language look like Java. He obliged somewhat and gave Javascript some key functional programming features. As the language exploded in popularity, Javascript developers are now taking advantage of these features.

## What is Functional Programming? (15 minutes)

Functional programming is characterized by **pure functions** and **function composition** and avoiding:
* shared state
* mutable data
* side-effects

_Huh?_

Trying to understand the terminology associated with functional programming can be incredibly daunting. In the scope of this class, we're not going to go too in the weeds with the concepts, but we'll have initial exposure.

**Pure Functions**

Pure functions are a fundamental part of functional programming.

When we say __pure__ we mean a function, given the same inputs, will always return the same output. Such a function **does not** rely on or modify the **state** of variables outside it's scope.

The execution of a pure function doesn't depend on the state of the system. That is, avoiding **shared state**.

We also avoid the **side-effect** of modifying an external variable. As discussed earlier in the course, a side effect is an observable change in the application other than the return value of a called function.

// What's an example of a side-effect we've commonly seen?

Here's an example of an impure function:

```js
var age = 27
function increaseAgeBy(int){
  return age += int
}
increaseAgeBy(2)
```

<details>
  <summary>What makes this function impure?</summary>
  <p>The function changes variables outside of the function. This is a side-effect
  of the calling the function.</p>
</details>

<details>
  <summary>How can you demonstrate the impurity?</summary>
  <pre>console.log(age)</pre>
</details>

We can make this function pure by not changing anything outside the function. Instead, we modify the parameter, which is in the scope of the function.

```js
var age = 27
function increaseAgeBy(age,int){
  return age += int
}
increaseAgeBy(2)
// how can we demonstrate the purity here?
```

### Immutability

In the above example, `collection` is a __mutable__ data structure. `Mutable`
objects are objects whose state can be modified after creation.

When working with pure functions, it is important to avoid changing (or mutating)
objects outside of the function. Immutability, the idea of not changing data at all, is another core concept in functional programming because it allows you to change data flow.

Javascript has a method that will freeze an object one-level deep.

```js

const person = Object.freeze({
  name: 'Nayana',
  age: 13
});

person.name = 'Andy';
//will cause error
```
This method is only superficially immutable.

```js
const person = Object.freeze({
  name: { first: 'Nayana' },
  age: 13
});

person.name.first = 'Andy';
```
But there are Javascript libraries, such as Immutable.js, that can be used for deep freezing.

## Higher-Order Functions (15 minutes)

How can we start implementing functional programming practices now?

**Higher-Order Functions**

These functions are considered to be another key area -- perhaps the most important -- in the functional programming paradigm.

In functional programming languages, functions are values. That is, they can be stored in variables, or passed into other functions.

Higher-order functions are functions that can take functions as arguments and/or return a function as output. They are good for **function composition.** That is, taking a function and putting it into another allows us to compose a lot of smaller functions into a bigger function.

We've already seen an example of a higher-order function with `forEach`:

```js
var fruits = ["apples", "bananas", "cherries"];

fruits.forEach(function(currentFruit) {
  console.log("Every day I eat two " + currentFruit)
});

//vs

for(var i = 0; i < fruits.length; i++) {
  console.log("Every day I eat two " + fruits[i]);
}
```

<details>
  <summary>Anyone remember another one we've used quite frequently?</summary>
  <p>`.on('click')`</p>
</details>

## Examples of functions that take functions as arguments:

### Filter

 [`Filter`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) is a method on an array that accepts another function as it’s argument, which it will then use to return a new filtered version of the array.


```js
var naysayers = [
  {name: 'Adam', age: 320},
  {name: 'Jared', age: 222},
  {name: 'Will', age: 187},
  {name: 'Isaac', age: 320},
  {name: 'Rodney', age: 423},
  {name: 'Fiona', age: 320},
  {name: 'Mike', age: 239}
]

naysayers.filter(function(naysayer){
  return naysayer.age === 320;
})
```

Much nice than...

```js
var age320 = [];

for(var i =0; i < naysayers.length; i++) {
  if(naysayers[i].age === 320) {
    age320.push(naysayers[i])
  }
}
```

## Break (15 minutes)

### You do: Teach Back (90 Minutes)

You will be working in pairs. For each of these higher-order functions:

1. Create an "explain it to me like i'm 5" explanation
1. Create a codepen / jsfiddle demoing how it works
1. Come up with a way to remember what it is and what it does

1. [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
1. [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
1. [sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
1. [find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
1. [every](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
1. [some](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)

After one hour, pairs will be called at random to give a 5-minute presentation on one of the above functions.


## Resources

- [Don't Be Scared of Functional Programming](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/)
- [Eloquent Javascript](http://eloquentjavascript.net/05_higher_order.html)
- [Master the Javascript Interview](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0#.9u4dyrpyc)
- [Functional Programming in Javascript](- [Functional Programming in Javascript](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0#.9u4dyrpyc)
)
