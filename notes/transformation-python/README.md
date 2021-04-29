# Spark Transform 


1.  Spark Transform Overview

      -  Combining Dataframe -> Joins , Unions
	  -  Aggregating and Summarizing -> Grouping Windowsing and Rollup 
	  -  Applying Function and build in Transformation
      -  Using Build-in column-level functions
      -  Creating and using UDFs
      -  Referencing Row / Columns
      -  Creating Column Expressions	  

       	  


2.  Manually Creating Rows and Dataframe [Used mostly in test cases]

      	  
	      
	  - Sample - RowDemo.py
		  
          ```
          
		  from pyspark.sql import *
		  from pyspark.sql.functions import *
		  from pyspark.sql.types import *
		  
		  from lib.logger import Log4j
		  
		  def to_date_df(df, fmt, fld):
			  return df.withColumn(fld, to_date(col(fld), fmt))
		  
		  if __name__ == "__main__":
		       spark = SparkSession \
			        .builder \
					.master("local[3]") \
					.appName("RowDemo") \
					.getOrCreate()

			   logger = Log4j(spark)

		  
		  
			   ## Step 1
			   my_schema = StructType([StructField("ID", StringType()),StructField("EventDate", StringType())])
          
			   ## Step 2
			   my_rows = [Row("123", "04/05/2020"), Row("124", "4/5/2020"), Row("125", "04/5/2020"), Row("126", "4/05/2020")]
		  
			   ## Step 3
			   my_rdd = spark.sparkContext.parallelize(my_rows, 2)
			   my_df = spark.createDataFrame(my_rdd, my_schema)

			   my_df.printSchema()
		       my_df.show()	
               new_df = to_date_df(my_df,  "M/d/y", "EventDate")
		       new_df.printSchema()
		       new_df.show()		  
		  
          ```		  
	  
           ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/data_frame_creation.jpg?raw=true)
	  
	  
3.  PyTest Sample  
          
	  - Sample - RowDemo_Test.py
    
          ```
			from datetime import date
			from unittest import TestCase

			from pyspark.sql import *
			from pyspark.sql.types import *

			from RowDemo import to_date_df


			class RowDemoTestCase(TestCase):

			    @classmethod
			    def setUpClass(cls) -> None:
			      cls.spark = SparkSession.builder.master("local[3]").appName("RowDemoTest").getOrCreate()
				
				my_schema = StructType([StructField("ID", StringType()),StructField("EventDate", StringType())])
				 
				my_rows = [Row("123", "04/05/2020"), Row("124", "4/5/2020"), Row("125", "04/5/2020"), Row("126", "4/05/2020")]
			      my_rdd = cls.spark.sparkContext.parallelize(my_rows, 2)
			      cls.my_df = cls.spark.createDataFrame(my_rdd, my_schema)

                def test_data_type(self):
				    rows = to_date_df(self.my_df, "M/d/y", "EventDate").collect()
				    for row in rows:
				        self.assertIsInstance(row["EventDate"], date)

                def test_date_value(self):
				    rows = to_date_df(self.my_df, "M/d/y", "EventDate").collect()
				    for row in rows:
			               self.assertEqual(row["EventDate"], date(2020, 4, 5))
		  ```

4.  Unstructered Data to Structured - Eg - Apache Standard Logs	  

      - LogFileDemo.py 
	      
		  ```
		   file_df = spark.read.text("data/apache_logs.txt")
           file_df.printSchema()

           log_reg = r'^(\S+) (\S+) (\S+) \[([\w:/]+\s[+\-]\d{4})\] "(\S+) (\S+) (\S+)" (\d{3}) (\S+) "(\S+)" "([^"]*)'

           logs_df = file_df.select(regexp_extract('value', log_reg, 1).alias('ip'),
                             regexp_extract('value', log_reg, 4).alias('date'),
                             regexp_extract('value', log_reg, 6).alias('request'),
                             regexp_extract('value', log_reg, 10).alias('referrer'))
							 
		   logs_df.printSchema()

           #sample spark-sql on logs-df
           
           logs_df \
			.where("trim(referrer) != '-' ") \
			.withColumn("referrer", substring_index("referrer", "/", 3)) \
			.groupBy("referrer") \
			.count() \
			.show(100, truncate=False)		   
		  ```
		  
		   ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/logfile_data_sample.jpg?raw=true)
		   
5.  Working with Dataframe Column - Column String And Column Object 


      ```
      airlinesDF = spark.read \
						.format("csv") \
						.option("header", "true") \
						.option("inferSchema","true") \
						.option("samplingRatio", "0.0001") \
						.load("/databricks-datasets/airlines/part-00000")
						
		
      # Column String
	  airlinesDF.select("Origin", "Dest", "Distance" ).show(10)
      
	  # Column Object 
      from pyspark.sql.functions import *
	  airlinesDF.select(column("Origin"), col("Dest"), airlinesDF.Distance).show(10)

      # Mixing Both 
      airlinesDF.select(column("Origin"), col("Dest"), "Distance").show(10)	  
	  
	  
						
      ```

6.  Column Expressions String/SQL Expressions And Column Object Expressions	

      ```
       airlinesDF.select("Origin", "Dest", "Distance", "Year","Month","DayofMonth").show(10)
	   
	   #Column String Expression - Add dateColumn using to_date sql function
	   1.  airlinesDF.select("Origin", "Dest", "Distance", expr("to_date(concat(Year,Month,DayofMonth),'yyyyMMdd') as FlightDate")).show(10)
	   2.  airlinesDF.selectExpr("Origin", "Dest", "Distance", "to_date(concat(Year,Month,DayofMonth),'yyyyMMdd') as FlightDate").show(10)
	   
	   #Column Object Expression - Add dateColumn using to_date sql function
	      from pyspark.sql.functions import *
	   1. airlinesDF.select(column("Origin"), column("Dest"), column("Distance"), to_date(concat("Year","Month","DayofMonth"),"yyyyMMdd").alias("FlightDate")).show(10)
	   2. airlinesDF.select("Origin", "Dest", "Distance", to_date(concat("Year","Month","DayofMonth"),"yyyyMMdd").alias("FlightDate")).show(10)
      ```	   
		 
        

