---
title: "Install TA-Lib Without Homebrew"
date: 2021-01-03T08:12:21-05:00
draft: false
---

The only package I ever install using [Homebrew](https://brew.sh/) is `TA-Lib`.

Everything else I need is already available.

`TA-Lib` isn't updated often and it's easy to install by compiling from source.


## How-To
This guide will work on macOS 11.1 (Big Sur). It works perfectly on an M1 (or Intel) Mac.

First, download `TA-Lib` from [SourceForge](https://sourceforge.net/projects/ta-lib/).

Then run:

```console
tar xf ta-lib-0.4.0-src.tar.gz
cd ta-lib
./configure --prefix=/usr/local
make
sudo make install
```

That's all it takes.

The `--prefix` flag is important. macOS Big Sur doesn’t let you modify `/usr` even when you use sudo.

Installing the Python TA-Lib library should work fine now:

`pip install TA-Lib`
