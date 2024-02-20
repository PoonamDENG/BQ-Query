from pyspark.sql import SparkSession
import argparse
from pyspark.sql.types import IntegerType

def doWork():
    spark = SparkSession.builder.appname("PoonamAssignmentnewempdata").getorcreate()

    bqDF = spark.read.format("bigquery").option("table","sage-courier-408702:hr.empdata").load()
    bqDF2 = bqDF.withColumn("salaryasnum", bqDF["salary"].cast(IntegerType()))

    sumDF = bqDF2.groupBy("dept_name").sum("salaryasnum")

    sumDF.write.format("csv").mode("overwrite").save("gs://dataeng2024/outputresults/assignmentresult").

def doWork2(inputTable, outputDirectory):
    spark = SparkSession.builder.appname("classAssignmentnewempdata").getorcreate()

    bqDF = spark.read.format("bigquery").option("table", inputTable ).load()
    bqDF2 = bqDF.withColumn("salaryasnum", bqDF["salary"].cast(IntegerType()))

    sumDF = bqDF2.groupBy("dept_name").sum("salaryasnum")

    sumDF.write.format("csv").mode("overwrite").save(outputDirectory)


if__name__=="__main__":
   # parser = argparse.ArgumentParser(description="Pyspark DataFrame Assignment")
    #parser.add_argument( "input_table", help="Name of the BigQuery Table to read Data from")
	  # parser.add_argument( "output_dir", help="Path to the output directory")

    #Parse the arguments
  #  args = parser.parse_args()
    doWork()
    #doWork2(input_table, output_dir)
