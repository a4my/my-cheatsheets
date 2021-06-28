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

```js
    /////////////////
    //shoppingCart.js
    export default function(product, quantity) {
        cart.push({product, quantity})
        console.log(`${quantity} ${product} added to cart`)
    }

    ///////////
    //script.js
    import add from './shoppingCart.js'
    add('pizza', 2)
```

## Module pattern

```js
    const ShoppingCart2 = (function() { 
    const cart = []
    const shippingCost = 10
    const totalPrice = 237
    const totalQuantity = 23

    const addToCart = function(product, quantity) {
        cart.push({product, quantity})
        console.log(`${quantity} ${product} added to cart`)
    }

    const orderStock = function(product, quantity) {
        console.log(`${quantity} ${product} ordered from supplier`)
    }

    return {
        addToCart,
        cart,
        totalPrice,
        totalQuantity,
    }
})() // IFFE

    ShoppingCart2.addToCart('apple', 4)
    ShoppingCart2.addToCart('pizza', 2)
    console.log(ShoppingCart2)
```

# Tooling

## NPM

### Initiating npm
In each project we need to use npm, we need to initate it first:

```
 npm init
```

This will trigger a list of question about the project. This will also add a package.json file to the project.

### Using a package manager

```
    npm install leaflet // or npm i leaflet
```

This will install the package onto the project as well as a node_modules folder which contains the leaflet folder

Also, leaflet will be added in the dependencies list on the package.json file.

### Adding the lodash-es library

Lodash is a collection of a ton of useful functions for arrays, objects, functions, etc that are not included in the JavaScrpt language.

```
    npm i lodash-es
```

❗ not lodas but lodash-es

The lodash-es library will be added onto the node_modules folder and the dependencies list.

Once installed you can use a method from the lodash-es library by importing it onto your JS script: 

```js
    import cloneDeep from './node_modules/lodash-es/cloneDeep.js'
```

👍 FYI cloneDeep() is used to deep clone objects.


### Installing the packages again

Let's say you copied your project onto another computer and don't have the node_modules folder in the project. You won't have to install all the pckages you used one by one you only need to run the npm install command to install them. You need to have the package.json file in your project though.

```
 npm install // or npm i
```

## Parcel (bundler tool)

### Install Parcel

```
    npm i parcel --save-dev
```

A dev dependency is a tool that we need to build our application but it's not a dependcy that we actually include in our code. 

Once installed, Parcel will appear in the dev dependency list in the package.json file.


### using npx to use Parcel

```
    npx parcel index.html
```

To set up the entry point (index.html where the js scripts are linked up). I

It will bundle index.html, script.js and shoppingCart.js

Parcel will aslo open a new local live server to work on our project. the link will be in the command line.

💢 If you encounter a bug while installing Parcel try :

```
    sudo npx index.html
```

💢 Also, make sure your scripts are not module types in your index.html file


Once Parcel is installed, it creates a dist folder where the bundle of our files is.

Parcel will also allow you to write the your imports by only pointing at the name of the file:

```js
    import cloneDeep from './node_modules/lodash-es/cloneDeep.js'

    // can be written this way with Parcel:

    import cloneDeep from 'lodash-es'

```


### using npm scripts to use Parcel

You can simply add a script onto the scripts list of the package.json file:

```
    "scripts": {
        "start": "parcel index.html"
    },
```

then run the following command in the terminal:

```
    npm run start
```

to build the bundle you then need to add another script onto the list:

```
    "scripts": {
        "start": "parcel index.html",
        "build": "parcel build index.html"
    },
```

and run the command:

```
    npm run build
```


## Babel

Babel is used to transpile our modern code into code that can be read by old browsers.

### polifying Promises
But Babel cannot transpile some of the ES6 concepts like promises, for that, you'll need to add a polifier library such as core-js which you can install:

```
    npm i core-js
```

and add in your imports:

```js
    import 'core-js/stable'
```

### polifying async/await

Install:

```
    npm i regenerator-runtime
```
Then add import:

```js
    import 'regenerator-runtime/runtime'
```
