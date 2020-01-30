---
date: 2020-01-30 19:26:40
layout: post
title: Cloud Tag Animated Component
subtitle: A component which creates an animated cloud tag display on your dashboard to certainly grab the attention of your end-user.
description: This blog is all about the new cloud tag component I have released for universaldashbord.
image: https://i0.wp.com/ridicurious.com/wp-content/uploads/2019/12/6.png
optimized_image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcShB9lmI0UHEV02eiKKqWjXc9Y6aE7ZU6fXj1I5-nYyJ-us1gbYcA&s
category: component
tags:
  - CloudTag
  - WordCloud
  - Animation
  - component
author: psdevuk
---

## Welcome
It has been a while since my last blog. I cannot believe it is nearly the end of the first month of 2020.  Well I am behind on writing blogs, this is due to a number of things, mainly there not being enough hours in the day.  I have been developing lots of new components, which is partly the reason I am behind on the blogging.  So this blog will cover the CloudTag component I have released, which is as always is
[ available on the universal dashboard marketplace](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDTagCloud).

## Origin Of Component

  Well I saw a blog on twitter about how you could use some modules on the powershell gallery, do something with Azure, then you had an outputted word cloud.  I thought the end result looked cool and it was all done in powershell.  So this got me thinking did a react component exist out there that I could put onto a dashboard?

## CloudTag Demo

 So here is an example of how to actually use the component, the main thing to note, is for every word you want displayed in your cloudtag you need to pump all those words into a hashtable.  Then call that hashtable from a script block.  This is all shown in the demo below.

 ```
Import-Module -Name UniversalDashboard
Import-Module -Name UniversalDashboard.UDTagCloud
Get-UDDashboard | Stop-UDDashboard
$theme = New-UDTheme -Name "Basic" -Definition @{
    'main' = @{
        'padding-left'   = "5px"
        'padding-right'  = "5px"
        'padding-top'    = "5px"
        'padding-bottom' = "5px"
    }
} -Parent "Default"
Start-UDDashboard -Port 1000 -AutoReload -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Theme $theme -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 4 -Content {
                $words = "Powershell", "UniversalDashboard", "Conference", "June 2020", "Adam Driscoll", "Animation", "Dashboards", "Stylish", "Beautiful", "Amazing", "Web Framework", "User Interface", "Europe", "#PSConf"
                $hash = @()
                foreach ($item in $words) {
                    $hash += @{
                        label    = $item
                        fontSize = $(Get-Random -Maximum 5 -Minimum 1)
                        opacity  = $(Get-Random -Maximum 10 -Minimum 3)
                    }
                }

                New-UDTagCloud -data { $hash } -rotate 0 -padding 7 -height "400px" -spiral "archimedean" -timeInterval 6000 -colorarray @('#3772ff','#df2935','#fdca40','#09e85e','#16c172','#172a3a','#004346','#fa7921','#fe9920','#0c4767')

            }
        }
    }
)
 ```

![placeholder](https://raw.githubusercontent.com/psDevUK/Cloud-Tag/master/Demo.gif "example demo")
)

## Further Information
 Please do spend the time to inspect the function of this component, as you will see there are a few paramters to give you extra custom control over the look and feel
- height
- padding
- fontFamily
- rotate
- colorarray
- data
- fontSize
- spiral
- timeInterval

## Conclusion
  This was a fun component to release, and since my company I work for has implemented new core values and got lots of posters up everywhere with the new core values, I thought that these core values would look splendid in a TagCloud and placed on the main landing screen.  Which is now how my dashboard looks.  I hope you also find the space for this component on your dashboard.
