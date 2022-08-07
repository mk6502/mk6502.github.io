---
title: "Writing Huge CSVs Easily and Efficiently With PySpark"
date: 2018-02-05T13:15:34-05:00
draft: false
---

I recently ran into a use case that the usual Spark CSV writer didn't handle very well — the data I was writing had an unusual encoding, odd characters, and was really large.

I needed a way to use the Python `unicodecsv` library with a Spark dataframe to write to a huge output CSV file.

I don’t know how I missed this RDD method before, but `toLocalIterator` was the cleanest, most straight-forward way I got this to work. Here's the code (with a bunch of data cleanup and wrangling omitted):

```python
with open("output.csv", "w+") as f:
    w = unicodecsv.DictWriter(f, fieldnames=["num", "data"])
    for rdd_row in df.rdd.toLocalIterator():
        w.writerow(rdd_row.asDict())
```

That’s all there is to it! `toLocalIterator` returns a Python iterator which yields RDD rows. It's essentially doing a collect to the driver, but only one partition is being processed at a time, saving memory.
