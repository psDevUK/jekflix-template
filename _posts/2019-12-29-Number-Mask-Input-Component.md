---
date: 2019-12-29 19:26:40
layout: post
title: Number Mask Input Component
subtitle: Allows you to create custom input fields that only support numeric formats given to them as a parameter.
description: This blog covers my latest and greatest powershell universal dashboard custom component.
image: https://miro.medium.com/max/1060/1*VVqqeKJsVCG-qrm6uqxB5A.png
optimized_image: https://miro.medium.com/max/1060/1*VVqqeKJsVCG-qrm6uqxB5A.png
category: component
tags:
  - numeric
  - mask
  - input
  - component
author: psdevuk
---

## Welcome
So I hope you had a nice Christmas and made it onto the good list to receive some presents? Well moving on swiftly this blog is covering the new component I managed to build for universaldashboard. What makes this a bit different from the rest of my components is I had some help in getting this working correctly with universal dashboard. It feels like some sacred ninja art in binding the component you are building to read the values that have been put in state by the user.
  As I like comic-books yes I am 37, but I saw this as an amazing super-hero team-up of two different nations.  So without babbling on too much @bosen29 is my super-sidekick in this thrilling tale of **the missing link**
[ get your copy right here on the universal dashboard marketplace](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDCustomGauge).

> Before using Universal Dashboard I had only used github to grab a bit of code from a repository. I didn't really understand github or what having open source software was all about. This soon changed when I became addicted to Universal Dashboard

I just want to say that me and my crime fighting react partner had nothing to do with open source prior to using powershell universal dashboard. Like me @bosen29 is also an avid user of the universal dashboard forums.  In fact although I have created some weird and wacky components, @bosen29 has done a lot of contributions and commits as well as adding new cmdlets to the official universal dashboard repository.

So naturally I was honured to team up with @bosen29 when he offered his assistance.  See my problem was I built the component it worked, I could pass the pattern of the format I wanted and it worked...but sadly it was the binding bit that I couldn't figure out, so I couldn't actually read the input of what had been typed.  Meaning the component was pretty useless.

