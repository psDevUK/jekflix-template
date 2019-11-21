---
date: 2019-11-21 22:10:40
layout: post
title: Creating Custom Components
subtitle: Going over the principal of creating custom components
description: This blog covers creating custom components, take your dashboards to the next level and build a control you specifically require.
image: https://www.makodesign.com/wp-content/uploads/2018/12/invention.jpg
optimized_image: https://www.burrosabio.net/wp-content/uploads/Invento-500x277.jpg
category: Custom
tags:
  - custom
  - component
  - idea
author: psdevuk
---

## Custom Components

There are so many cool things about Powershell Universal Dashboard. One of those many cool things is the ability to build custom components for Universal Dashboard. What does this mean exactly?
Well say you wanted to be able to include a parallax image on your dashboard, this component does not exist out of the box with UD. However it does exist on a website like <a href="npmjs.com">npmjs</a> you can then use the code provided on that website along with the universal dashboard template for building custom controls which is located here on <a href="https://github.com/ironmansoftware/ud-custom-control-template">github</a>

Adam Driscoll the creator of Universal Dashboard was even kind enough to put a youtube video together which explains this process in more detail <a href="https://www.youtube.com/watch?v=5lu1eDzfRK8">here</a> so I **highly recommend you watch this video** several times, then get ready to build something.

So I have built quite a few custom components now for universal dashboard. So I thought it would be worth showing some of these off in this blog. I have created a repository for each of these custom components I built on my github page <a href="https://github.com/psDevUK/psUniversalDashboard">located here</a>

One of the first components I built was something so simple, and great for filling a blank space on your dashboard, yes the react kawaii component:-

![Ghost]({{site.baseurl}}/assets/img/ghost.jpg "Spooky right")

I used the kawaii cup and ghost in one dashboard I am using, these really do a great job of just filling some space on your dashboard.

As mentioned near the top of the page, the parallax effect was something I was after ever since I got using UD I wanted to be able to apply this effect on images on my dashboard. So I managed to pull this off and here is an example of the parallax component I built for UD:-

![Parallax]({{site.baseurl}}/assets/img/parallax.gif "nice parallax effect")

One day on the UD forums which is a great place to communicate with other dashboard users. A user requested more icons to use within UD.

I mean UD comes with loads and loads of icons the font awesome and line awesome icon sets, so I mean there is thousands to choose from. I guess human nature you always want more.

As they made a movie the other year about them, I thought what better icons to bring to UD the mighty emoji icons you see absolutely everywhere. To try and bring some more life to my dashboard pages I like to do something like:-

![Emoji]({{site.baseurl}}/assets/img/emoji.gif "example")

One evening when I was round a friends house, he showed me this website he had been working on, and had applied an image effect to the images on the website. This made me think, there was currently no image effects to apply to images within UD. So I made it my mission to change that, so I stumbled upon a react component that had over 30 different image effects to choose from. So I thought what better logo to demonstrate this custom component other than the awesome universal dashboard logo:-

![Image Effect]({{site.baseurl}}/assets/img/udlogo.gif "image effects")

My next component was inspired by a post in the UD forums. one user was showing how they created a custom loading component before the component loaded. I thought this was a neat solution as not all the components within UD have auto loaders built into them, some do but some don't. I liked the approach that was used to created this custom loader, apart from it was relying on a GIF from the internet. So there are a couple of loaders built into UD, like the circle spinner, and the bar loader. However I was looking for a bunch of different loaders. So I managed to find a react component that had a stupid amount of loading spinners to choose from. I asked for help on how to dynamically load the specified spinner into the import within react on the UD forums. I was so happy when Adam Driscoll gave me a method to do this. So then next was to publish it on the powershell gallery, here is a few of the many spinners available in the module:-

![Spinners]({{site.baseurl}}/assets/img/spinners.gif)

The graphs and charts are the main reason I purchased UD, as I was blown away by the selection, and customisation you could do, and there is no other application I know of, or uses powershell to produce such amazing charts and graphs. However I was looking for a specific chart component, a percentage pie chart, with the percentage amount in the middle. I have done a complaint dashboard to raise external complaints from customers. So to try and encourage end-users to use it, I could show them the percentage of complaints they have raised on the system, to let them know they are appreciated for using the system. I inlcuded one of my custom spinners to animate whilst the other component is loading:-

![Percentage]({{site.baseurl}}/assets/img/circle.gif)
