---
date: 2021-01-02 10:58:20
layout: post
title: Page Filtering Highlight Component
subtitle: Search bar allowing you to highlight specific text on the page, and filter it for a given time
description: Search bar allowing you to highlight specific text on the page, and filter it for a given time making that element the only visiable element on the page
image: https://github.com/psDevUK/ud-flix/blob/master/assets/img/NavbarSearch.PNG?raw=true
optimized_image: https://github.com/psDevUK/ud-flix/blob/master/assets/img/NavbarSearch.PNG?raw=true
category: Component
tags:
  - Page
  - Filtering
  - Highlight
  - Text
  - Component
author: psdevuk
---

## Welcome

Happy 2021, lets hope this year is better than the previous year in terms of getting back to a normal life. Like I mean I have read so many comics and still do to today. So I do feel like I have had some preparation for the various lockdowns we been through. Lets just hope for a better year.
 So this latest blog is about another new component I have built. I say I, and I really mean we. As I had some help on constructing this component from a fellow dashboarder who is also a javascript ninja going by the online alias @bosen29

[Please remember you to can also build cool looking custom components like this one, by buying my course on how to create custom components here](https://psdevuk.github.io/ud-flix/Video-Course-With-Me/)

## Why build this component?

So this component was inspired by yet another fellow dashboarder @itfranck who released a search filter aka dudsearch for UD, and kindly put this on the marketplace. So having built a number of components, I was running low on ideas to build for a useful component. Thankfully @itfranck had uploaded the code to github, so I was able to see the function file and the component file. I was still a bit confused on using it, so I looked at the demo file given in the repository, as the gif posted on the forum looked pretty damn cool. 
 However after analysing the code to do the demo, I was just like thinking damn, I would have to change how I construct my dashboards to be able to use this, and I would have to give everything an ID to match it on, and well it seemed a bit complex.
  Being a simple lad from a smallish town I just wanted to keep it simple. I had seen various posts that @itfranck was looking to update it at somepoint, well as a good period of time has past and no updates have come about, and to my knowledge no-one else has had a go at doing this. So I wanted to bring out my own version of a search bar, and just try to keep it simple, so I could still design dashboards how I am used to designing dashboards. 

## What does this component do then?

So as mentioned above this was inspired by a fellow dashboarder, and I seeked permission to use this as I don't want to tread on any toes and I got blessing.
I wanted to be able to search and highlight text on the page the equivalent to doing a Ctrl+F in a browser. I know this is not game changing stuff, but figured it would be cool to do all the same. I also really liked the ability in the dudsearch to be able to hide the other components on the page that did not meet the search criteria. So wanted to implement that to. 
So yeah that is what this component does, it will highlight matching text, and hide other content on the page for 5 seconds by default, and this will match text in card-content class only by default.
To make this component more flexible it is using the classname as oppose to an id of a component. I used this approach as by default all objects are given the same class names and for ud-card the class name of all the content of the ud-card is card-content. You can easily identify the class names by right clicking and inspecting the element and looking through the HTML highlighted to identify the class name. The other really cool thing on doing stuff by class name as oppose to id is that you can specify multiple class names to search on. As mentioned by default I set this to card content, but you can choose any valid class name to filter the page contents on.
 Demo of component below.

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/NavSearchBar.gif?raw=true "Simple Demo")

## So how did you do this?

