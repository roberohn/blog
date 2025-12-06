---
title: Blood Donation Tracking
description: Showing my NHS blood donation milestones
date: '2025-10-02'
categories:
  - svelte
published: true
---

### 🩸

Over two years ago I signed up to donate my blood, I'm not a fan of needles or looking at my own blood being extracted from my arm but I go anyway. I hope the blood I've donated over the years has contributed to advance science and even save a few lives.<br><br>

I wanted to visualise the donations I've made against the milestones the NHS show on your account. Unfortunately there's no API or a method for me to extract the data out so for now I'm updating this manually but that's fine as I can only donate once every few months.<br><br>

I found online an [SVG pictorial fraction animation](https://codesandbox.io/p/sandbox/svelte-svg-pictorial-fraction-f1hv2) which I thought was perfect for this little project. I set that up as a component in a SvelteKit project and found the HEX code for the colour of blood (it's #8a0303).<br><br>

The site started off with just the one droplet showing the current donations to milestone.<br><br>

<img src="/blood-donations/blood.png" alt="A pictorial fraction that in the shape of a droplet with simulated liquid flowing within it like a wave"><br><br>

I wanted to take this further though, I wanted to show all the milestones from the blood.co.uk website so I copied the component five more times and applies some props so I can set a level against each one.<br><br>

To get the fill level I simply divide the number of donations against the milestone to give my a percentage of how full the component should be.<br><br>

I made the page into a grid of three columns and two rows and it'll shuffle down to one column when resized for mobile displays.<br><br>

Finally I wanted to have a go at self-hosting this so I've got the app deployed on a Docker container on my RPi. I use a small `.sh` script that pulls the main branch from GitHub and rebuilds the app. I'm next going to take a look at automating deployment when changes to main are committed<br><br>

Go and check it out! [blood.imjr.me](https://blood.imjr.me)
