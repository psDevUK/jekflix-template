---
date: 2019-11-15 12:26:40
layout: post
title: Content vs Endpoint
subtitle: Learn about the difference between using content or using endpoint.
description: To actually get your content to display on the page you need to use either the content parameter or the endpoint parameter. This post explains the difference.
image: https://media.jamf.com/images/news/total-cost-of-ownership-mac-versus-pc-in-the-enterprise.jpg?q=80&w=800
optimized_image: https://media.jamf.com/images/news/total-cost-of-ownership-mac-versus-pc-in-the-enterprise.jpg?q=80&w=800
category: Performance
tags:
  - content
  - endpoint
  - refresh
  - runspace
author: psdevuk
---

Thanks for taking the time to read this blog. This blog was inspired by the great article <a href="https://ironmansoftware.com/best-practices-for-universal-dashboard-performance/">Adam Driscoll wrote here</a>, and when looking on the forum today it was clear that this is still not talked about enough as some people are not understanding why their dashboard might not be behaving as they expected. So hopefully after reading this post this will become clear, on when to use the **content** parameter and when to use the **endpoint** parameter to display your data. As both of these parameters are used to display what you want the end-user to physically see on the dashboard you have created

> Runspaces allow you to run multiple powershell commands that can all run at the same time instead of having to wait for the previous command to finish.

## Content

Using the content parameter will load the content you want to display on your page quicker as all data is returned on the first request back to the universal dashboard server. I use the content parameter whenever I am displaying **static** elements on my page that will not be dynamically changing. Data inside the content script block will be executed immediately, and run just the once. If you did put a dynamic element in the content script block such as `get-date` then this would only run that command everytime you press the **F5** key or refresh symbol on the browser you are using.

## Endpoint

Maybe I should mention that not all the commands within powershell universal dashboard support the endpoint parameter. Endpoints can take longer to physically display on your page as they make the request back to the universal dashboard server, then the server executes the endpoint data you have passed then returns the data back to your dashboard screen. Any data that I am displaying on my dashboard that will be dynamically changing or I want to check if certain values of a page every X amount of seconds then I would place this data inside an endpoint scriptblock.

So it goes without saying one of those fundamental powershell commands will help you to identify which commands within powershell universal dashboard support the endpoint parameter.
`Get-Command -Module UniversalDashboard -ParameterName Endpoint`
This will display all the commands that support the **endpoint** scriptblock. It is also important to mention that when using the endpoint scriptblock to display your data dynamically I always use the following two parameters straight after the closing curly brace scriptblock, the `-AutoRefresh` parameter followed by the `-RefreshInterval` parameter then specify a **number** for the **refresh interval** powershell universal dashboard will then refresh just that particular component every X amount of seconds you specify in the `-RefreshInterval` parameter.

## Using both Endpoint and Content

It is recommend that you wrap the most outer command with an endpoint, then apply the inner command / component with the content scriptblock. It did take me sometime to realise that the `New-UDColumn` command actually supported the endpoint parameter, meaning I could refresh anything being held in that column on my page if I put the column to use an endpoint, but the data/components inside the column to use content, and it would still be refreshed.

## Code

Cum sociis natoque penatibus et magnis dis `code element` montes, nascetur ridiculus mus.

```js
 New-UDElement -Tag 'div' -Endpoint {
                    $DateTime = Get-Date
                    New-UDElement -Tag 'div' -Content { $DateTime.Hour }
                    New-UDElement -Tag 'div' -Content { $DateTime.Minute }
                    New-UDElement -Tag 'div' -Content { $DateTime.Second }
                } -AutoRefresh -RefreshInterval 2
```

So this example will update each of these `$DateTime` variables every 2 seconds even though these `$DateTime` variables are being held within a **content** script block so are not dynamic but because they are nested within an **endpoint** script block they will get refreshed. The reason each of these `$DateTime` variables were put in a **content** scriptblock was for performance and scoping.

## Conclusion

I hope you have enjoyed this blog and I hope you have gained some new knowledge from it. Till next time peace out.
