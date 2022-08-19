---
title: "CloudFormation Wishlist"
date: 2022-08-18T20:29:08-05:00
draft: false
---

This post originally started as a post about Terraform, but I decided to break that out into a separate post.

It turned out that I had a wishlist for improvements I'd like to see in CloudFormation.

I've been using CloudFormation for years and have been pushing teams I work with to do the same - with mixed results.

# Problems with CloudFormation
## Writing Templates
CloudFormation templates are tedious to write.

CloudFormation consists of JSON or YAML files that define "stacks". You can create VPCs, Lambda functions, S3 buckets - and pretty much anything else.

No matter what we tried, these templates always ended up being a big mess of 2000+ lines of YAML. We tried nested stacks. We tried modules. No matter what, **the code just never looked clean**.

Don't get me started about **`!Ref` and `!Join`** and other CloudFormation syntax either.

## Deploying
There is no way to know whether a CloudFormation template will deploy correctly without actually trying to deploy it. **There is no "dry run" to update an existing stack** (that I know of).

There are plenty of editor/IDE plugins to lint and validate CloudFormation templates, but that only goes so far.

Deploying CloudFormation stacks also **takes a long time**. For whatever reason, it seems like CloudFormation takes a minute or two before it actually begins provisioning or updating a stack. Then it takes 3 more minutes to actually make changes.

The feedback cycle just _takes a long time_.

It's like waiting 5 minutes for code to compile.

To be fair to CloudFormation - it does a lot of work during that first minute or two.

CloudFormation needs to go out to every service and come up with a plan for what to change. Terraform does not handle this gracefully.

## Stacks
I think a problem with CloudFormation is the notion of "stacks".

Software engineering teams at Nielsen have broad access to AWS - they can do pretty much anything, with some guardrails and best-practice enforcement.

Teams generally created 1-2 CloudFormation templates for their "stacks" - things like a stack for a CodePipeline, a stack for some web application or API and it's database, and maybe another stack for some backend data processing.

The problem? **Shared resources**. Multiple teams shared an AWS account and VPCs and subnets. Multiple stacks within a single team might share resources too (maybe your frontend and backend both need access to something in AWS Secrets Manager). 

What stack do those kinds of things go in?

Do you make **one main stack**, and then multiple nested stacks? Probably not, since you want to be able to deploy things separately.

Do you make a **separate stack** for shared resources? What if you accidentally put a resource in a non-shared stack, and then need to move it to a different stack? You can't - a resource can only be in one CloudFormation stack at a time.

# Wishlist
## YAML, JSON, and Templates
AWS should **deprecate either JSON or YAML** (or both?) and focus on one syntax, and develop more tooling around template development - **IDE plugins, visualization tools, and the ability to perform dry runs (or to generate plans)**.

## Stacks
Maybe every AWS account should come with a "base" stack or a "shared" or "common" stack?

Maybe everything not in a stack should belong to this new shared stack?

Do resources need to be in "stacks" all the time?

## AWS UI+CLI Exports
GCP has a neat feature where many of its UI pages have a button to show the equivalent CLI command to generate whatever resource you're about to provision.

AWS should take this a step further - **generate the JSON/YAML CloudFormation snippets that would generate the equivalent resources**.

## UI/API "Lockdown"
AWS CloudFormation is great at detecting drift - when someone makes a change to a stack outside of CloudFormation.

Maybe someone changed S3 bucket permissions using the UI or modified an autoscaling group - CloudFormation is able to detect and handle this drift and fix it the next time the stack is deployed.

Here's an idea: **let me enable a "lockdown" mode**. Make it so that any resources managed in a stack cannot be modified using the AWS UI or CLI - preventing drift altogether. This would enforce best practices.

# Terraform
Terraform is a topic for next time - it doesn't solve everything, but I've started using it extensively.
