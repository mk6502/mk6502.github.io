---
title: "Installing Spark on Ubuntu in 3 Minutes"
date: 2018-09-19T12:57:59-05:00
draft: false
---

One thing I hear often from people starting out with Spark is that it’s too difficult to install. Some guides are for Spark 1.x and others are for 2.x. Some guides get really detailed with Hadoop versions, JAR files, and environment variables.

Here’s yet another guide on how to install Apache Spark, condensed and simplified to get you up and running with Apache Spark 2.3.1 in 3 minutes or less.

All you need is a machine (or instance, server, VPS, etc.) that you can install packages on (e.g. “sudo apt” works). If you need one of those, check out [DigitalOcean](https://m.do.co/c/18e08da59ad4). It’s much simpler than AWS for small projects.

First, log in to the machine via SSH.

Now, install OpenJDK 8 (Java):

```console
sudo apt update && sudo apt install -y openjdk-8-jdk-headless python
```

Next, download and extract Apache Spark:

```console
wget http://www-us.apache.org/dist/spark/spark-2.3.1/spark-2.3.1-bin-hadoop2.7.tgz && tar xf spark-2.3.1-bin-hadoop2.7.tgz
```

Set up environment variables to configure Spark:

```console
echo 'SPARK_HOME=$HOME/spark-2.3.1-bin-hadoop2.7' >> ~/.bashrc
echo 'PATH=$PATH:$SPARK_HOME/bin' >> ~/.bashrc
echo 'export PYSPARK_PYTHON=python3' >> ~/.bashrc
source ~/.bashrc
```

That’s it — you’re all set! You've installed Spark and it's ready to go. Try out `pyspark`, `spark-submit` or `spark-shell`.

Try running this inside `pyspark` to validate that it worked:

```python
spark.createDataFrame([{"hello": x} for x in range(1000)]).count() # hopefully this equals 1000
```
