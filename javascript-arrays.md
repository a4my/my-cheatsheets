---
title: JavaScript Arrays 
category: JavaScript
updated: 2021-06-05
intro: |
  Workings with arrays / Array methods
---

# Working with arrays

### slice() method:

```js
let arr = ['a', 'b', 'c', 'd', 'e']

console.log(arr.slice(2)) // ['c', 'd', 'e']
console.log(arr.slice(2, 4)) // ['c', 'd']
console.log(arr.slice(-2)) // ['d', 'e']
console.log(arr.slice(-1)) // ['e']
console.log(arr.slice(1, -2)) // ['b', 'c']
console.log(arr.slice()) // ['a', 'b', 'c', 'd', 'e']
console.log(arr.slice(...arr)) // ['a', 'b', 'c', 'd', 'e']
```

❗ The end parameter is not included in the output

### splice() method:

❗ Mutates the original array as opposed to the slice method

```js
console.log(arr.splice(2)) // ['c', 'd', 'e']
console.log(arr) // ['a', 'b']

console.log(arr.splice(1,2)) // ['c', 'd']
console.log(arr) // ['a', 'd']
```

### reverse() method
❗ Mutates the original array as opposed to the slice method

```js
const arr2 = ['j', 'i', 'h', 'g', 'f']
console.log(arr2.reverse()) // ['f', 'g', 'h', 'i', 'j']
console.log(arr2) // ['f', 'g', 'h', 'i', 'j']
```

### concat() method

```js
const letters = arr.concat(arr2)
console.log(letters) // ['a', 'b', 'c', 'd', 'e','f', 'g', 'h', 'i', 'j']
console.log(...arr, ...arr2) // ['a', 'b', 'c', 'd', 'e','f', 'g', 'h', 'i', 'j']
```

### join() method

```js
console.log(letters.join(' - ')) // a - b - c - d - e - f - g - h - i - j
```

### forEach(function(current Element, current Index, entire Array)) method

Instead of:

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300];

for (const [i, mov] of movements.entries) {
  if (mov < 0) {
    console.log(`Movement ${i + 1}: You deposited ${mov}`)
  } else {
    console.log(`Movement ${i + 1}: You withdrew ${Math.abs(mov)}`)
  }
}
```

Use forEach() :

```js
movements.forEach(function(mov, i, arr) {
  if (mov < 0) {
    console.log(`Movement ${i + 1}: You deposited ${mov}`)
  } else {
    console.log(`Movement ${i + 1}: You withdrew ${Math.abs(mov)}`)
  }
})
```

### forEach() on maps

```js
const currencies = new Map([
  ['USD', 'United States dollar'],
  ['EUR', 'Euro'],
  ['GBP', 'Pound sterling'],
]);

currencies.forEach(function(value, key, map)) {
  console.log(`${key}: ${value}`)
}
```

### forEach() on sets

```js
const currenciesUnique = new Set(['USD','GBP','USD', 'EUR', 'EUR']);

console.log(currenciesUnique)
currenciesUnique.forEach(function(value, _, map)) {
  console.log(`${value}: ${value}`)
}
```


## Data Transformations: Map, Filter and Reduce

Map returns a new array containing the results of applying an operation on an original array elements.

Filter returns a new array containing the array elements that have passed a specified test condition.

Reduce boils all array elements down to one single value (eg adding all elements together)

### The Map() method

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1700]

const euroToUSD = 1.1

const movementsToUSD = movements.map(function(mov) {
  return move * euroToUSD
})

console.log(movementsToUSD) // [220, 495, -440, 3300, -715, -143, 77, 1430]
```

➕ you can also use arrow function to replace the function above 

```js
const movementsToUSD = movements.map(mov => mov * euroToUSD)
```

### The filter() method

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1700]

const deposits = movements.filter(function(mov, i, arr) {
  return mov > 0
})

console.log(deposits) // [200, 450, 3000, 70, 1700]
```

### The reduce() method

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1700]

const balance = movements.reduce(function(acc, cur, i, arr) {
  return acc + cur
}, 0)

// acc = sum
// in this example the sum is set to 0 and will add the movements to the sum

console.log(balance) // 3840
```

### Chaining methods (Map, Filter and Reduce)

Example:

```js
const eurToUsd = 1.1
const totalDepositUSD = movements
  .filter(mov => mov > 0 )
  .map(mov => mov * eurToUsd)
  .reduce((acc, mov) => acc + mov, 0)

  console.log(totalDepositUSD) // will return the sum of the movements array in USD and with values that greater than 0
```

