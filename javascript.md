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

## Template literals (backticks)

```js
function fruitProcessor(apples, oranges) {
  const juice = `Juice with ${apples} apples and ${oranges} oranges`
  console.log(juice)
}

fruitProcessor(5, 0)
```
Template literals are string literals allowing embedded expressions
