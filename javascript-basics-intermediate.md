---
title: JavaScript Basics and Intermediate
category: JavaScript
updated: 2021-05-03
intro: |
  A quick overview of new JavaScript features in ES2015, ES2016, ES2017, ES2018 and beyond.
---

# BASICS

## Functions

```js
function fn() {
  console.log("This is a function");
}

fn(); //This is called calling, running, executing or invoking a function
```

## Functions declarations VS Expressions

• Function declaration:

```js
function calcAge1(birthyear) {
  return 2021 - birthyear;
}

const age1 = calcAge1(1986);
```

• Function expression (or anonymous function):

```js
const calcAge2 = function (birthyear) {
  return 2021 - birthyear;
};

const age2 = calcAge2(1986);
```

You can call a function declaration before you declare it but you can't call a function expression before declaring it.

• Arrow functions:

```js
const calcAge3 = (birthyear) => 2021 - birthyear;

const age3 = calcAge3(1986);
```

## Template literals (backticks)

```js
function fruitProcessor(apples, oranges) {
  const juice = `Juice with ${apples} apples and ${oranges} oranges`;
  console.log(juice);
}

fruitProcessor(5, 0);
```

Template literals are string literals allowing embedded expressions

## Arrays

2 ways to create arrays:

```js
const friends = ["Mike", "Steven", "John"];

OR;

const friends = new Array("Mike", "Steven", "John");
```

```js
console.log(friends[1]); // will return Steven
console.log(friends.length); // will return 3
console.log(friends.length - 1); // will return John
friends[2] = "Jay";
console.log(friends); // will return 'Mike', 'Steven', 'Jay'

friends = ["Bob", "Alice"]; // will NOT replace the first array and will throw an error

const years = [1990, 1967, 2000, 2007, 2015];
calcAge(years); // will NOT work and will throw an error
// BUT
calcAge(years[1]); // will work
```

## Array Methods

ADD ELEMENTS

• PUSH

```js
friends.push("Jay");
console.log(friends); // will return 'Mike', 'Steven', 'John', 'Jay'
```

• UNSHIFT

```js
friends.unshift("Peter");
console.log(friends); // will return 'Peter', 'Mike', 'Steven', 'John', 'Jay'
```

REMOVE ELEMENTS

• POP

```js
friends.pop();
console.log(friends); // will return 'Peter', 'Mike', 'Steven', 'John'
```

• SHIFT

```js
friends.shift();
console.log(friends); // will return 'Mike', 'Steven', 'John',
```

EXTRA METHODS

```js
friends.indexOf("Steven");
console.log(friends); // will return 1

console.log(friends.includes("Bob")); // will return False
console.log(friends.includes("Mike")); // will return True
```

## Random numbers

```js
Math.random(); // will create a random DECIMAL number between 0 and 1
Math.trunc(); // will remove the decimals
```

Example with a dice:

```js
let dice = Math.trunc(Math.random() * 6) + 1;
console.log(dice);
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
  firstName: "John",
  lastName: "Doe",
  birthYear: 1986,
  calcAge: function () {
    this.age = 2021 - this.birthYear;
    return this.age;
  },
};
```

# LOOPS

## For Loop

Instead of doing this:

```js
console.log("Lifting weights repetition 1");
console.log("Lifting weights repetition 2");
console.log("Lifting weights repetition 3");
console.log("Lifting weights repetition 4");
console.log("Lifting weights repetition 5");
console.log("etc...");
```

A for loop will keep your code 'DRY'

```js
for (let rep = 1; rep <= 10; rep++) {
  console.log(`Liftin weights repetition ${rep}`);
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
  "Jonas",
  "Schmedtmann",
  2021 - 1986,
  "teacher",
  ["Michael", "John", "Mikey"],
];

for (let i = jonas.length - 1; i >= 0; i--) {
  console.log(jonas[i]);
}
```

## Looping inside a loop

```js
for (let exercise = 1; exercise < 4; exercise++) {
  console.log(`----Starting exercise ${exercise}`);

  for (let rep = 1; rep < 6; rep++) {
    console.log(`Exercise: ${exercise}: Lifting weight repetition ${rep}`);
  }
}
```

outcome:
----Starting exercise 1
Exercise 1: Lifting weight repetition 1
Exercise 1: Lifting weight repetition 2
Exercise 1: Lifting weight repetition 3
Exercise 1: Lifting weight repetition 4
Exercise 1: Lifting weight repetition 5
----Starting exercise 2
Exercise 1: Lifting weight repetition 1
Exercise 1: Lifting weight repetition 2
Exercise 1: Lifting weight repetition 3
Exercise 1: Lifting weight repetition 4
Exercise 1: Lifting weight repetition 5
----Starting exercise 3
Exercise 1: Lifting weight repetition 1
Exercise 1: Lifting weight repetition 2
Exercise 1: Lifting weight repetition 3
Exercise 1: Lifting weight repetition 4
Exercise 1: Lifting weight repetition 5

## While Loop

```js
let rep = 1;
while (rep <= 10) {
  console.log(`Lifting wheight repetition ${rep}`);
  rep++;
}
```

# INTERMEDIATE

## Destructuring Arrays

• Instead of:

```js
const arr = [2, 3, 4];
const a = arr[0];
const b = arr[1];
const c = arr[2];
```

• do this:

```js
const [x, y, z] = arr;
```

