---
date: 2020-02-19 21:55:20
layout: post
title: Google Charts For UniversalDashboard
subtitle: An amazing team-up between 2 nations happened to bring you 4 brand-new components, all chart components for UniversalDashboard.
description: This blog is all about the 4 new chart components that Augustin Ziegler and myself released for universaldashbord.
image: https://financesonline.com/uploads/2019/08/Google-Chart-Tools-logo1.png
optimized_image: https://financesonline.com/uploads/2019/08/Google-Chart-Tools-logo1.png
category: component
tags:
  - GoogleCharts
  - WordTree
  - TimeLine
  - Gantt
  - Gauge
author: psdevuk
---

## Welcome
As I started off with my last blog...It has been a while since my last blog. Wow nearly mostly through the second month of 2020 and I been really busy, hence this delay in blogging.  Having a tough time with life at the moment, so thought the solution was to literally just work all the time and then hopefully get paid for all the over-time I put in for work...sadly that bit of optimism I actually had was crushed like an ant being stepped on.
But as they say always try and look on the bright side of life, and in the development of these Google Chart components I was blessed to have a brand new crime-fighting partner aka Augustin Ziegler.  Now I without showing my age there is a decade between us. So was quite in awe when Augustin busted out the powershell moves to solve the puzzle, and also keep crime at an all time low.

## It started with a Tree
So this whole adventure began with me stumbling upon the [google chart page](https://react-google-charts.com/).  I was like wow, some of these charts look amaze-balls. The one that really caught me eye was the WordTree chart. As I work for a company distributing drink and food, I always get asked to produce information on which customer bought what products.  Putting this information into a grid can end up producing a lot of results, and either mean a lot of clicking or filtering, or even exporting to Excel. So I was thinking in my head I could write an SQL query concat the results into a sentence, then display this in a [WordTree Chart](https://react-google-charts.com/wordtree-chart).  Easy right? I mean I was thinking I could place all results into one chart that would fit on the page.
 I managed to build this component but I couldn't somehow place the contents of the file into a WordTree chart, I could only get it working by manually typing the sentences into the script...I got to the head-banging against a wall stage as was not making any progress with reading the data from a file, or variable...so the place to go when you have a [problem or question with UniversalDashboard](forums.universaldashboard.io/) the forum is the place to head to.  So I posted my problem and asked for help.  now this is the amazing thing with the Internet and open-source software is that is brings people together, and you can even team-up with people from different nations with different ideas, and different approaches.  Augustin came up with the goods at stupid oclock his time, and I was like WTF the next day in the office as he told me how long it took him, and I knew how long I had looked at it. Either way I was chuffed as nuts to finally have this being able to read from a file or variable and display the contents.  I used over 275,000+ rows from SQL output and it all rendered without issues, and no delay using this as a WordTree Chart locally.  However I did find using this across the network wasn't that practical due to the size of the file.  Still was interesting to see how much data I could realistically chuck at this component. [Get your copy of WordTree here](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDWordTree)

 ## Favour for a favour
  I like to think like you probably think, that you are a decent human being and life is not just about taking but also giving. So when Augustin asked if I could replay the favour by doing another super hero team-up to save the world for a second time I was like damn yeah lets go fight some bad guys.  Although there were no actual bad guys to fight, and the world didn't really need saving, was able to use some of the super-sweet Augustin had done on the WordTree to make this work.  However he had to go show me that he didn't need any mentoring in the Powershell department and once again showed an ageing crime-fighter that this new side-kick had some super neat skills to display. Then boom the [Google TimeLine Chart component for UniversalDashboard](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDTimeLine)

## Gantt it up
 So whilst working on the TimeLine component I came across the Gannt Chart which I personally preferred as it seemed to offer more flexibility and was also time related. So thought I should try and put this together...but I swear some kryptonite is in my local water as felt my react skills were fading me, and was struggling to make this more powershelly if thats even a word. So once again boy wonder aka Augustin stepped in beat up all the bad guys and showed me a few new moves in the art of powershelling someone with a good right hand, and put another super solution in place to pass the data in a pure-powershell way to the component. [The Gantt Chart is here on the marketplace](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDGantt)

## Google Gauge Chart
  The gauge chart that I put on the marketplace proved to be my most popular component. That was before it got re-vamped with the D3 library when someone requested this on the forum. Again on the forum someone mentioned monitoring remote computers, and although I have done this I thought that this Google Gauge Chart would be the perfect solution to that problem giving nice clear easy-to-understand display and the fact it doesn't take up any real space on the dashboard page. With all the new tricks I learnt off of my new side-kick I thought I better show that I can still pull of some components on my own. But in reality I used the same method Augustin had used, and just tweeked this to my needs. [Get the Google Gauge Chart here](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.UDGaugeChart)

## Where's all the code dude?
Hmm good question...no only joking so I tried to clever and add a half decent readme to these new components, all of which you will find on the marketplace, as that pulls the readme from the project site.  All my projects you can find here [on my github page](https://github.com/psDevUK/)

## No I'm not mental I read comics
   Yep I read comics...and I love reading comics...so I been doing so much work lately, I had to ban myself from working by locking down my work account to only be accessible via the 9-5 hours I work. Well I did that the other day and been on a comic-book fest.  So thought I would try and implement that in this post



## Conclusion
  These were super-cool components to release, and felt extra good to be able to team-up, learn some new tricks, and along the way bring some brand-new charts to the world of UniversalDashboard. Thanks for taking the time to read this blog any questions on using these specific components please post the issue on the related github page. Peace.
