---
date: 2019-12-01 23:23:45
layout: post
title: Bringing a slider component
subtitle: Another new control walk through.
description: This post was inspired by another fellow universal dashboard user the mighty Alon Gvili who to me is a legend for all the contributions he has done to universal dashboard.
image: https://cdn0.tnwcdn.com/wp-content/blogs.dir/1/files/2017/03/Facebook-React-796x398.jpg
optimized_image: https://cdn0.tnwcdn.com/wp-content/blogs.dir/1/files/2017/03/Facebook-React-796x398.jpg
category: slider
tags:
  - slider
  - component
  - custom
author: psdevuk
---

## Slider Component

So I was on the <a href="https://forums.universaldashboard.io/">universal dashboard forum</a>, the other day and I saw that Alon had updated his <a href="https://udantd.site/home">universal dashboard antd library</a> mentioning about the slider component. I looked at this slider component in **awe** and was like why doesn't this component exist already in universal dashboard?

> So this whole blog has been inspired by the amazing work Alon is doing on his UDantd project which is integrating a whole new library of components to powershell universal dashboard. Go Alon!

## Please check out the UDAntd site

As mentioned this blog has been inspired by the outstanding work Alon is currently doing **please go check out all the goodness he is cooking up** <a href="https://udantd.site/home">on his website by clicking this link</a>

## Inspiration started...

So after seeing the amazing new components coming to powershell universal dashboard courtesy of Alon, I was thinking there is not a `New-UDSlider` in powershell universal dashboard at the moment. To be sure I visited [the official documentation site](https://docs.universaldashboard.io/) but could not see any mention of a slider. Coming to think of it, I had not seen or used one myself, but like the `New-UDInputField -Type time -Name StartTime -Placeholder 'Start Time'` you always must be sure it does not exist before you go off and build the component, that already exists in powershell universal dashboard, else you are duplicating something that already exists.

## Time to get building

As always I like to build components that do not currently exist in powershell universal dashboard, and have as little or no dependencies as possible. So as always I looked on [npmjs.com](https://www.npmjs.com/) and I found numerous sliders on that site. So after having a good long hard think, I decided to roll with [this choice](https://www.npmjs.com/package/react-range) I could see that other sliders only went up to 100, and I was thinking I have done percentage before, so wanted a slider that could go above 100. I also liked the fact of how this slider was styled, and it had a good few different examples of how you could use this.

## Take two...

So after a few attempts, which does seem a lot less than all the attempts of my first few components, I had a working slider with some modifications I had thrown in. So here is the slider in action:-

![placeholder](https://user-images.githubusercontent.com/44211223/69921344-b0a60700-1488-11ea-84b5-8c9ef602000e.gif "Demo of component")

I am thinking of adding this as a statistical slider to show performance by depot on my complaints dashboard I got at work. I mean like I believe with this product, is that the only thing that holds you back is your imagination.

## JSX file

```js
{% raw %}
import React from 'react';
import { Range, getTrackBackground } from 'react-range';

const STEP = 1;
const MIN = 0;
class <%=$PLASTER_PARAM_ControlName%> extends React.Component {
  state = {
    values: [this.props.values]
  };
  render() {
    return (
      <div
        style={{
          display: 'flex',
          justifyContent: 'center',
          flexWrap: 'wrap'
        }}
      >
        <Range
          values={this.state.values}
          step={STEP}
          min={MIN}
          max={this.props.max}
          onChange={values => this.setState({ values })}
          renderTrack={({ props, children }) => (
            <div
              onMouseDown={props.onMouseDown}
              onTouchStart={props.onTouchStart}
              style={{
                ...props.style,
                height: '36px',
                display: 'flex',
                width: '100%'
              }}
            >
              <div
                ref={props.ref}
                style={{
                  height: '5px',
                  width: '100%',
                  borderRadius: '4px',
                  background: getTrackBackground({
                    values: this.state.values,
                    colors: ['#548BF4', '#ccc'],
                    min: MIN,
                    max: this.props.max
                  }),
                  alignSelf: 'center'
                }}
              >
                {children}
              </div>
            </div>
          )}
          renderThumb={({ props, isDragged }) => (
            <div
              {...props}
              style={{
                ...props.style,
                height: '21px',
                width: '21px',
                borderRadius: '4px',
                backgroundColor: '#FFF',
                display: 'flex',
                justifyContent: 'center',
                alignItems: 'center',
                boxShadow: '0px 2px 6px #AAA'
              }}
            >
              <div
                style={{
                  position: 'absolute',
                  top: '-28px',
                  color: '#fff',
                  fontWeight: 'bold',
                  fontSize: '14px',
                  fontFamily: 'Arial,Helvetica Neue,Helvetica,sans-serif',
                  padding: '4px',
                  borderRadius: '4px',
                  backgroundColor: '#548BF4'
                }}
              >
                {this.state.values[0]}
              </div>
              <div
                style={{
                  height: '16px',
                  width: '5px',
                  backgroundColor: isDragged ? '#548BF4' : '#CCC'
                }}
              />
            </div>
          )}
        />
      </div>
    );
  }
}

export default <%=$PLASTER_PARAM_ControlName%>
{% endraw %}
```

## PS1 file

```
function <%=$PLASTER_PARAM_CommandName%> {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [int]$Max,
        [Parameter()]
        [int]$Value

    )

    End {

        @{
            # The AssetID of the main JS File
            assetId  = $AssetId
            # Tell UD this is a plugin
            isPlugin = $true
            type     = "<%=$PLASTER_PARAM_ControlTypeName%>"
            # An ID is mandatory
            id       = $Id

            values   = $Value
            max      = $Max
        }

    }
}
```

## Demo Dashboard

```
Import-Module UniversalDashboard.Community
Import-Module "C:\UD\UDSlider\Slider\src\output\UniversalDashboard.udslider\UniversalDashboard.udslider.psd1"
Get-UDDashboard | Stop-UDDashboard
#$endpointinit = New-UDEndpointInitialization -Module @("UniversalDashboard.UDNumber")
$theme = get-udtheme "DarkRounded"
$dashboard = New-UDDashboard -Title "New-UDSlider" -theme $theme -Content {
    New-UDRow -Columns {
        New-UDColumn -Size 3 -Content {
            New-udcard -Content {
                new-udslider -Value 23 -Max 400
            }
        }
    }
}
Start-UDDashboard -Dashboard $dashboard -Port 10005
```

The above code produces the dashboard which I used in this demo

![placeholder](https://user-images.githubusercontent.com/44211223/69921344-b0a60700-1488-11ea-84b5-8c9ef602000e.gif "Demo of component")

So will probably update this blog when I put this component onto a dashboard I am using, to show what it looks like. As you can see in the style, it uses 100% of the page width, so if you do not want it to span the whole page, you will need to put it in a column or layout that does not go the whole distance of the page.

I didn't modify any of the default colours being used as I thought they would work well for any theme you are using.

As mentioned this whole thing was inspired by the UDantd library Alon is working on.

## Conclusion

I have now posted this module to the powershell gallery I hope this component is useful for a dashboard you are working on.
