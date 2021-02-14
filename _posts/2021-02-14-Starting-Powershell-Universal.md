---
date: 2021-02-14 17:38:20
layout: post
title: Starting Powershell Universal
subtitle: This is a blog all about Powershell Universal the latest and greatest from ironmansoftware
description: Powershell Universal contains Universal Dashboard, but also includes Automation and API so this is me using it for the first time
image: https://static.vecteezy.com/system/resources/previews/000/164/715/non_2x/learn-something-new-lettering-vector.jpg
optimized_image: https://static.vecteezy.com/system/resources/previews/000/164/715/non_2x/learn-something-new-lettering-vector.jpg
category: Blog
tags:
  - Powershell
  - Universal
  - Dashboard
  - New
  author: psdevuk
---

## Welcome

First off thanks for taking the time to visit this blog. This blog is going to be a tad different to all my previous blogs. Why is that? Well it's because I am now covering Powershell Universal which is the latest and greatest release from ironman software. I have been looking forward to using this, but due to troubling times, other life things have just got in the way. 
 However I was extremely lucky to have a mystery donation of a license for this product. I cannot thank this person enough for donating me a license for this software, but also for all the help they have given me in personal circumstances is beyond belief, this person is a true legend. 
 I like to hang out at the ironman software forum which I have mentioned in numerous previous blogs, once again the link is [right here if you want to visit or bookmark it](https://forums.universaldashboard.io/) but it does seem every question these days is all Powershell Universal. I know I built a lot of components for Universal Dashboard, which can be used in this new product Powershell Universal, but seriously I was very envious of the great looking components that come built in. 
 I mean like my work PC has so many scheduled jobs that run off of it, a lot of them critical to various staff members but it seems this product is like scheduled jobs but on steriods. Like you get so much information on the jobs you want to schedule. So again I really, really wanted to get my hands on this product to try this.

## Starting My Journey With Powershell Universal

So the first thing I had to do was to download and install the product. I decided to use my trusted 32-bit personal laptop to run this off of.  Well that was my hurdle, was the fact this software only supports 64-bit installations on Windows at least. I have a PC with 64-bit windows 10 installed, so decided to use this as my machine of choice. [So you can download Powershell in various formats from this link](https://ironmansoftware.com/downloads) and I decided to use the MSI install, as this should be the easiest way of installing it. The installation was very easy (being an MSI) and everything installed without a glitch. After installing the product [I figured my next best step would be here](https://docs.ironmansoftware.com/) where I could read all about using and getting started with this software.
  Without any spoiler alerts, if you decided to choose the root I chose then this will install Powershell Universal as a service on the computer, and once installation is complete you can open up a web browser and head on to localhost:5000 which should then take you to what is known as the Admin Console. Now I had seen screen shots of this, but to actually use it, was a much better experiance than anticipated. Like the whole thing has been built really nice, like really really nice. 
 Coming from using Universal Dashboard to now using Powershell Universal I was like WOW, but at the same time very lost, on what to do and where to begin.  [So I have seen that the Visual Studio Code extension](https://docs.ironmansoftware.com/get-started/visual-studio-code-extension) is the way outside of the Admin Console to manage various aspects of Powershell Universal. So I downloaded and installed this. However this is where my first problem encountered, I was getting an error in VS Code stating ```Unable to locate Powershell Universal Server binary...Did you set the server path setting? ``` so although everything appeared to be working, and I could use the VS Code extension, and it updated the Admin Console, I couldn't figure out how to get rid of this error. Well it was very simple, I simply needed to press F1 go to settings, Extensions, Powershell Universal and uncheck the Start Server option. As the server was already running via the service. Once unchecking this option I no longer got the VS Code alert on this extension.  
 I mean I know Universal Dashboard had the option of running as a service, but as I had used IIS to configure Universal Dashboard, I had never used this feature. But yeah having Powershell Universal install itself as a service, and be ready from the get-go was a big plus for making the transition that bit easier. 
 [To be fair there is a whole section here which is dedicated about transitioning from Universal Dashboard to Powershell Universal](https://docs.ironmansoftware.com/dashboard/dashboards/migrating-from-universal-dashboard-2.9) and how to go about adjusting your dashboard pages.
 I personally followed along with the instructions and configured a job to run. Just having the ability to then also add triggers to the job running within PSU is super cool, which I will make sure I use. But quite simply this is scheduled powershell jobs on a whole new level, so I will certainly be looking to add my exisiting scripts from the scheduled jobs so I have better visibility and reporting on the job itself. Whilst following along with the instructions I also set up another credential to run my jobs, [and stored this within the secrets vault](https://docs.ironmansoftware.com/automation/variables#creating-a-secret-variable).
   
![placeholder](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fgblobscdn.gitbook.com%2Fassets%252F-M6jY7sXTmhiAIMGYw_m%252F-MHDZ35FwxJNZI2rDnr2%252F-MHD_OeHV1jBS-M5k6X3%252Fimage.png%3Falt%3Dmedia%26token%3D82927a6f-3db5-4fe4-a17d-22ab40f4fab2&f=1&nofb=1 "Admin Console")


## Conclusion

It was a long time coming, but so glad I have got onto using Powershell Universal. There is so much documentation which makes the whole process a lot easier to follow along to learn and use Powershell Universal. Although I didn't do a lot with it just yet, I have great ambitions for this new software.
