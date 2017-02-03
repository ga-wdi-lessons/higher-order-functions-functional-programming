# Higher-Order Functions

#### Please Clone this Repository Locally

## Learning Objectives

- Identify the benefits of pure functions and avoiding side effects
- Define immutability and how it relates to pure functions
- Explain what recursion is and why we use it
- Explain the concepts of first class and higher order functions
- Use `filter`, `map`, `reduce`, `sort`

## Framing

Programming at it's most basic level is the process developers undergo to instruct a computer to perform a task. But there are a number of programmatic approaches that can be taken to enable your computer to solve a specific problem. We call these approaches **programming paradigms.**

So far in WDI, we've largely relied on the *procedural programming* paradigm, which is the notion of writing a series of step-by-step instructions for your computer to carry out. For example, we wrote out every `console.log()` or `alert()` message we wanted to appear based on what our user would input as a response in "Choose You Own Adventure".

Most recently, we dipped our toes into the **object-oriented programming** paradigm. This design pattern allows us to considerably DRY up our code to achieve *abstraction*, *encapsulation* and *modularity*.

Let's look at another programming paradigm, __functional programming__.

Functional programming is characterized by **pure functions**, which avoid *changing state*, *mutable data* and *side-effects.*

## Let's Break it Down...

>In mathematics, a function is a relation between a set of inputs and a set of permissible outputs with the property that each input is related to exactly one output.

<https://en.wikipedia.org/wiki/Function_(mathematics)>

When we say __pure__ we mean a function, given the same inputs, will always return the same output.

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

We can make this function pure by not changing anything outside the function:

```js
var age = 27
function increaseAgeBy(age,int){
  return age += int
}
increaseAgeBy(2)
// how can we demonstrate the purity here?
```

### You do: Purify the function

[Purify the Function](./01-purify-the-function.html)

### Immutability

In the above example, `collection` is a __mutable__ data structure. `Mutable`
objects are objects whose state can be modified after creation.

When working with pure functions, it is important to avoid changing (or mutating)
objects outside of the function.

## Higher Order && First Class Functions

JavaScript supports both!

When we say JS supports first-class functions, we mean that they
are treated as values. They can be assigned to a variable.

Higher Order functions are functions that can take functions as arguments and/or
return a function as output.

<details>
  <summary>Anyone remember where we've seen one?</summary>
  <p>`.on('click')`</p>
</details>

You may have also seen with `forEach`:

```js
["a","b","c"].forEach((element, index) => {
  console.log(`element ${element} is in position ${index}`)
})
```

## Examples of functions that take functions as arguments:

### Sort

The [`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) method in JS takes a callback argument, specifying how to order the elements:

```js
var people = [
  {name: 'Jamie', age: 32},
  {name: 'Jessica', age: 22},
  {name: 'Jocelyn', age: 23}
]
people.sort((person1, person2) => {
  return person1.age - person2.age
})
```

### You do: Teach Back

Break up into groups of three:

1. [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
1. [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
1. [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
1. [find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
1. [every](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
1. [some](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)

Once in your groups...

1. Create an explain it to me like i'm 5 explanation
1. Create a codepen / jsfiddle demoing how it works
1. Come up with a way to remember what it is and what it does

## Recursion

<http://lmgtfy.com/?q=recursion>

Recursion is when a function calls itself.

Here's an infinite example:

__Running this code in a browser will freeze your page__

```js
function loop(){
  loop()
}
loop()
```

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

### You do: Factorial

<https://en.wikipedia.org/wiki/Factorial>

[Factorial](./02-factorial.html)

### Loops can be replaced with recursion

Let's count:

```js
function countUpTo(n, current = 0){
  console.log(current)
  if(current === n) return
  countUpTo(n,++current)
}

countUpTo(10)
```


### You do: count down

[Count Down From](./03-count-down-from.html)

## Addendum w/r/t the DOM

Functional principles can be applied to the DOM as well.

Instead of creating objects with `render` methods, you have many functions
responsible for generating small amounts of html.

Here's a sample nav menu:

```js
document.body.appendChild(ul(
  li(a('Home','/')),
  li(a('About','/about')),
  li(a('Contact Us','/contact'))
))

function ul(...children){
  console.log(children)
  var el = document.createElement('ul')
  for(var i = 0; i < children.length; i++){
    el.appendChild(children[i])
  }
  return el
}
function li(child){
  var el = document.createElement('li')
  el.appendChild(child)
  return el
}
function a(text,href){
  var anchor = document.createElement("a")
  anchor.innerHTML = text
  anchor.href = href
  return anchor
}
```
