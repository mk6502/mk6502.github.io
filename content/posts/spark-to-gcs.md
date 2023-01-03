---
title: "Spark to Google Cloud Storage"
date: 2023-01-21T19:31:00-06:00
draft: true
---

Let's get right down to business - here is how to connect to Google Cloud Storage
using Spark 3.x.

First, create a service account in GCP, then download the JSON key file.
Save it somewhere secure (e.g. import it into Vault or Secrets Manager).

Grant that service account permission to read and write to the bucket.

Grab the Hadoop 3.x JAR (`gcs-connector-hadoop3-latest.jar`) from [Google](https://cloud.google.com/dataproc/docs/concepts/connectors/cloud-storage).

Place that JAR into Spark's `jars` directory.

Finally, fire up a Spark shell (or PySpark as in this example), and run:

```
from pyspark.sql import SparkSession

spark = SparkSession.builder.getOrCreate()

spark.conf.set("google.cloud.auth.service.account.enable", "true")
spark.conf.set("google.cloud.auth.service.account.json.keyfile", "PATH-TO-JSON-KEYFILE.json")

df = spark.createDataFrame([{"num": x} for x in range (10000)])
df.write.mode("overwrite").parquet("gs://BUCKET-NAME/hello/")
```

That's all there is to it.

This was a quick post mainly for myself if I ever need to come back to it.
