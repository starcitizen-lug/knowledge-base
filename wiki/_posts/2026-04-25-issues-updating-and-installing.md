---
layout: post
title:  "Recent issues updating/installing Star Citizen"
categories: game-news install-update-problems
tags: "active"
excerpt_separator: <!--more-->
---

{: .warning-title }
> (Apr 25, 2026)
>
> {{ page.title }}
>
> RSI Launcher may crash at calculating disk space. You may see an out of space or error code 3004/3005/5006/5008  
> Log may show *"[Pipeline] Phase compute_size timed out after 60000ms, cancelling and skipping."*  
> Sometimes caused by a slow or unreliable network connection.
>
> 1. [Locate your Star Citizen LIVE](/Tips-and-Tricks#where-is-my-wine-prefix-where-is-my-liveptu-directory) directory.
> 2. Create a new empty file in your LIVE directory named `Data.p4k.part`
> 3. If you're installing the game for the first time, also create a new empty file named `Data.p4k`
> 4. Re-launch the game and try the update or verify again.