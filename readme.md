# Functional Programming

#### Please Clone this Repository Locally

## Learning Objectives

- Identify the benefits of pure functions and avoiding side effects
- Define immutability and how it relates to pure functions
- Explain what recursion is and why we use it
- Explain the concepts of first class and higher order functions
- Use `filter`, `map`, `reduce`, `sort`

## Framing

### Why functional programming? Why now?

We started with __imperative__ programming: `First do this and then do that`

Imperative programming reminds me of Christmas Lights. One goes out and the whole
thing's broken. How do you know which one is the culprit? How is this related to imperative
programming?

Then we moved on to __object oriented__ programming. This made it easier to:

- abstract
  - hide the complexity
- encapsulate
  - privatizing the complexity
- inherit
  - sharing the complexity

Object oriented programming reminds me of an LCD display. If one pixel goes out,
no problem. It doesn't affect the rest of the system. It's easy to identify where
something's broken.

>The problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle. — Joe Armstrong

>I’ll never forget that day when I was ready to cash in on the promise of Reuse by inheriting from an existing class. This was the moment I had been waiting for.
A new project came along and I thought back to that Class that I was so fond of in my last project.
No problem. Reuse to the rescue. All I gotta do is simply grab that Class from the other project and use it.
Well… actually… not just that Class. We’re gonna need the parent Class. But… But that’s it.
Ugh… Wait… Looks like we gonna also need the parent’s parent too... And then… We’re going to need ALL of the parents. Okay… Okay… I handle this. No problem.
And great. Now it won’t compile. Why?? Oh, I see… This object contains this other object. So I’m gonna need that too. No problem.
Wait… I don’t just need that object. I need the object’s parent and its parent’s parent and so on and so on with every contained object and ALL the parents of what those contain along with their parent’s, parent’s, parent’s…

- https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53#.rmqoman2q

Let's look at another programming paradigm, __functional programming__.

Functional programming is characterized by:

- Pure functions without side effects
- Avoiding changing state and mutable data

## Pure Functions (stateless)

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

01-purify-the-function.html

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

02-factorial.html

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

03-count-down-from.html

### You do: FizzBuzz without loops!

Bonus: Complete this exercise without loops or conditionals.

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
