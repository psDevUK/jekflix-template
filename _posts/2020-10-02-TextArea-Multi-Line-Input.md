---
date: 2020-10-02 10:29:40
layout: post
title: TextArea Multi Line Input
subtitle: A blog covering a forum topic on multi line input and how I approached answering it.
description: This blog is about another new component I built to solve an issue other users of Universal Dashboard presented. Which was how to get a multi line input text box.
image: https://react-spectrum.adobe.com/ReactSpectrum_976x445_2x.711c2311.png
optimized_image: https://reactnativecode.com/wp-content/uploads/2017/12/Gradient_TextInput_Thumb.png
category: component
tags:
  - TextArea
  - Input
  - Multi
  - Line
author: psdevuk
---

## Welcome
Another day another blog. Trying to keep the momentum of these blogs going. I still think Universal Dashboard is the best thing since sliced bread. I mean I know Powershell Universal is out now, which kind of now super-seeded Universal Dashboard but with having 4 kids and working full time, just not even had the chance to try it out yet.  So this is on my list of things to do and I think if you haven't added it to your list of things to do, do it. 


## What is this blog about?
This blog is going to cover a recent forum post that got resurrected from April. The post can be found here:- [forum question on UD](https://forums.universaldashboard.io/t/multiline-for-new-udtextbox/2651) 
Well I did my best at the time to answer it, and well got no reply from the initial person who raised the question. Then another UD forum user brought the thread back to life, asking if there was ever an official answer to the question.  
 So I thought this would make a good blog to cover, and that folks is what this blog is about.


## Steps I took next
No official answer had been posted, I had actually taken the afternoon off work, as I needed to do some DIY, which is not something I am good at (should of taken two weeks off). So after doing some manly DIY I got onto the forum, and saw a post that I was involved in back in April 2020 had been brought back to life by another user wanting to know how to do this. So as I was involved in the initial discussion I thought I would take on the challenge and whip-up a dedicated component to do just this, as the original topic owner had gone quiet thought would be good to put something out there for everyone who might stumble across this in the future, like the user who resurrected the thread. In hindsight I should have looked through the updates on github for UD, and paramters of my UD cmdlets/functions as a user mentions in the thread (after I built it) that a parameter was added to allow multi line input. 
  Doh!
 When looking to solve something don't re-invent the wheel.  Have a look what has been done out there already and what is availble to use, and integrate it with the mighty universaldashboard. [So I found this react component](https://alioguzhan.github.io/react-editext/) which to me looked like it ticked all the boxes.  I am running an old core i3 laptop, and the initial build takes about 10 minutes to complete on my laptop. Ten minutes later I had a new multi line component that was working in Universal Dashboard. Wahoo! Problem solved.  Well not quite yet. Although I had proved the theory that yes this react component worked in UD, it was still pretty useless, as it wasn't bound to UD so the text entered into the textbox couldn't be read back from UD.
  Thankfully I have built quite a few custom components for Universal Dashboard (60+) and I was able to look through my existing code samples from previous components, and worked out how I could set the text entered to be held in the state of the component, which you can then read from in UD. 
 When building a component it is always good to find as many examples as you can and to read through the documentation so you can understand all the parameters used, and how you can incorporate them into your powershell function as parameters for the component. 


## New-UDMultiLine Parameters
 It was pretty late when I built this component, and New-UDMultiLine was the best name I could think of at the time, so that is the name of this component and here is a list of the parameters:-
- **-Placeholder** is a string parameter used for the placeholder of the textarea
- **-Rows** is an integer value used to determine how many rows high the textarea is
- **-Text** is a string value and is used to set the initial text for the textarea
- **-Hint** is a string value which displays small text underneath the textarea
- **-ButtonAlign** is a validated set of **before** or **after** to determine the button location
- **-SaveButtonText** is a string value for if you want text on the save button
- **-CancelButtonText** is a string value for if you want text on the cancel button
- **-EditButtonText** is a string value for if you want text on the edit button
- **-HideIcons** is a boolean value defaulted to `$true` if you wish to hide these set it to `$false`
- **-EditOnClick** is a boolean value defaulted to `$true` to allow you to click in the textarea to edit the text instead of being forced to click on the edit button.
- **-Outline** is a validated set of **none** or **solid** depending if you want an outline appearing on the textarea, this is defaulted to **none**

## Demo of component

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/MultiLineFinal.gif?raw=true "Component Demo")
[This component is now on the marketplace download your copy here](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDMultiLine)
## Code behind the Demo

