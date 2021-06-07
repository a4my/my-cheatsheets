---
title: JavaScript Numbers and Dates 
category: JavaScript
updated: 2021-06-05
intro: |
  A closer look to Numbers, Dates, Intl and Timers
---

# Working with Numbers

## Conversion

• Use Number() to convert a string of numbers to a number

```js
console.log(Number('23')) // 23
```

🤫 adding the + sign can also convert a string to number:

```js
console.log(+'23') // 23
```

## Parsing

### parseInt()

```js
console.log(Number.parseInt('30px')) // 30
```

❗ The string needs to start with a number, 'e23' won't work with parseInt()


### parseFloat()

```js
console.log(Number.parseInt('2.5rem')) // 2
console.log(Number.parseFloat('2.5rem')) // 2.5
```


### isNAN()

```js
console.log(Number.isNAN(20)) // false
console.log(Number.isNAN('20')) // false
console.log(Number.isNAN(+'20X')) // true
```

### isFinite() checks if the value is a real number

```js
console.log(Number.isFinite(20)) // true
console.log(Number.isFinite('20')) // false
console.log(Number.isFinite(+'20X')) // false
```

### isInteger() 

```js
console.log(Number.isInteger(20)) // true
console.log(Number.isInteger('20')) // true
console.log(Number.isInteger(+'20X')) // false
```

## The Math() methods

### sqrt()

```js
console.log(Math.sqrt(25)) // 5
```

### max() and min()

```js
console.log(Math.max(5, 18 , 23, 11 , 2)) // 23
console.log(Math.max(5, 18 , '23', 11 , 2)) // 23
console.log(Math.max(5, 18 , '23px', 11 , 2)) // NaN


console.log(Math.min(5, 18 , 23, 11 , 2)) // 2
console.log(Math.max(5, 18 , '23', 11 , 2)) // 2
```

### PI() 

calculates the area of a circle with a radius (ie 10px)

```js
console.log(Math.PI * Number.parseFloat('10px') ** 2 // 314.159etc
```

### random() 

returns a random decimal number between 0 and 1

```js
console.log(Number.random() * 6) // ie a random throw of dice
```

❗ This will return a DECIMAL number between 0 and 5


### trunc() 

removes the decimals from a number

```js
console.log(Math.trunc(Number.random() * 6)) // ie a random throw of dice
```

❕ Will now return a random number between 0 and 5 with no decimals
❗ Still returns a number between 0 and 5 and not between 0 and 6

```js
console.log(Math.trunc(Number.random() * 6) +1 ) // 
```

Adding + 1 fixes the issue and now we will get a random number between 0 and 6 with no decimals


### Rounding integers

```js
console.log(Math.trunc(23.3) // 23
```

other methods:

```js
console.log(Math.round(23.3) // 23
console.log(Math.round(23.9) // 24

console.log(Math.ceil(23.3) // 24
console.log(Math.ceil(23.9) // 24

console.log(Math.floor(23.3) // 23
console.log(Math.floor(23.9) // 23
```

❗ floor() and trunc() do the same thing with positive numbers but not with negative numbers:

```js
console.log(Math.trunc(-23.3) // -23
console.log(Math.floor(-23.3) // -24
```

👍 returning a random number between a min and a max value

```js
const randomInt = (min, max) =>
    Math.floor(Math.random() * (max - min) + 1) + min

console.log(10, 20) // returns a random number between 10 and 20 
```

### Rounding decimals

```js
console.log(2.7).toFixed(0) // 3
console.log(2.7).toFixed(3) // 2.700
console.log(2.345).toFixed(2) // 2.35
console.log(+(2.345)).toFixed(2) // 2.35
```


### The remainder operator

```js
console.log(5 / 2) // 2.5 // 5 = 2 * 2 + 1 // 1 is the remainder
console.log(5 % 2) // 1
console.log(8 % 3) // 2
```

🤫 Checking if a value is an even number or an odd number:

Even numbers can be divided by 2 and the remainder is always 0

```js
console.log(6 / 2) // 3 
console.log(6 % 2) // 0

console.log(7 / 2) // 3.5 
console.log(7 % 2) // 1
```

so we can create a function to check if a number is an even or odd number:

```js
const isEven = n => n 5 % 2 === 0
console.log(8) // true
console.log(23) // false
console.log(514) // true
```

😎 we can use the remainder operator as a condition in a function to higlight lines in a table 

```js
// example with my-bank-app

labelBalance.addEventListener('click', function() {
    [...document.querySelectorAll('.movements__row')].forEach(function(row, i) {
        // 0, 2, 4, 6, ...
        if(i % 2 === 0) row.style.backrgoundColor = 'orangered'
        // 0, 3, 6, 9, ...
        if(i % 3 === 0) row.style.backrgoundColor = 'blue'
    })
})
```

## Working with Big Integers

Biggest number JS can handle is:

```js 
console.log(2 ** 53 - 1) // 9007199254740991
console.log(Number.MAX_SAFE_INTEGER) // 9007199254740991
```

but you can use n to handle bigger numbers:

```js
console.log(4030948745873498204935745985093409) // will return 4.0309487458734
console.log(4030948745873498204935745985093409n) // will return 4030948745873498204935745985093409
```

which means you can perform operations wiht n

```js
console.log(1000n + 1000n) // 2000n
console.log(4030948745873498204935745985093409n * 234903284098234n) //(result)n
```

❗ You cannot mix BigInt and other types:

```js
const huge = 4030948745873498204935745985093409n
const num = 23
console.log(huge * num) // will return an error
```

❕ You will need to convert the other type of number into a BigInt to perform the operation:

```js
console.log(huge * BigInt(num)) // will work
```

❕ comparision will work with < > and == but not with ===:

```js
console.log(23n > 15) // true
console.log(20n === 20) // false
console.log(20n == 20) // true
```

❗❗ Math() operator doesn't work on BigInt


## Working with dates

### Creating dates

```js
const now = new Date()
console.log(now) // will return current date and time

console.log(new Date('Aug 02 2020 18:05:41'))
console.log(new Date('December 24, 2020'))
console.log(new Date(accounts1.movementsDates[0]))

console.log(new Date(2037, 10, 19, 15, 23, 5)) // Thu Nov 19 2037 15:23:05
console.log(new Date(2037, 10, 31)) // Thu Dec 31

console.log(new Date(0)) // Thu Jan 01 1970 01:00:00
console.log(new Date(3 * 24 * 60 * 60 * 1000)) // will return the date 3 days later the line above
```

### Methods with dates

```js
const future = new Date(2037, 10, 19, 15, 23, 5)
console.log(future.getFullYear()) // 2037
console.log(future.getMonth()) // 10
console.log(future.getDate()) // 19
console.log(future.getDay()) // 4 (= THU)
console.log(future.getHours()) // 15 
console.log(future.getMinutes()) // 23
console.log(future.getSeconds()) // 05

console.log(future.toISOString()) // 2037-11-19T15:23:05.000Z
console.log(future.getTime()) // 2142256980000 (milliseconds that have passed since the 1st Jan 1970)

console.log(Date.now()) // will return current time

future.setFullYear(2040) // will set 2040 as a new year 
console.log(future)
```

### Operations with dates

The below will return a number in milliseconds:

```js
const future = new Date(2037, 10, 19, 15, 23, 5)
console.log(future) // 2142256980000
```

Which means we can do operations:

```js
const calcDaysPassed = (date1, date2) => (date2 - date1) / (1000 * 60 * 6 * 24)

const days1 = calcDaysPassed(
    new Date(2037, 3, 4)) 
    new Date(2037, 3, 14))

console.log(days1) // 10
```

