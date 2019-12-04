---
date: 2019-12-04 22:17:00
layout: post
title: Clipart for your dashboard
subtitle: Adding react clipart graphic to your dashboard.
description: So tonight I found a super cool looking react clipart graphic package which included 618 different graphics to choose from.
image: https://user-images.githubusercontent.com/44211223/70180862-bdb93500-16d8-11ea-95c0-a58151db2e92.PNG
optimized_image: https://user-images.githubusercontent.com/44211223/70180862-bdb93500-16d8-11ea-95c0-a58151db2e92.PNG
category: clipart
tags:
  - clipart
  - unDraw
  - custom
author: psdevuk
---

## Please remember

As always these blogs are my own opinions and thoughts. So as I am always looking to improve my universaldashboard skills I found <a href="https://github.com/justinlettau/react-undraw/blob/HEAD/ILLUSTRATIONS.md">these 618 amazing looking react graphics</a>, and I thought these would look proper professional on a dashboard. If you are reading for the ride, lets get going.

> I love the fact that as a user of powershell universaldashboard I have the opportunity to customize and add additional components to the product, to fit my requirements.

## My problem

The dashboard pages I have constructed at work, I have have used images off of the internet to display a **finance** or **sales** image. However the problem is, consistency. It is hard to find a **finance** image that matches the same look and feel of the **sales** image. Then there is also the possibilty the website you are **borrowing** the image from, may cease hosting. Or move to a different website host, which then causes a change in the URL and the image stops displaying on your dashboard.

## My solution

