# globant_challenge
The main objective of this project is to solve a problem for a professional challenge proposed by a global company. Which consists mainly in a data migration, where the source will be CSV files and its final destination will be a SQL database (in this case I chose the MySQL engine because AWS has a free tier version for it).

The first part of the challenge consists of sending the files in batches (with the possibility to do it from 1 to 1000), then performing the validations for each .csv file, writing the transactions (batches) that meet all the conditions in the database. If they do not meet the conditions, a log will be written with the batch information. For my part, I have decided to create a final log to see a summary of the behavior of all batches. On the other hand, we have to create a feature to make a backup in AVRO format and later another feature to be able to restore it.

The second part consists of creating two endpoints to be able to consult two reports that are requested and then create a BI dashboard.



***Solution***

I decided to create the following architecture, which uses 100% cloud services. First, the files are uploaded to s3, then an object creation notification is generated in s3 and this notification triggers a lambda that will start sending the data by batches to the REST API created in API Gateway. The requests made to the API will be the same amount of batches that come out after defining the batch size. The endpoint containing the /migrate method was defined for this task.

Later this API will fire lambda functions that will do the validations of each batch (1 lambda for 1 batch). If the validations are correct, then the lambda will write to the database. On the contrary, if they are incorrect, the lambda will write in S3 a log with the batch and its respective errors. In the end, the initial lambda will create a history log with the responses of all the lambdas generated by the API.


![image](https://github.com/user-attachments/assets/174b5471-9d47-46f2-8d7e-06cfd8dbdf02)

Next, the idea was to create the endpoints to connect Power BI to the MYSQL moto and create a bar chart and a dynamic table for the reports requested by the business.
