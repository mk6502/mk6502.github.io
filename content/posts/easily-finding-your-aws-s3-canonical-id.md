---
title: "Easily Finding Your AWS S3 Canonical ID"
date: 2019-02-28T10:54:19-05:00
draft: false
---

Another quick post — found this in the AWS Console UI. If you ever need to share your AWS Canonical ID with someone, e.g. to share S3 buckets.

You can find your AWS Canonical ID by using various APIs — but I was also able to find it using the AWS Console UI.

By opening up the S3 console and selecting a bucket you own, you can view the Canonical ID by viewing the Access Control List in the Permissions tab.

![AWS S3 Console Canonical ID](/img/aws_s3_canonical_id.png)

Nice and easy, no API documentation needed!