Although I no longer use Powershell Studio since purchasing universal dashboard, the one thing I did miss was having the ability to have a masked input control. To me this makes the application you are building more **fool proof** as end-users are wonderful, and all have their own ideas on how to input something.  Just like a date format, there are numerous ways this could be inputted, but having a masked control removes that issue. So after searching [npmjs.com I found this number mask](https://www.npmjs.com/package/react-number-format) it looked like it ticked all the boxes for numeric input, so I got building it.

## React Number Format

As mentioned I was able to build this component and had it working with the parameters I passed it for the number format mask, but I couldn't figure out how to read the values. So this is where @bosen29 stepped in and did some magic. The below JSX file is what makes this component talk to universal dashboard so it can be bound to the session you are running and reading from the state of the component when requested.

## JSX File

So my final built JSX file looked like:-

```js
import React from 'react';
import NumberFormat from 'react-number-format';
class UDNumberMask extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: this.props.value,
      displayType: 'input',
      isNumericString: true,
      format: this.props.format,
      mask: this.props.mask,
      placeholder: this.props.placeholder,
      hidden: false
    }
  }

  componentWillMount() {
    this.pubSubToken = PubSub.subscribe(this.props.id, this.onIncomingEvent.bind(this));
  }

  componentWillUnmount() {
    PubSub.unsubscribe(this.pubSubToken);
  }

  onIncomingEvent(eventName, event) {
    if (event.type === "requestState") {
      var data = {
        attributes: {
          value: this.state.value,
          hidden: this.state.hidden,
        }
      }
      UniversalDashboard.post(`/api/internal/component/element/sessionState/${event.requestId}`, data);
    }
    else if (event.type === "setState") {
      this.setState(event.state.attributes);
    }
    else if (event.type === "clearElement") {
      this.setState({
        value: null
      });
    }
    else if (event.type === "removeElement") {
      this.setState({
        hidden: true
      });
    }
  }

  onChanged(e) {

    this.setState({
      value: e.target.value
    });

    if (this.props.onChange == null) {
      return
    }

    var val = e.target.value;

    UniversalDashboard.publish('element-event', {
      type: "clientEvent",
      eventId: this.props.id + "onChange",
      eventName: 'onChange',
      eventData: val.toString()
    });
  }

  render() {

    if (this.state.hidden) {
      return null;
    }
    return (
      <NumberFormat getInputRef={(el) => this.inputElem = el}
        format={this.state.format}
        mask={this.state.mask}
        placeholder={this.state.placeholder}
        value={this.state.value}
        onValueChange={(values) => {
          const { formattedValue, value } = values;
          this.setState({ value: formattedValue })
        }}
        onChange={this.onChanged.bind(this)}
      />
    )
  }
}
export default UDNumberMask

```

## Function

The end powershell function looked a bit more complex than my usually functions as this was using the **onChange** which was used to **bind** to universal dashboard.

```
function New-UDNumberMask {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [string]$Format,
        [Parameter()]
        [array]$Mask = '',
        [Parameter()]
        [object]$OnChange,
        [Parameter()]
        [string]$PlaceHolder
    )

    End {

        if ($null -ne $OnChange) {
            if ($OnChange -is [scriptblock]) {
                $OnChange = New-UDEndpoint -Endpoint $OnChange -Id ($Id + "onChange")
            }
            elseif ($onChange -isnot [UniversalDashboard.Models.Endpoint]) {
                throw "OnChange must be a script block or UDEndpoint."
            }
            $activeOnChange = "true"
        }

        @{
            # The AssetID of the main JS File
            assetId     = $AssetId
            # Tell UD this is a plugin
            isPlugin    = $true
            # This ID must be the same as the one used in the JavaScript to register the control with UD
            type        = "UD-NumberMask"
            # An ID is mandatory
            id          = $Id
            # The keys are case-sensitive in JS.
            format      = $Format
            mask        = $Mask
            placeholder = $PlaceHolder
            onChange    = $activeOnChange
        }

    }
}
```

## Demo

 Below you will see this component being used within a dashboard which produces the results which are shown in the gif below this demo script.

```
Import-Module UniversalDashboard
Import-Module UniversalDashboard.UDNumberMask
Get-UDDashboard | Stop-UDDashboard
$theme = New-UDTheme -Name "Basic" -Definition @{
    '::placeholder' = @{
        'color'   = "black"
        'opacity' = "1"
    }
} -Parent "Default"
$dashboard = New-UDDashboard -Title "New Component" -Theme $theme -Content {
    New-UDRow -Columns {
        New-UDColumn -size 2 -Content {
            New-UDNumberMask -Id "num1" -Format "##/##" -PlaceHolder "MM/YY" -Mask "M", "M", "Y", "Y"  -OnChange {
                Show-UDToast -Message "You have entered:-$eventData" -Position topLeft -Duration 2000
            }
            New-UDNumberMask -Id "num2" -Format "###.###.#.##" -PlaceHolder "Ip Address"
            New-UDNumberMask -Id "num3" -Format "####-####-####-####" -PlaceHolder "Formatted Card"
            New-UDNumberMask -Id "num4" -Format "+44 (#####)-######" -PlaceHolder "Phone Number"
            New-UDButton -Text "Toast" -OnClick {
                #Show-UDToast -Message "You typed $(Get-UDElement -Id 'num2')" -Duration 4000
                $val = (Get-UDElement -id "num2").Attributes.value
                Show-UDToast -Message "IP Address:- $val" -Position topLeft -Duration 4000
            }
            New-UDButton -Text "RemoveMe" -OnClick {
                Remove-UDElement -id "num2"
            }
            New-UDButton -text "ShowME" -OnClick {
                Set-UDElement -id "num2" -Attributes @{
                    hidden = $false
                }
            }
            New-UDButton -Text "ClearMe" -OnClick {
                Clear-UDElement -Id "num2"
            }

        }
    }

}
Start-UDDashboard -Dashboard $dashboard -Port 10005
```

![placeholder](https://user-images.githubusercontent.com/44211223/71381263-a4feb980-25ca-11ea-8651-e1bd9219b031.gif "example image")
)

## Conclusion

I was super chuffed to have received enough interest from a fellow dashboarder who was kind enough to donate me his time and knowledge in this open source project that is universal dashboard.  These were the **missing links** that I didn't understand, but after having a good super-hero team-talk on it, the whole mystery was unfolded.  So big-up to @bosen29 for all the help you gave in making this component. [You can find the component here](https://www.powershellgallery.com/packages/UniversalDashboard.UDNumberMask/1.0.0)
 Thanks for reading.