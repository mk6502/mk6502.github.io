---
title: "Chipee - CHIP-8 Emulator in C"
date: 2020-01-01T11:28:33-05:00
draft: false
---

I **finished** a thing in my free time! [Chipee](https://github.com/mk6502/chipee/)!

## Goals

I’ve always wanted to write an emulator and this is the first time I actually got around to finishing one!

My goals were to learn about how to write an emulator and to re-learn C. It’s been years since I wrote any halfway decent C.

I’ve also never done anything using SDL, sound, or even a window with graphics.

## Why CHIP-8?
I chose CHIP-8 because it’s the simplest thing I could find. It's simpler than a NES or Gameboy.

I wanted the code to be as simple as possible. That’s partly why I stayed away from any sort of cleverness too — I wanted the code to be readable for others. No complex build systems, no C++ templates, etc.

## Development
Maybe others will find it useful.

The most difficult thing was getting started and getting the hang of bitwise shifting operations after years of not using them.

The 2nd most difficult thing was SDL graphics and sound.

The actual CPU operations were pretty straightforward and documentation online is easy to find.

## The Code
The code is available on [GitHub](https://github.com/mk6502/chipee) under the MIT license: [chipee: Adventures in CHIP-8](https://github.com/mk6502/chipee)