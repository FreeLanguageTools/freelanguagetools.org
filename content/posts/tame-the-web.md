---
title: "Taming the Web"
date: 2021-09-20T16:11:49-04:00
draft: false
tags: ['miscellaneous']
---
Over 30 years since its inception, the World Wide Web has grown into a data-hungry, attention-seeking monster. This article details my method of taking back control from increasingly manipulative Web services, in an attempt to improve my life and have more time for things that matter.
<!--more-->
A "Tamed Web" is the ideal according to which I designed this website. This website does not serve ads, use centralized content services, or misrepresent content in order to attract your attention. Taming the Web is essential to immersion-based language learning, since that is what you can do when you are not constantly distracted or anxious.

## What's wrong with the modern Web?
### Invasion of privacy
You have been told this countless times by now, but you are being constantly tracked on the Web. Every time you open a website, they collect everything from you to the best of their ability. On most proprietary platforms, everything you ever saw or said are recorded into their database. Often, deletion of your data is never truly executed, only hiding them from you. 

The usual purpose of this is to recommend you content or advertisement in order to make money. This directly leads to the next problem.

### Culture of overconsumption
On the Web, everything attempts to get our attention at all costs. But what for? Ads. 

Endless streams of advertising induce us to buy things that we don't need, with catastrophic impacts on the environment and our mental health. We are led to believe that having "more" can bring us happiness. But they do the opposite: wanting leads to misery. The Web makes everything as convenient as possible, just so that we would consume more and more "stuff", including both physical objects and media.

### Manipulation of our attention
Decades of psychology research has helped companies perfect the formula for creating advertisements that attract people's attention. With the advent of the Web, the possibilities became endless. Clickbaits, animations, recommendation algorithms keep us hooked for hours on end receiving useless content. 

The accessibility of these attention-seeking services enables their use as an escape from life. Over time, this diminishes opportunity for deep thought and reduces our productivity.

Social media is a particularly egregious example of this. They manipulate the evolutionary drive to socialize and turned it into a data mining mega-operation to profit off. This had disastrous impacts on the mind, especially for younger people who are less suspicious of technology and whose brains are more malleable. This is a part of why depression is at an all time high despite the apparently improved material conditions.

### Centralization of power
The Web was once a much more varied place, with personal websites, forums, full of freedom and possibility. Today, that has largely consolidated. Most of the traffic today is to a small number of large websites, such as Facebook, Instagram, Youtube, or Reddit.

The consequences of this consolidation are quite apparent. These large platforms have gained and exercised immense power over what people are and are not allowed to see. They often favor certain viewpoints over others. While it is perfectly within their power to do this as private companies, that doesn't make it right. A society needs dissent to progress and flourish, which becomes difficult when people are only exposed to a narrow range of viewpoints.

## How to protect yourself
### Device configuration

#### Blocking major websites
In the hosts file (Linux: /etc/hosts), add the following.
```
# Protection of sanity
127.0.0.1 reddit.com www.reddit.com
127.0.0.1 twitter.com www.twitter.com
127.0.0.1 instagram.com www.instagram.com
127.0.0.1 facebook.com www.facebook.com
127.0.0.1 youtube.com www.youtube.com
```
This will block all the mentioned sites. Don't worry if you think you need Youtube. There is a workaround for that later.

#### Browser addons
You don't have to install or use all of them. This is just what I use, and what I think will be useful for others.
##### uBlock Origin
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/) [Chromium](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm?hl=en)

Mitigates: Consumption, manipulation, tracking

Convenience impact: Negligible

Blocks advertising and other kinds of undesirable content.

##### NoScript
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/noscript/)	[Chromium](https://chrome.google.com/webstore/detail/noscript/doojmbjmlfjjnbmnoijecmcbfeoakpjm?hl=en)

Mitigates: All

Convenience impact: Medium

This addon blocks JavaScript from running on pages by default. Without JavaScript, Web pages are little more than formatted documents downloaded from a server. This allows you to choose which scripts to allow. Often this will show you how websites are configured to use analytics (often Google Analytics) to track you. This will block them by default. 

##### ClearURLs
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/clearurls/)	[Chromium](https://chrome.google.com/webstore/detail/clearurls/lckanjgmijmafbedllaakclkaicjfmnk?hl=en)

Mitigates: Tracking

Convenience impact: Negligible

This addon will remove the strings on your URLs that provide extra information to servers, such as who referred the link to you or other forms of data used for tracking.

##### Decentraleyes
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/decentraleyes/)	[Chromium](https://chrome.google.com/webstore/detail/decentraleyes/ldpochfccmkkmhdbclfhpagapcfdljkj?hl=en-US)

Mitigates: Centralization, tracking

Convenience impact: Negligible

Replaces remote JavaScript with locally cached files to avoid sending requests to central servers. Can also speed up some pages.

##### GIF Blocker
[Firefox](https://addons.mozilla.org/en-GB/firefox/addon/gif-blocker/)	[Chromium](https://chrome.google.com/webstore/detail/gif-blocker/ahkidgegbmbnggcnmejhobepkaphkfhl)

Mitigates: Manipulation

Convenience impact: Low

Block GIFs from playing. This saves bandwidth, but more important protects your attention from being spent on them.

##### Detect Cloudflare
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/detect-cloudflare/)

Mitigates: None, but provides information about tracking and centralization

Cloudflare is a service that stands in between you and the server. It provides many features, including content delivery and checking whether you are a bot. However, it also does a lot of tracking. In addition to concerns posted by usual trackers, it is also capable of performing a man-in-the-middle attack by intercepting HTTPS encrypted packets. [More info on why this is a bad thing](https://unixsheikh.com/articles/stay-away-from-cloudflare.html)

##### Redirector
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/redirector/)	[Chromium](https://chrome.google.com/webstore/detail/redirector/ocgpenflpmgnfapjedencafcfakcekcd?hl=en)

Mitigates: Tracking

Convenience impact: Low

This addon allows you to set auto redirects. We will use it to redirect all links to youtube.com (now blocked if you set the hosts file) to piped.jae.fi, which is an alternative frontend of Youtube that do not use an algorithm to recommend you content based on your usage data. Though, it is best to avoid using the official instance of Piped, because it is cloudflared and is more likely to track you.

Go to addons preferences, and "Edit Redirects". Download this [file](https://freelanguagetools.org/redirect-youtube.json), and click on "Import" and select it. This will redirect all Youtube links to piped. It is useful when you receive links to youtube, as you can still watch the video without being manipulated by Youtube.

#### Other browser configuration
- Disable video autoplay: Protects attention
- Set security setting to "Strict" (Firefox)

### Personal choices
It is important to realize that technical measures alone cannot solve the problem for you. They are meant to complement it by make undesirable Web content less attractive. However, it is still up to you to use the Web reasonably.

You must recognize the harms that the modern Web is causing to you. You should also focus more on other pursuits, such as reading or simply going outside. 

You should also delete or disable your accounts to avoid temptation.


