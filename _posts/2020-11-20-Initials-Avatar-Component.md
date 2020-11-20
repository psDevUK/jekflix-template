---
date: 2020-11-20 18:24:20
layout: post
title: Initials Avatar Component
subtitle: Nice simple component to display initials as an icon or avatar
description: This blog covers a brand new component I have built for Universal Dashboard. The blog will cover this initials avatar component and how to add it to your dashboard
image: https://www.gravatar.com/avatar/b116f04b79df87fb95b7bd41c3c85a07?d=https%3A%2F%2Fwww.elitefts.com%2Fmedia%2Fgravatar%2Fprofile-default.png&s=30
optimized_image: https://i1.wp.com/aaronphelan.me/wp-content/uploads/2020/06/undraw_male_avatar_323b.png?fit=2113%2C2113&ssl=1
category: component
tags:
  - Component
  - Initials
  - Avatar
  - Demonstration
author: psdevuk
---

## Welcome

 Just a quick note to say thanks for clicking on the link which has taken you to this blog page. In this blog I am looking to document this new **Initials Avatar** that I have now built and got working in UniversalDashboard.  

## Where Did You Find It?

As with pretty much all of the components I build I found this on **npmjs.com** the exact link to the [project can be found by clicking on this link](https://www.npmjs.com/package/react-initials-avatar) so as the example code didn't look overly complicated, I thought I should be able to pull this off.
However sadly I couldn't figure out how to style this within the JSX file you compile when building a component for UniversalDashboard.  However as always with Powershell there is still a way to achieve all the styling you could possibly want to do with this component, and that is once again all thanks to **Adam Driscoll** who released a great module a while ago, which I did blog on Universaldashboard.Style which is on the marketplace and powershell gallery. 
![placeholder](https://github.com/ironmansoftware/ud-style/raw/master/images/logo.png "UniversalDashboard.Style")


## What Parameters Does It Have?

Well if you have a butchers at the original project on npmjs I have included the only **prop** as a powershell parameter ```-Name``` So literally you just specify a name as a string object for this parameter for it to display the initials.  How hard can that be...right?


## Example Using The Component

I'm sure any dashboard user could get this component working with ease, but you might then be like, well it's not that fancy as it always produces the same type of avatar style for each name, so how can you personalise it a bit?

```
Import-Module -Name UniversalDashboard.Community -RequiredVersion 2.8.1
Import-Module -Name UniversalDashboard.Style
Import-Module -Name UniversalDashboard.NoAvatar
Get-UDDashboard | Stop-UDDashboard

$Initialization = New-UDEndpointInitialization -Module 'UniversalDashboard.NoAvatar'

$Footer = New-UDFooter -Copyright 'PSDEVUK' -Endpoint {New-NoAvatar -Id "LOOK4ME" -Name $env:USERNAME} -RefreshInterval 2
$NavBarLinks = @((New-NoAvatar -Id "NavAvatar" -Name $env:USERNAME))
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Footer $Footer -EndpointInitialization $Initialization -NavbarLinks $NavBarLinks  -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 2 -Content {
                New-UDStyle -Style '.initials-avatar {
	width: 48px;
	height: 48px;
	cursor: pointer;
	border-bottom-left-radius: 25%;
	border-bottom-right-radius: 25%;
	border-top-right-radius: 25%;
	border-top-left-radius: 25%;
	background-color: lightblue;
	display: inline-block;
	box-sizing: border-box;
}
.initials-avatar div {
	color: #000;
}' -Content {
New-NoAvatar -id "AVATAR" -Name "Adam Bacon"
                }

            }
            New-UDColumn -Size 1 -Content {
               New-UDStyle -Style '.initials-avatar {
	width: 48px;
	height: 48px;
	cursor: pointer;
	border-bottom-left-radius: 0%;
	border-bottom-right-radius: 0%;
	border-top-right-radius: 0%;
	border-top-left-radius: 0%;
	background-color: blue;
	display: inline-block;
	box-sizing: border-box;
}
.initials-avatar div {
	color: #fff;
}' -Content {
New-NoAvatar -id "AVATAR2" -Name "Some.Name"
                }

            }
            New-UDColumn -Size 1 -Content {
                                           New-UDStyle -Style '.initials-avatar {
	width: 24px;
	height: 24px;
	cursor: pointer;
	border-bottom-left-radius: 0%;
	border-bottom-right-radius: 0%;
	border-top-right-radius: 12%;
	border-top-left-radius: 12%;
	background-color: pink;
	display: inline-block;
	box-sizing: border-box;
}
.initials-avatar div {
	color: #fff;
}' -Content {
New-NoAvatar -id "AVATAR3" -Name "Bruce Banner"
                }
            }
            New-UDColumn -Size 4 -Content {
                                           New-UDStyle -Style '.initials-avatar {
	width: 124px;
	height: 124px;
	cursor: pointer;
	border-bottom-left-radius: 12%;
	border-bottom-right-radius: 12%;
	border-top-right-radius: 12%;
	border-top-left-radius: 12%;
	background-color: darkorange;
	display: inline-block;
	box-sizing: border-box;
    font-size: xxx-large;
}
.initials-avatar div {
	color: #f0f0f0;
}' -Content {
New-NoAvatar -id "AVATAR4" -Name "Adam Driscoll"
                }
            }
        }


    }
)

```

## Which Gives You This

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/InintialsavatarDemo.PNG?raw=true "Component Demo")

  I figured the CSS I needed to edit from the same methods described in my CSS blog I wrote on this site. I know this demo picture doesn't look that amazing, but just showing you the possibilities of what you can do with this component. I did see a post on the UD forums requesting either an avatar picture or initials to appear where the sign out is.  As I am not using a pro version in this demo I am merely proving the theory that this is possible and looks sweet. I will be looking to implement this in the top navbar on my work dashboards. 

## Conclusion

Thanks for taking the time to read this blog. I think there are many places you could use this component, and I really do hope it finds its way to your dashboard. Once again thanks for reading
