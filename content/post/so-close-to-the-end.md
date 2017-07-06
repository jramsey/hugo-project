---
author: "Seth"
categories: [flatiron blog]
date: 2017-07-05T15:22:54-05:00
description: "Day 129 of Flatiron School"
featured: "stairs.jpg"
featuredalt: "stairs"
featuredpath: "../../images/"
title: Final Project Complete...
---

It's been about 3 weeks since I last blogged. I put my head down and sprinted towards the finish line. I can't say that I'm 100% done, yet, but I will be soon. I have completed my final portfolio project and have my assessment for it tomorrow. I must say, [Redux][1] threw me for one while working on this project. I hit many stumbling blocks building this project. I think my sprint was alittle ambitious and I ended up not knowing the Redux stuff as in depth as I wanted to. I definitely created some of my own frustration because of this. However, I hacked away at it and got it. I watched YouTube videos, [Wes Bos's Redux Course][2], and I even used [HackHands][3] a couple times thanks to the [Github Education Student Developer Pack][4] $25 credit I received.

HackHands was an interesting experience. Getting help from people who were not native English speakers (I assumed that's who I'd get considering I was doing this on July 4th) and being able to communicate how I was stuck. The two times I used it I didn't get a direct answer to my question. However, I did see someone debug my code live and in the end the source of my problem was illuminated by the help.

So one problem I ran into was not getting the data from my API when I called `fetchPlaces()`. I was stumped. By all accounts it should be working. My API was returning proper JSON formatted data. I had:

```javascript
// fetch places
function fetchPlaces () {
  return (dispatch) => {
    dispatch({type: 'FETCH_PLACES'})
    return fetch('http://localhost:3001/api/places')
      .then(response => {
        dispatch({type: 'RECEIVED_PLACES', payload: response})
      })
      .catch((err) => {
        dispatch({type: 'FETCH_PLACES_ERROR', payload: err})
      })
  }
}
```

I couldn't for the life of me figure out why I wasn't getting the data that I needed back. I considered using `parseJSON()` but I didn't think I needed to since the data being returned was already JSON. I was going to use it just like that as well. I wasn't accounting for the fact that I was using `fetch()` to retrieve the JSON from my API. For more about the small, but important piece, that I was missing take a look at [Using Fetch][5] followed by [Body.json()][6] on MDN. With that knowledge I was able to fix my call by implementing `.json()` on line 7 below followed by another `.then` which now has the proper data to pass into the payload.

```javascript
// fetch places
function fetchPlaces () {
  return (dispatch) => {
    dispatch({type: 'FETCH_PLACES'})
    return fetch('http://localhost:3001/api/places')
      .then(response => {
        response.json()
        .then(json => {
          dispatch({type: 'RECEIVED_PLACES', payload: json})
        })
      })
      .catch((err) => {
        dispatch({type: 'FETCH_PLACES_ERROR', payload: err})
      })
  }
}
```

Another issue I ran into was a CORS violation. CORS stands for "Cross-origin resource sharing" and can be described as:

> Cross-origin resource sharing is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served. A web page may freely embed cross-origin images, stylesheets, scripts, iframes, and videos. Certain "cross-domain" requests, notably Ajax requests, however are forbidden by default by the same-origin security policy.  
> -- [Wikipedia][7]

If that doesn't make sense, don't worry. Just know that CORS is implemented for security on the web. However, it also meant that unless I explicitly stated that my React app could talk to my Rails API I wasn't going to be able to get the data. Luckily, there is a pretty easy way to enable this and it only took a few lines of code. I first added `gem 'rack-cors', :require => 'rack/cors'` to my Gemfile and ran `bundle`. Next I had to add some code:

```ruby
# /config/initializers/cors.rb

Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'localhost:3000'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

This enabled my React application running on `localhost:3000` to talk to my Rails API server running on `localhost::3001` with no problems.

Ultimately I learned **A LOT** doing this project. I'm not 100% happy with where my app is at currently. However, to my understanding it fulfills all the requirements of the project and that's what I was shooting for. I can see abstracting it away from the back end and setting it up to pull all data from an external API call instead. Having built the back end though I know that it'll always work the way I want it to and thus is a more stable project to include in a portfolio.

Check out [Foodie View][8] and see what you think for yourself. I'll get it up on Heroku soon and will link to it from GitHub.

Time spent total: 457:50  
Lessons completed total: 689

  [1]: http://redux.js.org
  [2]: https://learnredux.com
  [3]: https://hackhands.com/
  [4]: https://education.github.com/pack
  [5]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
  [6]: https://developer.mozilla.org/en-US/docs/Web/API/Body/json
  [7]: https://en.wikipedia.org/wiki/Cross-origin_resource_sharing
  [8]: https://github.com/itzsaga/foodie-view
