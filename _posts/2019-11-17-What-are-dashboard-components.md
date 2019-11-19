---
date: 2019-11-17 12:26:40
layout: post
title: What are dashboard components?
subtitle: Explaining what a component is and how they are their own object on the webpage.
description: Explaining what a react component is and how they allow you to build awesome looking sites that allow the user to interact with the site.
image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQKgZWObQbHhYnUBO-vyA6T_CAtIfyjfSsbIZ_BK8m4b6XgypoRsg&s
optimized_image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQKgZWObQbHhYnUBO-vyA6T_CAtIfyjfSsbIZ_BK8m4b6XgypoRsg&s
category: Component
tags:
  - component
  - runspace
author: psdevuk
paginate: true
---

So way back when the internet was first about, the whole web page was just rendered as a single component. So pressing the F5 key would reload the page and everything on the page which was being treated as one big object

> Facebook changed the way webpages displayed with using React which is a JavaScript library for building user interfaces. It is maintained by Facebook and a community of individual developers and companies.

So using react technology on web pages allows the webpage to be rendered as many different objects instead of one big webpage. This allows the webpage to load quicker, be more responsive and interactive.

As well as these components being their own object, some components allow you to also define their own endpoint. This will then run the task in the powershell runspace. Exactly like when you run powershell jobs for long running tasks. This means other components can load without having to wait on a particular component to load.

## Always read the documentation

As always I would advise you to go to the official documentation page where
<a href="https://docs.universaldashboard.io/components">components</a> have been described in depth.

## See it in action

To get a physical feel for the powershell universal dashboard components, and what they do, or what type of information they can display or data they can contain <a href="https://poshud.com/">head over to poshud</a> which is a site Adam Driscoll constructed that is actually running powershell universal dashboard. So what you see here is what you get when you are using the product. It blows my mind everytime thinking that all this graphical awesomeness can be displayed by using just powershell.

## Github Page For Universal Dashboard

If you are a bit geeky or looking to contribute to the project then as this project is open source you can see the react which <a href="https://github.com/ironmansoftware/universal-dashboard/tree/master/src/UniversalDashboard.Materialize/Components">makes the components what they are</a> on the **github page**. Then the corresponding powershell scripts that you are running as functions within the module are located <a href="https://github.com/ironmansoftware/universal-dashboard/tree/master/src/UniversalDashboard.Materialize/Scripts">right here</a>

## Default component theme

Materialize is the default theme and components you will be using. There is however also a MaterialUI library built into powershell universal dashboard. Although they are similar components, some are new components like the **chips** component.

## Custom components

On top of having oodles of components to choose from. You also have the ability to create your own custom component for powershell universal dashboard. Honestly this product is so flexible with high

<!--page-->
