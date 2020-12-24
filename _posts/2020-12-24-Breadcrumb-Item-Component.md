---
date: 2020-12-24 21:27:20
layout: post
title: Breadcrumb Item Component
subtitle: Breadcrumb navigation for your dashboard pages
description: A handy navigation component which allows simple navigation of your dashboard pages. This component requires 2 modules
image: https://www.eebew.com/wp-content/uploads/2015/03/breadcrumbs-seo-710x400.png
optimized_image: https://www.eebew.com/wp-content/uploads/2015/03/breadcrumbs-seo-710x400.png
category: Component
tags:
  - Breadcrumb
  - Navigation
  - Link
  - Custom
  - Component
author: psdevuk
---

## Welcome

Happy Christmas Eve to you all, well just chilling with my kids watching some netflix, and trying to prove my man powers and multi-task.  So apart from wishing you a very merry Christmas, I thought I should also write this blog about a component I have recently released to the powershell gallery.
[Please remember you to can also build cool looking custom components like this one, by buying my course on how to create custom components here](https://psdevuk.github.io/ud-flix/Video-Course-With-Me/)

## What Does This Components Do?

Adds a navigation menu showing the user the current page they are on, and other pages on your dashboard the user could navigate to. 

![placeholder](https://github.com/psDevUK/UDBreadCrumb/blob/main/Breadcrumb.PNG?raw=true "Simple Demo")

## Why Build This Component Then?

Saw this raised a while back on the UD forums that a fewllo UD dashboarder user was trying to develop their own Breadcrumb component, and well, quite simply I thought this was be a really good addition to the marketplace, as I had not seen it appear on the marketplace. 

### Please note you need both modules for this to work, just like for the Step Progress Bar component

### You need the Breadcrumb module and BreadcrumItem module both installed for this to work

# Demo 
```
    New-UDBreadcrumb -Id "BreadcrumbExample" -Content {
        New-UDBreadcrumbItem -Link "/Example"-LinkText "Example" -Icon "helicopter" -Active $true
        New-UDBreadcrumbItem -Link "/Home" -LinkText "Home" -icon "home"
        New-UDBreadcrumbItem -Link "/Links" -LinkText "Links" -icon "address_book"

    }
```

You will have to add this to each page you want the breadcrumb component to be displayed upon, but put the link to the page you are currently on as the first link in the list to get it to appear blue as active.  So for the home page it would be
```
New-UDPage -Name "Home" -Icon home -Content {
    New-UDBreadcrumb -Id "BREADCRUMB" -Content {
        New-UDBreadcrumbItem -Link "/Home" -LinkText "Home" -icon "Home"  -Active $true
        New-UDBreadcrumbItem -Link "/Links" -LinkText "Links" -icon "address_book"
        New-UDBreadcrumbItem -Link "/Example" -LinkText "Example" -Icon "helicopter"
    }
    New-UDCard -Title "This is the home page"
}
```

## Again you need both modules for this to work
![placeholder](https://github.com/psDevUK/UDBreadCrumb/blob/main/Breadcrumb.gif?raw=true "Simple Demo")

## Conclusion

Really suprised this has has not been requested by more users. Or that this component didn't make it as an official UD or PU component. I mean it is used on so many websites, and I think for the silver surfer user makes it a lot easier to navigate around your dashboard pages. I hope after reading this blog you realise you need both the **Breadcrumb** and **BreadcrumbItem** **modules** for this component to work correctly. I hope this is a nice Xmas stocking gift component for your dashboard and wishing you a very merry Christmas.