```
Import-Module -Name UniversalDashboard
Import-Module -Name UniversalDashboard.UDMultiLine
$Theme = New-UDTheme -Name "demo" -Definition @{
    '.styles_Editext__buttons_container__1kphL' = @{
        'display' = "block ruby !important"
    }
} -Parent "Default"
$endpointinit = New-UDEndpointInitialization -Module @("UniversalDashboard.UDMultiLine")
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10004 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Theme $Theme -EndpointInitialization $endpointinit -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 4 -Endpoint {
                New-UDMultiLine -Id "MULTILINE" -Text "Does this really work I wonder...?" -Outline none -Rows 4 -EditButtonText "Click 2 Edit" -SaveButtonText "Accept" -CancelButtonText "Cancel" -ButtonAlign after -Hint "Just type some stuff"
            }
            New-UDColumn -size 4 -Endpoint {

                New-UDButton -Text "Get Text" -OnClick {
                    $Session:mtext = ((Get-UDElement -Id "MULTILINE").Attributes.text)
                    Show-UDToast -Message "You typed:- $Session:mtext" -Position topLeft -Duration 3000
                }
            }
        }

    }
)

```

## New-UDSingleLine
Not that I am not bigging up this component as much as the multi line component, I only built the single line to keep the same look and feel if you wanted a single line input. I believe consistency is key when building good looking dashboards. So this component has all the same parameters as above, but **the single line component does not include the Rows parameter and also does not include the Placeholder parameter** all the other parameters which are descibed in the **New-UDMultiLine** above will also work in the **New-UDSingleLine**
![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/SingleLine.gif?raw=true "Single Line Demo")
[Get your copy of this custom component from the market place right here](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDSingleLine)
## Few Important things to consider
 So I have not used this component yet in production, just merely proved that it works with UD and can read the text entered into the component.  However I did notice that the button did change shape a bit depending on how much was typed column size etc. So I fixed this by tweaking the CSS behind the component, which I explained how to do in a previous blog. So please note to keep the **edit** button from resizing itself I used the following CSS in a custom theme, and combined this with the parent theme like so:-
 ```
 $Theme = New-UDTheme -Name "demo" -Definition @{
    '.styles_Editext__buttons_container__1kphL' = @{
        'display' = "block ruby !important"
    }
} -Parent "Default"
 ```
That is why that is in the code.  Please also remember which I have documented in a previous blog, as this is a custom component, as well as importing the custom component into powershell UD like so:-
```
Import-Module -Name UniversalDashboard.UDMultiLine
```
You  will also have to include this **powershell module** as an **New-UDEndpointInitialization** so I am doing this in the below code by storing the **New-UDEndpointInitialization** as a variable named `$endpointinit` then applying that into the dashboard using `-EndpointInitialization $endpointinit` this is all shown below:-
```
$endpointinit = New-UDEndpointInitialization -Module @("UniversalDashboard.UDMultiLine")
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10004 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Theme $Theme -EndpointInitialization $endpointinit -Content {
```
By doing these steps you will now be able to access this component in the endpoint script block.  Again I covered that in a previous blog. Although the demo code I have posted is simple, it proves that this component as long as you give the component an `-Id` like I did `New-UDMultiLine -Id "MULTILINE"` I can then access that component in my dashboard from another control by referencing the **ID** and the attributes the component has, which in this case is just the **text** I did this by using `$Session:mtext = ((Get-UDElement -Id "MULTILINE").Attributes.text)` you can find out more about **Session** variables on the official documentation page for UD, but I decided this would by the best variable to store this in. 

## Conclusion
 Not that I am ever looking for things to take on, as I already got 4 kids to look after, but this did turn out a fun challenge to take on, and prove any doubters out there that this could be done.  Yeah I might of taken the slightly longer route to achieve the goal, but now there is a component out there which can handle multiplle lines of text and be able to get what was typed into the **textarea** by reading the value of the text being held in the state of the component. Next step for me is to publish this to the powershell gallery. To keep your dashboard looking consistent I will do the single line of this same component as well.  Thanks for reading.
