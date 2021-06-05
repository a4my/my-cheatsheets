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

• parseInt()

```js
console.log(Number.parseInt('30px')) // 30
```

❗ The string needs to start with a number, 'e23' won't work with parseInt()


• parseFloat()

```js
console.log(Number.parseInt('2.5rem')) // 2
console.log(Number.parseFloat('2.5rem')) // 2.5
```


• isNAN()

```js
console.log(Number.isNAN(20)) // false
console.log(Number.isNAN('20')) // false
console.log(Number.isNAN(+'20X')) // true
```

• isFinite() checks if the value is a real number

```js
console.log(Number.isFinite(20)) // true
console.log(Number.isFinite('20')) // false
console.log(Number.isFinite(+'20X')) // false
```

• isInteger() 

```js
console.log(Number.isInteger(20)) // true
console.log(Number.isInteger('20')) // true
console.log(Number.isInteger(+'20X')) // false
```

## The Math() methods

• sqrt()

```js
console.log(Math.sqrt(25)) // 5
```

• max() and min()

```js
console.log(Math.max(5, 18 , 23, 11 , 2)) // 23
console.log(Math.max(5, 18 , '23', 11 , 2)) // 23
console.log(Math.max(5, 18 , '23px', 11 , 2)) // NaN


console.log(Math.min(5, 18 , 23, 11 , 2)) // 2
console.log(Math.max(5, 18 , '23', 11 , 2)) // 2
```

• PI() calculates the area of a circle with a radius (ie 10px)

```js
console.log(Math.PI * Number.parseFloat('10px') ** 2 // 314.159etc
```

• random() returns a random decimal number between 0 and 1

```js
console.log(Number.random() * 6) // ie a random throw of dice
```

❗ This will return a DECIMAL number between 0 and 5


• trunc() removes the decimals from a number

```js
console.log(Math.trunc(Number.random() * 6)) // ie a random throw of dice
```

❕ Will now return a random number between 0 and 5 with no decimals
❗ Still returns a number between 0 and 5 and not between 0 and 6

```js
console.log(Math.trunc(Number.random() * 6) +1 ) // 
```

Adding + 1 fixes the issue and now we will get a random number between 0 and 6 with no decimals


👍 returning a random number between a min and a max value

```js
const randomInt = (min, max) =>
    Math.trunc(Math.random() * (max - min) + 1) + min

console.log(10, 20) // returns a random number between 10 and 20 
```