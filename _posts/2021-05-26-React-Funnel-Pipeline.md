---
date: 2021-05-26 13:55:20
layout: post
title: React Funnel Pipeline
subtitle: A simple yet effective funnel chart
description: New component for Powershell Universal dashboards, the ability to display data in a funnel chart that has quite a few options to customise it
image: https://raw.githubusercontent.com/psDevUK/PSU_Trendline/main/FunnelMain.PNG
optimized_image: https://raw.githubusercontent.com/psDevUK/PSU_Trendline/main/FunnelMain.PNG
category: Component
tags:
  - React
  - Funnel
  - Chart
  - Component
author: psdevuk
---

## Welcome

 Thanks for visiting this page. Today is a special day for me, as it is my wifes' birthday, and I didn't mess-up this year, I got cards and gifts. I am rubbish with remembering birthdays, maybe that should be my next component, a birthday component? 
 Todays' blog is about a new component I cooked up and wanted to share this component, and I think writing a quick blog on it is good for others interested in using it.

## Why build this component?

 Well the other day I was looking at the documentation page for Powershell Universal, and well randomly a word popped into my head **funnel** I searched for this but got zero results. I thought perfect, I will bring the funnel to the users of Powershell Universal. Hopefully that is a good enough reason, as I am always looking to bring new user interface components to this amazing bit of software.

## What does this component do then?

This component will take an input of array data and then display that data in a **funnel chart** which you have a number or powershell parameters to customise the look and feel of the funnel chart.  Below you will see the parameter list, and what each parameter is for

```
   param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(), #Allows you to give this component an ID to reference it
        [Parameter()]
        [string]$Title, #Shows a title above the funnel chart
        [Parameter()]
        [switch]$showValues, #Shows the actual value in the funnel for which the value represents in the chart
        [Parameter()]
        [switch]$showNames, #Shows the name representing the section of the funnel chart
        [Parameter()]
        [switch]$showRunningTotal,  #Instead of showing the value in the segment it will show the running total of all values underneath it
        [Parameter()]
        [int]$chartWidth, #Numerical value to control the width of the chart
        [Parameter()]
        [int]$chartHeight, #Numerical value to control the height of the chart
        [Parameter()]
        [switch]$heightRelativeToValue, #Each segment will have its own height relative to the value
        [Parameter(Mandatory)]
        [array]$Data, #Mandatory array of data
        [Parameter(Mandatory)]
        [array]$Colors #Mandatory array of colours to render the funnel chart colours
    )
```

Above I have listed all the parameters I included for this component and used the **#** comment to give a brief description on what that parameter does to the component if you use it or not. 


![placeholder](https://raw.githubusercontent.com/psDevUK/PSU_Trendline/main/Funnel1.PNG "Demo")

## Demonstration File

I made a super simple CSV for testing purposes which contains the following:

```
Name,Score
bob,34
fred,56
simon,78
jim,33
wes,12
```

I then wanted to display this data in the funnel chart component

# Demo 
```
New-UDDashboard -Title "Funnel Demo" -Content {
 $myTable = import-csv C:\adam\scores.csv

$dataArray=@()
foreach($r in $mytable)
{
    $dataArray += @{
    name = [string]$r.Name
    value = [int]$r.Score
    }
}

$colors = @('#f14c14', '#f39c35', '#68BC00', '#1d7b63', '#4e97a8', '#4466a3')
New-UDFunnel -ID "FUNNELDEMO" -Title "Funnel Demo" -Colors $colors -showNames -showValues -Data $dataArray -chartWidth 600 -chartHeight 300 -showRunningTotal
}
```

![placeholder](https://raw.githubusercontent.com/psDevUK/PSU_Trendline/main/Funnel2.PNG "Demo")

Please note how I created the array with a **name** and **value** and forced the variable to either be a **string** or an **int** I found that if I didn't do this I didn't get the component working correctly.  



## Conclusion

Again it was really nice to find a component with minimal dependencies, this had zero so it allowed me to put it together quite quickly with the demo data provided on the site. As mentioned in my last blog I will look to update my course with new material on how to build custom component in Powershell Universal. I need to do some more studying myself as there is another UDFactory allowing you to customise the framework being used. I will be uploading this component to the powershell gallery very soon and you should see it on the marketplace today.
