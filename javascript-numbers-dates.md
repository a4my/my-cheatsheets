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