---
title: JavaScript Modules
category: JavaScript
updated: 2021-06-28
intro: |
  A closer look to Modules / Tooling / Functional Principles/ 
---

# Modules

Reusable piece of code that encapsulates implementatio details.

## Importing modules

```js
    ///////////
    //script.js
    import {addToCart, totalPrice, totalQuantity} from './shoppingCart.js'
    console.log('importing module')

    addToCart('bread', 5)
    console.log(totalPrice, totalQuantity)

    /////////////////
    //shoppingCart.js
    const shippingCost = 10
    const cart = []

    export const addToCart = function(product, quantity) {
        cart.push({product, quantity})
        console.log(`${quantity} ${product} added to cart`)
    }

    const totalPrice = 237
    const totalQuantity = 23

    export {totalPrice, totalQuantity}
```

Imports can also be written like this:

```js
    ///////////
    //script.js
    import {addToCart, totalPrice as price, totalQuantity as tq} from './shoppingCart.js'

    console.log(price, tq)

```

or like that: 

```js
    import * as ShoppingCart from './shoppingCart.js' // it means to import everything from the module

    ShoppingCart.addToCart('bread', 5)
    console.log(ShoppingCart.totalPrice)
```

## Exporting modules

