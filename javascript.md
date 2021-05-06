---
title: JavaScript Basics
category: JavaScript
updated: 2021-05-03
intro: |
  A quick overview of new JavaScript features in ES2015, ES2016, ES2017, ES2018 and beyond.
---

# BASICS

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

## Array Methods

ADD ELEMENTS

• PUSH
```js
friends.push('Jay')
console.log(friends) // will return 'Mike', 'Steven', 'John', 'Jay'

```

• UNSHIFT
```js
friends.unshift('Peter')
console.log(friends) // will return 'Peter', 'Mike', 'Steven', 'John', 'Jay'

```

REMOVE ELEMENTS

• POP
```js
friends.pop()
console.log(friends) // will return 'Peter', 'Mike', 'Steven', 'John'

```

• SHIFT
```js
friends.shift()
console.log(friends) // will return 'Mike', 'Steven', 'John', 

```

EXTRA METHODS

```js
friends.indexOf('Steven')
console.log(friends) // will return 1 

console.log(friends.includes('Bob')) // will return False
console.log(friends.includes('Mike')) // will return True
```

## Objects

Example:

```js
const alex = [
  firstname: 'Alex',
  lastName: 'Fourmy',
  age: 2021 - 1986,
  job: 'Web developer',
  friends: ['John', 'Mary', 'Tim'],
  hasDriversLicense: true
]

console.log(alex.lastName) // will only return Fourmy
```

## The this. operator

```js
const john = {
  firstName: 'John',
  lastName: 'Doe',
  birthYear: 1986,
  calcAge: function() {
    this.age = 2021 - this.birthYear
    return this.age
  },
}
```

# LOOPS

## For Loop

Instead of doing this:

```js
console.log('Lifting weights repetition 1')
console.log('Lifting weights repetition 2')
console.log('Lifting weights repetition 3')
console.log('Lifting weights repetition 4')
console.log('Lifting weights repetition 5')
console.log('etc...')
```

A for loop will keep your code 'DRY'

```js
for(let rep = 1; rep <= 10; rep++) {
  console.log(`Liftin weights repetition ${rep}`)
}
```

Other examples:

```js
//ex1
const jonasArray = [
  'Jonas',
  'Schmedtmann',
  2021 -1986,
  'teacher',
  ['Michael', 'John', 'Mikey']
]

for (let i = 0; i < jonasArray.length ; i++) {
  console.log(jonasArray[i], typeOf jonasArray[i])
}

// ex2
const years = [1991, 2007, 1969, 2020]
const ages = []

for(let i = 0; i < years.length; i++) {
  ages.push(2021 - years[i]) // will return an array with ages for all 4 values of the years array
}
```

## Looping backwards

```js
const jonas = [
  'Jonas',
  'Schmedtmann',
  2021 -1986,
  'teacher',
  ['Michael', 'John', 'Mikey']
]

for (let i = jonas.length - 1; i >= 0  ; i--) {
  console.log(jonas[i])
}
```