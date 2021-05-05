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
	  
	  * Cluster Mode - Refer [2]
	  
	      ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_cluster_mode.jpg?raw=true)	

4.  Spark Cluster Managers And Most Common Spark Execution Models 
     
	  *  local[n]   --> [IDE]
	       -  n = no of threads
		   
		   ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_local.jpg?raw=true)
           		   
	    
	  *   YARN
	  *   K8S
	  *   MESOS
	  *   Standalone
	  
# Most Common Spark Execution Models 
    
![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/most_common_spark_execution_models.jpg?raw=true)

# Spark Shell -> Cluster Manager [local[n]] + Execution Mode [Client]
    
1.  Command Sample	

      ```
	  open spark-shell 
	  
      spark-shell --master local[3]  --driver-memory 2G 
	  
	  ```
	  
	  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_shell_cm_local_em_client1.jpg?raw=true)

2.  Spark Context     
      
	  ```
	  1. In local cluster every thing is handled by driver. every thing run in single JVM.
      2. Event timeline shows one executor driver. (figure 1)
      3. Figure 2 shows one driver with3 cores (3 threads)	  
	  ```
	  
	  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_shell_cm_local_em_client2.jpg?raw=true)
      ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_shell_cm_local_em_client3.jpg?raw=true)
    

# Setting up Spark Cluster - Google Dataproc 

Navigate Google Dataproc >>> Cluster >>> Create Cluster >>> GiveName 
	    
  * Config driver and executor 
		    
	![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/google_proc_1.jpg?raw=true)
		  
  * Config spark version to 2.4 [Advanced Options]
		  
	![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/google_proc_2.jpg?raw=true)
		  
  * Other Components  [ pyspark , notebooks]
		  
	![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/google_proc_3.jpg?raw=true)
		  
  * Config Storage Bucket
		  
	![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/google_proc_4.jpg?raw=true)
		  
  * Enable scheduled deletion
		      
	![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/google_proc_5.jpg?raw=true)
		  
  * Create
		     
	![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/google_proc_6.jpg?raw=true)
		  
  * Delete 
		     
	![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/google_proc_7.jpg?raw=true)
    

# Spark Shell -> Cluster Manager [YARN] + Execution Mode [Client]


1.  Command Sample
    
      ```
	  ssh into master 
	  
      spark-shell --master yarn  --driver-memory 1G --executor-memory 500M --num-executors 2 ~--executor-core 1
	  ```
	  
	 ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_shell_cm_yarm_em_client.jpg?raw=true)

2.  History Server	& Spark Context

	  ```
	  History Server
	  **************
	  1. Shows list of application executed in past + current running application.
	  2. From history server click on application id , we can navigate to spark context
	  ```
		 
      ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_shell_spark_history_server_cm_yarn_plus_em_client.jpg?raw=true)
		 
      ```
	  Spark Context - [1 driver + 2 executor ] 
	  ****************************************
	  1. YARN dynamic allocation policy is to release the resource when not doing anything. So one executor is released.
	  ```
	     
      ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_shell_spark_context_cm_yarn_plus_em_client.jpg?raw=true)
    
    

#   Spark Submit -> Cluster Manager [YARN] + Execution Mode [Cluster]

1.  Command Sample

      ```
	  ssh into master 
	  
	  copy/upload sample project from spark.
	  
	  scala ? 
	  spark-submit --master yarn  --deploy-mode cluster --class org.apache.spark.examples.SparkPi spark-examples_2.11-2.4.5.jar 100 
	  
	  python ?
	  spark-submit --master yarn  --deploy-mode cluster pi.py 100 
	  
	  Watch below figures: 
	  1. spark submit command and output
	  2. spark context from spark history server
	  ```
	  
	  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_submit1.jpg?raw=true)
	  
	  ![alt text](https://github.com/IAmZero247/spark-setup/blob/main/repo_images/spark_submit2.jpg?raw=true)
