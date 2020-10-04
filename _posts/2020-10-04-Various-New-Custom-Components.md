---
date: 2020-10-04 01:12:40
layout: post
title: Various New Custom Components
subtitle: 5 new custom components to blog about.
description: This blog is about 5 new components I built to expand the eco-system of Universal Dashboard. So this will cover each of these new components and how to use them in your dashboard
image: https://newsroom.cisco.com/documents/10157/14740/rubo-10-strategies_round1-Layout.png/f6b8ed0a-22cf-486e-8218-680881c994be?t=1513898202489
optimized_image: https://newsroom.cisco.com/documents/10157/14740/rubo-10-strategies_round1-Layout.png/f6b8ed0a-22cf-486e-8218-680881c994be?t=1513898202489
category: component
tags:
  - Component
  - Skillbar
  - Icons
  - Gallery
author: psdevuk
---

## Welcome

Back for another blog.  This time I will be discussing 5 custom components I have built for UniversalDashboard, what these components are and how to use them. I am not a professional developer, well not by trade, I seem to be involved in anything and everything at work. So although I know these components work, and how to use them, it may not be that apparent to everyone else.  I have tried to do my best in the past when I release a new custom component, I got into the routine of creating a [github repository here](https://github.com/psDevUK?tab=repositories) uploading the module to the repository then creating a README in the repository to explain about the component and how to use it.  However I am now leaning to the idea of simply publishing that information here on my blog site. 


## Simple Icons

[So I stumbled across this super sweet icon pack which is right here](https://simpleicons.org/) and thought this would make a great addition to the current icons UniversalDashboard has. As this icon pack seems to hold a lot of useful icons for the technology sector.
![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/simpleIcons.PNG?raw=true "Sample of website images to select")
 Every icon you see on the website I have built into select from in this component as a validated list in the function.  This is pretty straight-forward to use, here is a demo example I used to prove this works in UniversalDashboard

## Simple Icon Demo and Parameters

```
Import-Module UniversalDashboard
Import-Module UniversalDashboard.UDSimpleIcon

Get-UDDashboard | Stop-UDDashboard

$dashboard = New-UDDashboard -Title "New UniversalDashboard Icon Component" -Content {
    New-UDRow -Columns {
        New-UDColumn -size 4 -Content {
            New-UDSimpleIcon -Icon "Zoom" -Title "We use Zoom" -Size 300 -Color "#F35B04"
        }
        New-UDColumn -size 4 -Content {
            New-UDSimpleIcon -Icon "Microsoftteams" -Title "and MS Teams" -size 300 -Color "#C14953"
        }
        New-UDColumn -size 4 -Content {
            New-UDSimpleIcon -Icon "Powershell" -Title "But this is my favourite" -Size 300 -Color "#090C9B"
        }

    }
}
Start-UDDashboard -Dashboard $dashboard -Port 10005
```
Please note there are a total of **4 different parameters**

- **-Icon** validated string, same as used on the website for the icons
- **-Title** string, for when the user hovers the mouse over the icon
- **-Size** integer value in the demo I set these super large just for demo purposes
- **-Color** string value for the colour of the icon to have applied to it again the website shows a lot of the colours for the icons to match the vendor of the icon


## Tabler Icons

Again I stumbled across a [really nice icon pack located here](https://tabler-icons-react.vercel.app/) and again decided I would like to incorporate these into UniversalDashboard, as you may simply want even more choice and depending what you are working on these icons could tick those boxes for you. 
![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/tablerIcons.PNG?raw=true "Sample of website images to select")
I also learnt a nice neat new trick to formalise the naming of these icons. As these names I got from the website were all seperated by a hyphen and needed to be in camel case. So I stored all the names I gathered from the website then used a foreach loop on these doing `$names | % {(get-culture).Textinfo.ToTitleCase($_)` then I removed the hyphens and was good to go.

## Demo of Tabler Icons and Parameters

So here is my demo code I used to prove that this component worked within UniversalDashboard

```
Import-Module UniversalDashboard.Community -RequiredVersion 2.8.1
Import-Module "C:\UD\UDTablerIcons\TablerIcon\src\output\UniversalDashboard.UDTablerIcon\UniversalDashboard.UDTablerIcon.psd1"

Get-UDDashboard | Stop-UDDashboard

$dashboard = New-UDDashboard -Title "New UniversalDashboard Icon Component" -Content {
    New-UDRow -Columns {
        New-UDColumn -size 4 -Content {
            New-UDTablerIcon -Icon "Anchor" -Size 300 -Color "#F35B04"
        }
        New-UDColumn -size 4 -Content {
            New-UDTablerIcon -Icon "Alien" -size 300 -Color "#C14953"
        }
        New-UDColumn -size 4 -Content {
            New-UDTablerIcon -Icon "ThreeDCubeSphere" -Size 300 -Color "#090C9B"
        }
    }
}
Start-UDDashboard -Dashboard $dashboard -Port 10005
```

 Please note with this component there are **only 3 different parameters** to use. 

- **-Icon** string value from a validated set list of all the icons available on the webiste
- **-Size** integer value in the demo I did these super big number to prove it worked
- **-Color** string value to set the colour of the icon you have selected


## SkillBar Component
 
 I always like to try and develop new components that are not already available within UniversalDashboard.  I mean everthing you need to produce amazing looking dashboards comes included with UniversalDashboard. Adam Driscoll did an amazing piece of work making this available to the masses. What was even more amazing, was that he allowed it so other people could contribute and make additional components. So going back to my previous blog on the multi-text-box the forum poster want to get skill sets, so as not component existed for this I thought this would be a great chance to build one. [So I found this really nice looking react component that also had lots of options to customise it](https://crisboarna.github.io/react-skillbars/#globalColoring) I could see this being used for lots of different scenarios when you would like a nice way to show the top percentages of certain things your company may wish you to display on the dashboard you are building. This component uses a 2 dimentional multi array list to populate the data in a script block. Although this isn't super complicated to do, it is always good to have a **read me** on how to do it. **Lets remember what they taught you at school a percentage only goes up to 100** as this uses percentages it is best to keep the numbers you are passing to the component under the 100 threshold

## SkillBar Demo and Parameters

So on the dashboard I decided to test this component on I was using the dark theme, and I just wanted to prove that whatever your dashboard colours you can style this component to match
![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/skillbarIcon.gif?raw=true "Component Demo")
```
Import-Module UniversalDashboard.Community
Import-Module UniversalDashboard.UDSkillBar
Get-UDDashboard | Stop-UDDashboard
$theme = get-udtheme "DarkRounded"
$dashboard = New-UDDashboard -Title "New-UDSkillBar" -theme $theme -Content {
    New-UDRow -Columns {
        New-UDColumn -size 5 -Content {
            $Processes = get-process | select Name, CPU | sort -Descending CPU | select -first 10
            $hash = @()
            foreach ($item in $Processes) {

                $hash += @{
                    type  = $item.Name
                    level = $item.CPU
                }
            }
            New-UDSkillBar -Skills { $hash } -BackgroundColor "#22181C" -BarColor "#7D7878" -AnimationDuration 4000
        }
    }
}

Start-UDDashboard -Dashboard $dashboard -Port 10006
```
So as you can see in the demo code above, when passing the hash array you need a **type** which is a **string value** and you also need **level** which must be an **integer value under 100** you can use the method above to grab a csv file, or sql query and pass the data into the array as shown above. 
 Please look through the default parameters
```
[Parameter()]
        [scriptblock]$Skills,
        [Parameter()]
        [string]$BarColor = "#0C6291",
        [Parameter()]
        [string]$TextColor = "#FBFEF9",
        [Parameter()]
        [string]$BackgroundColor = "#A63446",
        [Parameter()]
        [int]$AnimationDelay = 3000,
        [Parameter()]
        [int]$AnimationDuration = 7000,
        [Parameter()]
        [int]$Height = 30
```
  So any of the above parameters can be tweaked to match your colour scheme on your dashboard.


## UDPlayer
 Really cannot believe I have not seen this requested on the forums, for like a dedicated mediaplayer for web videos. [I was looking at this component, and was like wow this would be another great edition to UniversalDashboard](https://www.npmjs.com/package/react-player) I could also see being asked in the future to include video clips on a dashboard, so thought let make a dedicated component to do just that. As it was the weekend when I developed this, thought I would blast out some tunes to make sure this component really did work.
![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/UDPlayer.gif?raw=true "Component Demo")
 I was happy enough with the results from my test, this component **only has 3 parameters associated with it**

```
        [Parameter()]
        [string]$URL,
        [Parameter()]
        [string]$Height = "360px",
        [Parameter()]
        [string]$Width = "640px"
```

  So all you really need to do is provide the `-URL` parameter and give it the string of the url of the video you want displayed. If you want to adjust the default height and width you just need to pass in a string value, as the **px** is required. 

## Demo of New-UDPlayer

```
Import-Module -Name UniversalDashboard
Import-Module UniversalDashboard.UDPlayer

Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10004 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 8 -Content {
                New-UDPlayer -URL "https://www.youtube.com/watch?v=yRYFKcMa_Ek&list=RDU7-q1WRaKNg&index=2"
            }
        }
    }
)

```

## UDGallery Component

Just felt I needed to find another component to add to the [UniversalDashboard Marketplace](marketplace.universaldashboard.io/) to make my evening complete. [Then I found this beautiful looking component I couldn't take my eyes off](https://benhowell.github.io/react-grid-gallery/) although I did start having second thoughts, as it only listed two dependencies, but one of them required a load more. Just to show how much more...
```
prop-types
resize-observer-polyfill
loose-envify
object-assign
react-is
js-tokens
a11y-focus-store
cross-env
glam
html-react-parser
raf-schd
react-focus-on
react-full-screen
react-transition-group
react-view-pager
react-images
cross-spawn
path-key
shebang-command
which
fbjs
inline-style-prefixer
@types/htmlparser2
html-dom-parser
react-property
style-to-object
aria-hidden
react-focus-lock
react-remove-scroll
react-style-singleton
use-callback-ref
use-sidecar
shebang-regex
isexe
css-in-js-utils
core-js
cross-fetch
fbjs-css-vars
loose-envify
object-assign
promise
setimmediate
ua-parser-js
hyphenate-style-name
@types/domutils
@types/node
domhandler
@types/domhandler
domhandler
htmlparser2
inline-style-parser
aria-hidden
react-focus-lock
react-remove-scroll
react-style-singleton
use-callback-ref
use-sidecar
tslib
@babel/runtime
focus-lock
prop-types
react-clientside-effect
use-callback-ref
use-sidecar
react-remove-scroll-bar
react-style-singleton
tslib
use-callback-ref
use-sidecar
get-nonce
invariant
detect-node-es
domelementtype
domhandler
domutils
entities
fscreen
@babel/runtime
dom-helpers
animation-bus
get-prefix
mitt
react-motion
resize-observer-polyfill
tabbable
performance-now
prop-types
raf
```
 All these needed installing to make this component work.  So it took a little while to gather all the things I needed to install.  Please bear this in my if you decide to build some custom components, you need every denpendency listed for the component to work correctly. I try to cut some time, by copying and pasting all the required npm packages into a text file, doing a `Get-Content` of that text file, then doing a foreach loop and using the `Invoke-Expression` to automatically install each package listed in my text file. Else you can spend hours just installing all the required dependencies. Again this component needs a multi-dimension array passing to it as a script block in order for the component to display all the images. 

## Demo of New-UDGallery and Parameters

Firstly I needed a bunch of decent images [I built a component for this using unsplash.com](https://unsplash.com/) so I went to unsplash and put the following images into a text file.
```
https://images.unsplash.com/photo-1579785626622-f7a3f2278048?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1589632555093-c2e95ec00fbd?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1571168878366-104bf4d155c6?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1553954870-e3bd21028735?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1590339360843-b2529666af11?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1592118829208-de1511706a02?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1590339360261-e7f854745e6d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1579729131238-2444987e8de9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1530271899533-f4fd8365a374?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1591337302294-f70bd61f2d3a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1590339361030-63189cfdc8ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
https://images.unsplash.com/photo-1590340429778-3fdd9bc3b1b2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&w=1000&q=80
```
I then compiled the following script
```
Import-Module -Name UniversalDashboard
Import-Module UniversalDashboard.UDGallery

Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10004 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 12 -Content {
                $Images = gc C:\UD\filepath\images.txt
                $hash = @()
                foreach ($item in $Images) {

                    $hash += @{
                        src             = $item
                        thumbnail       = $item
                        thumbnailWidth  = 320
                        thumbnailHeight = 300
                    }
                }

                New-UDGallery -Images { $hash }
            }
        }
    }
)

```
Which then produced this beautiful looking dashboard with ease

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/UDGallery.gif?raw=true "Component Demo")

## Conclusion
 
 Been probably the longest blog I done so far writing all this up.  I hope this also goes to show the dedication put into developing these new components, and that some can take a lot longer than other components to develop. I wouldn't have seen myself being able to do this stuff a few years back, but using UniversalDashboard really does make me believe that anything is possible if you do a bit of research and development you can pull off some really sweet looking components.  It still blows my mind that you can have any amazing looking dashboard and it is all running off of Powershell. 
