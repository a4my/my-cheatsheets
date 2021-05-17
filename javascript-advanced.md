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


