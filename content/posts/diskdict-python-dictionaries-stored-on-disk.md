---
title: "DiskDict — Python dictionaries stored on disk"
date: 2016-12-05T09:25:59-05:00
draft: false
---

This weekend while running a rather large Python job, I ran into a memory error. It turned out that a dictionary I was populating could potentially become too big to fit into RAM. This is where `DiskDict` saved me some time.

[https://github.com/AWNystrom/DiskDict/](https://github.com/AWNystrom/DiskDict/)

It's definitely not the best way to solve an issue, but in this case I was working with a limited system where rewriting the surrounding code would have been intrusive. Plus, the job didn’t have time constraints, so `DiskDict` was a decent workaround.

Wanted to share because it proved useful to me!
