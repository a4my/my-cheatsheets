---
title: JavaScript Basics
category: JavaScript
updated: 2021-05-03
intro: |
  A quick overview of new JavaScript features in ES2015, ES2016, ES2017, ES2018 and beyond.
---

### BASICS

## Functions

```js
function fn () {
  console.log('This is a function')
}

fn() //This is called calling, running, executing or invoking a function
```

## Functions declarations VS Expressions

• Function declaration:

```js
function calcAge1 (birthyear) {
  return 2021 - birthyear
}

const age1 = calcAge1(1986)
```

• Function expression (or anonymous function):

```js
const calcAge2 = function (birthyear) {
  return 2021 - birthyear
}

const age2 = calcAge2(1986)
```
You can call a function declaration before you declare it but you can't call a function expression before declaring it.

• Arrow functions:

```js
const calcAge3 = birthyear => 2021 - birthyear
  
const age3 = calcAge3(1986)
```


## Template literals (backticks)

```js
function fruitProcessor(apples, oranges) {
  const juice = `Juice with ${apples} apples and ${oranges} oranges`
  console.log(juice)
}

fruitProcessor(5, 0)
```
Template literals are string literals allowing embedded expressions


## Arrays

2 ways to create arrays:

```js
const friends = ['Mike', 'Steven', 'John']

OR

const friends = new Array('Mike', 'Steven', 'John')

```

```js
console.log(friends[1]) // will return Steven
console.log(friends.length) // will return 3
console.log(friends.length - 1) // will return John
friends[2] = 'Jay'
console.log(friends) // will return 'Mike', 'Steven', 'Jay'

friends = ['Bob', 'Alice'] // will NOT replace the first array and will throw an error

const years = [1990, 1967, 2000, 2007, 2015]
calcAge(years) // will NOT work and will throw an error
// BUT
calcAge(years[1]) // will work
```