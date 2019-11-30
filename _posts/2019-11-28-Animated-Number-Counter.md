---
date: 2019-11-28 22:21:00
layout: post
title: Animated Number Counter
subtitle: Blog covering another custom component I just built.
category: counter
image: https://user-images.githubusercontent.com/44211223/69887084-135a9f80-12dd-11ea-8ad0-f5ee736fff75.jpg
optimized_image: https://user-images.githubusercontent.com/44211223/69887084-135a9f80-12dd-11ea-8ad0-f5ee736fff75.jpg
tags:
  - animated
  - counter
author: psdevuk
---

# Welcome

> As always these blogs are my own opinions and thoughts, I do not get paid to write these, I just try to give honest reviews and feed-back.

So I swear I was watching some introduction to either materialize or react dashboards to try and learn more about the whole world of HTML to try and beef up my universaldashboard skills, and I saw this dashboard that had several counters on it, with icons like how the old universaldashboard counters used to look, except these counters were animating until it reached the given number. I thought **wow** that looks really cool, and a good way of getting the end-user to focus on your dashboard, by giving them something flashy to look at, then before you know it, the actual number is then displayed.

## Then lots of time past...

Although I thought this looked super cool, I didn't really give it much thought. I guess all the entertainment of 4 daughters and a Mrs to keep happy I had other things on my mind.

## Then even more time past...

Then last night when I was on <a href="https://www.npmjs.com/">npmjs</a> I thought I would randomly search for **number counter** and I got back to this result <a href="https://www.npmjs.com/package/number-counter">number-counter</a>

This was it. This is what I had seen all that time ago in the video that I cannot really remember, but this is it.

Very happy I had found this **number counter animation** I then went to look at what dependencies it had listed, as it was showing 3.

- `prop-types`
- `webpack`
- `react`

So without knowing too much, but knowing enough, I thought, universaldashboard is built on top of **react**, so this is already in the custom template I mentioned in my previous blog that I use to create custom components. And I am pretty damn sure that **webpack** is what is used to build the compoent get the JSX compiled into a powershell function. So that just left me with **prop-types** which I have previously used in some other custom components

If you click on **prop-types** you will see to install this (remember you must be in the SRC directory of the custom template) you type the following command `npm i prop-types --save` however as also mentioned in a previous blog, you now have to download all the dependencies of **prop-types** for this to work:-

- `loose-envify --save`
- `object-assign --save`
- `react-is --save`
- `js-tokens --save`

Remember this is just one extra dependency that we needed, and we have had to actually install another 4 things on-top of the 1 **prop-type** we needed.

This is why I do not build everything people ask for. As if that component relies on 14 dependencies, and each of those could have multiple dependencies, then you looking at spending a long time to download all these dependencies, and you might not even get the component working.

## Start small

It was always on my **bucket list** to put something on github. Prior to using universal dashboard I had used github to find certain powershell code, and thought **wow** this is a super cool place for code. Also on my **bucket list** was to put something on the powershell gallery, as again I had used this prior to using universal dashboard and again though **wow** super cool, would love to be listed on here.

So I managed to contribute a theme towards powershell universal dashboard on github, then I published a custom component to the powershell gallery. Since then I been creating lots of repositories on github of the components I been building and posting onto the powershell gallery which in-turn goes onto the powershell universal dashboard market place.

I really need to still learn a lot as binding controls in universaldashboard is still a tricky subject to me, and I have had help on doing this on previous components, and only so far pulled it off by myself once.

- As the title states, start small.

So this component seemed pretty basic, and after reading the example this is my finished JSX code:-

```js
import React from 'react';
import NumberCounter from 'number-counter';
class <%=$PLASTER_PARAM_ControlName%> extends React.Component {
  render() {
      return (
        <NumberCounter
          start={this.props.start}
          end={this.props.end}
          delay={this.props.delay}
          preFix={this.props.preFix}
          postFix={this.props.postFix}
          reverse={this.props.reverse}
        />
    );

  }
}
export default <%=$PLASTER_PARAM_ControlName%>
```

I did originally include the header in the `div` tag, but as I was using a custom theme on my dashboard, this had adverse effects displaying the text, so I removed it.

## Powershell code