• Example:

```js
const resto = {
  name: "Classico",
  location: "Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian"],
};

const [first, second] = resto.categories;
console.log(first, second); // will return 'Italian' and 'Pizzeria'
```

❗ leave a space between 2 comas to skip an index of the array

```js
const [first, , second] = resto.categories;
console.log(first, second); // will return 'Italian' and 'Vegetarian'
```

• Nested destructuring:

```js
const nested = [2, 4, [5, 6]];
const [i, , [j, k]] = nested;
console.log(i, j, k); // will return 2, 5 and 6
```

• Default values:

```js
const [p = 1, q = 1, r = 1] = [8, 9];
console.log(p, q, r); // will return 8, 9 and 1
```

## Destructuring Objects

```js
const resto = {
  name: "Classico",
  location: "Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian"],
  openingHours: {
    thu: {
      open: 12,
      close: 22,
    },
    fri: {
      open: 11,
      close: 23,
    },
    sat: {
      open: 0,
      close: 24,
    },
  },
};
```

```js
const { name, openingHours, categories } = resto;
console.log(name, openingHours, categories); // will return the selected properties of the array resto
```

```js
const { name: restaurantName, openingHours: hours, categories: tags } = resto;
console.log(restaurantName, hours, tags); // will return the selected properties of the array resto and change the name of the propreties by the one listed in the const
```

## The spread operator (...)

Used to expand an array:

```js
const arr = [7, 8, 9]
const newArr = [1, 2, ...arr]
console.log(newArr) // will return 1, 2, 7, 8, 9
```

```js
const newCategories = [...resto.categories, 'Takeaway']
console.log(newCategories) // will return ["Italian", "Pizzeria", "Vegetarian", "Takeaway]
```

Used to join 2 arrays together:

```js
const menu = [...restaurant.starterMenu, ...restaurant.mainMenu]
```

You can also console.log a whole array with the spread operator:

```js
const ingredients = ['mushroom', 'olives', 'cheese']
console.log(...ingredients)
// will return mushroom, olives and cheese
```

## The Rest Pattern

SPREAD, because on RIGHT side of =

```js
const arr = [1, 2, 3, ...[4, 5]]
```

REST, because on LEFT side of =

```js
const [a, b, ...others] = [1, 2, 3, 4, 5]
console.log(a, b, others)
//will return 1, 2 [3, 4, 5]
```

```js
const [pizza, risotto, ...otherFoods] = [
  ...resto.mainMenu,
  ...resto.starterMenu
]
console.log(pizza, risotto, otherFoods)
// will return pizza Risotto ['Focaccia', 'Bruschetta', 'Garlic Bread', 'Salad']
```

❗ REST element must be the last element in the array

• Destructuring an OBJECT with the REST pattern:

```js
const {sat, ...weekdays} = resto.openingHours
console.log(weekdays)
//will return every week day opening hours except Saturday's
```

• In a function, the REST parameters will take multiple parameters and return them in an array:

```js
const add = function(...numbers) {
  console.log(numbers)
}

add(2, 3)
add(5, 3, 7, 2)
add(8, 2, 5, 3, 2, 1, 4)
//will return 3 arrays:
// [2, 3]
// [5, 3, 7, 2]
// [8, 2, 5, 3, 2, 1, 4]
```

```js
const add = function(...numbers) {
  let sum = 0
  for (let i = 0; i <numbers.length; i++) sum += numbers
  console.log(sum)
}

add(2, 3)
add(5, 3, 7, 2)
add(8, 2, 5, 3, 2, 1, 4)
//will return:
// 5
// 17
// 25
```

```js
const x = [23, 5, 7]
add(...x)
// will return 35
```

```js
const resto = {
  name: "Classico",
  location: "Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian"],
  openingHours: {
    thu: {
      open: 12,
      close: 22,
    },
    fri: {
      open: 11,
      close: 23,
    },
    sat: {
      open: 0,
      close: 24,
    },
  },
  orderPizza : function(mainIngredient, ...otherIngredient) {
    console.log(mainIngredient)
    console.log(otherIngredient)
  }
};

restaurant.orderPizza('mushrooms', 'onion', 'olives', 'spinach')
// will return
// mushrooms
// ['onion', 'olives', 'spinach']
```

## Short circuiting (&& and ||)

• || operator will return the first truthy value or the last value if all of them are falsy. Falsy value = 0, null, undefined, and ''.

Use ANY data, return ANY data type, and can short circuit

```js
console.log(3 || 'Alex')
console.log('' || 'Alex')
console.log(true || 0)
console.log(undefined || null)

// 3
// Alex
// true
// null
```

```js
const guests1 = resto.numGests ? resto.numGuest : 10
//will return 10 because resto.numGuest doesn't exist
```

```js
resto.numGuests = 23
const guests1 = resto.numGests ? resto.numGuest : 10
//will return 23 
```
Could also be written this way:

```js
resto.numGuests = 23
const guests2 = resto.numGests || 10
//will return 23 
```

• && returns the first falsy value or the last value if all of them are truthy

```js
console.log(0 || 'Alex')
console.log(7 || 'Alex')
// 0
// Alex
```

## Nullish coalescing operator (??)

Null and undefined not 0 or '':

```js
resto.numGuests = 0
const guests2 = resto.numGests ?? 10
//will return 0 because the value is not null or undefined
```