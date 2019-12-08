---
date: 2019-12-08
layout: post
title: Updated Gauge Component
subtitle: Blog about updating one of my exisiting modules.
description: There was a request on the universal dashboard for a gauge control that had certain features. Thought this would be a good time to update my gauge component.
image: https://user-images.githubusercontent.com/44211223/70394169-375b6680-19ea-11ea-9bf3-b32d7ec50c27.PNG
optimized_image: https://user-images.githubusercontent.com/44211223/70394169-375b6680-19ea-11ea-9bf3-b32d7ec50c27.PNG
category: code
tags:
  - Forum
  - Gauge
  - Custom
  - Component
author: psdevuk
---

## Universal Dashboard Forum

So I mentioned this before but the powershell universal dashboard forum that Adam Driscoll setup is a <a href="https://forums.universaldashboard.io/">super cool place to see what other people are doing with the product</a>, the forum is broken down into different sections. It has also recently grown in size by adding the additional products Adam Driscoll is producing. It makes sense to house it all under one URL, and I guess this is the idea behind it

> Always feel blessed when random people you do not know believe you have the power to create some custom component for powershell universal dashboard that does not currently exist.

I love reading comic books and believe that people can be super in their own way

> **Do good to others and every man can be a Superman.**

## Gauge Component

I don't pay attention to what I have posted on the powershell gallery, and I had some issues with two factor authentication, so used a different account to carry on uploading things, as I was locked out of my original account for one month. So I knew I had posted a `New-UDGauge` component to the powershell gallery under this account that I originally used. So unknown to me, this gauge component has had by far the most downloads but in my opinion was pretty naff [you can see a picture of it on this forum post](https://forums.universaldashboard.io/t/some-new-svg-universaldashboard-components/1206). This was one of the first components I built, and as I mentioned in a previous blog, start small, and go for as little or no dependencies as possible.

The component didn't exist, and at the time, and at that time that was my best effort. Until I stepped up to the challenge of [building this project here](https://www.npmjs.com/package/react-d3-speedometer) which list **6** dependencies, but one of those dependencies has **31** dependencies. [I did try and build this component prior](https://www.npmjs.com/package/react-gauge-chart) but it would just not render for me. So as I had spent some-time already downloading a load of dependencies, what is a load more depndencies to download?

I am glad I went for the second choice, as this component was a lot better documented, I only went for the other project first, as this listed only **1** dependency, which actually turned out to be **31** dependencies and as you know I prefer to use less dependencies.

## JSX Code

As I just mentioned this component had a lot better documentation with it, and it also meant you could pass loads more **props** to the component. So here is my completed **JSX** file for the component

```js
import React from "react";
import ReactSpeedometer from "react-d3-speedometer";
class UDGauge extends React.Component {
  render() {
    return (
      <ReactSpeedometer
        maxValue={this.props.maxValue}
        value={this.props.value}
        needleColor={this.props.needleColor}
        startColor={this.props.startColor}
        endColor={this.props.endColor}
        segments={this.props.segments}
        needleHeightRatio={this.props.needleHeightRatio}
        needleTransitionDuration={this.props.needleTransitionDuration}
        needleTransition="easeElastic"
        labelFontSize={this.props.labelFontSize}
        valueTextFontSize={this.props.valueTextFontSize}
        paddingHorizontal={this.props.paddingHorizontal}
        paddingVertical={this.props.paddingVertical}
        currentValueText={this.props.currentValueText}
        width={this.props.width}
        height={this.props.height}
      />
    );
  }
}
```

## Powershell Code

So for each prop, I want to pass as a parameter in the powershell function to run this component. The final powershell file looked like.

