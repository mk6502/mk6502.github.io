---
title: "S3A on Spark"
date: 2020-11-29T22:25:58-05:00
draft: false
---

Quick post mostly for my own reference since I always need to re-learn how to do this.

This used to be more difficult in older versions of Spark, but when using Spark 2.4 or later, all you have to do is:

```console
wget https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk/1.7.4/aws-java-sdk-1.7.4.jar -P $SPARK_HOME/jars/
wget https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.7.3/hadoop-aws-2.7.3.jar -P $SPARK_HOME/jars/
```

That’s all there is to it. The `s3a://` prefix should work now for reading and writing data using Spark.
