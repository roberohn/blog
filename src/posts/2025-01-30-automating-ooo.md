---
title: Automating OOO Replies
description: How I created a set-and-forget automation with my out of office replies.
date: '2025-01-30'
categories:
  - automation
published: false
---

## Automating Out Of Office Replies

I got tired of setting my out of office when I was going on any planned annual leave. Having to turn it on and set a message was tedious and I wondered if there was a method to automate it.
<br>
I have an o365 account for work which included PowerAutomate which I had never dabbled with before and thought it was perfect for this scenario.
<br>
<br>
I started by creating a flow that would check for any upcoming calendar events with the keyword “holiday” within it. Employees request annual leave through HR software which is then approved or rejected by a manager. Departmental calendars can be added to employees email clients which synchronises approved annual leave automatically.
<br>
<br>
The PowerAutomate script I wrote will regularly check in for the “Holiday” keyword and if there’s a match on the day an action will automatically set your out of office with whatever message you want.
<br>
<br>
This automation has been happily running for 3 years now. Truly set and forget.
<br>
<br>
Lately after sharing this automation with a colleague I wanted to improve on it a little and have the auto reply include a date when I will return from annual leave. Fortunately this can be done dynamically.
