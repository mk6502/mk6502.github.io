---
title: "Apache Spark on Google Colaboratory"
date: 2018-03-07T09:01:31-05:00
draft: false
---

Google recently launched a preview of [Colaboratory](https://colab.research.google.com/), a new service that lets you edit and run IPython notebooks right from Google Drive — free! It’s similar to [Databricks](https://databricks.com/try-databricks) — give that a try if you’re looking for a better-supported way to run Spark in the cloud, launch clusters, and much more.

Google has published some tutorials showing how to use Tensorflow and various other Google APIs and tools on Colaboratory, but I wanted to try installing Apache Spark. It turned out to be much easier than I expected. [Download the notebook](https://drive.google.com/file/d/1mI1PnM7QDmXdMLQL79TrW1NA45gJ6I_L/view?usp=sharing) and import it into [Colaboratory](https://colab.research.google.com/) or read on...

Under the hood, there’s a full Ubuntu container running on Colaboratory and you’re given root access. This container seems to be recreated once the notebook is idle for a while (maybe a few hours). In any case, this means we can just install Java and Spark and run a local Spark session. Do that by running:

```console
!apt-get install openjdk-8-jdk-headless -qq > /dev/null
!wget -q http://apache.osuosl.org/spark/spark-2.2.1/spark-2.2.1-bin-hadoop2.7.tgz
!tar xf spark-2.2.1-bin-hadoop2.7.tgz
!pip install -q findspark
```
Now that Spark is installed, we have to tell Colaboratory where to find it:

```python
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64" os.environ["SPARK_HOME"] = "/content/spark-2.2.1-bin-hadoop2.7"
```

Finally (only three steps!), start Spark with:

```python
import findspark
findspark.init()
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[*]").getOrCreate()
```

That's all there is to it — Spark is now running in local mode on a free cloud instance. It's not very powerful, but it’s a really easy way to get familiar with Spark without installing it locally or setting up and maintaining an EC2 instance.
