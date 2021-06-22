---
title: JavaScript Object-Oriented Programming
category: JavaScript
updated: 2021-06-21
intro: |
  A closer look to OOP with Javascript
---

# What is OOP?

Classes are like blueprint from which we can create new objects.

We call all objects created through a class instances. Creating instances is called instantiation.

The 4 fundamental principles of OOP: Abstraction, Encapsulation, Inheritance and Polymorphism


### Abstraction

--> Ignoring or hiding details that don't matter, allowing us to get an overview.

### Encapsulation

--> Keeping properties and methods private inside the class so they are not accessible from outside the class

### Inheritance

--> Making all properties and methods of a certain class available to a child class, forming a hierarchical between classes. This allows us to reuse common logic and to model real world relationships.

### Polymorphism

--> A child class can overwrite a method it inherited from a parent class.


# Prototypes

All objects in JS are linked to a prototype object.

The prototype contains methods (behavior) that are accessible to all objects linked to that prototype. Behavior is delegated to the linked prototype object.


## How to implement prototypes?

### Constructor functions

•Technique to create objects from a function

• This is how built-in objects like arrays, maps or sets are actually implemented

### ES6 Classes

• Modern alternative to constructor function syntax

• 'Syntactic sugar': behind the scenes, ES6 classes work exactly like constructor functions

• ES6 classes do not behave like classes in classical OOP

### Object.create()

• The easiest and most straight forward way of linking an object to a prototype object.


## Constructor Functions and the new Operator

```js
const Person = function(firstName, birthYear) {
    // Instance porperties
    this.firstName = firstName
    this.birthYear = birthYear

    // Never do this:
    // this.calcAge = function() {
    //     console.log(2037 - this.birthYear)
    // }
}

const alex = new Person('Alex', 1986)

// 1. New {} is created
// 2. Function is called, this = {}
// 3. {} linked to protoype
// 4. function automatically returns {}

const annie = new Person('Annie', 1984)
const tom = new Person('Tom', 2020)

console.log(annie, tom)

const jay = 'Jay'
console.log(annie instanceof Person) // true
console.log(jay instanceof Person) // false

```

❗ constructor names always start with a capital letter.


## Prototype inheritance

```js
Person.prototype.calcAge = function() {
        console.log(2037 - this.birthYear)
    }
```

```js
    alex.calcAge() 
    annie.calcAge()
```

will return the result of the function.


```js
    console.log(Person.prototype)
    // OR
    console.log(alex.__proto__)
```
it will return the constructor, the functions and properties of Person

```js
    console.log(alex.__proto__ === Person.prototype) // true

    console.log(Person.prototype.isPrototypeOf(alex)) // true
    console.log(Person.prototype.isPrototypeOf(annie)) // true
    console.log(Person.prototype.isPrototypeOf(Person)) // false
```

```js
    Person.prototype.species = 'Homo Sapiens'

    console.log(alex.species, annie.species) // Home Sapiens Home Sapiens

    console.log(tom.hasOwnProperty('firstName')) // true
    console.log(tom.hasOwnProperty('species')) // false
```

You can go up in the prototype chain by doing this:

```js
    console.log(alex.__proto__)
    //Object.prototype (top of prototype chain)
    console.log(alex.__proto__.__proto__) // will return the prototype of the object prototype
    console.log(alex.__proto__.__proto__.__proto__) // will return null
```

# Classes

```js
    // class expression
    const PersonCl = class {
        // etc
    }

    // class declaration
    class PersonCl {
        constructor(fistName, birthYear) {
            this.firstName = firstName
            this.birthYear = birthYear
        }
        //Methods goes outside of the constructor block and will be added to prototype property of the PersonCl class
        calcAge() {
            console.log(2021 - this.birthYear)
        }
    }

    const jessica = new PerconCl('Jessica', 1996)

    console.log(jessica) // will return the PersonCl instance/object with Jessica
    jessica.calcAge() // 25

    console.log(jessica.__proto__ === PersonCl.__proto__) // true

    PersonCl.prototype.greet = function() {
        console.log(`Hey ${this.firstName}!`)
    } // Note that this method can also be added in the PersonCl class directly instead
    jessica.greet() // Hey Jessica!

```

❗ Classes are NOT hoisted
❗ Classes are first class citized
❗ Classes are executed in strict mode

