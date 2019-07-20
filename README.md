# azure-databricks-cosmosdb-spark-blob-API
This is a general instruction to create Jobs in Databricks with Notebook which reads data from Azure, massages it and then saves result back to azure blob, exits with the blob path. It also includes the samples which calls Databricks API to run the jobs and get the job result (the blob path). Alternatively, in the notebook, you can save result to Databricks tables and exit with the result at the end as well.

1.	Dowload the latest azure-cosmosdb-spark connector from maven
  https://search.maven.org/artifact/com.microsoft.azure/azure-cosmosdb-spark_2.4.0_2.11/1.4.0/jar
            Choose uber.jar when download.

![image](https://user-images.githubusercontent.com/25307063/61577342-2306e380-aab4-11e9-9a2b-f49e9d0ef7ba.png)

2.	Create new Databricks workspace from Portal Azure and Launch Workspace

![image](https://user-images.githubusercontent.com/25307063/61577370-78db8b80-aab4-11e9-974b-bf4fcc6a05d9.png)


3.	Create new Cluster in databricks workspace

![image](https://user-images.githubusercontent.com/25307063/61577384-97da1d80-aab4-11e9-9477-e76017611dd0.png)


4.	Navigate to Libraries and install azure-cosmosdb-spark connector

![image](https://user-images.githubusercontent.com/25307063/61577394-af190b00-aab4-11e9-9866-82fb4dbe940e.png)

5.	Create new Notebook in Workspace

![image](https://user-images.githubusercontent.com/25307063/61577402-c7892580-aab4-11e9-9897-0b24aa36b158.png)

6.	Attach the notebook to cluster created at step 3.

7.	Write notebook and run test:

a)	For how to read data from CosmosDB:
https://github.com/Azure/azure-cosmosdb-spark

b)	For Spark programming:
https://spark.apache.org/docs/latest/sql-programming-guide.html

c)	For Aggregations examples using Apache Spark and Azure Cosmos DB together:
https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples

d)	For how to write data from Databricks to Azure Blob
https://gist.github.com/Zifah/ba0c3771069a11ba53969b000b038b82


8.	Create a Job on the notebook and cluster

![image](https://user-images.githubusercontent.com/25307063/61577425-07500d00-aab5-11e9-9253-0a1f3e36bf44.png)


9.	Run the Job to check any errors

![image](https://user-images.githubusercontent.com/25307063/61577429-1fc02780-aab5-11e9-8a60-90c26ae2112a.png)


10.	Click Last Run to see the details of result

![image](https://user-images.githubusercontent.com/25307063/61577439-349cbb00-aab5-11e9-8ae7-d51faca7160f.png)

11.	In Databricks, go to User Settings to generate New Token for Rest API

![image](https://user-images.githubusercontent.com/25307063/61577445-4716f480-aab5-11e9-9bbb-1345f450f7c9.png)


12.	 Save the Token displayed in the Popup as you never see it again in Databricks

![image](https://user-images.githubusercontent.com/25307063/61577449-6c0b6780-aab5-11e9-8cc3-9fb4edf0b728.png)

13.	 For details of Rest Jobs API:

https://docs.azuredatabricks.net/api/latest/jobs.html

Here we only use Run Now and Runs Get Output:

a)	https://docs.azuredatabricks.net/api/latest/jobs.html#run-now

b)	https://docs.azuredatabricks.net/api/latest/jobs.html#runs-get-output


14.	API Examples using Postman:


a)	Run the job created in step 8, which pass the job_id and the parameters for Notebook. 

![image](https://user-images.githubusercontent.com/25307063/61579151-82262180-aacf-11e9-9e47-b42676a35fb2.png)


  It returns the run_id if the job starts successfully.

![image](https://user-images.githubusercontent.com/25307063/61577489-e6d48280-aab5-11e9-9f50-00ddc988594d.png)


b)	Call get-output  Api to get Output of the job. This is a get request with the run_id which is returned from the above step.

![image](https://user-images.githubusercontent.com/25307063/61579169-b6014700-aacf-11e9-9a6f-48e27549f8a0.png)

The  return result contains state object, which need checks. Get the “notebook_output” when the "life_cycle_state": "TERMINATE” and  "result_state": "SUCCESS". The value of “notebook_output” depends on the notebook exit.
