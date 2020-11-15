---
date: 2020-11-14 22:05:20
layout: post
title: Animate SVG Component
subtitle: Fancy SVG animation from SVG path
description: This blog covers a brand new component I have built for Universal Dashboard. The blog will cover this new SVG animation component and how to add it to your dashboard
image: https://www.lapa.ninja//assets/blog/Free-Illustrations-Library-For-Your-Project-Feature.svg
optimized_image: https://freewebillustrations.com/static/images/intro.svg
category: component
tags:
  - Component
  - SVG
  - Path
  - Animation
author: psdevuk
---

## Welcome

 I wasn't expecting to be blogging again so soon, but I have recently published 4 new powershell modules to the powershell gallery, and this is the 4th module, but I figured this could to with a bit of explaining.

## Where Did You Find It?

As with most of the components I build I found this on **npmjs.com** the exact link to the [project can be found by clicking on this link](https://www.npmjs.com/package/react-mt-svg-lines) I saw this component a long-time ago, but just never got round to building it.

## What Parameters Does It Have?

Well if you have a butchers at the original project on npmjs I have included each **prop** as a powershell parameter:-

```
 param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [int]$Duration = 3000,
        [Parameter()]
        [string]$ViewBox = "0 0 20 20",
        [Parameter()]
        [string]$Stroke = "black",
        [Parameter()]
        [decimal]$StrokeWidth = 0.2,
        [Parameter()]
        [string]$Fill = "none",
        [Parameter()]
        [string]$d = "M17.431,2.156h-3.715c-0.228,0-0.413,0.186-0.413,0.413v6.973h-2.89V6.687c0-0.229-0.186-0.413-0.413-0.413H6.285c-0.228,0-0.413,0.184-0.413,0.413v6.388H2.569c-0.227,0-0.413,0.187-0.413,0.413v3.942c0,0.228,0.186,0.413,0.413,0.413h14.862c0.228,0,0.413-0.186,0.413-0.413V2.569C17.844,2.342,17.658,2.156,17.431,2.156 M5.872,17.019h-2.89v-3.117h2.89V17.019zM9.587,17.019h-2.89V7.1h2.89V17.019z M13.303,17.019h-2.89v-6.651h2.89V17.019z M17.019,17.019h-2.891V2.982h2.891V17.019z"

    )
```

As you can see I have provided default values for each parameter so if you just specify the name of the module then this will show a 5 second animated bar-chart icon. However I am assuming that most users will want to animate their own choice of SVG graphic. Well this blog will cover how to achieve this. So [this is the first link for some SVG icons](http://svgicons.sparkk.fr/) and [I even made a component for this icon library](https://simpleicons.org/) which has so many amazing icons, opening the SVG image in your browser then right clicking on the image and selecting **inspect element** this will then show you a ```<path>`` tag inside this tag there is a ```d="``` which shows the path of the SVG. This is what is needed to make the SVG animated on your screen. You also need to make a note of the **viewBox** to get the proper dimensions for the SVG you want to display. As these are SVG they will look just as clean in a size 12 container as a size 1 container, thats the beauty of SVGs. Finally I [found this website hosting SVG graphics](https://www.svgrepo.com) which I found a nice looking Batman SVG logo which I opened in my FireFox browser inspected the element and got the **d** tag for the vector paths of the SVG and the **viewBox** for the dimensions. 

## Example Using The Component

So after waffling on about this component, it is time to show it on a dashboard so here is a bunch of SVG icons that will nicely animate just the once, till they show the completed SVG. 

```
Import-Module -Name UniversalDashboard.Community -RequiredVersion 2.8.1
Import-Module "C:\UD\WalkWay\AnimateSvg\src\output\UniversalDashboard.AnimateSvg\UniversalDashboard.AnimateSvg.psd1"
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 3 -Content {
                New-AnimateSvg -ViewBox "0 0 213.167 213.167" -StrokeWidth 0.9 -duration 10000 -d "M106.583,167.873c-28.275,0-54.889-6.26-74.938-17.625C11.239,138.678,0,123.172,0,106.583s11.239-32.095,31.646-43.664  c20.049-11.366,46.663-17.625,74.938-17.625c28.276,0,54.889,6.26,74.938,17.625c20.407,11.569,31.646,27.076,31.646,43.664  s-11.238,32.095-31.646,43.664C161.473,161.614,134.859,167.873,106.583,167.873z M106.583,49.294C50.019,49.294,4,74.994,4,106.583  c0,31.59,46.019,57.29,102.583,57.29s102.583-25.7,102.583-57.29C209.167,74.994,163.148,49.294,106.583,49.294z M106.584,152.017  c-0.857,0-1.619-0.546-1.895-1.357c-1.904-5.609-8.217-20.886-14.479-24.175c-2.021-1.062-3.857-1.6-5.457-1.6  c-2.834,0-4.435,1.683-5.604,2.911l-0.326,0.34c-1.648,1.688-4.735,5.793-4.766,5.834c-0.359,0.479-0.915,0.77-1.512,0.796  c-0.599,0.031-1.177-0.217-1.576-0.663c-0.088-0.097-8.854-9.76-17.168-9.835l-0.137,0c-2.721,0-4.726,0.75-5.958,2.23  c-2.114,2.539-1.581,6.52-1.367,7.68c0.81,4.398,4.182,10.027,4.216,10.083c0.44,0.73,0.369,1.658-0.176,2.313  c-0.545,0.655-1.445,0.892-2.243,0.591c-1.285-0.485-31.527-12.151-35.551-36.035c-2.75-16.321,8.916-31.372,32.849-42.38  c8.49-3.906,22.902-7.795,23.512-7.958c0.855-0.23,1.764,0.133,2.226,0.89c0.462,0.758,0.37,1.73-0.228,2.387  c-0.463,0.513-11.284,12.715-2.284,22.52c2.735,2.98,6.157,4.555,9.895,4.555c7.319,0,13.888-5.828,14.655-10.842  c1.396-9.113,1.578-21.362,1.58-21.485c0.013-0.902,0.627-1.685,1.501-1.91c0.876-0.226,1.79,0.164,2.237,0.948l4.979,8.75  l3.035-0.061l3.115,0.061l4.979-8.75c0.446-0.783,1.361-1.171,2.236-0.948c0.874,0.225,1.489,1.007,1.502,1.91  c0.002,0.123,0.184,12.372,1.579,21.485c0.769,5.014,7.338,10.842,14.656,10.842c3.739,0,7.161-1.575,9.896-4.555  c9.035-9.842-1.817-22.007-2.283-22.52c-0.598-0.657-0.69-1.629-0.228-2.387c0.461-0.758,1.368-1.122,2.226-0.89  c0.609,0.164,15.021,4.053,23.511,7.958c23.934,11.008,35.6,26.059,32.85,42.38c-4.025,23.884-34.267,35.55-35.552,36.035  c-0.798,0.3-1.697,0.063-2.242-0.591s-0.616-1.583-0.177-2.313c0.034-0.056,3.409-5.699,4.217-10.084  c0.213-1.16,0.745-5.141-1.368-7.68c-1.232-1.479-3.236-2.229-5.957-2.229l-0.136,0c-8.315,0.075-17.081,9.737-17.169,9.835  c-0.399,0.444-0.969,0.692-1.576,0.663c-0.598-0.026-1.153-0.318-1.513-0.796c-0.03-0.042-3.119-4.148-4.766-5.834l-0.325-0.338  c-1.169-1.229-2.77-2.913-5.604-2.913c-1.599,0-3.435,0.538-5.457,1.6c-6.269,3.293-12.577,18.567-14.479,24.174  C108.202,151.471,107.441,152.017,106.584,152.017z M84.753,120.885c2.254,0,4.716,0.692,7.317,2.059  c6.336,3.328,11.771,14.738,14.513,21.439c2.743-6.701,8.176-18.111,14.513-21.439c2.601-1.367,5.063-2.059,7.316-2.059  c4.552,0,7.122,2.704,8.504,4.156l0.288,0.301c1.066,1.092,2.583,2.972,3.686,4.382c3.24-3.12,10.702-9.386,18.438-9.456l0.173,0  c3.964,0,7.002,1.235,9.03,3.67c3.139,3.77,2.604,8.923,2.229,10.964c-0.379,2.059-1.195,4.272-2.045,6.198  c8.579-4.322,25.225-14.637,27.92-30.635c3.104-18.423-14.914-30.877-30.576-38.081c-5-2.3-12.379-4.661-17.395-6.159  c3.579,6.26,5.8,15.43-1.212,23.068c-3.513,3.827-7.954,5.85-12.843,5.85c-8.752,0-17.448-6.653-18.609-14.237  c-0.753-4.914-1.161-10.578-1.38-14.936l-2.074,3.646c-0.363,0.637-1.05,1.051-1.778,1.01l-4.225-0.084l-4.145,0.084  c-0.754,0.033-1.416-0.373-1.778-1.01l-2.074-3.646c-0.219,4.357-0.627,10.022-1.38,14.936c-1.162,7.584-9.857,14.237-18.609,14.237  c-4.889,0-9.329-2.023-12.842-5.85c-7.012-7.639-4.791-16.808-1.211-23.068c-5.016,1.497-12.396,3.858-17.396,6.159  c-15.662,7.204-33.68,19.659-30.576,38.081c2.696,15.998,19.341,26.313,27.92,30.635c-0.849-1.926-1.665-4.14-2.044-6.198  c-0.376-2.041-0.912-7.194,2.227-10.963c2.028-2.436,5.067-3.671,9.032-3.671l0.173,0c7.736,0.07,15.198,6.336,18.438,9.456  c1.103-1.41,2.619-3.29,3.686-4.383l0.29-0.302C77.633,123.588,80.204,120.885,84.753,120.885z"
            }
            New-UDColumn -Size 3 -Content {
                New-AnimateSvg
            }
        }
    }
)

```

## Which Gives You This

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/batman.gif?raw=true "Component Demo")

## Conclusion

 Once again this component is really for the end-user of your dashboards, to look at in amazement, and think wow our I.T person is one cool human being. I thought it looked fancy enough to make into it's own component, and will only serve to make your page look a bit more bling-tastic. I hope you enjoyed reading this blog and that this component finds its way to your dashboard you are building.

