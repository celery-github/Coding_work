## Simple Data Frame Actions ##
df.printSchema()                         ###### return the schema
df.show(n,False)                         ###### show n rows without truncation
df.count()                               ###### return number of rows
df.filter(condition)                     ###### apply filter to dataframe
df.withColumn('<col_name>',udf_eg(*col)) ###### Create new column or modify existing column

## Spark Submit: Need to create a spark session for spark submit, add two lines below at the beginning of your code ##
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName('App Name').enableHiveSupport().getOrCreate()

## Read Hive Table ##
q = '''select * from database.table'''
df = spark.sql(q)

## Read HDFS files (Need to know the file format) ##
df = spark.read.<format>('/PATH/file')   ###### format: parquet, orc, etc..

## UDF: User Defined Function ##
def udf_eg():
   print("Hello World")

spark.udf.register('udf_eg', udf_eg)     ###### For functions you want to apply in a sql query

udf_eg = udf(udf_eg)                     ###### For function you want to apply to a dataframe column
