# Spark Execution  


1.  Spark Execution
    
	  * Interactive Client 
	      [Spark Shell , Notebooks]
	  * Submit Job
	      [Spark submit]
		  
2.  Spark Distributed Processing Model [Master-Slave]	
        
	   ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_ecosystem.jpg?raw=true)		
       
      *  In Spark Terminology Master -> Driver  && Slave ->Executor

      *  Spark Engine going to ask for a container from the underline cluster manager [YARN] to start driver process 
	  
	  *  The driver is again going to ask some more containers to start the executors process. This happen for each application 
      	  
			  
		 ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_distrubuted_processing_model.jpg?raw=true)	  


3.  Spark Execution 