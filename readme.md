# Functional Programming & Higher-Order Functions

## Learning Objectives

- Explain the idea of programming paradigms
- Highlight advantages of functional programming
- Identify the benefits of pure functions
- Define the concepts of state and immutability
- Explain the benefits of higher order functions
- Implement `filter`, `map`, `reduce`, `sort` and other higher order functions

## Framing (5 minutes)

Programming at its most basic level is the process developers undergo to instruct a computer to perform a task. But there are a number of programmatic approaches that can be taken to enable your computer to solve a specific problem. We call these approaches **programming paradigms**.

So far in WDI, we've largely relied on the *procedural programming* paradigm, which is the notion of writing a series of step-by-step instructions for your computer to carry out. For example, we wrote out every `console.log()` or `alert()` message we wanted to appear based on what our user would input as a response in "Choose You Own Adventure".

Most recently, we dipped our toes into the **object-oriented programming** paradigm. This design pattern allows us to considerably DRY up our code to achieve ***abstraction***, ***encapsulation***, and ***modularity***.

Let's look at another programming paradigm...

## Why Functional Programming? (10 minutes)

Functional programming is a [hot and trendy topic](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/) in web development right now, but it's far from being a new concept. LISP, one of the first programming languages ever created -- back in the 1950s -- had already embraced the paradigm, and has its foundations in [Alonzo Church](https://en.wikipedia.org/wiki/Alonzo_Church)'s work in [lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus) in 1930s, which very strongly influenced the development of LISP.

