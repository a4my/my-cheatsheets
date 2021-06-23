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


# Setters and Getters

```js
    const amount = {
        owner: 'Alex',
        movements: [200, 53, 120, 300],

        get latest() {
            return this.movements.slice(-1).pop()
        }

        set latest(mov) {
            this.movements.push(mov)
        }
    }

    console.log(account.latest) //300

    account.latest = 50
    console.log(account.latest) // [200, 53, 120, 300, 50]
```

❗ set needs at least 1 parameter


```js
    class PersonCl {
        constructor(fullName, birthYear) {
            this.fullName = fullName
            this.birthYear = birthYear
        }
        
        calcAge() {
            console.log(2021 - this.birthYear)
        }

        get age() {
            return 2021 - this.birthYear
        }

        // Set a property that already exists
        set fullName(name) {
            if(name.includes(' ')) this._fullName = name
            else alert(`${name} is not a full name!`)
        }

        get fullName() {
            return this._fullname
        }
    }

    console.log(jessica.age) // 25

    const jessica = new PerconCl('Jessica Davis', 1996)
```

❗ Note the _ before fullName, this is to create a new variable to avoid naming conflicts (fullName has already been declared as a class parameter)


# Static method

Not available on instances methods

```js
    class PersonCl {
        constructor(fullName, birthYear) {
            this.fullName = fullName
            this.birthYear = birthYear
        }
        
        // Instance method
        calcAge() {
            console.log(2021 - this.birthYear)
        }

        get age() {
            return 2021 - this.birthYear
        }

        // Set a property that already exists
        set fullName(name) {
            if(name.includes(' ')) this._fullName = name
            else alert(`${name} is not a full name!`)
        }

        get fullName() {
            return this._fullname
        }

        // Static method
        static hey() {
            console.log('Hey there ✌')
        }
    }

    console.log(jessica.age) // 25

    const jessica = new PerconCl('Jessica Davis', 1996)
```


# Object.create

Sets a prototype object to any other object

```js
    const PersonProto = {
        calcAge() {
            console.log(2021 - this.birthYear)
        }

        init(firstName, birthYear) {
            this.firstName = firstName
            this.birthYear = birthYear
        }
    }

    const steven = Object.create(PersonProto)
    console.log(steven) // will return the object but with no data
    steven.name = 'Steven' // will assign the name
    steven.birthYear = 2002 // will assign the birth year
    steven.calcAge() // 19
```

we can then use the prototype above to easily create new objects:

```js
    const sarah = Object.create(PersonProto)
    sarah.init('Sarah', 1986)
    sarah.calcAge()
```


# Inheritance between classes

## Using constructor function

```js
    const Student = function(firstName, birthYear, course) {
        this.firstName = firstName
        this.birthYear = birthYear
        this.course = course
    } 

    Student.prototype.introduce = function() {
        console.log(`My name is ${this.firstName} and I study ${this.cours}`)
    }

    const mike = new Student('Mike', 2000, 'Computer Science')
    mike.introduce()
```

The Student Object can inherit the properties from another object:

```js
    const Person = function(firstName, birthYear) {
        this.firstName = firstName
        this.birthYear = birthYear
    }

    const Student = function(firstName, birthYear, course) {
        Person.call(this, firstName, birthYear)
        this.course = course
    } 

```

To create a connection manually between the prototypes using Object.create():

```js

    const Student = function(firstName, birthYear, course) {
        Person.call(this, firstName, birthYear)
        this.course = course
    } 

    Student.prototype = Object.create(Person.prototype) // Manual connection, needs to be added here, before adding methods to the prototype

    Student.prototype.introduce = function() {
            console.log(`My name is ${this.firstName} and I study ${this.course}`)
        }

    const mike = new Student('Mike', 2000, 'Computer Science')
    mike.introduce()
    mike.calcAge()
```


## Using ES6 classes

```js
    class Student extends PersonCl {
        constructor(fullName, birthYear, course) {
        // Student.prototype = Object.create(Person.prototype) // No need to link the prototypes manually.
        super(fullName, birthYear) // Needs to happens first in the lock !
        }
    }

    const martha = new Student('Martha Jones', 2012)
    console.log(martha) // will return the object even if the constructor block above is empty
```

