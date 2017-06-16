---
author: "Seth"
categories: [flatiron blog]
date: 2017-06-15T23:01:31-05:00
description: "Day 109 of Flatiron School"
featured: "puzzle.jpg"
featuredalt: "puzzle pieces"
featuredpath: "../../images/"
title: Sometimes The Logic Is Flawed
---

So I'm banging away at my jQuery project. I got hung up on some code tonight but got it working right before I stopped for the night! I was stoked! So what was I stuck on? In my app a user can create as many places as they want. Each place can have as many items as they want. A user can look at a specific item and see the name of it, the rating they gave it, any notes they wrote about it and where the item is available (the places they've added it to). I wanted to implement a "Next Item" button/link that when clicked will load the next item for the current user.

First things first I needed an array of the current users item ID #'s. I needed this because my show pages follow RESTful conventions and use the item ID in the URL. This is what the show page is expecting in it's params. So I got that done relatively easily:

```javascript
let itemsValues

$(() => {
  $.getJSON('/items.json', function (data) {
    itemsValues = $.map(data, function (e) {
      return e.id
    })
  })
})
```

Then, I wanted the functionality that I stated above. However, I didn't want to get to the last item and just have a button that does nothing because there's no next item. I also didn't want the button to just disappear (I did that and I thought it was weird). So I decided when we reached the last item we should loop back around and go to the first item again. So I started coding and got to this point:

```javascript
$('.js-next').on('click', function() {
  let nextIndex = itemsValues.indexOf(parseInt($('.js-next').attr('data-id'))) + 1
  $.getJSON('/items/' + itemsValues[nextIndex], function(data) {
    $('#name').html(data['name'])
    $('#rating').html(data['rating'])
    $('#notes').html(data['notes'])
    if (nextIndex === itemsValues.length)
      $('.js-next').attr('data-id', itemsValues[0])
    else
      $('.js-next').attr('data-id', data['id'])
  })
})
```

So my "Next Item" link has a class of 'js-next'. Then I set a `nextIndex` variable by getting the current `data-id` of my link (ie, the current item being displayed ID number), turning that into an integer, finding the index of that ID in the `itemsValues` array and adding one to it. Then I call my internal API and get the next item's info as a JSON object. I then fill in the new data to the DOM. Finally, I have an [if...else][1] block where I try and set the `data-id` to the first item ID if the new item is the last item in the array. If not, set it to the now current item ID.

Looking at this now I think the logic is flawed because, I increment by one on the API call after the click. So setting it to the first item _before_ the click will eliminate one item from ever showing up. I actually had this happen and couldn't figure out why. This logic was fuzzy but is probably why I ended up moving the [if...else][1] logic to the top of my function and when I did it worked!

```javascript
$('.js-next').on('click', function() {
  let nextIndex
  let dataIdIndex = itemsValues.indexOf(parseInt($('.js-next').attr('data-id')))
  if (dataIdIndex === itemsValues.length - 1)
    nextIndex = 0
  else
    nextIndex = dataIdIndex + 1
  $.getJSON('/items/' + itemsValues[nextIndex], function(data) {
    $('#name').html(`${data['name']} -
        <a href="/items/${data['id']}/edit">Edit</a> -
        <a data-confirm="Are you sure?" rel="nofollow" data-method="delete" href="/items/${data['id']}">Delete</a>`)
    $('#rating').html(`Rating: ${data['rating']}`)
    $('#notes').html(`Notes: ${data['notes']}`)
    $('.js-next').attr('data-id', data['id'])
  })
})
```

I also filled out the HTML for the name section of the page using those lovely [template literals][2] I talked about in my last blog post. This project is coming along well. I'm hoping to be done with it tomorrow night at some point in time. If I can finish this off before the weekend I'll be super happy and think right on track to be done before the end of the month.

Time spent today: 2:16  
Time spent total: 394:16  
Lessons completed today: 0  
Lessons completed total: 646

  [1]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else
  [2]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