❕ Do not chain method like splice or reverse 
❗ Do not overuse chaining as it slow down performances (large scales applications)


### The find() method

This method loops through an array and returns the first value that satisfies the condition

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1700]

const firstWithdrawal = movements.find(mov => mov < 0) 

console.log(firstWithdrawal) // will return -400
```

Other example:

```js
const account = accounts.find(acc => acc === 'Jessica Davis') 

console.log(account) // will return the object of Jessica Davis
```

### The some() method

Checks a condition and return a boolean

```js
 const movements = [200, 450, -400, 3000, -650, -130, 70, 1700]

 const anyDeposits = movements.some(mov => mov > 0)
 // will return true

 const anyDeposits = movements.some(mov => mov > 5000)
// will return false
```

### The every() method

Returns true if every elements satisfy the condition

```js
 console.log(movements.every(mov => mov > 0))
 // will return false
```


### The flat() method

❗ 2020 method, will not work with super old browser

```js
 const arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
 console.log(arr.flat())
 // will return [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```js
 const arrDeep = [[[1, 2], 3], [4, [5, 6]], 7, 8]
 console.log(arr.flat(1))
 // will return [Array(2), 3, 4, [Array(2), 7, 8]

 console.log(arr.flat(2))
 // will return [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### The flatMap() method

❗ 2020 method, will not work with super old browser

• Instead of chaining methods like this:

```js
 const overalBalance = accounts
  .map(acc => acc.movements)
  .flat()
  .reduce((acc, mov) => acc + mov, 0)
 console.log(overalBalance)
```

• Do this:

```js
const overalBalance = accounts
  .flatMap(acc => acc.movements)
  .reduce((acc, mov) => acc + mov, 0)
 console.log(overalBalance)
```

❕ flatMap() only goes 1 level deep, use map().flat() if you need to go deeper


### The sort() method

❗ mutates the original array

• on strings:

```js
 const owners = ['Jonas','Zach', 'Adam', 'Martha']
 console.log(owners.sort())
 // will return ['Adam', 'Jonas', 'Martha', 'Zach']
 console.log(owners)
 // will return ['Adam', 'Jonas', 'Martha', 'Zach']
```

• on numbers:

```js
 const movements = [200, 450, -400, 3000, -650, -130, 70, 1700]
 // ASCENDING ORDER
 movements.sort((a, b) => {
   if(a > b) return 1
   if(a < b) return -1
 })
 console.log(movements)
 // will return [-650, -400, -130, 70, 200, 450, 1700, 3000]

 // DESCENDING ORDER
 movements.sort((a, b) => {
   if(a > b) return -1
   if(a < b) return 1
 })c
 console.log(movements)
 // will return [3000, 1700, 450, 200, 70, -130, -400,-650]
```

Tips:

```js
movements.sort((a, b) => {
   if(a > b) return 1
   if(a < b) return -1
 })
 ```

 can also be written this way

 ```js
movements.sort((a, b) => a - b)
 ```

 and 

```js
movements.sort((a, b) => {
   if(a > b) return -1
   if(a < b) return 1
 })
 ```

 can also be written this way

 ```js
movements.sort((a, b) => b - a)
 ```


### The fill() method

This method is used to fill in arrays

```js
console.log([1, 2, 3, 4, 5, 6, 7])
console.log(new Array(1, 2, 3, 4, 5, 6, 7))

const x = new Array(7)
console.log(x)
// will return (7) [1, 2, 3, 4, 5, 6, 7]
// will return (7) [1, 2, 3, 4, 5, 6, 7]
// will return (7) [empty x7]

x.fill(1)
// will return (7) [1, 1, 1, 1, 1, 1, 1]
```

❗ This methods mutates the original array

🔹 The fill() method also has parameters: fill(value, begin, end)

```js
x.fill(1, 3)
// will return (7) [empty x3 1, 1, 1, 1]
```

```js
x.fill(1, 3, 5)
// will return (7) [empty x3 1, 1, empty x2]
```

```js
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
arr.fill(23, 4, 6)
// will return [1, 2, 3, 4, 23, 23, 7]
```

### The Array.from() method

This method is used on the array constructor and not directly on the array

```js
const y = Array.from({length: 7}, () => 1)
console.log(y)
// will return (7) [1, 1, 1, 1, 1, 1, 1]
```

```js
const z = Array.from({length: 7}, (_, i) => i + 1)
console.log(z)
// will return (7) [1, 2, 3, 4, 5, 6, 7]
```



