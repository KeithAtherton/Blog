---
title: "Power App Performance Measuring"
date: 2024-02-26
tags: ["PowerApps","PowerFx","Performance"]
---

Recently, I needed a way to measure how long some Power Fx code in a Power App took to process.

This was so that I could measure the performance *before* and *after* I made changes to the Power Fx code, to see if my changes improved the performance.

[Spoiler alert: In this case, the performance was actually *worse* after my changes! Still, by measuring the performance, I was able to know this for sure then change direction...]

So, I developed the following Power Fx snippet to wrap around the slow-running code to measure how long the code took to run:

```
UpdateContext({locStartTime:Now()});

// My slow code goes here...

UpdateContext({locTimeDiffSeconds:DateDiff(locStartTime, Now(), TimeUnit.Milliseconds)});
Notify($"Done: {locTimeDiffSeconds / 1000} second(s)");
```

After running the code (in this case, using a button OnSelect action), a notification popped up like this:

![Power App notification showing duration taken.](/img/2024-02-28-power-app-performance-measuring/power-app-notification.png "Power App notification showing duration taken")

**Disclaimer:** If you want more information from a user's session to diagnose and troubleshoot problems then I would recommend using [Power Apps Monitor](https://learn.microsoft.com/en-us/power-apps/maker/monitor-overview).

However, if you need a quick measure of how long something takes, then give this a shot!