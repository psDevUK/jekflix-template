---
date: 2020-01-29 19:26:40
layout: post
title: Minesweeper The Game
subtitle: Fully featured game from back in the day Windows 95
description: Releasing the first full component game for universaldashbord.
image: https://lh3.googleusercontent.com/proxy/Yw011WYWLRdg2IuRo4-i9eqG-Bv-rTPMWuh3MIXeaKsq8nTr5xDE-e3Byzp0LpqdEsxVcG4gOfvzNi3p
optimized_image: https://lh3.googleusercontent.com/proxy/Yw011WYWLRdg2IuRo4-i9eqG-Bv-rTPMWuh3MIXeaKsq8nTr5xDE-e3Byzp0LpqdEsxVcG4gOfvzNi3p
category: component
tags:
  - Minesweeper
  - Game
  - Windows95
  - component
author: psdevuk
---

## Welcome
Ok so I saw react had minesweeper, and I was like what! Minesweeper! I used to play this game like 20 odd years ago and it never made any sense. Would it now make sense to me as a grown man? Just the thought of having Windows 95 game in my browser was too much of a temptation to pass up.  I needed to build this game.
[ available on the universal dashboard marketplace](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDMineSweeper).

## Origin Of Component

  Well I guess this component started way back in 1995 on Windows 95.  When this type of graphics and display was cutting edge technology and everyone had huge mobile phones, that's if you could afford one back in 1995.  After seeing a demo of minesweeper for react I thought there is nothing better than a super retro component, and will be the first full interactive component game for universaldashboard.  So thought this would make some amazing history in man-kind.

## Minesweeper Demo

You will notice there is a lot of custom CSS going on here. I had to spend more time on customising the CSS than actually building the component!  The component didn't seem to be rendering correctly in universaldashboard, but after some TLC with CSS it was looking all good to go

```
Import-Module -Name UniversalDashboard
Import-Module -Name UniversalDashboard.UDMineSweeper
Get-UDDashboard | Stop-UDDashboard
$theme = New-UDTheme -Name "Basic" -Definition @{
    'main'                                                                           = @{
        'padding-left'   = "5px"
        'padding-right'  = "5px"
        'padding-top'    = "5px"
        'padding-bottom' = "5px"
    }
    '.digitalSign_vertical'                                                          = @{
        'height' = "10px !important"
    }
    '.winMine_brickContainer.winMine_easy'                                           = @{
        'width' = "190px !important"
    }
    '.winMine_brickContainer.winMine_medium'                                         = @{
        'width' = "340px !important"
    }
    '.winMine_brickContainer.winMine_hard'                                           = @{
        'width' = "505px !important"
    }
    '*, ::after, ::before'                                                           = @{
        'box-sizing' = "content-box !important"
    }
    '.winMine_winmine-header'                                                        = @{
        'height' = "33px !important"
    }
    '.statucBrick_container'                                                         = @{
        'width'  = "30px !important"
        'height' = "30px !important"
    }
    '.digitalNumber_container'                                                       = @{
        'width'  = "15px !important"
        'height' = "30px !important"
    }
    '.brick_container > span'                                                        = @{
        'position'  = "relative !important"
        'bottom'    = "4px !important"
        'font-size' = "larger !important"
    }
    '.brick_container'                                                               = @{
        'width'  = "16px !important"
        'height' = "16px !important"
        'cursor' = "pointer !important"
    }
    '.brick_container.brick_broken, .brick_container:active, .brick_container:focus' = @{
        'border-width' = "medium !important"
    }
} -Parent "Default"
Start-UDDashboard -Port 1000 -AutoReload -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Theme $theme -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 6 -Content {
                New-UdMineSweeper -level "easy"
            }
        }
    }
)
```

![placeholder](https://raw.githubusercontent.com/psDevUK/MineSweeper/master/MineSweeperDemo.gif "example demo")
)

## Further Information
 There is only one parameter in this component which is
 - level
 This has an option of easy, medium or hard

## Conclusion
 This component gave me a blast from the past, and reminded me of how much the world has really changed since 1995. Even as a fully grown man I can still certify that I am totally rubbish at this game as can be seen in the demo gif. I hope that this component finds space on your dashboard and doesn't get you sacked from your day job, by trying to become the 2020 Minesweeper champion of the world.