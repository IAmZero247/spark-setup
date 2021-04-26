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
	  

