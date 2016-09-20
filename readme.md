# Functional Programming

## Learning Objectives

- Identify the benefits of pure functions
- Create a function that returns a function using closure.
- Explain what recursion is and why we use it
- Explain the concept of a first-class function
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
// how can we demonstrate the impurity here?
```

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

Given an impure function:

```js
function reverse(collection){
  var reversed = collection.reverse()
  return reversed
}

var nums = [1,2,3]
console.log("before", nums)
reverse(nums)
console.log("after", nums)
```

Modify `reverse` so that the original `nums` remains in the correct order.

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

The `sort` method in JS takes a callback argument, specifying how to order the elements:

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

1. map
1. reduce
1. filter
1. find
1. every
1. some

Once in your groups...

1. Create an explain it to me like i'm 5 explanation
1. Create a codpen / jsfiddle demoing how it works
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

Define a function `factorial` that takes one argument `n`.

This function multiplies `n` by `n - 1` and repeates that process
down to 1.

<https://en.wikipedia.org/wiki/Factorial>

### Loops can be replaced with recursion

Let's count:

```js
function countDownFrom(n){
  console.log(n)
  if(n === 0)
    return
  countDownFrom( --n )
}
countDownFrom(10)
```

### You do: count up

```js
function countUpTo(n){
  // ???
}
countUpTo(10)
```

### You do: FizzBuzz without loops!

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
