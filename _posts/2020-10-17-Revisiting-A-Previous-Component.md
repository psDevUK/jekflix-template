---
date: 2020-10-17 18:20:20
layout: post
title: Revisiting A Previous Component
subtitle: I have updated the date and time component I released a while back
description: This blog covers an updated component I have built for Universal Dashboard. The blog will cover this updated component and how to it in your dashboard
image: https://blog.planview.com/wp-content/uploads/2020/02/Project-Planning-and-Delivery.jpg
optimized_image: https://blog.planview.com/wp-content/uploads/2020/02/Project-Planning-and-Delivery.jpg
category: component
tags:
  - Component
  - Date
  - Time
  - Picker
author: psdevuk
---

## Welcome

 Wasn't planning on any blogs as I actually been really busy lately with work and life. But when a fellow dashboard user reaches out for some assistance it's just to hard for me to say no.  So without doing a Conner McGregor and releasing the personal DM basically I was asked by another UniversalDashboard user if I could add the ability to set the initial date on the **UniversalDashboard.UDSelectDateTime** component I release a while back.
 Weirdly enough although I could think of several reasons to use this component, I never actually used this specific component I built for any of my dashboards. So why did I build it then?

## The original Story Behind The Component
This is the true story of a component to select the date and the time.  It was requested on the UD forums to have a component that was like a calendar component
but would also allow you to select the time. Both things built into one component.  This folks is the answer to that request.  This component is based upon the component shown on reactdatepicker.com I tried to implement as many of the useful props and pass them as powershell parameters
* **TimeIntervals** - Will set the minutes apart on the time display so a setting of 10 will show every 10 minutes on the time select.
* **OnChange** - Allows you to add a scriptblock to do something when the value in the component changes
* **Locale** - Gives you the choice to set the defined locale, this by default is set to en-GB
* **ModalView** - Displays the component centered screen as if it were a modal referred to as portal view on website defaulted false
* **Clearable** - Boolean option allowing you to add a mini clear button to the component defaulted to true
* **WeekNumbers** - This will show the current week numbers in the calendar display defaulted to true
* **showPreviousMonths** - Is set to false by default but would allow you to open the calendar to display previous months
* **monthsShown** - Is defaulted to 1 but changing this number would display the amount of calendar months, and if you select true on 
* **timeFormat** - This is defaulted to HH:mm please see documentation on website for more information
* **dateFormat** - Is defaulted to MMMM d, yyyy h:mm  please see documentation on website for more informaiton

# I have now updated this component new parameters listed below
 
 I had a request to allow the user to specify the start date.  Whilst I was at it, I noticed some other handy parameters I could add. So please see the 11 additional things I done to upgrade this component
 
* **-StartDate** allows you to define the initial date shown on the calendar to stop it defaulting to current date time
* **-Placeholder** you can now specify a string to be displayed when the date has been cleared
* **classname** a dedicated classname of **udSelectDateTime** has been added to allow custom CSS styling
* **-shouldCloseOnSelect** is a boolean set to $false to determine if the calendar should automatic close after date and time selection
* **-dateFormatCalendar** is a string value to determine how the calendar displays the month and year it is showing
* **-showPopperArrow** is a boolean value set to $true to determine if the calendar should have a pooper arrow or not
* **-showYearDropdown** is a boolean value to allow you to show a year drop down menu in the calendar for quick year selection
* **-showMonthDropdown** same as above but for the month names
* **-startOpen** a boolean value to determine if the calendar should show without the user clicking in the field area
* **-fixedHeight** boolean value to detemrine if you should keep a fixed height on the calendar
* **-inline** also a boolean value, setting this to true, will only ever show the calendar and not the text field

## Example Using The Component
```
Import-Module -Name UniversalDashboard
Import-Module -Name UniversalDashboard.UDSelectDateTime
Get-UDDashboard | Stop-UDDashboard
$theme = New-UDTheme -Name "Basic" -Definition @{
    '.react-datepicker__input-container' = @{
        'width' = "140% !important"
    }
} -Parent "Default"
$endpointinit = New-UDEndpointInitialization -Module @("UniversalDashboard.UDSelectDateTime")
Start-UDDashboard -Port 1000 -AutoReload -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Theme $theme -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 3 -Endpoint {
                New-UDSelectDateTime -Id "Picker" -TimeIntervals 5 -WeekNumbers $true -Clearable $true -Locale "en-GB" -OnChange {
                    Show-UDToast -Message "Date Changed $eventData" -Position topLeft -Duration 3000
                }
            } -AutoRefresh
            New-UDColumn -Size 4 -Endpoint {

                New-UDButton -Text "Toast" -OnClick {
                    $val = (Get-UDElement -id "Picker").Attributes.startDate
                    Show-UDToast -Message "Selected:- $val" -Position topLeft -Duration 4000
                }
                New-UDButton -Text "RemoveMe" -OnClick {
                    Remove-UDElement -id "Picker"
                }
                New-UDButton -text "ShowME" -OnClick {
                    Set-UDElement -id "Picker" -Attributes @{
                        hidden = $false
                    }
                }
                New-UDButton -Text "ClearMe" -OnClick {
                    Clear-UDElement -Id "Picker"
                }
            }
        }

    } -EndpointInitialization $endpointinit

)
```

# Demo with new parameters

```
 New-UdColumn -Size 3 -Endpoint {
           $future = (get-date).AddDays(4).AddHours(3).AddMinutes(15)
           $Exclude = (get-date).AddDays(-3)
                New-UDSelectDateTime -Id "Picker" -StartDate $future -TimeIntervals 5 -WeekNumbers $true -Clearable $true  -OnChange {
                     $Session:Selected = $eventData
                 } -DateFormatCalendar "MMMM yyyy" -CloseOnSelect $true -showPopperArrow $true -showYearDropdown $true -showMonthDropdown $true -startOpen $false -inline $true -fixedHeight $true
            } -AutoRefresh
```

## Also

  As I am from the United Kingdom I fixed the locale issue and this is now defaulted to enGB sorry I do not know how to dynamically change this, but if you are from another country really wanting this in your home language I am more than happy to make it happen and release a language specific component for you 

 
![placeholder](https://github.com/psDevUK/UDSelectDateTime/blob/master/Example.gif?raw=true "Component Demo")

## Conclusion

  Not that I don't have enough to deal with (I have 4 daughters) the challenge of adding the one additional parameter requested was super tricky to pull off, I encourage you to have a butchers of the JSX file included with the module to see all the magic behind the component.
 Adding the ability to select a specific start date did take numerous builds, and also involved me tweeting **BoSen29** who is based outside the UK so this was an international call for help, and he was kind enough to send me some links which would ultimately lead to me solving the puzzle. This request was on Friday, and I managed to pull it off by Saturday morning, so I was really happy with the results, despite this taking me lots more goes than I initially planned to actually nail this. I looked at the main website of this component which [can be found by clicking on this link](https://reactdatepicker.com/) and noticed there were some cool additional props I could add so [went to this documentation page on all of the props available on this component](https://github.com/Hacker0x01/react-datepicker/blob/master/docs/datepicker.md) and added these as additional parameters to the component to allow further customisation of the component, and get it to behave how you want it to for the users accessing your dashboard.
 I hope this has been a good read and that this component will find it's way to your dashboard. 
 
