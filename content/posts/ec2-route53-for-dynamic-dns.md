---
title: "EC2 + Route53 for Dynamic DNS"
date: 2016-03-12T10:28:06-05:00
draft: false
---

Recently I ran into a problem while working with Amazon EC2 servers. Servers without dedicated elastic IP addresses would get a different IP address every time they were started up! This proved to be a challenge when trying to SSH in to the servers.

**How can I have a dynamic domain name that always points to my EC2 server?**

Amazon’s Route53 came to mind. Route53, however, does not have a simple way to point a subdomain directly to an EC2 instance. You can set up load balancers between Route53 and your instance, but that’s a hassle. You can also set up an elaborate private network with port forwarding — yuck.

I wanted a simple way to set a Route53 subdomain's `A` record to point to an EC2 instance's public IP address, on startup.

Enter [go-route53-dyn-dns](https://github.com/mk6502/go-route53-dyn-dns). This is a simple Go project that solves this problem. It is a small binary that reads a JSON configuration file and updates Route53 with an EC2 instance’s public IP address.

Included in the GitHub `README.md` file is how to set everything up.

The project is here: [go-route53-dyn-dns](https://github.com/mk6502/go-route53-dyn-dns).
