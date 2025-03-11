# PySpark Functions Documentation

# Table of Contents

- [1. take() - Retrieve specific number of rows](#take)
- [2. partitionBy() - Partition data by columns](#partitionBy)



# 1. take() Function
### take
The take() function is an action operation in PySpark that retrieves a specified number of rows from a DataFrame or RDD.

## Syntax

```python
DataFrame.take(n)
# or
RDD.take(n)
```

## Parameters

| **Parameter** | **Description** |
| --- | --- |
| n | Number of rows to return (integer) |

## Return Value

Returns a list containing the first n rows of the DataFrame/RDD.

## Example Usage

```python
# Create a sample DataFrame
df = spark.createDataFrame([(1, "John"), (2, "Jane"), (3, "Bob")], ["id", "name"])

# Take first 2 rows
result = df.take(2)

# Print the result
for row in result:
    print(row)
```

## Key Points

- take() is an action operation, meaning it triggers computation and returns results to the driver
- Returns actual data, not a DataFrame object
- Useful for testing and debugging with small samples of data
- Not recommended for large datasets as all data is loaded into driver memory

## Common Use Cases

- Quick data inspection
- Testing transformations on small samples
- Debugging data pipelines
- Creating small sample datasets

## Best Practices

<aside>
⚠️ Be cautious when using take() on large datasets as it can cause out-of-memory errors in the driver

</aside>

Consider using show() instead of take() when working with DataFrames for better formatted output

## Video Reference

[Watch Tutorial on my Channel - Youtube](https://youtube.com/shorts/hI75aSypdkE?feature=share)
[Watch Tutorial on my Channel - Tiktok](https://www.tiktok.com/@pencil_cravon/video/7439175515803585848?lang=en)



# 2. partitionBy() Function
### partitionBy
The partitionBy() function is used to partition data by specified columns when writing DataFrames to disk. It helps in organizing data storage and can improve query performance.

## Syntax

```python
DataFrame.write.partitionBy(cols).save(path)
```

## Parameters

| **Parameter** | **Description** |
| --- | --- |
| cols | String or List of columns to partition by |

## Example Usage

```python
# Create a sample DataFrame
df = spark.createDataFrame([
    (1, "Sales", "2023"), 
    (2, "HR", "2023"),
    (3, "Sales", "2024")
], ["id", "department", "year"])

# Write DataFrame partitioned by department and year
df.write \
    .partitionBy("department", "year") \
    .parquet("/path/to/output")
```

## Key Points

- Creates a directory structure based on partition columns
- Improves query performance when filtering on partition columns
- Helpful for data organization and management
- Supports multiple partition columns

## Common Use Cases

- Organizing data by date/time fields
- Separating data by categories or regions
- Optimizing query performance
- Managing large datasets efficiently

## Best Practices

<aside>
⚠️ Choose partition columns carefully - too many partitions can lead to small files and poor performance

</aside>

Consider the cardinality of partition columns and typical query patterns when designing the partition strategy

## Video Reference

[Watch Tutorial on YouTube](#)
