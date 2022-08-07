---
title: "Execute Interactive Programs From Go"
date: 2018-02-21T09:11:22-05:00
draft: false
---

I had a hard time figuring out how to make a Go program execute a command and make that program take over the console. I wanted my program to launch an SSH session.

I recently started working on a tool to help me SSH into EC2 instances (more details coming in a future blog post). The goal was to automatically open up an SSH session into an EC2 instance.

It’s easy to execute a program like ssh but the input and output of that program is lost. After trying to figure it out — I had a realization — this was easy! Truly one of those moments where it’s obvious once you see it.

```golang
cmd := exec.Command(, "root@127.0.0.1))
cmd.Stdout = os.Stdout
cmd.Stdin = os.Stdin
cmd.Stderr = os.Stderr
cmd.Run()
```

That's all these is to it. I bet a similar approach would work in other languages — you're setting the stdin, stdout, and stderr of your command to go to your terminal. When the program is finished running, control is given back to your Go program.
