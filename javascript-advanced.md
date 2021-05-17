---
title: JavaScript Advanced Concept
category: JavaScript
updated: 2021-05-16
intro: |
  Advanced concepts of new JavaScript features in ES2015, ES2016, ES2017, ES2018 and beyond.
---

# Advanced

## For Of Loop


```js
const menu = [...resto.startMenu, ...resto.mainMenu]

for (const item of menu) console.log(item)
// will return all items of menu
```

## Enhanced Object Literals

• New way of writting object properties:
```js
const openingHours = {
  fri: {
    open: 19,
    close: 23,
  },
  sat: {
    open: 18,
    close: 24,
  },
  sun: {
    open: 0,
    close: 24,
  }
}

const restaurant = {
  name: 'Classico',
  location: 'Italy',
  categories: ['Italian', 'Pizzeria', 'Vegetarian'],
  starterMenu : ['Focaccia', 'Bruschetta', 'Garlic Bread'],
  mainMenu : ['Pizza', 'Salad', 'Risotto',],
  openingHours // ES6 enhanced object literals // This will include the const hours into the restaurant object
}
```

• New ways of writting methods:

```js
const restaurant = {
  name: 'Classico',
  location: 'Italy',
  categories: ['Italian', 'Pizzeria', 'Vegetarian'],
  starterMenu : ['Focaccia', 'Bruschetta', 'Garlic Bread'],
  mainMenu : ['Pizza', 'Salad', 'Risotto',],
  hours,
  orderPasta(ing1, ing2, ing3) {
    console.log(`Here is your delicious pasta with ${ing1}, ${ing2} and ${ing3}`)
  }
}
```

Instead of:

```js
const restaurant = {
  name: 'Classico',
  location: 'Italy',
  categories: ['Italian', 'Pizzeria', 'Vegetarian'],
  starterMenu : ['Focaccia', 'Bruschetta', 'Garlic Bread'],
  mainMenu : ['Pizza', 'Salad', 'Risotto',],
  hours,
  orderPasta: function(ing1, ing2, ing3) {
    console.log(`Here is your delicious pasta with ${ing1}, ${ing2} and ${ing3}`)
  }
}
```

## Optional chaining

Using ?.

```js
console.log(restaurant.openingHours.mon?.open)
console.log(restaurant.openingHours?.mon?.open)
```

Only if the property before the ?. exists will then the following property be read

```js
const days = ['mon', 'tue', 'wed', 'thu', 'fri', 'sat', 'sun']

for (const day of days) {
  console.log(day)
  const open = restaurant.openingHours[day]?.open ?? 'closed'
  console.log(`On £${day}, we open at ${open}`)
}
```

On methods:

```js
console.log(restaurant.order?.(0,1) ?? 'Method does not exist')
//will return ["Focaccia", "Pasta"]

console.log(restaurant.orderRisotto?.(0,1) ?? 'Method does not exist')
//will return 'Method does not exist' because is not a method
```

On arrays:

```js
const users = [{name: 'John', email: 'john@email.com'}]

console.log(users[0]?.name ?? 'User array empty')
```

## Looping Objects

On property names:

```js
const properties = Object.keys(openingHours)
let openStr = `We are open on ${properties.length} days:`
for (const day of properties) {
  openStr += `${day}`
}

console.log(openStr) // will return "We are open on 3 days: thu, fri, sat"

```

On property values:

```js
const values = Object.values(openingHours)
console.log(values) //will return the following values in arrays:
// fri: {
//     open: 19,
//     close: 23,
//   },
//   sat: {
//     open: 18,
//     close: 24,
//   },
//   sun: {
//     open: 0,
//     close: 24,
//   }

```

On the entire object:

```js
const entries = Object.entries(openingHours)
for (const[key, {open, close}] of entries) {
  console.log(`On ${key}, we open at ${open} and close at ${close}`)
}
//will return the following:
// On thu, we open at 12 and close at 22
// On fri, we open at 11 and close at 23
// On sat, we open at 0 and close at 24
```