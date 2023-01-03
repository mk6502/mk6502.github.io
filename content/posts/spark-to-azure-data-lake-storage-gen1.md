---
title: "Spark to Azure Data Lake Storage Gen1"
date: 2023-01-30T19:44:32-06:00
draft: true
---

This is another quick post for how to connect Spark to various platforms.

I used Azure Data Lake Storage on a project in the past and had a tough time figuring out what to do (there are huge differences between Azure Blob Storage, Azure Data Lake Gen1, and Azure Data Lake Gen2).

This guide assumes that you have a `client_id`, `tenant_id`, and `client_secret` from Azure.

### Code Example
```
# Acquire these JARs from Maven:
# azure-data-lake-store-sdk-2.3.10. jar
‡ hadoop-azure-datalake-3.2.3.jar
# wildfly-openssl-1.0.7. Final.jar
# place them in $SPARK HOME/jars/

spark = SparkSession.builder.getOrCreate()
tenant_id = "some-identifier-here"
client_id = "some-identifier-here"
client_secret = "super-top-secret-here"

spark.conf.set("fs.adl.account.auth.type", "OAuth") spark.conf.set("fs.adl.oauth2.refresh.url", f"https://login.microsoftonline.com/{tenant_id}/oauth2/token")
spark.conf.set("fs.adl.oauth2.client.id", client_id) spark.conf.set("fs.adl.oauth2.credential", client_secret)

# That's all there is to it:
df = spark.read.parquet("adl://something.azuredatalakestore.net/folder/")
```

Finding the correct JARs and Spark configurations was more than half the battle. Hopefully this post helps someone out in the future!
