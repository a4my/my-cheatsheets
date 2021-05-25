---
title: JavaScript Functions 
category: JavaScript
updated: 2021-05-23
intro: |
  A closer look at functions.
---

# A closer look at functions

## Default parameters

• The old ES5 way 

```js
const bookings = []

const createBooking = function(flightNum, numPassengers, price) {
  
  //ES5 way of creating default parameters:
  numPassengers = numPassengers || 1
  price = price || 199

  const booking = {
    flightNum,
    numPassengers,
    price
  }

  console.log(booking)
  bookings.push(booking)
}

createBooking('LH123')
```

• The new way:

```js
const bookings = []

const createBooking = function(flightNum, numPassengers = 1, price = 199) {

  const booking = {
    flightNum,
    numPassengers,
    price
  }

  console.log(booking)
  bookings.push(booking)
}

createBooking('LH123')
```

❗ You cannot skip a default parameter unless you declare it undefined:

```js
createBooking('LH123', undefined, 1000)
```

## The call and apply methods

### Using .call() to use a method in another object

```js
const lufthansa = {
  airline: 'Lufthansa',
  iataCode: 'LH',
  bookings: [],
  book(flightNum, name) {
    console.log(
      `${name} booked a seat on ${this.airline} flight ${this.iataCode}${flightNum}`
    )
    this.bookings({flight: `${this.iataCode}${flightNum}`, name})
  }
}

lufthansa.book(239, 'Alex Fourmy')
console.log(lufthansa) // to look at the whole object and see that the bookings array has been updated with the flight details

const eurowings = {
  airline: 'Eurowings',
  iataCode: 'EW',
  booking: [],
}

// ❗ Does NOT work:
// book(23, 'Sarah Williams')

book.call(eurowings, 23, 'Sarah Williams')
console.log(eurowings) // to look at the whole object and see that the bookings array has been updated with the flight details
```

❕ Note that the first parameter of .call() is pointing at the object to call

• book.call() also works on the object where the method is from:

```js
book.call(lufthansa, 945, 'Maggie Smith')
console.log(lufthansa)
```

### Using the .apply() method

❔ Does the same thing as the .call() method but the difference is that it doesn't receive a list of argument after the this.keyword but instead an array  

```js
const flightData = [583, 'George Cooper']
book.apply(swiss, flightData)
console.log(swiss)
```

❗ But you can still use .call() on an array buy using the spread operator:

```js
book.call(swiss, ...flightData)
```

## The bind() method

❔ bind() does not immediately call the function instead it returns a new function where the this.keyword is bound

```js
const bookEW = book.bind(eurowings)
const bookLH = book.bind(lufthansa)
const bookLX = book.bind(swiss)
bookEw(23, 'Steve Williams')
```
Which leads to:

```js
const bookEW23 = book.bind(eurowings, 23)
bookEW23('Alex Smith')
bookEW23('Martin Cooper')
```

### With event listerners

```js
lufthansa.planes = 300
lufthansa.buyPlane = function () {
  console.log(this)
  this.planes++
  console.log(this.planes)
}
document.querySelector('.buy').addEventListener('click', lufthansa.buyPlane).bind(lufthansa)
```

### Partial application (pre-set parameters)

```js
const addTax = (rate, value) => value + value * rate
console.log(addTax(0.1, 200))

const addVAT = addTax.bind(null, 0.23) 
// equals addVAT = value => value + value *0.23

console.log(addVAT(100))
```

## Immediately Invoked Function Expression (IIFE)

• IIFE will only be run once:

```js
(function() {
  console.log('This function will only run once!')
})()
```

❗ Note that the function needs to be wrapped in parentheses
❗❗ Note that the function needs to be called too ()

• IIFE arrow function:

```js
(()=> console.log('This function will ALSO only run once!')
)()
```