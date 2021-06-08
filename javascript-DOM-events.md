---
title: JavaScript DOM and Events
category: JavaScript
updated: 2021-06-08
intro: |
  A closer look to DOM and Events / Selecting, creating, deleting Elements/ Types of events /
---

# Manipulating Elements

## Selecting elements

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

## Creating and inserting elements

• Creating and inserting elements:

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

• Deleting elements

```js
document.querySelector('.btn--close-cookie').addEventListener('click', function() {
    message.remove()
})
```