---
date: 2019-11-23 15:44:08
layout: post
title: Custom Date Picker
subtitle: A blog about using custom components on your dashboard.
description: So I have created a few custom components for powershell universal dashboard. This blog covers importing a custom component for universal dashboard
image: /ud-flix/assets/img/DatePicker.png
optimized_image: /ud-flix/assets/img/DatePicker.png
category: Date Picker
tags:
  - date
  - module
  - custom
  - forum
author: psdevuk
---

## First Step

As always the first step I recommend is to <a href="https://docs.universaldashboard.io/endpoints/endpoint-initialization">read the official documentation</a>, which describes how to import a _powershell module_ into your dashboard you are building. This is critical you understand how to do this so that you can use the custom component within powershell universal dashboard.

> Remember the best place to find custom components for powershell universal dashboard is to look on the official marketplace:- https://marketplace.universaldashboard.io/ or the powershell gallery.

this blog will cover how to download and use the **custom date picker** I built for powershell universal dashboard.

## Forum

I just want to shout-out to everyone who uses the <a href="https://forums.universaldashboard.io/">powershell universal dashboard forum</a> there is so much useful information and inspiration on the forum it's a great place to hang-out to get some extra knowledge on the product from the people using it.

There are quite a few different sections of the forum so hopefully **I will see you in the forum soon**

## Date Picker

So prior to using powershell universal dashboard, I used to use powershell studio to build windows forms for end-users to give them the data that they kept asking me to provide, or to build applications to provide business solutions.

In the majority of the forms I built I used to use a date picker to choose a start date and an end date then press the button to get the results. This method seemed to work really well. Most importantly it was simple enough for end-users to use.

Although there was not a specific **start and end date picker** in powershell universal dashboard, I was able to construct one which worked without issues. Here is my code for how I did this:-

```js
New-UDColumn -Size 3 -Content {
    New-UDCard -Endpoint {
        New-UDInput -Title "Select Range (DAY/MONTH/YEAR)" -Id "DateForm2" -Content {
            New-UDInputField -Type 'date' -Name 'DateFrom' -Placeholder 'FROM:' -DefaultValue "01-01-2019"
            New-UDInputField -Type 'date' -Name 'DateTo' -Placeholder 'TO:'-DefaultValue "01-02-2019"

        } -Endpoint {
            param(
                $DateFrom,
                $DateTo
            )
            $var = get-date $DateFrom
            $DateFormat = $var.ToString('yyyy-MM-dd')
            $var2 = get-date $DateTo
            $DateFormat2 = $var2.ToString('yyyy-MM-dd')
            if (-Not(Test-Path $Root\$User)) { mkdir $Root\$User }
            if (Test-path $Root\$User\search.txt)
            { Remove-Item -Path "$Root\$User\search.txt" }
            $DateFormat | Out-File (Join-Path $Root\$User "search.txt")
            $DateFormat2 | Out-File (Join-Path $Root\$User "search.txt") -Append
            New-UDInputAction -Toast "$DateFormat to $DateFormat2" -duration 2000

        }
    }

}
```

However I was asked by a fellow dashboard user if I could produce a date picker. I thought that this was also a cool idea, as it did feel that this would be a useful custom component to have to save people having to do something in the above code sample.

## Custom Date Picker

So as mentioned in my custom component blog, I did some research on this website <a href="https://reactjsexample.com/">react examples</a> and <a href="https://www.npmjs.com/">npmjs</a> which gave me plenty of ideas. I prefer to choose something which has as few dependencies as possible. To be totally honest I am no react ninja but as I tell my kids, **just try your best** that's all you can do.

So after quite a bit of twitter messages back and forth, decided on which date picker I was proposing to choose and then I got building it. The hardest part for me is linking the custom component to powershell universal dashboard so that you can use `Get-UDElement` to read the values of what has been selected from the component.

So unknown to me, another dashboard user had posted their custom component on the forum which was a day picker on a calender allowing you to select one date. The other super cool thing with react components, is all the different styles there are for the same object. As the person who asked me for a date picker was not a fan of the default calendar in universal dashboard for whatever reasons.

I released my date picker shortly afterwards.

## Installation

`Install-Module -Name UniversalDashboard.UDDatePicker`

## Code

So this is a **complete** dashboard page which shows how I import this module and use it within your dashboard.

Most of the work I do is to do with **SQL** and that normally has the date format in `yyyy-mm-dd` format which is how I am formatting my output for the toast message below:-

```js
Import-Module -Name UniversalDashboard.Community
Import-Module -Name UniversalDashboard.UDDatePicker
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -BackgroundColor 'white' -Content {
        New-UDRow -Columns {
            New-UDColumn -size 6 -Content {
                New-UDDatePicker -Id "Picker"
                New-UDButton -Text "Get Dates" -OnClick {
                    $from = (Get-UDElement -Id "Picker").Attributes.from
                    [datetime]$s = "$from"
                    $Start = get-date $s -format 'yyyy-MM-dd'
                    $to = (Get-UDElement -Id "Picker").Attributes.to
                    [datetime]$e = "$to"
                    $End = get-date $e -format 'yyyy-MM-dd'
                    show-udtoast -message "You Selected $Start until $End" -duration 5000 -Position center

                }
            }

        }
    }
)
```

## Demo

![placeholder](https://user-images.githubusercontent.com/44211223/68488110-4361d600-023c-11ea-92f5-f64f6f19b7f7.gif "Date Picker")

## Conclusion

If you have not already please see my custom components blog which runs over custom components in a bit more detail. Hopefully you have learnt something from this post and will continue to follow me with my powershell universal dashboard journey.
