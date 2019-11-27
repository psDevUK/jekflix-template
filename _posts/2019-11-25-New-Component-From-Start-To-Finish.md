---
date: 2019-11-25 21:54:00
layout: post
title: New Component From Start To Finish
subtitle: So in this blog I cover a new component which I built this evening.  I cover everything from start to finish. This is a basic component which will give a count indicator.
category: New Component
image: https://user-images.githubusercontent.com/44211223/69577694-d7ff5e80-0fc6-11ea-8524-f530fe3e85d1.PNG
optimized_image: https://user-images.githubusercontent.com/44211223/69577694-d7ff5e80-0fc6-11ea-8524-f530fe3e85d1.PNG
tags:
  - building
  - component
  - create
author: psdevuk
---

So me and my big mouth. I posted this blog-site on twitter and asked for some suggestions on what would be a good blog to write about. I got some replies on technoloy I had never heard of. They were good suggestions don't get me wrong, but as mentioned before I am no react ninja, and felt that these were quite big projects for anyone.

Being a dad to 4 daughters and working full-time means I just didn't see myself being able to pull off one of those requests in time for this next blog, just due to the amount of reading and studying, not saying I will not look at one of the challenges, but they were setting the bench-mark pretty high.

So looking for something to write on my next blog, thought it would be a good topic to talk about building a new component. So should you wish to build something custom for powershell universal dashboard, then you know the steps to take.

> This is just how I go about building my components for Powershell Universal Dashboard. I am not a react developer. I just try my best.

## Where to start?

As mentioned in a previous blog, the powershell universal dashboard forum is a great place to go to learn, or get inspiration on the product. The forum is broken down into different forum rooms for different aspects of the product. [The UD Development](https://forums.universaldashboard.io/t/about-the-ud-development-category/1285) section of the forum has all the links you should need to get started on building a component.

## Next step

So after looking through the links mentioned on the forum page I am hoping you have downloaded your copy of the [custom component template from github](https://github.com/ironmansoftware/ud-custom-control-template) so you are pretty much half way there on the journey now.

Now you need to find a component to build. So I found the component I am blogging about on
[react js example website](https://reactjsexample.com/) so after I found out the name of the component on this site, by looking at the code on the page I saw `npm install --save react-score-indicator` so then I headed over to [npmjs](https://www.npmjs.com/) to search for `react-score-indicator`

Most of importantly is now to look at the dependencies for the component you wish to build. Thankfully this component had zero dependencies. Should the component you wish to build does have dependencies, then you need to `--save` each of those dependencies and sub-dependencies. Personally I do not know a quick way to do this, so it involves downloading each package on it's own. Some components I built it's taken me so long to get all the dependencies. So I recommend for an easier ride, the less dependencies the better, as not only will this save you shed loads of time downloading, but will also make your component smaller in file size, meaning quicker loading on your dashboard page.

## JSX Code

So from the template I ended up with this:-

```js
import React from 'react';
import ReactStoreIndicator from 'react-score-indicator';
class <%=$PLASTER_PARAM_ControlName%> extends React.Component {

  // state is for keeping control state before or after changes.
  state = {

    // the things you want to put in state.
    // text: this.props.text //un comment the line to use state insted props
  }


  render() {

      // These props are returned from PowerShell!
      // return <h1>{this.state.text}</h1> // un comment the line to render using value from state.

      return (
      <ReactStoreIndicator
        value={this.props.value}
          maxValue={this.props.maxValue}
          width={this.props.width}
          lineWidth={this.props.lineWidth}
          lineGap={this.props.lineGap}
      />
    )

  }
}

export default <%=$PLASTER_PARAM_ControlName%>
```

So now for some **more code** we need to call each of these **props** we have defined in the **JSX** in the **powershell function** file.

```js
function <%=$PLASTER_PARAM_CommandName%> {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [int]$Value = 1,
        [Parameter()]
        [int]$MaxValue = 100,
        [Parameter()]
        [int]$Width = 200,
        [Parameter()]
        [int]$LineWidth = 5,
        [Parameter()]
        [int]$LineGap = 5
    )

    End {

        @{
            # The AssetID of the main JS File
            assetId   = $AssetId
            # Tell UD this is a plugin
            isPlugin  = $true
            # This ID must be the same as the one used in the JavaScript to register the control with UD
            type      = "UD-Indicator"
            # An ID is mandatory
            id        = $Id

            # This is where you can put any other properties. They are passed to the React control's props
            # The keys are case-sensitive in JS.
            value     = $Value
            maxValue  = $MaxValue
            width     = $Width
            lineWidth = $LineWidth
            lineGap   = $LineGap

        }

    }
}
```

## Time to build

So you have to make sure **before** building this component you have **CD** to the **src** directory in the custom component template and run `npm install --save react-score-indicator` to download the required nodejs files. Now **CD** back a level to the root of the template, and run the udbuild script, specifying an output directory. Something like:- `.\UD.Build.ps1 C:\ud\Score\Indicator`

On my old laptop this takes a good few minutes to fully build.

## Code to test component

So I like to write a simple as possible dashboard to test that my component will load and can display some sort of indicator of a score. As I tried to keep things as simple as possibly in the JSX file I did not **bind** this component to universaldashboard. Nor in the function have a included extra code to handle an `-Endpoint` script block, as the component is not **bound** to universaldashboard.

I wanted to see that this component could dynamically tell me how many services were running out of all the services on my computer. So I came up with the following script:-

```js
Import-Module -Name UniversalDashboard.Community
Import-Module -Name UniversalDashboard.UDIndicator
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10005 -Dashboard (
  New-UDDashboard -Title "Powershell UniversalDashboard" -Content {
    New-UDLayout -Columns 6 -Content {
      New-UDHeading -Size 4 -Text "Running Services"
      $services = get-service
      $running = ($services | ? { $_.Status -eq 'Running' })
      New-UDIndicator -Value $running.count -MaxValue $services.count -Width 200
    }

  }
)
```

Boom I got a working powershell universal dashboard component that has multiple parameters. **Big up to @BoSen29 for the modification on the above example**

## Next step

After verifying that the component worked, the next thing I like to do is to then share this with the community. So I signed up to the powershell gallery and got my API key and I posted the module to the powershell gallery

![placeholder](https://user-images.githubusercontent.com/44211223/69577694-d7ff5e80-0fc6-11ea-8524-f530fe3e85d1.PNG "Custom Component")

As I included the required tags, this module will then also be synchronized to the powershell universal dashboard marketplace.

## Conclusion

I hope this blog inspires you to go out and find some super cool react components to help extend the components which are available to powershell universal dashboard users. Peace.