[Ardent fans](https://www.youtube.com/watch?v=BMUiFMZr7vk&t=1s) have lauded functional programming for its emphasis on writing programs that will result in fewer bugs and more reusable code. The paradigm has historically been used with large-scale systems spanning thousands of networked computers, where it's critical that the program do exactly what's expected every time in the interest of performance and integrity. Many shied away from it, however, because "pure" functional languages are challenging to grasp and the paradigm was perceived as too "computer science-y" and academic.

***So why is functional programming seeing a resurgence?***

[Javascript is cool now](http://blog.salsitasoft.com/why-now/) and more developers than ever are writing Javascript. Increasinly the number of javasript developers means that the language has absorbed influences from LISP, Clojure, and functional programming paradigms. Technologies like React and Redux make extensive use of core concepts of functional programming, deriving their power and unique features from functional programming principles.

When [Brendan Eich](http://blog.salsitasoft.com/why-now/) created Javascript for his then-employer Netscape, he was ordered by management to make the language look like Java. He obliged somewhat and gave Javascript some key functional programming features. As the language exploded in popularity, Javascript developers are now taking advantage of these features and extending them with new techniques made available by ES6.

## What is Functional Programming? (15 minutes)

Functional programming is characterized by **pure functions** and **function composition** that avoids:
* shared state
* mutable data
* side-effects

***Huh?***

Trying to understand the terminology associated with functional programming can be incredibly daunting. In the scope of this class, we're not going to go too in the weeds with the concepts, but we'll have initial exposure to them.

**Pure Functions**

Pure functions are a fundamental part of functional programming.

When we say __pure__ we mean a function, *given the same inputs, will always return the same output*. Such a function **does not** rely on or modify the **state** of variables outside it's scope. With object-oriented programming we have stateful objects that encapsulate our data. However, in functional programming, we could encapsulate the same data in functions instead of objects. By avoiding stateful objects, each with an individual state, we could pass this data into functions as arguments.

```js
//object-oriented approach
class Sum {
  constructor(addend, augend) {
    this.value = addend + augend;
  }
}

//functional approach
const sum = (addend, augend) => addend + augend;
```

We don't live in a black-and-white world, and functional programming is well-suited some things, and object-oriented for others. Approaches can be combined, or used to address specific problems.

The execution of a pure function doesn't depend on the state of the system. That is, it avoids **shared state** and **tight coupling** between parts of an application.

Functions written in this way should not need to know about other functions. They should be independent and focused in the sense that each function deals with one task or problem. Functions also work together all the time, and some functions will depend on others. If function A depends on function B, function B should be a part of function A's **composition**. Building larger functions out of smaller functions gives us an approach that allows us to aggressively manage application complexity.

We also **avoid the side-effect** of modifying an external variable. As discussed in [Objects and Functions](https://github.com/ga-wdi-lessons/js-objects-functions), a [side-effect](https://github.com/ga-wdi-lessons/js-objects-functions/blob/master/functions.md#output-and-side-effects) is an observable change in the application other than the return value or [output](https://github.com/ga-wdi-lessons/js-objects-functions/blob/master/functions.md#output-and-side-effects) of a called function.

* What's an example of a side-effect we've commonly seen?

Here's an example of an impure function:

```js
let age = 27;
function increaseAgeBy(int) {
  return age += int;
}
increaseAgeBy(2);
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
let age = 27;

function increaseAgeBy(myAge, int) {
  return myAge += int;
}

increaseAgeBy(age, 2);
```

<details>
  <summary>How can you demonstrate the purity?</summary>
  <pre>console.log(age)</pre>
</details>

### Functional Programming and the DOM

The value of a pure function is evident with views: a Javascript function will construct a view by building parts of a view from some input, and create the *the exact same view from that input every time*. This adds a layer of predictability to how our views are constructed. Don't worry if the value of this isn't immediately obvious, it will be more apparent once we encounter frameworks later on in the course. In fact, modern views-libraries like React incorporate this idea into its core functioning.

In this example however, there are side-effects, mainly the interaction with the DOM. There are times when a functional programmer will be forced to write functions with side effects. Examples also include interactions with servers and databases. We are compromising the purity of these functions since we are introducing side effects, but only out absolute necessity.

In one sense, we have compromised the purity of the functions, but the aim of doing functional programmer developing web applications should be to keep functions as pure as possible and **only involve side effects when absolutely necessary**.

Note also that each function has one, specific purpose. The functions are individually designed to handle one task and do not depend on one another in order to execute. While that is true, these functions are obviously meant to work together and their purposes are linked.  

```js
document.body.appendChild(
  ul(
    li( a('Home','/') ),
    li( a('About','/about') ),
    li( a('Contact Us','/contact') )
  )
)

function ul (children) {
  console.log(children); // side effect: logging to the console
  var el = document.createElement('ul');
  for (var i = 0; i < children.length; i++) {
    el.appendChild(children[i]); // side effect: interaction with the DOM
  }
  return el;
}

function li (child) {
  var el = document.createElement('li');
  el.appendChild(child);
  return el;
}

function a (text, href) {
  var anchor = document.createElement("a");
  anchor.innerHTML = text;
  anchor.href = href;
  return anchor;
}
```

## Immutability & Data Flow

### Data Storage in Memory

Take a moment to enter in the follow code in your browser console:

```js
  let rabbitCount = 9000;
  let rabbitCensus = rabbitCount;
  rabbitCensus += 200;

  console.log(rabbitCount);
  console.log(rabbitCensus);
```

```js
  let cats = ["Meowy Mandel", "Peter Criss", "Lion-O", "Cheetara"];
  let copyCats = cats;

  copyCats.push("Garfield");

  console.log(cats);
  console.log(copyCats);
```

1. What happened here? is `copyCats` an independent copy of `cats`?
2. Why didn't this happen in the first example?
3. What might this suggest about how different types are stored in memory?



```js
  let spartacus = {
    isSpartacus: true
  }

  let noImSpartacus = spartacus;

  spartacus.isSpartacus = false;

  console.log(spartacus);
  console.log(noImSpartacus);
```

We have some intuitive basis now to see why immutability might be important as a concept. **Immutability** is another core concept in functional programming. It's simply the idea of *not changing data*, and instead *copying that data, and then applying a change to the copy of that data*.

This concept may seem like an awkward limitation at first, but think about the concept of an undo history: you want to make sure you have an accurate history of the commands you've entered. If you were coding a feature like an undo history, you'd want to make sure that you had an accurate record of user actions that didn't change in strange or difficult to predict ways.

When writing **pure functions**, it is important to completely avoid changing (or mutating) objects outside of the function, since that mutation would be a side-effect.  This grants you greater certainty about what your code is doing, by ruling out side-effect shenanigans. Ultimately, embracing this limitation of writing as many pure functions as possible grants you the most control over how data flows.

Why does the example below violate this concept of Immutability?

```js
let nayana = {
  name: 'Nayana',
  age: 13
}

instructor.name = "Andy"
```

### Techniques for Dealing with Immutable Data

#### Copying Objects

If we wanted to make this change ***immutably***, we could create a function that would return a **new** and **separate** version of `instructor` without modifying `instructor` directly:

```js
let instructor = {
  name: 'Nayana',
  age: 13
}

function updateName(instructor, newName) {
  let newInstructor = Object.assign({}, instructor);
  newInstructor.name = newName;
  return newInstructor;
}

let newAndy = updateName(instructor, "Andy");
```
> Object.assign() is the simplest way to make a copy of an existing object

This example does not violate immutability because the original object (`instructor`) is not directly mutated. Instead, a copy of that object is created, then mutated, and finally returned. This way, the original object `instructor` is still accessible with its original values.

#### Mutator Methods

A **mutator method** is a method which *changes the thing (an array in this case) it is called upon*.

[Splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

`.splice()` ***is a mutator method***, meaning it modifies whatever it is called on.

[Slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) does not change what it is called upon and instead creates a copy.

`.slice()` ***is not a mutator method***. Use it for ***copying*** all or part of an array!

It's easy to confuse slice and splice since there is a one letter difference; come up with mnemonic device. Here's one: s-**p**-lice **p**-ermanently mutates.


> Other mutator methods include `.reverse()`, `.pop()`, `.push()`, `.shift()`, `.unshift()`, and many others.

## Higher-Order Functions (15 minutes)

These functions are considered to be another key area -- perhaps the most important -- in the functional programming paradigm.

In functional programming languages, functions are values. That is, they can be stored in variables, or passed into other functions.

Higher-order functions increase the number of ways that we can easily use smaller functions. Higher-order functions take functions as arguments and/or return a function as output. They are often useful in composing larger functions out of smaller functions, since a higher-order function can expand the number of ways a small function is used. For example, it could take a function and use it to apply a transformation to a set.


### .forEach

We briefly saw an example with `forEach` in earlier lesson, but let's revisit this in greater detail.

```js
let fruits = ["apples", "bananas", "cherries"];

fruits.forEach( (currentFruit) => {
  console.log("Every day I eat two " + currentFruit);
});

// vs

for (let i = 0; i < fruits.length; i++) {
  console.log("Every day I eat two " + fruits[i]);
}
```

<details>
  <summary> Anyone remember another method that takes a function as an argument we've used quite frequently? </summary>
  <p>`.on('click')`</p>
</details>

### .map

```js
let values = [1, 2, 3, 4, 5];

function double(number){
  return number * 2;
}

let doubledValues = values.map( value => double(value) );
```

#### Copying arrays of objects

For arrays of objects, you can use `map()` in concert with `Object.assign()`

> Example:
```js
let todos = [
  { todo: "learn functional programming" },
  { todo: "learn about currying and partial-application" },
  { todo: "learn about thunks" },
  { todo: "prevent head from exploding" }
]
let todosCopy = todos.map(obj => Object.assign({},obj))
```

## Break (15 minutes)

## You do: Teach Back (45 Minutes)

You will be working in groups of three. For each of these higher-order functions:

- Create an ELI5 (Explain it to me Like I'm 5) explanation
- Create a codepen / jsfiddle demoing how it works
- Come up with a way to remember what it is and what it does

1. [sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
2. [find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
3. [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
4. [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

After one hour, pairs will be called at random to give a 5-minute presentation on one of the above functions.

## Recursion


A recursive function is a function which calls itself. Recursion happens when a function calls itself within its own scope. It is a more advanced, functional way to iterate over data or to repeat an operation an arbitrary number of times (as opposed to utilizing a loop or higher-order function). In certain circumstances, it can be much more *perfomant* or faster, meaning it requires fewer computational resource.

### Examples of Recursion

#### Infinite Recurison

___Running this code in a browser will freeze your page___

> In Chrome, access the task manager from the menu var at the top of your screen Window > Task Manager and End the Task on the appropriate tab. If you've done this correctly, the tab where the endless loop is occuring should 'break' and say "Ah Snap! Something went wrong."

```js
function loop(){
  loop()
}
loop()
```

### Fibonacci Sequence

The Fibonacci sequence is a classic example of recursion.

The fibonacci numbers of `n` are the fibonacci numbers of `n - 1` + the
fibonacci numbers of `n - 2`,
where the fibonacci numbers of `1` and `2` are both 1.

```
3: 1 + 1  = 2
4: 1 + 2  = 3
5: 2 + 3  = 5
6: 3 + 5  = 8
7: 5 + 8  = 13
```

```js
function fib(n){
  if(n === 1 || n === 2){
    return 1
  }
  return fib(n-1) + fib(n-2)
}
```

<!-- TODO: Consider adding back in factorial you-do activity from: https://github.com/ga-wdi-lessons/functional-programming/tree/1bc9b3ee3b88b0239ca70ef7fd4f516247da05bc/ -->


### Replacing Loops with Recursion

Let's count:

```js
function countUpTo(n, current = 0){
  console.log(current)
  if(current === n) return
  countUpTo(n,++current)
}

countUpTo(10)
```

<!-- TODO: Consider adding back in count down you-do activity from: https://github.com/ga-wdi-lessons/functional-programming/tree/1bc9b3ee3b88b0239ca70ef7fd4f516247da05bc/ -->

#### Reverse a String with Recursion

> Here is an example of using recursion to reverse a string...

```js
function reverse (str) {
    if (str.length == 0) {
        return "";
    } else {
        return reverse(str.substr(1)) + str.charAt(0);
    }
}
```

#### Recursive FizzBuzz

You can write a solution to FizzBuzz without loops using recursion

```js
function fizzBuzz(int, current = 1) {
  if(current == int) {
    return
  } else if (current % 3 == 0 && current % 5 == 0) {
    console.log('fizzbuzz')
  } else if (current % 5 == 0) {
    console.log('buzz')
  } else if(current % 3 == 0) {
    console.log('fizz')
  } else {
    console.log(current)
  }
  fizzBuzz(int, current + 1)
}

```
> Note that optional parameters are often used with recursion as they allow us to start a local variable at a certain value without having to set the value of it *within* the function body.


## Closing / Questions

## Resources

- [What is Functional Programming?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0#.9u4dyrpyc)
- [Don't Be Scared of Functional Programming](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/)
- [Eloquent Javascript](http://eloquentjavascript.net/05_higher_order.html)
- [Introducing Reduce: Common Patterns](https://egghead.io/lessons/javascript-introducing-reduce-common-patterns)

## Additional Reading
- [Currying and Partial Application](https://medium.com/javascript-inside/currying-partial-application-f1365d5fad3f)
- [Functional Programming in Javascript](https://stephen-young.me.uk/2013/01/20/functional-programming-with-javascript.html)
