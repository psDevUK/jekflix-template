---
date: 2020-11-28 19:27:20
layout: post
title: Burger Menu Component
subtitle: This is a CSS animated burger menu component for UniversalDashboard
description: This blog covers a brand new component I have built for Universal Dashboard. The blog will cover this new burger menu component and how to add them to your dashboard
image: https://codeclan.com/wp-content/uploads/2020/05/undraw_usability_testing_2xs4.png
optimized_image: https://codeclan.com/wp-content/uploads/2020/05/undraw_usability_testing_2xs4.png
category: component
tags:
  - Component
  - Custom
  - Burger
  - Menu
  - Demonstration
author: psdevuk
---

## Welcome

 Thanks for taking the time to have clicked on the link which brought you to this blog page. So this particular blog covers a component which was requested a while back on the UD forum, however at the time, I didn't think it would be possible. However since having built a few more components since then, I thought I would be able to pull this off. Plus I also saw this component a while back before being requested on the UD forum and thought it would be super amazing to bring to UniversalDashboard.  So this blog will cover this new burger menu component and how to use it.

## Where Did You Find It?

As with pretty much all of the components I build I found this on **npmjs.com** the exact link to the [project can be found by clicking on this link](https://www.npmjs.com/package/react-burger-menu)
 Soon as I saw this burger menu I thought damn this looks so nice, and to move the main page content, just added a wow factor, and with the subtle overlay it's the icing on the cake for me. Although this looked super cool, I just over-thought the process thinking it would be too complicated to implement into UniversalDashboard. So left it on my list of things to do before I die list.  Boom another item has now been checked off of that list.


## So what does it actually do?

This adds a burger navigation menu to the top of the UDNavBar on the dashboard page. You have the ability to place this burger menu anywhere along the top of the main UDNavBar section.  This burger menu has lots and lots of customisation parameters to allow you to fully control the look and feel of not only the burger menu item, but also the animation of how the side menu navigation animates. As well as having the ability to control the side bar menu colours. [You can see this burger menu in action right here on the demo website for this component](https://negomi.github.io/react-burger-menu/) all of the choices on the demo website have all been included in this component, and you can select which animation to use from the ```-Effect``` parameter.

## Another good use for the recent badge link component

So far I have only tested my previous component I released, the badge hyperlink component as the side menu navigation links. I have added a custom CSS to this burger menu component which styles the icons slightly bigger, and default places them on the left-hand-side of the badge link. Although I am not quite yet a silver-surfer I did find the bigger icons look better, and also added some padding to the inner menu to space the badge links better as well as making some CSS adjustments to align the text on the centre level of the icon. Although the badge component was a very simple component, I had big plans for this, and only after seeing this in the newer Powershell Universal and how nice it looked, I wanted to bring it to UniversalDashboard.
  Not to go off on a ramble, but seriously the software the Adam Driscoll has released for Powershell has literally changed the way I script stuff.  Mainly the scripts I write now, produce really elegant looking stylish web-pages and I am not a web-designer, but it just makes Powershell even more awesome than it already is.  And the massive bonus is all your colleagues can view these dashboards and get to see what you can bring to the table for the company you work for.  Being able to statistically display stuff from SQL without having to use Excel is such a time saver for me, being able to produce all the data that is returned into beautiful graphs or tables is just out of this world.
 So Honestly if you have not yet looked at Powershell Universal or UniversalDashboard please do, and help support the developer by buying a licensed copy.

## What Parameters Does It Have?

Well it has a lot of parameters. So many parameters I thought crikey that's a lot of parameters. However as I am a nice person I have given default values to pretty much all parameters so you can use it without specifying each parameter. As there is a lot of parameters, 22 I believe, I have put a comment next to each parameter below to give a basic explanation of what the parameter does. All parameters bar the ```-Links``` and ```-Content``` have default values supplied, or if they don't it is due to it being an additional styling feature that is not required, unless you want the menu on the right side of the page.

```
 param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(), #Sets the Id to refer to component
        [Parameter()]
        [ValidateSet(
            "slide",
            "stack",
            "elastic",
            "bubble",
            "push",
            "pushRotate",
            "scaleDown",
            "scaleRotate",
            "fallDown",
            "reveal"
        )]$Effect = "pushRotate", #animated effect for menu
        [Parameter()]
        [scriptblock]$Links, #provide links for the menu
        [Parameter()]
        [scriptblock]$Content, #Content of dashboard page
        [Parameter()]
        [Switch]$Right, #Will open the menu on the right hand side
        [Parameter()]
        [string]$BurgerMarginLeft, #To position the menu more to the right
        [Parameter()]
        [string]$BurgerBackgroundColor = "#373a47", #Burger menu background
        [Parameter()]
        [string]$BurgerHoverColor = "#a90000", #Burger menu hover color
        [Parameter()]
        [string]$MenuCrossColor = "#bdc3c7", #Cross to close the menu color
        [Parameter()]
        [string]$MenuInnerColor = "#3F51B5", #Inner menu background color
        [Parameter()]
        [string]$MenuOuterColor = "#1B224B", #Outer menu background color
        [Parameter()]
        [string]$MorphShapeFill = "#373a47",
        [Parameter()]
        [ValidateSet("fixed", "absolute")]$BurgerPosition = "absolute", #To scroll with the page or not
        [Parameter()]
        [string]$BurgerTop = "16px", #Top margin for burger menu
        [Parameter()]
        [string]$BurgerWidth = "36px", #Sets width of the burger menu
        [Parameter()]
        [string]$BurgerHeight = "30px", #Sets height of the burger menu
        [Parameter()]
        [string]$BurgerLeft = "36px", #Determines how far left of the page to display burger menu
        [Parameter()]
        [string]$Padding = "0px 50px 0px 50px", #Padding for the main content of the page
        [Parameter()]
        [string]$MenuMarginLeft = "-50px", #Allows you to set the left margin of the menu
        [Parameter()]
        [string]$MenuMarginRight, #Allows you to set the margin right of the menu
        [Parameter()]
        [string]$MenuMarginBottom = "-20px", #Prevents little gap at the bottom of the page
        [Parameter()]
        [decimal]$BurgerOpacity = 1 #Visibility of the button 0 sets it to invisible
    )
```
  The JSX file which I had to create to make this component is I think one of my most longest typed out JSX files, as the documentation for this component is super good, but it doesn't explain how to dynamically change the effect, and I didn't want to be releasing numerous animated burger menus, so although I have previously used a technique in the [UDSpinner component I released](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDSpinner) to dynamically load the selected loader from the given parameter. However this component uses HTML tags, so I needed to find a different method of how to achieve a dynamic HTML tag from a component.  I also had the issue of trying to figure out how I could dynamically pass hyperlinks into the menu. Thankfully having built so many different components, I could look back on some previous projects for guidence.  Ultimately I found something on github to do the dynamic HTML tag and figured I could use the same technique on the content parameter for the links parameter. I also created another separate CSS file to style the dashboard, and again I had to mess with the **main** CSS tag to get the menu to display correctly, but corrected the padding on the left and right in the div that now holds the main content which you can adjust using the **Padding** parameter as shown above. As well as using an external CSS there is a load of CSS that can be dynamically styled from the JSX file, hence so many parameters in this component, as everyone has different coloured dashboards, I wanted to give as much control as I could to the end user on how to style the menu.


## Example Using The Component

Before I go straight into an example, I just want to point out I was super chuffed to have got this working and although this component only lists it has 5 dependencies, it actually requires you to download all the following dependencies:-
```
browserify-optional
classnames
eve
prop-types
snapsvg-cjs
react-burger-menu
ast-transform
ast-types
browser-resolve
snapsvg
through
esprima
escodegen
tslib
resolve
is-core-module
path-parse
estraverse
esutils
esprima
optionator
source-map
has
function-bind
prelude-ls
deep-is
word-wrap
type-check
levn
fast-levenshtein
type-check
fastest-levenshtein
```
 Although I thought I had covered my basis, I had not checked if I could open the burger menu via a button on the page, as displayed in the demo of this component [which if you didn't check the project page they have a live demo for this component here](https://negomi.github.io/react-burger-menu/) so sadly this didn't work, so I revisited my JSX file and tweaked it, adding some additional lines of code from a previous component to make sure the STATE of the component could be read from UniversalDashboard. After I had made the changes, and [thankfully this component had some really nice documentation on what I needed to change](https://github.com/negomi/react-burger-menu/wiki/FAQ#i-want-to-control-the-open-state-programmatically-but-i-dont-understand-how-to-use-the-isopen-prop) I could open the menu from a button embedded in the dashboard page. So now I realy do think I got all my basis covered for using this component.  Well I said it last time as I got older I do find it best to read the instructions, or at least skim through them.  So thought it would be good to show a small demo of this component in use, because again it is making you design your dashboard a bit differently to normal as this component will have to be embedded in each page you want to actually display it on.  Despite the complexity of this component, and everything that is included techinically speaking 10 different components, the entire build came to 8.79kb so the performance impact should be minimal:-

```
Import-Module -Name UniversalDashboard
Import-Module -Name UniversalDashboard.UDBadgeLink
Import-Module -Name UniversalDashboard.UDBurger

Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Content {
        New-UDBurger -Id "BURGER_MENU" -Effect scaleRotate -BurgerBackground "#fff" -Links {
            New-UDBadgeLink -Text "Other thing page" -TextColor "#fff" -Link "/other" -HoverText "Other Thing"  -BadgeTextColor "#fff" -BadgeCount 23 -Icon home -MaxNumber 40
            New-UDBadgeLink -Text "Some thing page" -TextColor "#fff" -Link "/some" -HoverText "Some Thing" -BadgeTextColor "#fff" -BadgeCount 52 -Icon react -MaxNumber 40
            New-UDBadgeLink -Text "Click thing page" -TextColor "#fff" -Link "/click" -HoverText "Click Thing"  -BadgeTextColor "#fff" -BadgeCount 7 -Icon rainbow -MaxNumber 40
        }  -Content {
            New-UDRow
            New-UDHeading -size 6 -Text "Some random text"
            New-UDRow
            New-UDHeading -size 6 -Text "Some random text"
            New-UDButton -Text "Open Menu" -OnClick {
                Set-UDElement -Id "BURGER_MENU" -Attributes @{menuOpen = $true }
            }
            New-UDRow
            New-UDImage -Url "https://miro.medium.com/max/1190/1*8QgPF5tXwo5NqhvXXncwSQ.png"
            New-UDRow
            New-UDHeading -size 6 -Text "Some More random text"
            New-UDRow
            New-UDHeading -size 6 -Text "Some More random text"
        }

    }
)

```

## Which Gives You This

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/burgerDemo.gif?raw=true "Component Demo")

  Which is now super cool to have a side menu that can be triggered via a button, I mean I included an ```-BurgerOpacity``` parameter and setting that to 0 would make the burger menu invisible, so if you have some anti-burger-menu users you could now please them with a button that says **MENU** on it to save any confusion for the end-user. I could have made this blog super huge just showing how all the different parametes can be used to give different effects but I will leave that to you to test out, as I have given basic informaiton using comments to give a brief description what each parameter does. If you still unsure let me know, and will type it in more detail with an example.

## Conclusion
Although I saw this component a really long time ago, I never got round to building it, as I didn't believe I had the necessary skills required to do this, and like most things in life I just think I over-thought, and over-complicated this before I even got started so never got started.
Although having built a working sticky top nav bar which I thought looked super cool, gave me the encouragement I needed to get round to re-looking at this component and actually having a go of building it. Even whilst typing this blog I found another 4 parameters to add, to give more custom control over the menu. I think I need to stop else I will have too many parameters I feel. This was a really cool component to build as I learnt so new tricks, makes me think about rebuilding the NoAvatar component and add the CSS styling dynamically, like what is being done in this component.
  Anyways thanks for taking the time to read this blog, and hopefully this component will find its way to your dashboard you are building.
[You can download this component from either the powershell gallery or the universal dashboard marketplace](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDBurger)  
