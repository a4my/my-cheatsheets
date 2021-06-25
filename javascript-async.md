---
title: Asynchronous JavaScript
category: JavaScript
updated: 2021-06-25
intro: |
  A closer look to Promises / Async-Await/ AJAX /
---

# Asynchronous JS

• Most code is synchronous (executed line by line and each line of code waits for the previous line to finish)

👎 Long-running operations block code execution

• Asynchronous code is executed fter a task that runs in the background finishes. Async is non-blocking and the execution doesn't wait for an async task to finish its work. ie setTimeout()

❗ Callback functions alone and event listeners do NOT make code asynchronous!

# AJAX

Stands for Asynchronous JavaScript And XML.

Allows us to communicate with remote web servers in an asynchronous way. With AJAX calls we can request date from web servers dynamically.

XML is a data format which is no longer used, instead we now use JSON data format.

# API

Stands for Application Programming Interface. Piece of software that can be used by another piece of software in order to allow applications to talk to each other and exchange information.


# AJAX calls

# Old school way

```js
    const request = new XMLHttpRequest()
    request.open('GET', `https://restcountries.eu/rest/v2/name/${country}`)
    request.send()

    request.addEventListener('load', function(){
        const [data] = JSON.parse(this.responseText)
        console.log(data)

        const html = `
            <article class="country">
                <img class="country__img" src="${data.flag}" />
                <div class="country__data">
                    <h3 class="country__name">${data.name}</h3>
                    <h4 class="country__region">${data.region}</h4>
                    <p class="country__row"><span>👫</span>${(+data.population / 1000000).toFixed(1)} people</p>
                    <p class="country__row"><span>🗣️</span>${data.languages[0].name}</p>
                    <p class="country__row"><span>💰</span>${data.currencies[0].name}</p>
                </div>
            </article>
        `

    countriesContainer.insertAdjacentHTML('beforeend', html)
    countriesContainer.style.opacity = 1
    })

    getCountryData('france')
    getCountryData('usa')
    getCountryData('gb')
```

## Modern way (promises)

Promise: an object that is used as a placeholder for the future result of an asynchronous operation.

It is a container for an asynchronously delivered value.

A container for a future value.

```js
    const renderCountry = function(data, className = '') {
    const html = `
        <article class="country ${className}">
            <img class="country__img" src="${data.flag}" />
            <div class="country__data">
                <h3 class="country__name">${data.name}</h3>
                <h4 class="country__region">${data.region}</h4>
                <p class="country__row"><span>👫</span>${(+data.population / 1000000).toFixed(1)} people</p>
                <p class="country__row"><span>🗣️</span>${data.languages[0].name}</p>
                <p class="country__row"><span>💰</span>${data.currencies[0].name}</p>
            </div>
        </article>
    `

    countriesContainer.insertAdjacentHTML('beforeend', html)
    countriesContainer.style.opacity = 1
    }



    const getCountryData = function (country) {
        fetch(`https://restcountries.eu/rest/v2/name/${country}`) // fetch something
        .then((response) => response.json()) // then we get a response which gets transformed into JSON
        .then((data) => renderCountry(data[0])) // then we use the data to render the DOM
    }

    getCountryData('romania')

```


## Chaining Promises

```js
    const getCountryData = function (country) {
        //Country 1 
        fetch(`https://restcountries.eu/rest/v2/name/${country}`)
        .then((response) => response.json())
        .then((data) => {
            renderCountry(data[0])
            const neighbour = data[0].borders[0]

            if(!neighbour) return 

            // Country 2
            return fetch(`https://restcountries.eu/rest/v2/alpha/${neighbour}`)
        })
        .then(response => response.json())
        .then(data => renderCountry(data, 'neighbour'))
    }

    getCountryData('france')    
```


## Handling rejected promises

Add a catch method at the end of the promise chain:

```js
    const getCountryData = function (country) {
        //Country 1 
        fetch(`https://restcountries.eu/rest/v2/name/${country}`)
        .then((response) => response.json())
        .then((data) => {
            renderCountry(data[0])
            const neighbour = data[0].borders[0]

            if(!neighbour) return 

            // Country 2
            return fetch(`https://restcountries.eu/rest/v2/alpha/${neighbour}`)
        })
        .then(response => response.json())
        .then(data => renderCountry(data, 'neighbour'))
        .catch(err => {
            console.error(`${err} 💥`)
            errorRender(`Something went wrong 💥💥💥 ${err.message}. Try again`)
        })
    }

    getCountryData('france')
```

and create an error function :

```js
    const errorRender = function(msg) {
        countriesContainer.insertAdjacentText('beforeend', msg)
        countriesContainer.style.opacity = 1
    }
```

you can also add a .finally() method at the very end of the chain. used for something that always need to happen no matter the result of the promise:

```js
    const getCountryData = function (country) {
        //Country 1 
        fetch(`https://restcountries.eu/rest/v2/name/${country}`)
        .then((response) => response.json())
        .then((data) => {
            renderCountry(data[0])
            const neighbour = data[0].borders[0]

            if(!neighbour) return 

            // Country 2
            return fetch(`https://restcountries.eu/rest/v2/alpha/${neighbour}`)
        })
        .then(response => response.json())
        .then(data => renderCountry(data, 'neighbour'))
        .catch(err => {
            console.error(`${err} 💥`)
            errorRender(`Something went wrong 💥💥💥 ${err.message}. Try again`)
        })
        .finally(() => {
            countriesContainer.style.opacity = 1
        })
    }

    getCountryData('france')
```


## Throwing errors manually


```js
    const getJSON = function(url, errorMsg = 'Something went wrong') {
        fetch(url).then(response => {
            if(!response.ok) throw new Error(`${errorMsg} (${response.status}`)

            return response.json()
        })
    }


    const getCountryData = function (country) {
        //Country 1 
        getJSON(`https://restcountries.eu/rest/v2/name/${country}`, 'Country not found')
       
        .then((data) => {
            renderCountry(data[0])
            const neighbour = data[0].borders[0]

            if(!neighbour) throw new Error('No neighbour found!') 

            // Country 2
            return getJSON(`https://restcountries.eu/rest/v2/alpha/${neighbour}`, 'Country not found')
        })
        .then(data => renderCountry(data, 'neighbour'))
        .catch(err => {
            console.error(`${err} 💥`)
            errorRender(`Something went wrong 💥💥💥 ${err.message}. Try again`)
        })
        .finally(() => {
            countriesContainer.style.opacity = 1
        })
    }

    getCountryData('france')
```