```
function <%=$PLASTER_PARAM_CommandName%> {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [int]$End,
        [Parameter()]
        [int]$Start,
        [Parameter()]
        [int]$Delay,
        [Parameter()]
        [string]$PreFix,
        [Parameter()]
        [string]$PostFix,
        [Parameter()]
        [bool]$Reverse
    )

    End {

        @{
            # The AssetID of the main JS File
            assetId  = $AssetId
            # Tell UD this is a plugin
            isPlugin = $true
            # This ID must be the same as the one used in the JavaScript to register the control with UD
            type     = "<%=$PLASTER_PARAM_ControlTypeName%>"
            # An ID is mandatory
            id       = $Id

            # This is where you can put any other properties. They are passed to the React control's props
            # function <%=$PLASTER_PARAM_CommandName%> {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [int]$End,
        [Parameter()]
        [int]$Start,
        [Parameter()]
        [int]$Delay,
        [Parameter()]
        [string]$PreFix,
        [Parameter()]
        [string]$PostFix,
        [Parameter()]
        [bool]$Reverse
    )

    End {

        @{
            # The AssetID of the main JS File
            assetId  = $AssetId
            # Tell UD this is a plugin
            isPlugin = $true
            # This ID must be the same as the one used in the JavaScript to register the control with UD
            type     = "<%=$PLASTER_PARAM_ControlTypeName%>"
            # An ID is mandatory
            id       = $Id

            # This is where you can put any other properties. They are passed to the React control's props
            # The keys are case-sensitive in JS.
            end      = $End
            start    = $Start
            delay    = $Delay
            preFix   = $PreFix
            postFix  = $PostFix
            reverse  = $Reverse
        }

    }
}
            end      = $End
            start    = $Start
            delay    = $Delay
            preFix   = $PreFix
            postFix  = $PostFix
            reverse  = $Reverse
        }

    }
}
```

I forgot to mention it, although it is in the comments, but incase you don't read the comments here it is **The keys are case-sensitive in JS** this means it must match the case of the text in the **JSX** file for the props you are referencing.

## Images

This was a little demo example I knocked up

![placeholder](https://user-images.githubusercontent.com/44211223/69886893-36d11a80-12dc-11ea-9094-bf4695607f6c.gif "Demo of component")

I did this using some simple code:-

```js
Import-Module -Name UniversalDashboard.Community
$theme = get-udtheme DarkRounded
Import-Module -Name UniversalDashboard.UDNumber
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -theme $theme -Content {
        New-UDRow -Columns {
            New-UDColumn -Content {
                [int]$Finish = 12 / 555 * 100
                $number = (get-process).count
                if ($number -gt 1) {
                    New-UDElement -Tag H4 -Attributes @{
                        style = @{
                            color = 'white'
                        }
                    } -Content { New-UDNumber -End $number -Delay 2 -PreFix "Complaints you raised"
                        New-UDNumber -Start 100 -End $Finish -Delay 4 -Prefix "This equates to" -PostFix "%" -reverse $true
                    }
                }
            }
        }
    }
) -AutoReload
```

## More Dynamic

So you can get this component working more dynamically for you by placing the code inside an endpoint script block. So for this to work, you need to download and install the **UD Number** module in the default powershell module folder, which should be done automatically something like %programfiles%\WindowsPowerShell\Modules once the module is in there, you can then use the module in your endpoints by importing the module into the **New-UDEndpointInitialization** command. So now on every page refresh using the following code you will get a different set of results:-
```
Import-Module UniversalDashboard.Community
Import-Module UniversalDashboard.UDNumber
Get-UDDashboard | Stop-UDDashboard
$endpointinit = New-UDEndpointInitialization -Module @("UniversalDashboard.UDNumber")
$theme = get-udtheme "DarkRounded"
$dashboard = New-UDDashboard -Title "New-UDNumber" -theme $theme -Content {
    New-UDRow -columns {
        New-UDColumn -Endpoint {
            New-UDCard -Content {
                [int]$Finish = get-random -Maximum 99
                $number = get-random -Maximum 100
                New-UDElement -Tag H4 -Attributes @{
                    style = @{
                        color = 'white'
                    }
                } -Content { New-UDNumber -End $number -Delay 2 -PreFix "You have" -PostFix "friends"
                    New-UDNumber -Start 100 -End $Finish -Delay 6 -Prefix "This is" -PostFix "% more than me" -reverse $true
                }
            }
        }

    }

} -EndpointInitialization $endpointinit
Start-UDDashboard -Dashboard $dashboard -Port 10005
```
If you want the numbers to automatically refresh, then you need to use the `-AutoRefresh -RefreshInterval 15` which would then refresh these numbers being automatically generated by the `get-random` cmdlet every 15 seconds (you can specify any number here which is represented in seconds). For this example I only wanted the numbers refreshing on a page load hence I did not include those additional parameters on the endpoint parameter.

## Conclusion

As I was about to write this I just posted this component to the powershell gallery which if you search **simpleud** you will see all my collection of components I have done. I hope this helps to inspire you to get building your own custom component for this awesome module which is **powershell universal dashboard**
