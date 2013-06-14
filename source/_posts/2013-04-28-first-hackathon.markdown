---
layout: post
title: "First Hackathon"
date: 2013-04-28 23:56
comments: true
categories: [Hacking] 
---

<script type="text/javascript" src="https://raw.github.com/JoelSutherland/GitHub-jQuery-Repo-Widget/master/jquery.githubRepoWidget.min.js"></script>

I finally did it!  "Did what?" you ask.  "You finally wrote another blog post?"  No.  Well, yes, I did finally write another blog post after a six-month dry spell.  More importantly, though, I finally attended a hackathon!  During my three years so far at UW, there have been several hackathons, some sponsored by companies like Facebook and Microsoft, and some put on by CS student organizations.  I usually come up with some excuse for not attending, like "I have better things to do this weekend" or "I'll look like an idiot compared to everyone else there."  Yesterday I finally mustered up the courage to go.  Not only did I go, but miraculously I ended up winning first place!

## The hackathon
[The hackathon](https://www.facebook.com/events/466162720130325/) was sponsored by Microsoft and ran from 10am to 10pm on Saturday.  After a short introduction, the hacking began at around 11am and ended at 9pm to leave time for demos and prizes, which gave us about 10 hours of dedicated hacking time.  Although the hackathon was open to any kind of hacking, there was an emphasis on developing Windows 8 Metro (Windows Store) apps and Windows mobile apps.  Knowing this ahead of time, I installed Windows 8 and Visual Studio 2012 on a virtual machine on my Macbook.  Until a couple of days before the hackathon, I had never used Visual Studio and I had only used Windows 8 a couple of times.  I had also never developed an app in C# or C++, which left me the option of using JavaScript/HTML/CSS if I wanted to make a Windows Store app (which I did).  Fortunately, I've done quite a bit of hacking in JavaScript, so I knew the language would not be a barrier.  The most difficult part would be learning the WinJS framework and the code patterns specific to Metro apps.  I had done a little research prior to the hackathon, but not enough to really know what I was doing.

Once the hackathon started, there was no time to waste trying to learn everything about Metro apps.  I knew that to be successful I would have to dive right in without being fully prepared (which isn't something I do very often).  Before diving into code, however, I needed to have a solid app idea and figure out what it would do and what it would look like.  Luckily, I had taken some time before the hackathon to jot down a few app ideas.  The first idea was an app for [Stack Exchange](http://stackexchange.com/), which I'm slowly becoming more and more addicted to as I accumulate more reputation points.  I was sold on that idea until I found out that the Stack Exchange [APIs](http://api.stackexchange.com/) don't allow write access (except for comments, as of v2.1).  That made it pretty difficult to see how my app could possibly have an advantage over the website itself.  I had a couple of other ideas not worth mentioning because they were basically just improved versions of existing apps.  There was one other idea, though, which I ended up choosing because it was original and practical (and realistic given the time constraint of the hackathon).  **Badger Buzz**: an app for UW students to keep up with the latest campus news, events, and social media buzz.

<!-- more -->

If I could create a "wish list" of features for the app, I would include things like live updates, social media sharing, search, and notifications.  Unfortunately, I knew I wouldn't have time to get that fancy, so I would have to focus on the core feature: viewing content.  First I brainstormed the types of content the app could include: news, sports, weather, events, Facebook feeds, Twitter feeds, photos, and videos.  Obviously it wouldn't be realistic to implement all of these in a day, so I chose the ones I thought were most important: news, events, Twitter feeds, and photos.

## Implementation
Although I could hardly wait to start coding (as everyone around me appeared to be doing), I couldn't rid my mind of the image of my HCI professor saying "Design first!"  So I pulled out my sketchpad and a pencil and started sketching.  Once I had a (very) rough sketch of the layout, I created a new project in Visual Studio using one of the provided layout templates.  I'm glad I chose the template I did because it enabled me to really focus on the content side of things instead of worrying about the layout.  It gave me HTML, JS, and CSS files that were filled in with some default information and used a static data source.  If I had used a blank template I probably would've spent a couple hours just getting the basic layout right.

I spent the bulk of my time in the `data.js` file, where there was a chunk of static placeholder data to start with.  My job was to replace this static data with real data provided from live data sources.  This meant first figuring out where and how I could get my hands on the data I needed.

For campus news, there are several popular websites I could potentially get data from: [the University's official news site](http://news.wisc.edu), [The Badger Herald](http://badgerherald.com) (an independent student newspaper), or [The Daily Cardinal](http://host.madison.com/daily-cardinal/), another campus newspaper.  I ended up choosing the University's official news site ([news.wisc.edu](http://news.wisc.edu)) because its news stories tend to be slightly more professional and relevant.  Another perk of using their website is the availability of RSS feeds, which makes getting content for an app pretty easy.  I was able to use jQuery to get and parse the XML data from the RSS feed and display it the app pretty easily.  The only problem I ran into was that the RSS feed only contained a short description of news articles rather than the full text, and also didn't include the URLs for images in the article.  I considered simply having the app display the full website in a separate web view, but that would somewhat defeat the purpose of having an app.  The solution?  Scrape the text and image content from the news website using the [YQL API](http://developer.yahoo.com/yql/).  I hadn't used YQL before, but it turned out to be pretty simple to query the API and parse the data using jQuery.

I used a very similar approach for campus events.  I again used the University's website ([today.wisc.edu](http://today.wisc.edu)) which provides a handy RSS feed containing all of the important event data, including date, time, location, and a description.

Twitter feeds required a different, though simpler, approach.  After researching the different APIs they provide, I decided that Twitter's [Search API](https://dev.twitter.com/docs/api/1/get/search) would fulfill my needs and be much easier to use.  The University has different Twitter handles for different purposes, but I focused on their main handle, [@UWMadison](https://twitter.com/UWMadison).  Getting the content into the app was as simple as making an GET request to [http://search.twitter.com/search.json](http://search.twitter.com/search.json?q=from%3AUWMadison%20OR%20to%3AUWMadison%20OR%20%40UWMadison) using a standard Twitter search query as a request parameter.

Unfortunately, I ran out of time before getting to the photo part of the app.  I was planning on getting photos from the University's [Instagram account](http://instagram.com/uwmadison) using the [Instagram API](http://instagram.com/developer), which I'm certain would have been pretty easy.  If I had another half hour I would have been able to pull it off.

## Result
At 9:00, we put the finishing touches on our apps and then walked around the room for a quick demo by each individual/team (there were only 6-7 entries in all).  The four judges (all Microsoft interns) then left the room and came back a few minutes later with the results.  Somewhat to my surprise, Badger Buzz received first place!  Honestly, I was really impressed with the apps other people made, so I was kind of shocked when they called my name first.  With this being my first hackathon, I wasn't really sure what was expected for the end product.  Did they want something that looked pretty or just something functional?  It appears that my decision to focus on functionality and content rather than beauty was a good one.

Receiving first place meant that I got first pick among the prizes: a Windows 8 t-shirt, a travel mug, and a backback.  (Uber exciting, right?)  I took the t-shirt since I figured I might actually wear it.  (Sorry, but I'm not going to use a plastic mug that leaks or a backpack that can only hold two books.)

## Code
If you're interested, the [source code](https://github.com/JakeStoeffler/BadgerBuzz) for Badger Buzz is up on my Github!  If you're going to look at the code or try to run the app, just be aware that I haven't touched anything since the hackathon (aka, it's kind of messy).  If I have an overabundance of spare time this summer (which is unlikely) maybe I'll dig it up and work on it some more.  But unless I end up publishing it in the Windows Store, I have nothing to lose by open sourcing it.

<div class="github-widget" data-repo="JakeStoeffler/BadgerBuzz"></div>

## Final Screenshots

### App tile
[![app-tile](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/app-tile.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/app-tile.png)

### News
[![news-home](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/news-home.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/news-home.png)
[![news-group](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/news-group.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/news-group.png)
[![news-item](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/news-item.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/news-item.png)

### Tweets
[![tweets-home](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/tweets-home.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/tweets-home.png)
[![tweets-group](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/tweets-group.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/tweets-group.png)
[![tweets-item](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/tweets-item.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/tweets-item.png)

### Events
[![events-home](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/events-home.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/events-home.png)
[![events-group](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/events-group.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/events-group.png)
[![events-item](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/thumbs/events-item.png)](https://raw.github.com/JakeStoeffler/BadgerBuzz/master/screenshots/events-item.png)