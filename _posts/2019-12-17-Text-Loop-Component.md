---
date: 2019-12-17 12:26:40
layout: post
title: Text Loop Component
subtitle: Animated text loop component for your dashboard.
description: This blog covers my latest and greatest powershell universal dashboard custom component.
image: https://cdn.auth0.com/blog/illustrations/powershell.png
optimized_image: https://cdn.auth0.com/blog/illustrations/powershell.png
category: component
tags:
  - text
  - loop
  - component
author: psdevuk
---

## Welcome

So it's been like a whole 9 days since I published my last blog. During that time, I found some bugs in the gauge component I covered in my last blog, so I had to apply some fixes for that. I then was asked if it would be possible to customise the segment colours, and add custom stop points. So I went and achieved that, only to then find it broke my current gague so had to release that as another custom gauge component. Then tonight I find for whatever reasons the version I uploaded to the powershell gallery was dodgy and did not work correctly. So spent time tonight fixing that then pushing out release 1.0.1 so please check out that [right here on the universal dashboard marketplace](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDCustomGauge).

> I remember when I started my career in I.T and used to be amazed by people writing a batch file to complete a job. How things have changed. I never would of envisioned that one day it would be me automating things, and creating solutions to real-world business problems

I was thinking, what can I do for my next custom component. Like I am running out of ideas, as everything I build as a custom component I do it because it does not already exist in powershell universal dashboard. Like there is so many carousels out there but we have one already that the very talented Alon gave to the community.

After a while of randomly searching [npmjs.com I found this beauty](https://www.npmjs.com/package/react-text-loop) I thought it looked super nice. So lets get building

## React Text Loop

After looking at the demo and thinking **sweet** I then thought I should check how many dependencies this component consists of. It listed 3 components, so I was happy to go off and install each of those. I have covered how to do this in a previous blog, so please look at that for how to download and get building your own components.

After downloading each dependency I gave this a quick go to make sure it would work, which it did. Even better this custom component worked in Internet Explorer which I am forced to use at work, so that meant I could also implement this into one of my work dashboards.

## JSX File

So my final built JSX file looked like:-

```js
import React, { Fragment } from "react";
import TextLoop from "react-text-loop";
class UDTextLoop extends React.Component {
  render() {
    return (
      <span>
        {" "}
        <TextLoop
          children={this.props.children}
          springConfig={{
            stiffness: this.props.stiffness,
            damping: this.props.damping
          }}
          adjustingSpeed={this.props.adjustingSpeed}
          delay={this.props.delay}
          interval={this.props.interval}
        ></TextLoop>{" "}
      </span>
    );
  }
}

export default UDTextLoop;
```

## Function

The end powershell function looked like:-

```
function New-UDTextLoop {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [array]$Text,
        [Parameter()]
        [int]$Speed = 1000,
        [Parameter()]
        [int]$Stiffness = 180,
        [Parameter()]
        [int]$Damping = 8,
        [Parameter()]
        [int]$Delay = 2000,
        [Parameter()]
        [int]$Interval = 6000
    )

    End {

        @{
            # The AssetID of the main JS File
            assetId        = $AssetId
            # Tell UD this is a plugin
            isPlugin       = $true
            type           = "UD-TextLoop"
            # An ID is mandatory
            id             = $Id
            children       = $Text
            adjustingSpeed = $Speed
            stiffness      = $Stiffness
            damping        = $Damping
            delay          = $Delay
            interval       = $Interval
        }

    }
}
```

## Demo

![placeholder](https://user-images.githubusercontent.com/44211223/71037746-3926d780-2118-11ea-880c-7ce95493f76d.gif "Large example image")
![placeholder](https://user-images.githubusercontent.com/44211223/71037835-6a070c80-2118-11ea-84de-53a4c17305ad.gif "Medium example image")

## Conclusion

I am now using this custom component on my complaints dashboard at work. I really like this component, and is certainly an eye catcher for the user to look at. It is also a good way to get more text content on a card as you can change it on-the-fly. Well I hope to see the downloads for this custom component sky rocket after this blog.[You can find the component here](https://www.powershellgallery.com/packages/UniversalDashboard.UDTextLoop/1.0.0) hope to see you next time.
