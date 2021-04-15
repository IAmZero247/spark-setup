# spark-setup


1. https://spark.apache.org/downloads.html

     ```
	 
	 Spark-release ---> 3.1.1
     
	 Choose a build package ---> Prebuild for Apache Hadoop 2.7
	 
	 Download ---> spark-3.1.1-bin-hadoop2.7.tgz
	 
	 Use 7zip to extract in windows 
	 
2.  Set env Variable
    
      - SPARK_HOME=C:\Softwares\Spark3

      - HADOOP_HOME=C:\Softwares\hadoop27

      - PYSPARK_PYTHON=C:\Softwares\anaconda3\python    

3.  REPL setup For Scala 

      Open cmd and type 

      `spark-shell`

4.  REPL setup For Pyspark  
    
      Open cmd and type 

      `pyspark`	
	  
5.  PyCharm IDE 

      * Open sample project in repo 01-HelloSpark 
	   
	  * C:\Demo\01-HelloSpark
	  
	  * Preferences > Setting > Project: 01-HelloSpark > Python Interpretor 
	  
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
			   
			         -- Setting > Project: 01-HelloSpark > Python Interpretor> + (Click Plus icon)
				     -- Type "pyspark" (choose latest version) and click the install button 
					  
	          ```
			  
			  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/pycharm_setup_image1.jpg?raw=true)
			  
	  *  Open HelloSpark.py and Try Run it 
	      
		  (RUN ENV -> Config as in below) 
		  
		  
		  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/pycharm_setup_helloworld_run_arguments.jpg?raw=true)
		 
	
      * Setting Logs
           
		   * Open C:\Softwares\Spark3\conf and rename spark-defaults.config.template -> spark-defaults.config
		   
		   * Copy paste content from repo conf/spark-defaults.config 
		   
		   * Run again.
		    

6.  Jupyter Notebook 

      ```
	   
	  1. Set env --SPARK_HOME=C:\Softwares\Spark3 
	  
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
          		  

      		   
         		 
			   
			   
			   
	  
    	
   
