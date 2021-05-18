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

## Sets

• A set is a collection of unique values

```js
const orderSet = new Set([
  'Pasta',
  'Pizza',
  'Pizza',
  'Risotto',
  'Pasta',
  'Pizza',
  ])

  console.log(orderSet)
  //will return Set(3) {'Pasta', 'Pizza', 'Risotto'}
```

❗ Sets are not arrays

• Sets can also pass in strings

```js
console.log(new Set('Alex'))
// will return Set(4) {'A','l','e','x'}
```

some properties for sets:

```js
console.log(orderSet.size)
// will return 3
```

```js
console.log(orderSet.has('pizza'))
// will return true
```

```js
orderSet.add('Garlic bread'))
orderSet.add('Garlic bread'))
console.log(orderSet)
// will return Set(4) {'Pasta', 'Pizza', 'Risotto', 'Garlic Bread'}
```

```js
orderSet.delete('Risotto'))
console.log(orderSet)
// will return Set(3) {'Pasta', 'Pizza', 'Garlic Bread'}
```

```js
orderSet.clear
console.log(orderSet)
// will return Set(0)
```

❗ Sets have no indexes

🎉 Looping through a set is possible though

```js
for (const order of orderSet) console.log(order)
//will return
// Pasta
// Pizza
// Garlic bread
```

• Conversion from an array to a set:

```js
const staff = ['Waiter','Chef','Waiter','Chef','Manager','Waiter']
const staffUnique = new Set(staff)
console.log(staffUnique)
//will return Set(3) {'Waiter','Chef','Manager'}
```

• Conversion from a set to an array:

```js
const staffUnique = [...new Set(staff)]
console.log(staffUnique)
//will return (3) ['Waiter','Chef','Manager']
```

• get the number of unique values

```js
console.log(new Set(['Waiter','Chef','Waiter','Chef','Manager','Waiter']).size)
//will return 3
```

```js
console.log(new Set('alexfourmy').size)
//will return 10
```


## Maps

• A map is a data structure that we can use to map values to keys. In maps, the keys can have any types

```js
const rest = new Map() // creates a map
rest.set('name','Classico Italiano',) // .set fills up the map by creating a key argument
rest.set(1,'Firenze, Italy',)
console.log(rest.set(2,'Lisbon, Portugal',))

// will return Map(3) {"name" => "Classico Italiano", 1 => "Firenze; Italy", 2 => "Lisbon, Portugal"}
```

```js
rest
  .set('categories', ['Italian', 'Pizzeria', 'Vegetarian', 'Organic'])
  .set('open', 11)
  .set('close', 23)
  .set(true, 'We are open :D')
  .set(false, 'We are close :(')

console.log(rest.get('name'))
console.log(rest.get(true)))
// will return 
// Classico Italiano
// We are open :D
```