```
function New-UDGauge {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [int]$MaxValue = 100,
        [Parameter()]
        [int]$Value = 50,
        [Parameter()]
        [string]$NeedleColor = "steelblue",
        [Parameter()]
        [string]$StartColor = "green",
        [Parameter()]
        [string]$EndColor = "red",
        [Parameter()]
        [int]$Segments = 10,
        [Parameter()]
        [float]$NeedleHeight = "0.8",
        [Parameter()]
        [int]$NeedleTransition = 4000,
        [Parameter()]
        [string]$LabelFontSize = "20px",
        [Parameter()]
        [string]$ValueFontSize = "24px",
        [Parameter()]
        [int]$PaddingHorizontal = 17,
        [Parameter()]
        [int]$PaddingVertical = 17,
        [Parameter()]
        [string]$ValueText,
        [Parameter()]
        [int]$Width = 320,
        [Parameter()]
        [int]$Height = 195
    )

    End {

        @{
            type                     = "UD-Gauge"
            id                       = $Id
            maxValue                 = $MaxValue
            value                    = $Value
            needleColor              = $NeedleColor
            startColor               = $StartColor
            endColor                 = $EndColor
            segments                 = $Segments
            needleHeightRatio        = $NeedleHeight
            needleTransitionDuration = $NeedleTransition
            labelFontSize            = $LabelFontSize
            valueTextFontSize        = $ValueFontSize
            paddingHorizontal        = $PaddingHorizontal
            paddingVertical          = $PaddingVertical
            currentValueText         = $ValueText
            width                    = $Width
            height                   = $Height
        }
    }
}
```

I wanted people to be able to use this control out of the box so to speak, so that is the reason behind me giving a lot of these parameters default values. So lets just quickly go over all these parameters and what they do

- **MaxValue** - This is the last number which is displayed on the gauge. It can be any whole number
- **Value** This is the number which the needle of the gauge will be pointing at.
- **NeedleColor** Sets the colour of the needle being used on the gauge component
- **StartColor** Sets the colour which will be used for the lower numbers on the gauge component on the left hand side.
- **EndColor** Sets the colour which will be used for the highest numbers on the gauge component on the right hand side.
- **Segements** Specifies how many different colour segements you will have displayed
- **NeedleHeight** A floating number up to **1** currently set at 0.8 as default
- **NeedleTransition** Is the animation of the needle set in milliseconds default is 4000
- **LabelFontSize** Sets the outer number font size this is a string as needs the px adding
- **ValueFontSize** Sets the font which displays under the gauge component
- **PaddingHorizontal** Sets the horizontal padding for the outer labels being displayed
- **PaddingVertical** Sets the vertical padding for the outer labels being displayed
- **ValueText** Sets the text which is displayed under the gauge component, you will want to pass in the variable holding the `value` so it reads the number the needle is pointing at. If you do not include this parameter, no text will be displayed under the gauge.
- **Width** Sets the width of the gauge component.
- **Height** Sets the height of the gauge component

## Images

What would a blog be without some nice images of the finished product

![placeholder](https://user-images.githubusercontent.com/44211223/70393904-4ee52000-19e7-11ea-8bb8-86b471581b96.gif "Demo of component")
![placeholder](https://user-images.githubusercontent.com/44211223/70393915-6cb28500-19e7-11ea-8ef2-df1b36d34c2c.PNG "Example image")
![placeholder](https://user-images.githubusercontent.com/44211223/70393889-1f361800-19e7-11ea-9910-272b1db98ac5.PNG "Showing different segment amounts")

## Conclusion

This was by far the most dependencies I have ever had to download for any custom component which I have built. To be honest, I probably would never have thought I would have been able to achieve this result. Some-times the task seems more daunting than it actually turns out to be. The most time consuming thing for me was to download all the required npm packages for the component. Although I managed to get this built and working in a day, it did span across two days, as I noticed additional bottom padding was being caused by not having the width and height being passed to the component. I also added the ability to cusomize the font size and padding.
I could see this gauge control being used for many different reasons, and as it has a lot of parameters to customise the component, I am hoping you will see this as a good component to be added to the marketplace for universal dashboard
