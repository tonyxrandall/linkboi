---
template: post
title: How to check a bunch of pages for a link to your site using Sheets
slug: /posts/monitor-links-with-google-sheets
draft: false
date: '2016-12-01T22:40:32.169Z'
description: >-
  Screaming Frog > List Mode > Upload List > Crawl > Bulk Export > External
  Links > Find [domain.com]


  Or in case you'd rather do it in an automated G Sheet. 
category: automation
tags:
  - automation
---
Let’s say you’ve got a list of pages you need to check to see if they’re linking to your website or not.

Maybe you emailed a couple hundred websites asking for a link and want to check if they did before following up with them (I think we’ve all followed up with a webmaster or two only to have them reply “I ADDED IT ALREADY” very angrily. Happens to me way more than I wish it did.).

Maybe you found a bunch of target sites by scraping search results and want to check to see if they’re already linking to you. Or a competitor. Or a broken link.

Or maybe you’re doing your monthly client reports and want to do a quick last minute check to see if you missed any of the links you built this month.



There are lots of reasons I could see this being a useful skill to have. And it can literally save you hours over manually checking each site. I’ve seen people do that. WHY? Idiots.



There are also lots of great tools that can do this for you, like Buzzstream has this built in, and you can do it with Screaming Frog too. There are probably a billion others. But what if you don’t have subscriptions to those and need a tool that’s super simple, free as hell and will make you feel a little smarter while using it?



Build one!



It’s real easy. You just need Google Sheets (god I fuckin love Google Sheets) and this little function:



```
=iferror(substitute(IMPORTXML([CELL #],”//a[contains(@href, ‘[URL]‘)]/@href”),””,””),”Not linking.”)
```



Notes:



CELL # is (obviously) going to be the cell correlating to the page you’re checking.



URL is (obviously) going to be the website you’re checking links to.



For URL I exclude http://, www, any subdomains, etc. and just use the root domain. This can lead to Google Sheets importing a completely different website that happens to contain your root domain which is displayed in my example below, but more importantly it’ll make sure Google Sheets lets you know about any links to the non-www version of your site or any subdomain links as well (also luckily displayed in my example below).



Tutorial

I’ve done a quick Google search for some dog links pages (god i fuckin love dogs). Real basic search string: dog toys inurl:links.



And let’s say we want to check to see if any of them are linking to PetSmart.



I’ve pasted the pages I found all in a new Google Sheet.



![](/media/screen-shot-2019-12-21-at-9.01.18-pm.png)



Now for the fun. Paste your formula in any cell and reference the first page you want to check in CELL #. Also insert the website you’re checking links to in URL.



![](/media/screen-shot-2019-12-21-at-9.02.33-pm.png)



Hit enter and you’ll see this:



![](/media/screen-shot-2019-12-21-at-9.03.17-pm.png)



Click that little blue box at the bottom right corner and drag all the way to your last cell:



![](/media/screen-shot-2019-12-21-at-9.04.01-pm.png)



At first all will say “Not Linking” but give it a couple seconds to do its thing and then:



![](/media/screen-shot-2019-12-21-at-9.04.48-pm.png)



Cool! Now we know which of those pages are linking to PetSmart.



As you can see it also revealed all4petsmart.com, but if we would have used http://www.petsmart.com in our function this would have been the result and we wouldn’t have known about that subdomain link. And sure, we could use a regular expression here but I find it best to not be too specific here so we can make sure our doc finds all the links we want it to, even if it also returns a rare irrelevant link here and there.

![](/media/screen-shot-2019-12-21-at-9.05.37-pm.png)



That’s the quickest example I could think of. I’m sure you’ve got a long list of pages you’ve contacted for links. Take 5 minutes to do this with that list (after you do this the first time it becomes literally a 30 second process) and there’s a solid chance you’ll find at least 1 link you didn’t know existed.
