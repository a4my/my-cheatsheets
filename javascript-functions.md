---
title: JavaScript Functions 
category: JavaScript
updated: 2021-05-21
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