To fix the problem of not having to rely on images from the internet or search through numerous images on google or another internet image search site, I decided to use [react-unDraw which I found here](https://www.npmjs.com/package/react-undraw). This only had 1 dependency listed which I have used before which is the prop-types. I have mentioned in a previous blog on how to install this.

I looked at the brief documentation on the website on unDraw and ended up with the following JSX file

```js
import React from "react";
import Undraw from "react-undraw";
class UDunDraw extends React.Component {
  render() {
    return (
      <Undraw
        name={this.props.name}
        primaryColor={this.props.primaryColor}
        height={this.props.height}
      />
    );
  }
}

export default UDunDraw;
```

Then on the github page for this project it had all the illustrations listed in a markdown file. So I was able to get that list, and then use a powershell script to put it into an array list, to then pass into my powershell function to call this component from within universaldashboard

```
function New-UDunDraw {
    param(
        [Parameter()]
        [string]$Id = (New-Guid).ToString(),
        [Parameter()]
        [ValidateSet('3d-modeling', 'a-day-at-the-park', 'a-whole-year', 'about-me', 'about-us-page', 'accept-request', 'accept-terms', 'account', 'active-support', 'add-files', 'add-notes', 'add-to-cart', 'add-user', 'address', 'agreement', 'air-support', 'aircraft', 'airport', 'alert', 'algolia', 'alien-science', 'analysis', 'analytics', 'android', 'apartment-rent', 'app-installation', 'appreciation', 'around-the-world', 'art', 'art-lover', 'artificial-intelligence', 'artist', 'astronaut', 'at-work', 'authentication', 'autumn', 'awards', 'baby', 'back-in-the-day', 'back-to-school', 'balloons', 'barber', 'basketball', 'be-the-hero', 'beach', 'beer-celebration', 'before-dawn', 'begin-chat', 'bibliophile', 'birthday-cake', 'bitcoin', 'bitcoin-p2p', 'blank-canvas', 'blog-post', 'blogging', 'book-lover', 'booking', 'bookmarks', 'brainstorming', 'broadcast', 'browser-stats', 'buddies', 'buffer', 'bug-fixing', 'building', 'building-blocks', 'bus-stop', 'business-deal', 'business-plan', 'businessman', 'businesswoman', 'by-my-car', 'calculator', 'calendar', 'calling', 'campfire', 'camping', 'cancel', 'candidate', 'career-progress', 'cautious-dog', 'celebration', 'charts', 'chat', 'chatting', 'checking-boxes', 'checklist', 'chef', 'children', 'chilling', 'choice', 'choose', 'christmas-stocking', 'christmas-tree', 'circles', 'city-driver', 'city-girl', 'cloud-hosting', 'cloud-sync', 'co-workers', 'co-working', 'code-typing', 'coding', 'coffee-break', 'collaboration', 'collecting', 'collection', 'community', 'completed', 'compose-music', 'conference', 'conference-speaker', 'confirmation', 'confirmed', 'connected', 'connected-world', 'connecting-teams', 'contact-us', 'container-ship', 'contemplating', 'content', 'content-creator', 'contrast', 'control-panel', 'conversation', 'convert', 'country-side', 'couple', 'create', 'creation-process', 'creative-team', 'creative-thinking', 'creative-woman', 'creativity', 'credit-card', 'credit-card-payment', 'credit-card-payments', 'crypto-flowers', 'customer-survey', 'dark-alley', 'dark-analytics', 'dashboard', 'data', 'data-points', 'data-report', 'data-trends', 'deliveries', 'delivery', 'departing', 'depi', 'design-community', 'design-process', 'design-thinking', 'design-tools', 'designer', 'designer-girl', 'designer-life', 'destination', 'developer-activity', 'development', 'devices', 'digital-nomad', 'directions', 'discount', 'doctor', 'doctors', 'documents', 'dog-walking', 'doll-play', 'domain-names', 'done', 'download', 'dreamer', 'drone-delivery', 'drone-race', 'dua-lipa', 'easter-egg-hunt', 'eating-together', 'electric-car', 'elements', 'email-campaign', 'email-capture', 'emails', 'empty', 'envelope', 'environment', 'ether', 'ethereum', 'events', 'everyday-design', 'exams', 'experts', 'exploring', 'fall-is-coming', 'fans', 'fashion-blogging', 'fast-car', 'fast-loading', 'fatherhood', 'features-overview', 'feeling-blue', 'festivities', 'file-bundle', 'file-searching', 'files-sent', 'filing-system', 'filter', 'finance', 'financial-data', 'fingerprint', 'finish-line', 'fireworks', 'firmware', 'fish-bowl', 'fishing', 'fitness-tracker', 'floating', 'focus', 'folder', 'follow-me-drone', 'followers', 'following', 'for-sale', 'forever', 'forgot-password', 'freelancer', 'friendship', 'frozen-figure', 'game-day', 'gaming', 'gardening', 'gdpr', 'getting-coffee', 'gift', 'gift-card', 'gifts', 'girls-just-wanna-have-fun', 'goal', 'going-up', 'golden-gate-bridge', 'good-doggy', 'grades', 'graduation', 'grand-slam', 'grandma', 'group-chat', 'group-selfie', 'growing', 'growth-analytics', 'hamburger', 'hang-out', 'happy-2019', 'happy-birthday', 'happy-women-day', 'having-fun', 'healthy-habit', 'heartbroken', 'hello', 'high-five', 'hiking', 'hire', 'hiring', 'home-run', 'horror-movie', 'house-searching', 'houses', 'i-can-fly', 'image-folder', 'image-post', 'image-upload', 'images', 'in-love', 'in-progress', 'in-sync', 'in-the-office', 'in-the-pool', 'in-thought', 'inbox-cleanup', 'influencer', 'instant-support', 'instruction-manual', 'interaction-design', 'internet-on-the-go', 'interview', 'into-the-night', 'investing', 'invite', 'japan', 'jason-mask', 'java-script-frameworks', 'job-hunt', 'jogging', 'journey', 'joyride', 'judge', 'knowledge', 'laravel-and-vue', 'late-at-night', 'launching', 'learning', 'lighthouse', 'live-collaboration', 'loading', 'login', 'logistics', 'lost', 'love', 'love-is-in-the-air', 'mail', 'mail-sent', 'mailbox', 'maintenance', 'make-it-rain', 'maker-launch', 'makeup-artist', 'making-art', 'map', 'map-dark', 'map-light', 'marilyn', 'marketing', 'may-the-force', 'media-player', 'medicine', 'meditating', 'meditation', 'meeting', 'memory-storage', 'message-sent', 'messages', 'messaging', 'messaging-fun', 'messenger', 'metrics', 'millennial-girl', 'mind-map', 'mindfulness', 'mint-tea', 'missed-chances', 'mission-impossible', 'mobile', 'mobile-apps', 'mobile-browsers', 'mobile-life', 'mobile-marketing', 'mobile-payments', 'mobile-testing', 'modern-life', 'modern-woman', 'moment-to-remember', 'monitor', 'more-music', 'morning-essentials', 'motherhood', 'movie-night', 'moving-forward', 'multitasking', 'music', 'my-password', 'navigation', 'nerd', 'new-message', 'news', 'newsletter', 'night-calls', 'ninja', 'no-data', 'not-found', 'note-list', 'notebook', 'notes', 'notify', 'off-road', 'old-day', 'on-the-office', 'on-the-way', 'onboarding', 'online', 'online-friends', 'online-page', 'online-shopping', 'online-wishes', 'online-world', 'open-source', 'opened', 'operating-system', 'order-confirmed', 'ordinary-day', 'organize-photos', 'organize-resume', 'organizing-projects', 'outer-space', 'page-not-found', 'pair-programming', 'palette', 'passing-by', 'payments', 'pedestrian-crossing', 'pen-tool', 'people-search', 'personal-data', 'personal-notes', 'personal-settings', 'personal-site', 'personal-trainer', 'personalization', 'photo', 'photo-sharing', 'photocopy', 'photos', 'pie-chart', 'pilates', 'pizza-sharing', 'plain-credit-card', 'playful-cat', 'podcast', 'podcast-audience', 'portfolio', 'post', 'post-online', 'posting-photo', 'posts', 'powerful', 'preferences', 'presentation', 'press-play', 'printing-invoices', 'problem-solving', 'processing', 'product-hunt', 'product-teardown', 'product-tour', 'profile', 'profile-data', 'profile-pic', 'programmer', 'programming', 'projections', 'prototyping-process', 'qa-engineers', 'questions', 'queue', 'quitting-time', 'react', 'reading-list', 'real-time-sync', 'recording', 'refreshing', 'relaxation', 'relaxing-at-home', 'report', 'responsive', 'resume', 'resume-folder', 'revenue', 'ride-a-bicycle', 'rising', 'robotics', 'romantic-getaway', 'running-wild', 'safe', 'santa-claus', 'savings', 'schedule', 'science', 'scooter', 'scrum-board', 'sculpting', 'search', 'search-engines', 'secure-data', 'secure-server', 'security', 'security-on', 'segment', 'segmentation', 'select', 'selfie', 'selfie-time', 'server', 'server-down', 'server-status', 'setup', 'setup-analytics', 'setup-wizard', 'shopping', 'site-stats', 'skateboarding', 'sleep-analysis', 'smart-home', 'smiley-face', 'snowman', 'social-dashboard', 'social-growth', 'social-ideas', 'social-life', 'social-media', 'social-networking', 'social-share', 'social-strategy', 'social-tree', 'social-update', 'software-engineer', 'specs', 'speech-to-text', 'spreadsheets', 'stability-ball', 'starman', 'startled', 'startup-life', 'static-assets', 'statistics', 'status-update', 'staying-in', 'step-to-the-sun', 'street-food', 'stripe-payments', 'studying', 'subscriber', 'subway', 'successful-purchase', 'sunny-day', 'super-thank-you', 'super-woman', 'superhero', 'surfer', 'swipe-profiles', 'sync', 'synchronize', 'tabs', 'taken', 'taking-notes', 'target', 'task', 'tasting', 'teacher', 'teaching', 'team', 'team-page', 'team-spirit', 'team-work', 'teddy-bear', 'texting', 'thoughts', 'through-the-desert', 'throw-down', 'time-management', 'timeline', 'to-do', 'to-do-list', 'to-the-stars', 'together', 'toy-car', 'track-and-field', 'transfer-files', 'travel-booking', 'travelers', 'traveling', 'treasure', 'trip', 'true-friends', 'tweetstorm', 'typewriter', 'typing', 'unboxing', 'under-construction', 'update', 'upgrade', 'upload', 'upload-image', 'uploading', 'upvote', 'usability-testing', 'user-flow', 'vault', 'vehicle-sale', 'version-control', 'video-call', 'videographer', 'virtual-reality', 'visual-data', 'voice-control', 'vr-chat', 'walk-in-the-city', 'wall-post', 'wallet', 'warning', 'weather', 'weather-app', 'web-devices', 'website-setup', 'wedding', 'welcome', 'wind-turbine', 'window-shopping', 'windows', 'winners', 'winter-designer', 'winter-olympics', 'wireframing', 'wishes', 'wishlist', 'witch', 'woman', 'women-day', 'word-of-mouth', 'wordpress', 'work-chat', 'work-time', 'working', 'working-late', 'working-remotely', 'workout', 'world', 'xmas-surprise', 'yacht', 'young-and-happy', 'youtube-tutorial')]
        [string[]]
        $Name,
        [Parameter()]
        [string]$Colour,
        [Parameter()]
        [string]$Height
    )

    End {

        @{
            # The AssetID of the main JS File
            assetId      = $AssetId
            # Tell UD this is a plugin
            isPlugin     = $true
            # This ID must be the same as the one used in the JavaScript to register the control with UD
            type         = "UD-unDraw"
            # An ID is mandatory
            id           = $Id
            name         = $Name
            primaryColor = $Colour
            height       = $Height
        }

    }
}
```

## Time to test

After building the component it is always a good time to test your component. So I loaded up a basic dashboard with the following in it

```
Import-Module UniversalDashboard.Community
Import-Module UniversalDashboard.UDUndraw
Import-Module UniversalDashboard.SyntaxHighlighter
Get-UDDashboard | Stop-UDDashboard
$theme = get-udtheme "DarkRounded"
$dashboard = New-UDDashboard -Title "New-UDUnDraw" -theme $theme -Content {
    New-UDRow -Columns {
        New-UDColumn -Size 6 -Content {
            New-udcard -Content {
                New-UDSyntaxHighlighter -Language PowerShell -Style dark -Code "New-UDUnDraw -Name 'data' -Colour '#db4c40' -Height '300px'"
                New-UDUnDraw -Name "data" -Colour "#db4c40" -Height "300px"
                New-UDHeading -size 5 -text "Add some really cool looking graphics to your dashboard with ease." -Color "#fff"
            }
        }

    }
}
Start-UDDashboard -Dashboard $dashboard -Port 10005
```

The other module I am importing here is one produced by Adam Driscoll. As the name of the module implies, this highlights and displays the code you have chosen to display. In my case I wanted to show the command I used to produce the graphic on the dashboard.

## Images

Here is only a few of the 618 images you can choose from should you download and install this module

![placeholder](https://user-images.githubusercontent.com/44211223/70180862-bdb93500-16d8-11ea-95c0-a58151db2e92.PNG "Example image")
![placeholder](https://aws1.discourse-cdn.com/standard11/uploads/universaldashboard/original/1X/d4d20851d862ebc6ef5ffe71ff45d74380a9dbad.png "Example image")
![placeholder](https://aws1.discourse-cdn.com/standard11/uploads/universaldashboard/original/1X/8f88fbee67ce28daf6f1a6c8e4e3fe58c58b4233.png "Example image")

## Conclusion

I hope you agree with me that these do look beautiful clipart like react graphics that you can now use on your powershell universaldashboard pages, I have now uploaded this module to the powershell gallery just search for **psdevuk** to see my **UD component** modules I uploaded there, this new universaldashboard component is also on the powershell universal dashboard marketplace site which I have links to in a previous blog. Thought these illustrations would be a great way to fill any blank space on your dashboard with a professional looking image, that is consistant in style with all of the other 618 illustrations included with this component.
