---
title: "Semver vs. Calver and Why I Use Both"
subtitle: "How will people know I released a new version?"
date: 2021-04-03T11:25:05-05:00
draft: false
---

I began properly versioning the software I write recently. I’m working on a Python package that I hope others will use. My goal is to iterate and release new features and fixes over time, but I need a way to signal to the world that a new version is available.

## Why You Should Version Your Code

* It's a best practice.
* It makes you think about supporting users of your code.
* It only takes a few extra minutes during the software development lifecycle.
* You should version your code if you ever want to share it with others.

## Why You Should NOT Version Your Code

* It's a personal project. Unless your goal is to learn how to properly version your software, this can be a distraction.
* During the very beginning of a project. Making a decision about versioning should happen when you’re ready to share something with others — not before.
* Git and other version control systems version code for you. You can extend this with tags and releases.

## Popular Versioning Schemes
Two popular version schemes are Semantic Versioning and Calendar Versioning. Each have its strengths and weaknesses.

### Semantic Versioning

* Here’s the guide — the summary is exceptionally clear: https://semver.org [https://semver.org/]
* This method is more common and you’ve seen it. A version number is based on changes in the software.
* Examples of this: 1.0.0, 1.0.1, 1.1.0, 2.0.0.

### Calendar Versioning

* Here’s the guide: https://calver.org [https://calver.org/]
* This method uses the calendar to version software.
* Microsoft is starting to do this with Windows 10 — versions and updates are named after years and months they’re released.
* This is a little bit more loosely defined than Semantic Versioning.
* Examples: 2020.6, 2021.01.01, 21.04.

## When to Use Which

I use both of these approaches depending on what kind of application is being developed.

Even if you use neither of these approaches, consider using git tags, they’re very lightweight and you’ll thank yourself later. It’s like an easy-to-see snapshot your code at a point in time.

For “rolling” and fast-moving applications, I use CalVer:

* An example of this can be something like an ETL pipeline that’s continuously being modified.
* Easier to reason about and set up — it’s just a date.
* This is nicer than using only git for version history.

For slower-moving or shared components and libraries, use SemVer:
* Releases happen infrequently.
* Older releases are supported with patches.
* Great for shared libraries.
* Useful for when you want to provide some guarantees about compatibility to others.
