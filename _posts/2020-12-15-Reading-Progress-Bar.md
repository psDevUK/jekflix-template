---
date: 2020-12-15 11:53:20
layout: post
title: Reading Progress Bar
subtitle: Nice Looking Reading Progress Bar
description: Just like on this blog site there is a progress reading bar shown at the bottom of the page, this is the similar component I have built for UniversalDashboard.
image: https://images.squarespace-cdn.com/content/v1/59bb0667f09ca4cf98a04265/1546216821726-WS1M5KVW7404W4UDVKXE/ke17ZwdGBToddI8pDm48kEuP4pNSooF6wtMQPZEhxTx7gQa3H78H3Y0txjaiv_0fDoOvxcdMmMKkDsyUqMSsMWxHk725yiiHCCLfrh8O1z5QHyNOqBUUEtDDsRWrJLTmZ3auM-RT0ZNDd8RcEzv-Gv69AgZHSgQeQ95Y4RM7pzPDIsSmYFzhW_W1LC_R_1FY/undraw_reading_list_4boi.png
optimized_image: https://images.squarespace-cdn.com/content/v1/59bb0667f09ca4cf98a04265/1546216821726-WS1M5KVW7404W4UDVKXE/ke17ZwdGBToddI8pDm48kEuP4pNSooF6wtMQPZEhxTx7gQa3H78H3Y0txjaiv_0fDoOvxcdMmMKkDsyUqMSsMWxHk725yiiHCCLfrh8O1z5QHyNOqBUUEtDDsRWrJLTmZ3auM-RT0ZNDd8RcEzv-Gv69AgZHSgQeQ95Y4RM7pzPDIsSmYFzhW_W1LC_R_1FY/undraw_reading_list_4boi.png
category: Component
tags:
  - Reading
  - Progress
  - Bar
  - Custom
  - Component
author: psdevuk
---

## Welcome

Well I know 2020 has not been a good year for most people, and so many bad consequences have happened to businesses across the globe with this pandemic. My working hours have been reduced at work, so to make the most of this additional free-time I now have, I am building and blogging about some more custom components.
[This custom component I uploaded the raw JSX and function PS1 file to my video course](https://psdevuk.github.io/ud-flix/Video-Course-With-Me/) Which shows how this component was constructed.
 I was asked if this blog site was created in UD which it is not, this is a Jekyll based website, with markup as the language displaying the data on the screen.  Anyways, I rolled with this particular Netflix inspired template, and went with the name UD-Flix, anyways one of the cool things I think about this blog site is the automatic reading bar that is displayed at the bottom of the page as you scroll. I have noticed a good few other sites that use this as well, but the progress is shown at the top of the screen. Well I found a really simple component that had zero dependencies which can mimick this with ease.

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/ReadingBarGif.gif?raw=true "Simple Demo")

## What Does This Components Do?

As shown in the GIF demo above this will automatically add a reading progress bar to the top of the dashboard screen, what makes this even more awesome is it is super easy to incorporate into your dashboard. You can change the height of this component, the progress bar colour and the background colour of the reading progress bar.

## So Why Build This Component?

Do you need another excuse apart from it looks super cool, and is 23.1kb in size should shouldn't add any extra loading time to the webpage that this will be displayed upon. Oh and it has zero dependencies making this a super good project to build yourself.

## New-UDReadingBar

### Parameters
```
param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(), # Allows you to specify an ID for component
        [Parameter()]
        [int]$Height = 5, # Allows you to control the height of the component
        [Parameter()]
        [string]$BarColor = "#D03625", # Main progress bar colour
        [Parameter()]
        [string]$BarBackgroundColor = "#685478" # Main progress bar unfilled background colour
    )
```

 As always I try to give as many defaults as I can to my parameters so the component pretty much needs the minimal parameters supplying to it.

## Demo

So for the exact demo of the GIF I used above will be

```
Import-Module -Name UniversalDashboard.Community -RequiredVersion 2.8.1
Import-Module "C:\UD\ProgressRead\ReadingBar\src\output\UniversalDashboard.UDReadingBar\UniversalDashboard.UDReadingBar.psd1"
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10006 -Dashboard (
    New-UDDashboard -Content {
        New-UDReadingBar -BarColor "#D03625" -BarBackgroundColor "#685478" -Height 10
        New-UDHeading -Size 3 -Text "Reading Bar With Progress"
        New-UDRow
        New-UDHeading -size 6 -Text "What is Lorem Ipsum?"
        New-UDRow
        New-UDHeading -size 6 -Text "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum. Why do we use it?"
        New-UDRow
        New-UDHeading -size 6 -Text "It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal distribution of letters, as opposed to using 'Content here, content here', making it look like readable English. Many desktop publishing packages and web page editors now use Lorem Ipsum as their default model text, and a search for 'lorem ipsum' will uncover many web sites still in their infancy. Various versions have evolved over the years, sometimes by accident, sometimes on purpose (injected humour and the like)."
        New-UDRow
        New-UDHeading -size 6 -Text "Where does it come from?"
        New-UDRow
        New-UDHeading -size 6 -Text "Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source. Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of 'de Finibus Bonorum et Malorum' (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum, 'Lorem ipsum dolor sit amet..', comes from a line in section 1.10.32."
        New-UDRow
        New-UDHeading -size 6 -Text "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from 'de Finibus Bonorum et Malorum' by Cicero are also reproduced in their exact original form, accompanied by English versions from the 1914 translation by H. Rackham.
Where can I get some?"
        New-UDRow
        New-UDHeading -size 6 -Text "There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don't look even slightly believable. If you are going to use a passage of Lorem Ipsum, you need to be sure there isn't anything embarrassing hidden in the middle of text. All the Lorem Ipsum generators on the Internet tend to repeat predefined chunks as necessary, making this the first true generator on the Internet. It uses a dictionary of over 200 Latin words, combined with a handful of model sentence structures, to generate Lorem Ipsum which looks reasonable. The generated Lorem Ipsum is therefore always free from repetition, injected humour, or non-characteristic words etc."

    }

)
```
![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/ReadingBarGif2.gif?raw=true "Simple Demo")

## Super Easy To Implement

```
New-UDReadingBar -BarColor "#D03625" -BarBackgroundColor "#685478" -Height 10
```
Thats all you need to include at the top of your dashboard script file to get this exact looking bar I have in the demo above

## Conclusion

Although I have seen this effect on my blog site for just over a year now, believe it or not I just for what-ever reasons never bothered looking at implementing this to a dashboard environment. Not sure why, as I really liked the reading progress bar on this blog site, anyways I am just glad that the light builb sparked a bit above my head the other day and made me do a search on nmpjs.com which then lead to this component being built. I am glad I built this as I do think it is a really nice component to have on any dashboard page, and I hope it finds it's way to your dashboard you are building or have released. I will be publishing this to the powershell gallery soon.
