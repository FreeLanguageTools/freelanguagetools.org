---
title: "Tracking your time with free software"
date: 2021-10-11T15:10:59-04:00
tags: ["time-tracking", "tutorial"]
draft: false
---
Immersion-based language learning can be demotivating at times because of a
feeling of the lack of progress, unlike with traditional output-focused
techniques in which level can be assessed with the ability to speak. One of
the main ways to measure your progress in immersion is by tracking your time.
Unfortunately, most time tracking tools out there are online and proprietary,
which is unacceptable because what you spend your time on is sensitive and
valuable information.
<!--more-->
I classify total time into three types: studying, active immersion, and
passive immersion. 

I use [Timewarrior](https://timewarrior.net/), a simple command line tool for
tracking studying and active immersion when I am on my computer watching or
reading things, and 
[Track Work Time](https://f-droid.org/en/packages/org.zephyrsoft.trackworktime/) 
app on Android for tracking passive immersion, which usually consists of
listening to previously-watched shows or podcasts while doing other
activities.

I made a custom [Polybar](https://github.com/polybar/polybar) widget for
timewarrior. I can stop a task with a right click and continue it with a left
click on the widget. When there is no task running, it displays the previous
task.
![WebP for the result](/timew-widget.webp)
```
[module/timew]
type = custom/script
interval = 1
exec = timew su | tail -n4 | head -n1 | awk 'NF && NF-1 { print ( $(NF-4)" "$(NF-1) ) }'
format = <label>
format-underline = #e8f
click-right = timew stop
click-left = timew cont
```

The time spent are summed each week and then written in a spreadsheet in
Gnumeric. They are added together to give a total time spent on the language.
Studying and active immersion have a weight of 1, whereas passive immersion
have a weight of 0.4. 
![Tracking sheet](/tracking-sheet.png)
