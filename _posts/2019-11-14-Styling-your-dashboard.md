---
date: 2019-11-14 08:17:40
layout: post
title: Styling your dashboard
subtitle: Learn how to modify the look and feel of your dashboard.
description: Find out how you can pimp your dashboard to look the mutz nutz.
image: https://s15.postimg.cc/j1lqkbmjv/materialize.png
optimized_image: https://s15.postimg.cc/j1lqkbmjv/materialize.png
category: Theme
tags:
  - customize
  - style
  - css
author: psdevuk
---

> As powershell universal dashboard is built on Materialize, which is a UI component library created with CSS, JavaScript, and HTML. Materialize UI components help in constructing attractive, consistent, and functional web pages and web apps.

## Read the documentation

As always I advise reading the <a href="https://docs.universaldashboard.io/look-and-feel/themes">official documentation on themes</a>

## Predefined Themes

Powershell universal dashboard does come with a good few themes to choose from eight at the time of writing this blog. So how do I know about these eight different themes? Simple just run `Get-UDTheme` to display a list of all the themes to choose from

## Applying a theme

So lets decide you want to apply the power of green to your new dashboard. You can simply create a `$theme` variable then place the theme in that variable, then apply that variable as the theme to your dashboard like:-

```js
$theme = Get-UDTheme 'Green'
$Dashboard = New-UDDashboard -Title "TEST DASHBOARD" -Theme $theme -Content {
      New-UDHeading -Text "Hello, World!" -Size 1
}
Start-UDDashboard -Dashboard $Dashboard -Port 10001
```

This will now apply the **green** theme to my dashboard

## CSS

Cascading style sheet is the underlying code that styles the component on the dashboard page. Thankfully the following are predefined CSS classes and attributes have been done for you

- UDDashboard
- UDNavBar
- UDFooter
- UDCard
- UDChart
- UDCounter
- UDMonitor
- UDGrid
- UDTable
- UDInput

This allows you to style any of the above components easily

```js
$theme = New-UDTheme -Name "Basic" -Definition @{
  UDDashboard = @{
      BackgroundColor = "rgb(255,255,255)"
      FontColor = "rgb(0, 0, 0)"
  }
}
$Dashboard = New-UDDashboard -Title "TEST DASHBOARD" -Theme $theme -Content {
      New-UDHeading -Text "Hello, World!" -Size 1
}
Start-UDDashboard -Dashboard $Dashboard -Port 10001
```

So the above code styles the background colour and the font colour used throughout your dashboard.

## Styling components not predefined?

Unless your a CSS pro then like me you probably will not have a clue what the underlying class name is for the CSS to style. Thankfully modern browsers are a big help these days. I use firefox most of the time, but the same method applies to google chrome and internet explorer. So find something you want to style on your dashboard, right click on that component and choose **inspect element** this will open the browser tools normally from the bottom of the page.

Hovering your mouse over the code, should highlight the object on the page, once you are happy the correct component is highlighted click on the code, and then you will see the related CSS code for that component and seeing how it is styled.

To keep things basic say you want to apply a rounded edges to all your images you are displaying, we could modify the previous code to include

```js
$theme = New-UDTheme -Name "Basic" -Definition @{
  UDDashboard = @{
      BackgroundColor = "rgb(255,255,255)"
      FontColor = "rgb(0, 0, 0)"
  }
  'img' = @{
        'border-radius' = "8px"
    }
}
$Dashboard = New-UDDashboard -Title "TEST DASHBOARD" -Theme $theme -Content {
      New-UDHeading -Text "Hello, World!" -Size 1
}
Start-UDDashboard -Dashboard $Dashboard -Port 10001
```

You may find that your custom theme may end up spanning hundreds of lines of code. I always like to store all my dashboard pages as separate .PS1 files which I load within the main dashboard page.

Here is a small code sample of what it would take to modify the **tabs** via `New-UDTab` within powershell universal dashboard

```js
$Theme = New-UDTheme -Name "Basic" -Definition @{
  '.tabs .tab a:hover'= @{
  'background-color' = "#557583"
  'color'= "#ffffff"
 }
 '.tabs .tab a.active'  = @{
  'background-color' = "#2c505f"
  'color'= "#ffffff"
 }
 '.tabs .tab a:focus.active'  = @{
'background-color' = "#1e353f"
  'color'= "#ffffff"
 }
 '.tabs .indicator'  = @{
  'background-color' = "#fff"
 }
 '.tabs .tab a' = @{
  'color' = "#fff"
 }
}
```

## Pick and Mix

As powershell universal dashboard is so flexible you have the ability to pick and mix the modified theme you have created into one of the predefined themes.

So if you like everything in the DarkDefault theme apart from the font and background colour then you can create a hybrid theme of your own

```js
$theme = New-UDTheme -Name "Basic" -Definition @{
  UDDashboard = @{
      BackgroundColor = "rgb(255,255,255)"
      FontColor = "rgb(0, 0, 0)"
  }
  'img' = @{
        'border-radius' = "8px"
    }
} -Parent "DarkDefault"
$Dashboard = New-UDDashboard -Title "TEST DASHBOARD" -Theme $theme -Content {
      New-UDHeading -Text "Hello, World!" -Size 1
}
Start-UDDashboard -Dashboard $Dashboard -Port 10001
```

## Conclusion

It took me a good number of hours to figure out how to create my own custom themes, and even more time trying to figure out using inspect element within the browser. But once these things clicked for me, I was even able to contribute my own DarkRounded theme and Azure theme to the universal dashboard project. This really does go to show you can go from zero to hero if you put the time in to learn. I hope this helps you in your journey with powershell universal dashboard to become a better dashboarder.
