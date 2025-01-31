---
title: Automating OOO replies
description: How I created a set-and-forget automation with my out of office replies.
date: '2025-01-30'
categories:
  - automation
published: true
---

### Set and forget

A few years ago I got tired of setting my out of office when I was going on any planned annual leave. Having to turn it on and set a message was tedious and I wondered if there was a method to automate it.
<br>
I have an o365 account for work which includes PowerAutomate which I thought  was perfect for this scenario.
<br>
<br>
I started by creating a flow that would check for any upcoming calendar events with the keyword “holiday” within it. Employees request annual leave through HR software which is then approved or rejected by a manager. Departmental calendars can be added to employees email clients which synchronises approved annual leave automatically.
<br>
<br>
<img src="./automating-ooo/ooo-1.png" alt="Image showing the original flow of this automated process.">
<br>
<img src="./automating-ooo/ooo-2.png" alt="Here we define the calendar we want to monitor, the look-ahead time which I've set to 15 and how often we want to check for items which is set to 5 minutes.">
<br>
The PowerAutomate script I wrote will regularly check-in for the “Holiday” keyword and if there’s a match on the day an action will automatically set your out of office with whatever message you want.
<br>
<br>
<img src="./automating-ooo/ooo-3.png" alt="">
<br>
Once you've created the event and the condition you'll next want to set automatic replies.
<br>
<br>
<img src="./automating-ooo/ooo-4.png" alt="">
<br>
For extra flair I wanted the auto reply include a date when I will return from annual leave. Fortunately this can be done dynamically with the formatDateTime() function.
<br>
<br>
We need to format addToTime() as without it you'll get a standard javascript fomatted date which doesn't look great on auto-reply emails. Something more familar is needed.
<br>
<br>
<img src="./automating-ooo/ooo-5.png" alt="">
<br>
That's all there is to it! Nice and easy can be done in a few minutes and now you don't ever have to think about setting up your auto-replies again. This script has been running for 3 years for me and I've never had to check in on it once.
