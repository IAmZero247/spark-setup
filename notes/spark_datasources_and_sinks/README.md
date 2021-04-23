# Spark Data Sources And Sink 


1.  Spark Sources - External And Internal 

       ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_data_sources_and_sinks1.jpg?raw=true)
			  


2.  Internal Sources And Dataframe Reader

      *  General Structure 
      
          ```
          DataFrameReader
		   .format(...)
		   .option('key', 'value')
		   .schema(...)
		   .load
          ```	
		
	  *  Format 
          
		   ```
		    Build in Format -> csv , json , parquet , orc jdbc
			Community Format -> avro , mongodb , cassandra , xml , hbase , redshift etc 
           ```		  
		
	  *  Options - Read Mode

           ```
            1. Permissive    [places corrupted row in a column - "_CORRUPT_RECORD
		    2. Drop Malformed
		    3. Fail Fast
           ```
		  
	  *  Schema 
	       
		   ```  
           Explicit  
           Implicit		   
           ```
      *  Egs: 

          ```
		  FlightTimeCsvDF = spark.read \
						.format("csv") \
						.option("header", "true") \
						.option("inferSchema", "true")
						.data("data/flight*.csv")
		  
		  FlightTimeJsonDF = spark.read \
						.format("json") \
						.option("inferSchema", "true")
						.data("data/flight*.json")
						
		
          FlightTimeParquetDF = spark.read \
						.format("parquet") \
						.option("inferSchema", "true")
						.data("data/flight*.parquet")		
						
          
          ```		  
	  
	  * Print Schema 
	  
          ```
          
		  Eg 
		  
		  logger.info( "Schema :" + FlightTimeParquetDF.schmea.simpleString())
		  
          ```		  
	  
        	  
	  
3.  Spark Data Types 
    
      ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_datatypes_to_python.jpg?raw=true)
	  

4.  Creating Spark DF Schemas [ Explicit ]

      -  Programmatically [StructType]
	  -  Using DDL String

      ```
	  
	    1. Programmatically 
	  
			flightSchemaStruct = StructType([
				StructField("FL_DATE", DateType()),
				StructField("OP_CARRIER", StringType()),
				StructField("OP_CARRIER_FL_NUM", IntegerType()),
				StructField("ORIGIN", StringType()),
				StructField("ORIGIN_CITY_NAME", StringType()),
				StructField("DEST", StringType()),
				StructField("DEST_CITY_NAME", StringType()),
				StructField("CRS_DEP_TIME", IntegerType()),
				StructField("DEP_TIME", IntegerType()),
				StructField("WHEELS_ON", IntegerType()),
				StructField("TAXI_IN", IntegerType()),
				StructField("CRS_ARR_TIME", IntegerType()),
				StructField("ARR_TIME", IntegerType()),
				StructField("CANCELLED", IntegerType()),
				StructField("DISTANCE", IntegerType())
			])
			
			
			flightTimeCsvDF = spark.read \
								.format("csv") \
								.option("header", "true") \
								.schema(flightSchemaStruct) \
								.option("mode", "FAILFAST") \
								.option("dateFormat", "M/d/y") \                     # -> we need to specify the date or datetime format
								.load("data/flight*.csv")
								
		    
			logger.info("CSV Schema:" + flightTimeCsvDF.schema.simpleString())
			
        2. DDL String 

            flightSchemaDDL = """FL_DATE DATE, OP_CARRIER STRING, OP_CARRIER_FL_NUM INT, ORIGIN STRING, 
								ORIGIN_CITY_NAME STRING, DEST STRING, DEST_CITY_NAME STRING, CRS_DEP_TIME INT, DEP_TIME INT, 
								WHEELS_ON INT, TAXI_IN INT, CRS_ARR_TIME INT, ARR_TIME INT, CANCELLED INT, DISTANCE INT"""	


            flightTimeJsonDF = spark.read \
								.format("json") \
								.schema(flightSchemaDDL) \
								.option("dateFormat", "M/d/y") \
								.load("data/flight*.json")

            logger.info("Parquet Schema:" + flightTimeParquetDF.schema.simpleString())								

      ```	  
		

   
         		 
			   
			   
			   
	  
    	
   
