---
date: 2020-11-12 17:45:20
layout: post
title: New File Icon Component
subtitle: Boom a new month and another new component
description: This blog covers a brand new component I have built for Universal Dashboard. The blog will cover this new file icon component and how to add it to your dashboard
image: https://camo.githubusercontent.com/15ee5063ab228d63babb838fc3147d6fe83cd8e9857fdacb63b508bac9f490f4/687474703a2f2f662e636c2e6c792f6974656d732f327234303050333333333048306533543341316d2f72656163742d66696c652d69636f6e732e706e67
optimized_image: https://camo.githubusercontent.com/15ee5063ab228d63babb838fc3147d6fe83cd8e9857fdacb63b508bac9f490f4/687474703a2f2f662e636c2e6c792f6974656d732f327234303050333333333048306533543341316d2f72656163742d66696c652d69636f6e732e706e67
category: component
tags:
  - Component
  - File
  - Icon
  - New
author: psdevuk
---

## Welcome

 So this blog will cover this new component I built today. Yep I saw it last night on **npmjs.com** thought it looked lush and wanted to bring this component to the universaldashboard ecosystem of custom components

## Where Did You Find It?

As with most of the components I build I found this on **npmjs.com** the exact link to the [project can be found by clicking on this link](https://www.npmjs.com/package/react-file-icon) I thought instantly of several good places I could use this custom SVG icon creator on my existing dashboards.

## What Parameters Does It Have?

Well if you have a butchers at the original project I have included each **prop** as a parameter:-

```
[Parameter()]
        [string]$Color,
        [Parameter()]
        [string]$Extension,
        [Parameter()]
        [bool]$Fold,
        [Parameter()]
        [string]$FoldColor,
        [Parameter()]
        [string]$GlyphColor,
        [Parameter()]
        [string]$GradientColor,
        [Parameter()]
        [decimal]$GradientOpacity,
        [Parameter()]
        [string]$LabelColor,
        [Parameter()]
        [string]$LabelTextColor,
        [Parameter()]
        [bool]$LabelUppercase,
        [Parameter()]
        [int]$Radius,
        [Parameter()]
        [ValidateSet(
            "3d", "acrobat", "audio", "binary", "code", "compressed", "document", "drive", "font", "image", "presentation", "settings", "spreadsheet", "vector", "video"
        )]
        [string]$FileType

```

## Example Using The Component
```
Import-Module -Name UniversalDashboard.Community -RequiredVersion 2.8.1
Import-Module -Name UniversalDashboard.UDFileIcon
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Content {
        New-UDRow -Columns {
            New-UDColumn -Size 1 -Content {
                New-UDFileIcon -Color "#05299E" -Fold $true -Extension "docx" -LabelColor "#041F77" -LabelTextColor "#CCC" -LabelUppercase $true -Radius 4 -FileType "document" -GlyphColor "#FFF"
            }
            New-UDColumn -Size 1 -Content {
                New-UDFileIcon -Color "#2E4057" -Fold $true -Extension "jsx" -LabelColor "#DA4167" -LabelTextColor "#CCC" -LabelUppercase $false -Radius 4 -FileType "code" -GlyphColor "#F4D35E"
            }
            New-UDColumn -Size 1 -Content {
                New-UDFileIcon -Color "#E7E247" -Fold $true -Extension "mp3" -LabelColor "#3D3B30" -LabelTextColor "#E9EDDE" -LabelUppercase $false -Radius 4 -FileType "audio" -GlyphColor "#5C80BC"
            }
        }
    }
)
```

## Which Gives You This

![placeholder](https://github.com/psDevUK/ud-flix/blob/master/assets/img/fileicon.PNG?raw=true "Component Demo")

## Conclusion

 End-users are wonderful beings, for most of us they are the reason are job may exist. To serve the end-user. So I figured if your dashboard is serving any specific file types, or you have an upload but need certain filetypes uploading then this is a perfect component to use. I also thought it was quite stylish. I am looking to publish this on the powershell gallery and will update with the link once posted.

