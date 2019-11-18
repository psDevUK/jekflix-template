---
date: 2019-05-12T19:17:18.000Z
layout: post
title: How layouts work in Universal Dashboard
subtitle: This blog covers the various choices you have when it comes to designing the layout of your dashboard.
description: >-
  Blog covering the various layout design aspects of Powershell Universal Dashboard. Giving code example and explanations as well as links to essential youtube videos to get you started.
image: >-
  https://miro.medium.com/max/3009/1*hUNl8wHt7o0Cr281TOzW6Q.png
optimized_image: >-
  https://miro.medium.com/max/3009/1*hUNl8wHt7o0Cr281TOzW6Q.png
category: Layout
tags:
  - layout
  - design
  - grid
author: psdevuk
paginate: true
---

Thanks for landing on my second blog page. This blog I will cover the various ways you can layout the design of your dashboard. Powershell universal dashboard gives you several choices on how to construct your layout. As always this is <a href="https://docs.universaldashboard.io/components/formatting#formatting-with-layouts">well documented</a> on the official documentation website.

> We are using a standard 12 column fluid responsive grid system. The grid helps you layout your page in an ordered, easy fashion.

## New-UDLayout

This command will automatically divide your page for you equally. So the below example would split my page into **three** equally sized columns spanning the entire page. Each of those columns would contain one **card** component.

```js
New-UDLayout -Columns 3 -Content {
    New-UDCard
    New-UDCard
    New-UDCard
}
```

This is probably the easiest to use layout design to use if you just want to do things in minimal time, as long as you display the number of components to the number of columns defined you will get the desired results.

--page-break--

## Formatting with Rows and Columns

I now use this method when designing my dashboard layouts, however it did take me a few attempts for it to become my preferred method. This method requires two commands, the `New-UDRow` command and the `New-UDColumn` command. This method does provide you with customising the size of your own columns, as well as being responsive to the size of the screen the end-user of your dashboard is using. You must understand **12 is the magic number** as in the previous `New-UDLayout` method where we divded three equally sized columns would have to be written like this:-

```js
New-UDRow -Columns {
    New-UDColumn -Size 4 {
}
    New-UDColumn -Size 4 {
}
    New-UDColumn -Size 4 {
}
}
```

As well as being able to define the size, you can also use the following parameters to decide the size of the column depending on the size of the screen `-SmallSize <Int32>` `-LargeSize <Int32>` `-MediumSize <Int32>` to give you further control, you can even apply indents aka offsets on your columns using the following parameters `-SmallOffset <Int32>` `-MediumOffset <Int32>` `-LargeOffset <Int32>`

You have probably noticed yourself that when you visit the same website on a mobile device compared to a PC/Laptop that the website is displayed differently. This is how that technique is achieved. So using this method to layout the design of your dashboards really does give you the greatest control of how your dashboard will display for different sized device screens being used to access your dashboard.

Find out the final method for designing your layout next...

--page-break--

## Grid Layout

This final method of designing your layout even allows you to let the end-user of your dashboard re-arrange the dashboard layout. I have used this method on designing a really complex layout, as I paid for the premium version there was a tool which was designed to allow you to do **drag and drop** design.

The `New-UDGridLayout` uses JSON to display the layout. Which can be complex, thankfully the premium version has a tool allowing you to edit the page to make it look like what you want, then it gives you all the complicated JSON code behind the layout. To build a simple layout using this method, that will have the cards stacked until ordered would be:-

```js
New-UDGridLayout -Content {
    New-UDCard -Title "Card 1" -Id 'Card1'
    New-UDCard -Title "Card 2" -Id 'Card2'
    New-UDCard -Title "Card 3" -Id 'Card3'
}
```

You may have noticed that these card components have been given a `-Id` name which has to be unique for each component. This has to be unique as it allows you to get extra information from the component if the state or props of that component should change.

As mentioned if you purchase the premium version of the product you get something called **Admin Mode** which allows you to copy the contents of the JSON layout to the clipboard then paste in your code, so you have that awesome layout you just spent the time dragging and dropping to design. There is also
<a href="https://www.youtube.com/watch?v=vkh8wgm3JJY">a great youtube video</a> that Adam Driscoll presented showing you how to use this drag and drop capability in powershell universal dashboard.

## Other video resources

If like me you think you learn something quicker by watching it in action then there is another <a href="https://www.youtube.com/watch?v=QnqDnaoV8q0">youtube video on layouts</a> as well as having numerous dedicated videos to certain subjects, I recommend you <a href="https://www.youtube.com/watch?v=6nPGEIFqlXw">watch the start to finish</a> **powershell dev ops 2019** presentation Adam Driscoll did, as this is a great breakdown of the product and what it can do.
