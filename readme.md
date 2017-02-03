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

When [Brendan Eich](http://blog.salsitasoft.com/why-now/) created Javascript for his then-employer Netscape, he was ordered by management to make the language look like Java. He obliged somewhat and gave Javascript some key functional programming features.

### What is Functional Programming? (20 minutes)

Functional programming is characterized by **pure functions** and **function composition** and avoiding:
* shared state
* mutable data
* side-effects

*Huh?*

Trying to understand the terminology associated with functional programming can be incredibly daunting. In the scope of this class, we're not going to go too in the weeds with the concepts, but we'll have initial exposure using fairly simple examples. 

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


## Resources

- [Don't Be Scared of Functional Programming](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/)
