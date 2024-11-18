# globant_challenge
The main objective of this project is to solve a problem for a professional challenge proposed by a global company. Which consists mainly in a data migration, where the source will be CSV files and its final destination will be a SQL database (in this case I chose the MySQL engine because AWS has a free tier version for it).

The first part of the challenge consists of sending the files in batches (with the possibility to do it from 1 to 1000), then performing the validations for each .csv file, writing the transactions (batches) that meet all the conditions in the database. If they do not meet the conditions, a log will be written with the batch information. For my part, I have decided to create a final log to see a summary of the behavior of all batches. On the other hand, we have to create a feature to make a backup in AVRO format and later another feature to be able to restore it.

The second part consists of creating two endpoints to be able to consult two reports that are requested and then create a BI dashboard.
