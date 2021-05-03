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

3.  Spark Execution Modes
      
	  * Client Mode - [Spark Shell and Notesbooks]
	    
		  - Driver process runs locally in your client machine, However driver will still connect to YARN to start executors, and get back the results.
		  
		  - if we quit or logoff the client , driver dies inturn executors dies to 
	  
	      ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_client_mode.jpg?raw=true)	  
	  
	  * Cluster Mode 
	  
	      ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_cluster_mode.jpg?raw=true)	

3.  Spark Cluster Managers
     
	  *  local[n]   --> [IDE]
	       -  n = no of threads
		   
		   ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_local.jpg?raw=true)
           		   
	    
	  * YARN
	  * K8S
	  * MESOS
	  * Standalone