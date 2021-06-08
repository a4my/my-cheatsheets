---
title: JavaScript DOM and Events
category: JavaScript
updated: 2021-06-08
intro: |
  A closer look to DOM and Events / Selecting, creating, deleting Elements/ Types of events /
---

# Manipulating Elements

## Selecting, creating and deleting Elements

### Selecting elements

```js
 console.log(document.documentElement)
 console.log(document.head)
 console.log(document.body)
```

```js
document.querySelector('.header')
document.querySelector('#ection--1')
document.querySelectorAll('.section')
document.getElementById('section--1')
```

```js
document.getElementsByTagName('button')
doucment.getElementsByClassName('btn')
```

### Creating and inserting elements


```js
// .insertAdjacentHTML

const message = document.createElement('div')
message.classList.add('cookie-message')
message.textContent = 'We use cookies for improved functionality and analytics'
// OR
message.innerHTML =  'We use cookies for improved functionality and analytics. <button class="btn btn--close--cookie">Got it!</button>'

const header = document.querySelector('.header')
header.prepend(message) // will create a cookie div in the header section of the website BEFORE any elements
header.append(message) // will create a cookie div in the header section of the website AFTER any elements
```

```js
header.before(message) // will be added before the header section
header.after(message) // will be added after the header section
```

### Deleting elements

```js
document.querySelector('.btn--close-cookie').addEventListener('click', function() {
    message.remove()
})
```

## Manipulating types, classes and attributes

### Styles

```js
message.style.backgroundColor = '#37383d'
message.style.width = '120px'
```

👍 use getComputedStyle to retrieve what style porperties are in used on an element:

```js
console.log(getComputedStyle(message)) // will return a whole array of properties for the message element
console.log(getComputedStyle(message).color) // will return the color of the element
```

Use setProperty() to set a new value; setProperty(propertytochange, valuetochangewith)

```js
document.documentElement.style.setProperty('--color-primary', 'orangered')
```

### Attributes

```js
const logo = document.querySelector('.nav__logo')
console.log(logo.alt)
console.log(logo.src)
console.log(logo.className)
```

❗ you can only return standard attributes with the method above. If you create a custom (or non-standard) attribute use the getAttribute() method:

```js
console.log(logo.designer) // undefined
console.log(logo.getAttribute('designer')) // Alex
```

you can also set an attribute this way:

```js
logo.alt = 'Beautiful minimalist logo'
```

```js
console.log(logo.src) // absolute version: http://127.0.0.1:8080/img/logo.png
console.log(logo.getAttribute('src')) // relative version: img/logo.png
```

