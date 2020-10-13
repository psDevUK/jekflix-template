---
date: 2020-10-13 20:40:20
layout: post
title: Skeleton Loading Component
subtitle: Halloween is near so here is my skeleton all ready time for halloween
description: This blog covers the latest component I have built for Universal Dashboard. The blog will cover this new component and how to it in your dashboard
image: https://i.ytimg.com/vi/Fabqf3c1V70/maxresdefault.jpg
optimized_image: https://i.ytimg.com/vi/Fabqf3c1V70/maxresdefault.jpg
category: component
tags:
  - Component
  - Skeleton
  - Loading
  - Custom
author: psdevuk
---

## Welcome

So I am back with another blog, I didn't think I would be writing another blog so soon, but as it is taking me less time these days to build a component, let me share with you what I have cooked up this evening for Powershell UniversalDashboard

## React Loading Skeleton

 So a good while back I did come across a skeleton loading component, and I did get it to work, but never released it as a component, as I don't think I could get it to hide. Well it was a long time ago, and I basically gave up and moved onto something else. 
  However this evening as I was browsing [npmjs.com](https://www.npmjs.com/) which is where I found all the components I build I stumbled back on a [react loading skeleton which can be found here](https://www.npmjs.com/package/react-loading-skeleton) I looked at the dependencies as it's always nice if it is a low number, and this component lists one dependency.  Sadly that one dependency had another dependancy and another and another and so on, so if your wondering how many exactly here is the true number of dependencies
```
react-loading-skeleton
@emotion/core
@babeel/runtime
@emotion/cache
@emotion/css
@emotion/serialize
@emotion/sheet
@emotion/utils
regenerator-runtime
@emotion/stylis
@emotion/weak-memoize
babel-plugin-emotion
@emotion/hash
@emotion/memoize
@emotion/unitless
csstype
@babel/helper-module-imports
babel-plugin-macros
babel-plugin-syntax-jsx
convert-source-map
escape-string-regexp
find-root
source-map
@babel/types
cosmiconfig
resolve
safe-buffer
@babel/helper-validator-identifier
lodash
to-fast-properties
path-parse
@types/parse-json
import-fresh
parse-json
path-type
yaml
parent-module
resolve-from
callsites
@babel/highlight
chalk
js-tokens
is-arrayish
ansi-styles
supports-color
color-convert
color-name
has-flag
```
 All I can say is the person behind `Invoke-Expression` is a genius as you can use that command to install all of the above, so it's just a case of lots of copying and pasting, until I have all the dependencies, then I like to do something like `Get-Content C:\UD\packs.txt | % {Invoke-Expression "npm i $_ --save"}` to get all these installed.
 So all of the props mentioned on the page for this component I have included, please see all the parameters listed below.

## Parameters
```
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [bool]$Circle,
        [Parameter()]
        [string]$Color,
        [Parameter()]
        [string]$HighlightColor,
        [Parameter()]
        [int]$Count,
        [Parameter()]
        [int]$Duration,
        [Parameter()]
        [int]$Height,
        [Parameter()]
        [int]$Width
```
## Demo

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/Skeleton.gif?raw=true "Component Demo")

## Code From The Demo

```
Import-Module UniversalDashboard
Import-Module UniversalDashboard.UDSkeleton
Get-UDDashboard | Stop-UDDashboard
$endpointinit = New-UDEndpointInitialization -Module @("UniversalDashboard.Skeleton")
Start-UDDashboard -Port 1000 -AutoReload -Dashboard (
    New-UDDashboard -Title "UniversalDashboard" -EndpointInitialization $endpointinit -Content {
        New-UDRow -Columns {
            New-UDColumn -size 4 -Content {
                #Create the stuff you want to display but set a delay
                New-UDElement -Tag 'div' -Endpoint {
                    start-sleep -Milliseconds 3070
                    New-UDImage -Url "https://www.iconfinder.com/data/icons/free-social-icons/67/github_circle_black-512.png" -Height 100 -Width 100
                    New-UDElement -Tag "h3" -Content { "New-UDSkeleton" }
                    New-UDHeading -Text "hello add a fake loader to your dashboard to make it look"
                    New-UDElement -Tag 'br'
                    New-UDHeading -Text "like your site is super busy fetching the information when"
                    New-UDElement -Tag 'br'
                    New-UDHeading -Text "in actual fact you just delay the time to show this text. Clever?"
                }
		#Set the skeleton loading screen to match your actual content to be displayed
                New-UDSkeleton -Id "SKELETON3" -Count 1 -Circle $true -Color "#BEB7A4" -HighlightColor "#FF7F11" -Height 100 -Width 100 -Duration 2
                New-UDHtml -Markup "<br>"
                New-UDSkeleton -ID "SKELETON" -Count 1 -Color "#BEB7A4" -HighlightColor "#FF7F11" -Height 55 -Width 330 -Duration 2
                New-UDHtml -Markup "<br>"
                New-UDSkeleton -ID "SKELETON2" -Count 3 -Color "#BEB7A4" -HighlightColor "#FF7F11" -Height 15 -Width 330 -Duration 2
                #Add the fake delay to make the user wait then make the skeleton disappear
                New-UDElement -Tag 'span' -Endpoint {
                    Start-Sleep -Milliseconds 3050
                    Remove-UDElement -Id "SKELETON"
                    Remove-UDElement -Id "SKELETON2"
                    Remove-UDElement -Id "SKELETON3"
                }
            }
        }
    }
)
```

## Conclusion

  I thought this component looked really cool a while back, but didn't fully get round to completing the project. So really happy I spent the time tonight to pull this off, and I will be adding this to the powershell gallery and universaldashboard market-place very soon.