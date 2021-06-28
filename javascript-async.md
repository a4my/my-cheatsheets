---
title: Asynchronous JavaScript
category: JavaScript
updated: 2021-06-25
intro: |
  A closer look to Promises / Async-Await/ AJAX / Throwing errors / Chaining promises /
---

# Asynchronous JS

• Most code is synchronous (executed line by line and each line of code waits for the previous line to finish)

👎 Long-running operations block code execution

• Asynchronous code is executed after a task that runs in the background finishes. Async is non-blocking and the execution doesn't wait for an async task to finish its work. ie setTimeout()

❗ Callback functions alone and event listeners do NOT make code asynchronous!

# AJAX

Stands for Asynchronous JavaScript And XML.

Allows us to communicate with remote web servers in an asynchronous way. With AJAX calls we can request data from web servers dynamically.

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


# Building a simple promise

```js
    const lotteryPromise = new Promise(function(resolve, reject) {
        console.log('Lottery draw is happening 🔮')
        setTimeout(function() {
            if(Math.random() >= 0.5) {
                resolve('You WIN! 💰')
            } else {
                reject(new Error('You lost your money...💩'))
            }
        }, 2000)
    })

    letteryPromise.then(res => console.log(res)).catch(err => console.log(err))
    // will randomly return either the resolve or reject outcome depending on the random number
```

Promisifying means to convert callback based asynchronous behaviour to promise based:

```js
    // Promisifying setTimeout function
    const wait = function(seconds) {
        return new Promise(function(resolve) {
            setTimeout(resolve, seconds * 1000)
        })
    }

    wait(2).then(() => {
        console.log('I waited for 2 seconds')
        return wait(1)
    }).then(() => console.log('I waited for 3 seconds'))
```

❗ No reject function because t is impossible for the timer to fail 😉


## Promisifying the geolocation API

Let's take the following example:

```js
    navigator.geolocation.getCurrentPosition(
        position => console.log(position),
        err => console.error(err)
    )

    console.log('Getting position')
```
and promisify it :

```js
    const getPosition = function() {
        return new Promise(function(resolve, reject) {
            navigator.geolocation.getCurrentPosition(
            position => resolve(position),
            err => reject(err)
            )
        })
    }
```

which can also be written this way:

```js
    const getPosition = function() {
        return new Promise(function(resolve, reject) {
            navigator.geolocation.getCurrentPosition(resolve, reject)
            )
        })
    }

    getPosition().then(pos => console.log(pos))
```

# Consuming promises with Async / Await (modern way)

```js
    const whereAmI = async function(country) {
        const res = await fetch(`https://restcountries.eu/rest/v2/name/${country}`)
        const data = await res.json()
    }
```
is the modern way of doing :

```js
    const whereAmI = async function(country) {
        fetch(`https://restcountries.eu/rest/v2/name/${country}`)
        .then(res => res.json())
        .then(data => console.log(data))
    }
```

--> consuming the promise: 

```js
    const whereAmI = async function() {
        // Geolocation
        const pos = await getPosition()
        const { latitude: lat, longitude: lng} = pos.coords
        // Reverse geocoding
        const resGeo = await fetch(`https://geocode.xyz/${lat},${lng}?geoit=json`)
        const dataGeo = await resGeo.json()
        // Country data
        const res = await fetch(`https://restcountries.eu/rest/v2/name/${dataGeo.country}`)
        const data = await res.json()
        renderCountry(data[0])
    }

    whereAmI()
```


## Try / Catch


```js
    try {
        let y = 1
        const x =2
        x =3 // will return error, cannot assign to const variable
    } catch(err) {
        alert(err.message)
    }

```

```js
    const whereAmI = async function() {
        try{
            // Geolocation
            const pos = await getPosition()
            const { latitude: lat, longitude: lng} = pos.coords
            // Reverse geocoding
            const resGeo = await fetch(`https://geocode.xyz/${lat},${lng}?geoit=json`)
            const dataGeo = await resGeo.json()
            // Country data
            const res = await fetch(`https://restcountries.eu/rest/v2/name/${dataGeo.country}`)
            const data = await res.json()
            renderCountry(data[0])
        } catch(err) {
            console.error(err)
            renderError(`Something went wrong 💥 ${err.message}`)
        }
    }

    whereAmI()
```

❗ Remember that getPosition, renderCountry, whereAmI and renderError were created before in the lesson


```js
    whreAmI()
        .then(city => console.log(`1; ${city})`)
        .catch(err => console.error(`1: ${err.message} 💥)`)
        .finally(() => console.log(`2: Finished getting location`))
```

can be written with IFFEs:

```js
    (async function() {
        try {
            const city = await whereAmI()
            console.log(`1: ${city}`)
        } catch(err) {
            console.log(`2: ${err.message}`)
        }
        console.log('Finished getting location')
    })()
```

## Running promises in parallel (combinator function)

Executing the following will get the 3 promises to run one after the other:

```js
    const get3Countries = async function(c1, c2, c3) {
        try{
            const [data1] = await getJSON(`https://restcountries.eu/rest/v2/name/${c1}`)
            const [data2] = await getJSON(`https://restcountries.eu/rest/v2/name/${c2}`)
            const [data3] = await getJSON(`https://restcountries.eu/rest/v2/name/${c3}`)

            console.log([data1.capital, data2.capital data3.capitol])
        } catch(err) {
            console.error(err)
        }
    }

    get3Countries('portugal', 'canada', 'tanzania')
```

Using Promise.all() will run all 3 promises at the same time in parallel:

```js
    const get3Countries = async function(c1, c2, c3) {
        try{
            const data = await Promise.all([
                getJSON(`https://restcountries.eu/rest/v2/name/${c1}`),
                getJSON(`https://restcountries.eu/rest/v2/name/${c2}`),
                getJSON(`https://restcountries.eu/rest/v2/name/${c3}`)
            ])

            console.log(data.map(d => d[0].capital))
        } catch(err) {
            console.error(err)
        }
    }

    get3Countries('portugal', 'canada', 'tanzania')
```
❗ Promise.all() receives an array of promises and returns an array of promises, will sortcuts if a promise is rejected though.

## Other combinator function: race, allSettled and any

### Promise.race

The promise returned by Promise.race() is settled as soon as one of the input promises settles

```js
    (async function() {
        const res = await Promise.race([
            getJSON(`https://restcountries.eu/rest/v2/name/italy`),
            getJSON(`https://restcountries.eu/rest/v2/name/egypt`),
            getJSON(`https://restcountries.eu/rest/v2/name/mexico`)
        ])
    })

    conosle.log(res[0])
```

All 3 promises will race against each other and if the winning promise is a fulfilled promise, then the fulfillment value is going to be the fulfillment value of the winning promise. Therefore, only the winning promise will be returned as an array.


### Promise.allSettled

It takes in an array of all the promises and will return an array of all the settled promises (rejected or not). Never shortcuts the results, it will return the results of all the promises.

```js
    Promise.allSettled([
        Promise.resolve('Succes')
        Promise.reject('Error')
        Promise.resolve('Another Succes')
    ]).then(res => console.log(res[0]))
```

### Promise.any (ES2021)

Similar to Promise.race(), with the difference that rejected promises are ignored. Therefore the result of Promise.any() will always be a fulfilled promise unless all of them get rejected.

```js
    Promise.any([
        Promise.resolve('Succes')
        Promise.reject('Error')
        Promise.resolve('Another Succes')
    ]).then(res => console.log(res[0]))
```
