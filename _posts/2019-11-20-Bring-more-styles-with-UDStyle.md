---
date: 2019-11-20 22:10:40
layout: post
title: Bring more styles with UDStyle
subtitle: Find out how to multi-style the same object being displayed
description: Short blog post about a dedicated styling component that was released for powershell universal dashboard to add more style to your dashboard.
image: https://github.com/ironmansoftware/ud-style/raw/master/images/logo.png
optimized_image: https://www.wisdomgeek.com/wp-content/uploads/2019/06/emotion-js-730x410.png
category: UDStyle
tags:
  - UDStyle
  - CSS
  - Custom Component
author: psdevuk
---

If you did not know about it, you do now, the <a href="https://marketplace.universaldashboard.io">powershell universal dashboard marketplace</a>, as I have mentioned in previous blogs you can customize so much within this module it's crazy. So to make it even more spectacular Adam Driscoll released this dedicated marketplace which is full of add-ons for your dashboards.

> The powershell universal dashboard marketplace is a great place to find amazing add-on modules, dashboards, controls and tools for your dashboard.

So today I would like to mention one of the particular controls on the marketplace, and this control is **UDStyle**. So what does this do and why am I blogging about it. Please read on to find out.

## UDStyle

In a nutshell this allows the creation of custom **CSS** for your component or HTML object you are displaying on your dashboard. I did mention in my previous blog about how to change the look and feel of your components using a custom or pre-defined theme for your dashboard, or a pick and mix of both. But a theme being a theme will style all the components the same style defined in the theme.

So this is where **UDStyle** takes over, and allows you to style say one card different to the other themed cards on your dashboard. You could apply this same technique to any other components you are using on your dashboard.

## Code

So to show this in action I will be using the default example given on the description for the custom control **UDStyle**

```js
New-UDStyle -Style '
    padding: 32px;
    background-color: hotpink;
    font-size: 24px;
    border-radius: 4px;
    &:hover {
      color: white;
    }
    .card {
        background-color: green !important;
    }' -Content {
        New-UDCard -Title 'Test' -Content {
            "Hello"
        }
    }
```

This will display a card that is coloured green, with a hot pink div surrounding the card

![placeholder](https://raw.githubusercontent.com/ironmansoftware/ud-style/master/images/screenshot.png "Example")

## Conclusion

So if you want to apply a different look and feel to one drop down menu to another exisiting drop down menu, then **UDStlye** is the control you will need to use to achieve this. I hope this helps you out in your future dashboard projects.