❗ The super() needs to happens first in the lock !

```js
    class Student extends PersonCl {
        constructor(fullName, birthYear, course) {
        super(fullName, birthYear) 
        this.course = course
        }

        introduce() {
            console.log(`My name is ${this.firstName} and I study ${this.cours}`)
        }

        calcAge() { // will overwrite the first calcAge function
            console.log(`I'm ${2021 - this.birthYear} years old but as a student I feel more like ${2021 - this.birthYear + 10}`)
        }
    }

    const martha = new Student('Martha Jones', 2012, 'Computer Science')
    martha.introduce()
    martha.calcAge()
    martha.greet()
```

## Using Object.create()

```js
    const PersonProto = {
        calcAge() {
            console.log(2021 - this.birthYear)
        }

        init(firstName, birthYear) {
            this.firstName = firstName 
            this.birthYear = birthYear 
        }
    }

    const steven = Object.create(personProto)

    const StudentProto = Object.create(PersonProto)
    StudentProto.init = function(firstName, birthYear, course) {
        PersonProto.init.call(this, firstName, birthYear)
        this.course = course
    }

    StudentProto.introduce = function() {
        console.log(`My name is ${this.firstName} and I study ${this.course}`)
    }

    const jay = Object.create(StudentProto)
    jay.init('Jay', 2010, 'Computer Science')
    jay.introduce()
    jay.calcAge()
```
# Encapsulation

Means some methods and properties are kept unaccessible from outside the class (ie PIN number)

```js
    class Account {
        constructor(owner, currency, pin) {
            this.owner = owner
            this.currency = currency
            // Protected property
            this._pin = pin
            this._movements = []
            this.locale = navigator.language
        }

        // Public interface
        getMovements() {
            return this._movements
        }
    }

    console.log(acc.getMovements()) // will return the movements array, everyone can see them but cannot overwrite or set the movements
```

❗ It's a programming standard to add an uppercase in front of a property to declare a protected property that should'nt be accesible from outside the class 


## Private fields and methods

### Public fields

```js
    class Account {
        // Public fields (instances)
        locale = navigator.language
        _movements = []

        constructor(owner, currency, pin) {
            this.owner = owner
            this.currency = currency
            // Protected property
            this._pin = pin
            // this._movements = []
            // this.locale = navigator.language
        }
```

### Private fields

```js
    class Account {
        // Private fields
        #movements = []
        #pin; 

        constructor(owner, currency, pin) {
            this.owner = owner
            this.currency = currency
            // Protected property
            // this._pin = pin
            // this._movements = []
            this.locale = navigator.language
       }

        getMovements() {
            return this.#movements
        }
    }

    console.log(acc1.#movements) // will return a private field error
```

### Public methods

```js
    class Account {
        constructor(owner, currency, pin) {
            this.owner = owner
            this.currency = currency
            Protected property
            this.pin = pin
            this.movements = []
            this.locale = navigator.language
       }

        // Public methods
        getMovements() {
            return this.movements
        }
    }
```

### Private methods

```js
    class Account {
        constructor(owner, currency, pin) {
            this.owner = owner
            this.currency = currency
            Protected property
            this.pin = pin
            this.movements = []
            this.locale = navigator.language
       }

        // Public methods
        #approveLoan(val) {
            return true
        }
    }
```

❗ Private methods do not work on all browsers yet.

### Chaining methods

Doing the following chain won't work:

```js
    acc1.deposit(300).deposit(500).withdraw(35).requestLoan(2500).withdraw(4000)
    console.log(acc1.getMovements())
```

Unless you add 'return this' into the methods:

```js
    class Account {
        constructor(owner, currency, pin) {
            this.owner = owner
            this.currency = currency
            this._pin = pin
            this._movements = []
            this.locale = navigator.language
        }

        getMovements() {
            return this._movements
        }

        deposit(val) {
            this.movements.push(val)
            return this
        }

        withdraw(val) {
            this.deposit(-val)
            return this
        }

        requestLoan(val) {
            this.deposit(val)
            console.log('Loan approved')
            return this
        }
    }

    acc1.deposit(300).deposit(500).withdraw(35).requestLoan(2500).withdraw(4000)
    console.log(acc1.getMovements()) // will return the methods chain with the movements array updated

```