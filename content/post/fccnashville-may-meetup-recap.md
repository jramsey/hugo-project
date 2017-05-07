---
author: "Seth"
categories: [freeCodeCamp Nashville]
date: 2017-05-06T17:26:22-05:00
description: "A recap of the things we went through at our May meetup."
featured: "businessman.png"
featuredalt: "man in tie presenting"
featuredpath: "../../images/"
title: freeCodeCamp Nashville May Meetup Recap
---

So today [Dave Harned][1] and I hosted the monthly [freeCodeCamp Nashville][2] [Meetup][3]. There were 8 of us there and it was good to see new and "old" faces. I think we're starting to build more of a core group that will consistently attend the meetup. With that we've started exploring some other options for larger meetup locations. The library is nice but the wifi is awfully slow and that's a pretty big downside considering what we're meeting for.

Dave and I presented on RESTful APIs and general REST info. You can view the slides [here][4] and to get a feel for what it was like, the image above is what Dave looked like presenting. So after that we chatted for a bit about many things.

IDE's were brought up. Specifically [WebStorm][5] (which you can get for free with a .edu email address), [Brackets][6], and [Visual Studio Code][7] were discussed. As were the limitations of [CodePen][8] and using [Cloud9][9] instead and some of a Cloud9 setup.

In the discussion of local dev environments Dave brought up [MAMP][10] and how he was dabbling in some WordPress when he was using it.

Other resources that were mentioned were: [Eli the Computer Guy][11] and [The Coding Train][12] on YouTube. An algorithms course on Coursera was mentioned but not the specific one. We were talking about Stanford though so I think [this][13] is the right one.

We also worked through the freeCodeCamp [Truncate a string][14] challenge together. I didn't think to save it at the time but we used Dave's computer so hopefully he has the solution locally on his machine still. If so I'll update with it.

_UPDATE_ here's the code:

```js
function truncateString(str, num) {
  if (str.length <= num) {
    return str;
  } else if (num <=3) {
    return str.slice(0, num) + "...";
  } else {
    return str.slice(0, num - 3) + "...";
  }
}

truncateString("A-tisket a-tasket A green and yellow basket", 11);
```

We had a good time and there were a few extended conversations after the we officially ended which I liked. I'm not a Sr. Dev and can't mentor people too much, _yet_. However, I really do enjoy seeing people connect with each other and the community we're slowly building around the central theme of people new to coding utilizing freeCodeCamp to learn.

  [1]:https://github.com/davi3blu3
  [2]:https://www.facebook.com/groups/free.code.camp.nashville/
  [3]:https://www.meetup.com/freeCodeCamp-Nashville/
  [4]:https://docs.google.com/presentation/d/1u4wrdDL6gnVAo7JMxgjhLaHavO0XGYCMFI5hIxrJJEk/edit?usp=sharing
  [5]:https://www.jetbrains.com/webstorm/
  [6]:http://brackets.io/
  [7]:https://code.visualstudio.com/
  [8]:https://codepen.io/
  [9]:https://c9.io/
  [10]:https://www.mamp.info/en/
  [11]:https://www.youtube.com/user/elithecomputerguy
  [12]:https://www.youtube.com/user/shiffman
  [13]:https://www.coursera.org/specializations/algorithms
  [14]:https://www.freecodecamp.com/challenges/truncate-a-string