Thankfully I know a few other dashboarders, and well I take my hat off to the amazing Mr @bosen29 who totally smashed this in a stupid little amount of time. I was originally using the ```Invoke-UDJavaScript``` that @bosen29 had developed for UD. Using a little bit of googling I was able to have something that worked, but was using a function to use one id and was able to highlight text on that given id. I am not used to using JavaScript and then I found out using the id you could only specify one id. Apparently you can pass this as an array but I was struggling to get anything more fancy working than the original single id element being highlighted. Again lucky that Scandinavian people or at least @bosen29 are very polite and helpful people, he offered to teamviewer onto my laptop, and literally within a few minutes had re-written the function to accept class names as opposed to ids, something I had spent several hours trying to implement. I then mentioned to @bosen29 I thought originally I would have had to do all this in the JSX file for the component. He was like no problem, and again in a few moments, had made the function into a script, and binded it to the onclick part in the JSX file. Wow, I was amazed at how easy he seemed to make it all look, guess when you good at something you can always make something look easily. So after seeing how @bosen29 had implemented the javascript earlier, and showed me how to effectively use the console in my browser, I was able to add on an extra bit of code to the code @bosen29 had provided for me, to hide the elements of the same classname that did not contain the matching text for a period of time, as to me this would just bring more attention to the user showing them the matching text with the matching card the text is in, then to bring back all the other card components back onto the page, after a given time period. Then the next day after thanking @bosen29 for his assistance, he mentioned that I should change the hard-coded ```card-content``` to a parameter so that the user could specify any class they wish to filter on, and I did the same with the given time delay in the javascript I wrote.  That is basically how this component came about, I couldn't have done it without looking at the original project by @itfranck and certainly couldn't have pulled off the sweet page filtering without @bosen29 help.
 What makes this extra-sweet for me is that this component all works out of the box, with added CSS built in for styling, and is real easy to use, and you can build your dashboard pages how you are use to building them.

## Demonstration File

So I found a random text generator on the web and thought to construct a simple dashboard containing just cards with some random text in them...

# Demo 
```
Import-Module -Name UniversalDashboard.Community -RequiredVersion 2.8.1
Import-Module "C:\UD\SearchBar\UDNavbarSearch\src\output\UniversalDashboard.UDNavbarSearch\UniversalDashboard.UDNavbarSearch.psd1"

Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10005 -Name "Powershell Dashboard" -Dashboard (
    New-UDDashboard -Content {
        New-UDNavbarSearch -Id 'NavbarSearch' -ClassNameFilter "card-content" -Delay 10000 -onChange {
            if ($($EventData).length -gt 1) {
                Set-UDElement -id 'RESULTS' -Content { "Searching for text:- $EventData" }
            }
            else { Set-UDElement -id 'RESULTS' -Content { "Use the search bar to highlight text" } };
        }
        New-UDRow -Columns {
            New-UDColumn -Id "RESULTS" -size 12 -Content {
                $EventData
            }
            New-UDColumn -size 3 -Content {
                New-UDCard -Content { "Mutley, you snickering, floppy eared hound. When courage is needed, you’re never around. Those medals you wear on your moth-eaten chest should be there for bungling at which you are best. So, stop that pigeon, stop that pigeon, stop that pigeon, stop that pigeon, stop that pigeon, stop that pigeon, stop that pigeon. Howwww! Nab him, jab him, tab him, grab him, stop that pigeon now. " }
            }
            New-UDColumn -size 3 -Content {
                New-UDCard -Content { "Children of the sun, see your time has just begun, searching for your ways, through adventures every day. Every day and night, with the condor in flight, with all your friends in tow, you search for the Cities of Gold. Ah-ah-ah-ah-ah… wishing for The Cities of Gold. Ah-ah-ah-ah-ah… some day we will find The Cities of Gold. Do-do-do-do ah-ah-ah, do-do-do-do, Cities of Gold. Do-do-do-do, Cities of Gold. Ah-ah-ah-ah-ah… some day we will find The Cities of Gold." }
            }
            New-UDColumn -Size 3 -Content {
                New-UDCard -Content { "One for all and all for one, Muskehounds are always ready. One for all and all for one, helping everybody. One for all and all for one, its a pretty story. Sharing everything with fun, thats the way to be. One for all and all for one, Muskehounds are always ready. One for all and all for one, helping everybody. One for all and all for one, can sound pretty corny. If youve got a problem chum, think how it could be." }
            }
            New-UDColumn -size 3 -Content {
                New-UDCard -Content { 'Barnaby The Bears my name, never call me Jack or James, I will sing my way to fame, Barnaby the Bears my name. Birds taught me to sing, when they took me to their king, first I had to fly, in the sky so high so high, so high so high so high, so if you want to sing this way, think of what youd like to say, add a tune and you will see, just how easy it can be. Treacle pudding, fish and chips, fizzy drinks and liquorice, flowers, rivers, sand and sea, snowflakes and the stars are free.' }
            }
            New-UDColumn -size 3 -Content {
                New-UDCard -Content { "Knight Rider, a shadowy flight into the dangerous world of a man who does not exist. Michael Knight, a young loner on a crusade to champion the cause of the innocent, the helpless in a world of criminals who operate above the law." }
            }

            New-UDColumn -size 3 -Content {
                New-UDCard -Content { "Top Cat! The most effectual Top Cat! Whos intellectual close friends get to call him T.C., providing its with dignity. Top Cat! The indisputable leader of the gang. Hes the boss, hes a pip, hes the championship. Hes the most tip top, Top Cat. " }
            }
            New-UDColumn -size 3 -Content {
                New-UDCard -Content { "Ulysses, Ulysses Soaring through all the galaxies. In search of Earth, flying in to the night. Ulysses, Ulysses Fighting evil and tyranny, with all his power, and with all of his might. Ulysses no-one else can do the things you do. Ulysses like a bolt of thunder from the blue. Ulysses always fighting all the evil forces bringing peace and justice to all. " }
            }
            New-UDColumn -size 3 -Content {
                New-UDCard -Content { "Thundercats are on the move, Thundercats are loose. Feel the magic, hear the roar, Thundercats are loose. Thunder, thunder, thunder, Thundercats! Thunder, thunder, thunder, Thundercats! Thunder, thunder, thunder, Thundercats! Thunder, thunder, thunder, Thundercats! Thundercats!" }
            }
        }

    }
)

```
![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/NavSearchBar.gif?raw=true "Simple Demo")
The above GIF is using the exact code provided in the demonstration code.
If you look at the top just after the content for the dashboard, you will see all the required code I needed to use this component:-
```
        New-UDNavbarSearch -Id 'NavbarSearch' -ClassNameFilter "card-content" -Delay 10000 -onChange {
            if ($($EventData).length -gt 1) {
                Set-UDElement -id 'RESULTS' -Content { "Searching for text:- $EventData" }
            }
            else { Set-UDElement -id 'RESULTS' -Content { "Use the search bar to highlight text" } };
        }
        New-UDRow -Columns {
            New-UDColumn -Id "RESULTS" -size 12 -Content {
                $EventData
            }
```
  I literally could of just used ```New-UDNavbarSearch``` and you would still of been presented with a search-bar in the navbar which would search all card-content for 5 seconds. I stole the onchange bit from the original component dudsearch to show the user what they are searching for. As you can hopefully see this component is really easy to use and gives you loads of flexibilty for filtering the contents of the page by specifying the classname to filter on.  As I have read you can filter on more than one classname you literally add a space between the classnames you are searching for.
