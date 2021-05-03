# Spark Ecosystem 


![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_ecosystem.jpg?raw=true)
    
    

# Spark Setup [python]


1.  https://adoptopenjdk.net/

      ```
	  1. java -version
	  2. javac -version 
	  
	  ```


2.  https://spark.apache.org/downloads.html

      ```
	 
	 Spark-release ---> 3.1.1
     
	 Choose a build package ---> Prebuild for Apache Hadoop 2.7
	 
	 Download ---> spark-3.1.1-bin-hadoop2.7.tgz
	 
	 Use 7zip to extract in windows
	 
      ```	 
	 
3.  Set env Variable
    
      - SPARK_HOME=C:\Softwares\spark3

      - HADOOP_HOME=C:\Softwares\hadoop27

      - PYSPARK_PYTHON=C:\Softwares\anaconda3\python  

      ```
	  echo %SPARK_HOME%
	  echo %HADOOP_HOME%
	  echo %PYSPARK_PYTHON%
      ```	  

4.  REPL setup For Scala 

      Open cmd and type 

      `spark-shell`

5.  REPL setup For Pyspark  
    
      Open cmd and type 

      `pyspark`	
	  
6.  PyCharm IDE 

      * Open sample project in repo PY-HelloSpark 
	   
	  * C:\Demo\PY-HelloSpark
	  
	  * Preferences > Setting > Project: PY-HelloSpark > Python Interpretor 
	  
	      - Set Python Interpretor to No Interpretor (if pycharm has already automatically picked up some interpretor)
		   
		  -  Start configuring new one  >>>  Add >  Choose Conda Enviroment .
		      
			  ```
				 *  Location -> C:\Softwares\anaconda3\envs\my_pycharm
			     *  Py Version -> 3.8
			     *  Conda Executable -> C:\Softwares\anaconda3\Scripts\conda.exe
			     *  Enable make available for all the projects 
			   
			                      Or 
			   
			     * Choose existing env (if any)
			   
			     * Now add pySpark dependency 
			   
			         -- Setting > Project: PY-HelloSpark > Python Interpretor> + (Click Plus icon)
				     -- Type "pyspark" (choose latest version) and click the install button 
					  
	          ```
			  
			  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/pycharm_setup_image1.jpg?raw=true)
			  
	  *  Open HelloSpark.py and Try Run it 
	      
		  (RUN ENV -> Config as in below) 
		  
		  
		  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/pycharm_setup_helloworld_run_arguments.jpg?raw=true)
		 
	
      * Setting Logs
           
		   * Open C:\Softwares\spark3\conf and rename spark-defaults.config.template -> spark-defaults.config
		   
		   * Copy paste content from repo conf/spark-defaults.config 
		   
		   * Run again.
		    

7.  Jupyter Notebook 

      ```
	   
	  1. Set env --SPARK_HOME=C:\Softwares\spark3 
	  
	  2. Open Anaconda prompt and install find spark 
	       
		    python -m pip install findspark
			
	  3. Open jupyter notebook and create new notebook 

               import findspark 
			 findspark.init()
			 
			 
			 import pyspark 
			 from  pysparl.sql  import SparkSession 
			 
			 spark = SparkSession.builder.getOrCreate()
			 
			 spark.read.json("C:\demo\notebook\data\people.json").show()
			 
	  ```		 
          		  

8.  Scala Setup With IntellijIdea (SBT as Build Tool)
    
	  - Installing scala plugin in intellij idea 
	      
		  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/intellij_idea_scala_plugin.jpg?raw=true)	   
			   
	  
	  
	  - Import sample project in repo SCALA-HelloSpark and add below Run Config
	    
		  ```
		  -Dlog4j.configuration=file:log4j.properties
		  -Dlogfile.name=hello-spark
		  -Dspark.yarn.app.container.log.dir=app-logs
		  ```
		  
		  * Make sure the spark-scala version match up in sbt file
		    
			  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/sbt_scala_spark_version.jpg?raw=true)	   
			
		  
		  * Run config for HelloSpark.scala - Sample
		    
			  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/intellij_idea_main_run_config.jpg?raw=true)	   
			
		  
		  * Run Config for HelloSparkTest.scala
		      
			  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/intellij_idea_test_run_config.jpg?raw=true)	   
			
      		   
    
9.  Docker Container 

      ```
	  docker run -it --rm -p 4040:4040 --name spark3.0-centos8 -h localhost learningjournal/spark:spark3.0-centos8
	  
	  
	   * spark-shell
      ```	  
			   
	  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/docker_spark.jpg?raw=true)	   
			   
	  
    	
   
