# Functional Programming

## Learning Objectives

- Explain what recursion is and why we use it
- Identify the benefits of pure functions
- Create a function that returns a function using closure.
- Use `filter`, `map`, `reduce`, `sort`
- Explain the concept of a first-class function

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

## Sort

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