Please note for different themes you might have to fiddle with the CSS to get it to display properly. Like in the cover picture on the blog, I thought it would be better for a dark theme to be used. I used the DarkRounded theme I published to UD, however I had to make the following CSS adjustments:-
```
 $theme = New-UDTheme -Name "Basic" -Definition @{
 '.ud-navbar' = @{
     "z-index" = "0 !important"
 }
 '.react-search-field' = @{
     "margin-top" = "-40px !important"
 }
} -Parent DarkRounded
```
 

## UDNavbarSearch Parameters

```
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(), #Specify and ID for component
        [Parameter()]
        [string]$Placeholder, #Placeholder text for searchbar
        [Parameter()]
        [string]$SearchText, #You can provide default search text
        [Parameter()]
        [ScriptBlock]$onChange, #Scriptblock onChange for when a searchbar changes
        [Parameter()]
        [ScriptBlock]$onEnter, #Scriptblock for user pressing the enter key
        [Parameter()]
        [string]$ClassNameFilter = "card-content", #Sepcify the classname you want to filter on
        [Parameter()]
        [int]$Delay = 5000 #Hiding all other elements in MS so this is 5 seconds
    )   
```



## Conclusion

Really, really happy to have got the component working, I couldn't of done this without the help of others. That's what I really like about IT is that there is so many different ways to solve the problem, so this was my implementation of solving the find on page with a nice searchbar nested in the navbar as I always feel the navbar is not used enough, and it is a great place for me having a small laptop screen, that if I can make a useful component and make it work by nesting it in essentially an empty part of the screen so I do not loose any screen-space then it's all good with me. Thanks for taking the time to read this blog, lets all hope for a much better year this year. I will be uploading this component to the powershell gallery very soon.
