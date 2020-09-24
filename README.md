# BigData

# Background 

StopFire is a campaign started  to predict and stop the fire in Victorian cities. They have employed sensors in different cities of Victoria and have collected a large amount of data. The data is so big that their techniques have failed to provide the results on time to predict fire. They have hired us as the data analyst to migrate their data to the NoSQL database (MongoDB). They want us to analyse their data and provide them with results. In addition, they want us to build an application, a complete setup from streaming to storing and analyzing the data for them using Apache Kafka, Apache Spark Streaming and MongoDB. 

Datasets we have:
● Five datasets: 
<br/>
○ hotspot_historic.csv 
<br/>
○ climate_historic.csv 
<br/>
○ hotspot_AQUA_streaming.csv 
<br/>
○ hotspot_TERRA_streaming.csv 
<br/>
○ climate_streaming.csv 
<br/>
Information on Dataset 
<br/>
Climate data is recorded on a daily basis whereas Fire data is recorded based on the occurrence of a fire on a particular day. Therefore, for one climate data, there can be zero or many fire data. The data is NOT row per weather station basis. You can simply think of it as, Station 1 was reporting data for X number of days and then Station 2 started reporting data because Station 1 was shut down for instance. 
Total precipitation (rain and/or melted snow) reported during the day in inches and hundredths; will usually not end with the midnight observation --i.e., may include latter part of the previous day. 
.00 indicates no measurable precipitation (includes a trace). Missing = 99.99 (For metric version, units = millimeters to tenths & missing = 999.9.) 
Note: Many stations do not report '0' on days with no precipitation --therefore, '99.99' will often appear on these days. Also, for example, a station may only report a 6-hour amount for the period during which rain fell. See Flag field information below the source of data. 
<br/>
● A = 1 report of 6-hour precipitation amount. 
<br/>
● B = Summation of 2 reports of 6-hour precipitation amount. 
<br/>
● C = Summation of 3 reports of 6-hour precipitation amount. 
<br/>
● D = Summation of 4 reports of 6-hour precipitation amount. 
<br/>
● E = 1 report of 12-hour precipitation amount. 
<br/>
● F = Summation of 2 reports of 12-hour precipitation amount. 
<br/>
● G = 1 report of 24-hour precipitation amount. 
<br/>
● H = Station reported '0' as the amount for the day (eg, from 6-hour reports), but also reported at least one the occurrence of precipitation in hourly observations --this could indicate a trace occurred but should be considered as incomplete data for the day. 
<br/>
● I = Station did not report any precipitation data for the day and did not report any occurrences of precipitation in its hourly observations --it's still possible that precipitation occurred but was not reported. 
<br/>
Programming Tasks 
<br/>
Task A. MongoDB Data Model 
<br/>
1. Based on the two data sets provided i.e. hotspot_historic.csv and climate_historic.csv, design a suitable data model to support the efficient querying of the two data sets in MongoDB. Justify your data model design. The output of this task should be 
- An example of the data model - The justification for choosing that data model 
<br/>
Task B. Querying MongoDB using PyMongo 
<br/>
1. Write a python program that will read the data from hotspot_historic.csv and climate_historic.csv and load them to the new database (e.g. fit5148_assignment_db). The collection(s) in fit5148_assignment_db will be 
based on the document model you have designed in Task A1. Please DO NOT use mongo aggregation query to do this task. 
<br/>
2. Write queries to answer the following tasks on fit5148_assignment_db and corresponding collection(s). You need to write the queries as a python program using the pymongo library in Jupyter Notebook. 
<br/>
a. Find climate data on 10th December 2017.
<br/>
b. Find the latitude, longitude, surface temperature (°C), and confidence when the surface temperature (°C) was between 65 °C and 100 °C. 
<br/>
c. Find date, surface temperature (°C), air temperature (°C), relative humidity and 
max wind speed on 15th and 16th of December 2017. 
<br/>
d. Find datetime, air temperature (°C), surface temperature (°C) and confidence when the confidence is between 80 and 100. 
<br/>
e. Find the top 10 records with the highest surface temperature (°C). 
<br/>
f. Find the number of fire in each day. You are required to only display the 
total number of fire and the date in the output. 
<br/>
g. Find the average surface temperature (°C) for each day. You are required to only display average surface temperature (°C) and the date in the output. 
Combine all your answers for Task A and Task B into a single Jupyter Notebook file called Assignment_TaskA_B.ipynb. 
<br/>
Task C. Processing Data Stream 
<br/>
In this task, we will implement multiple Apache Kafka producers to simulate the real-time streaming of the data which will be processed by Apache Spark Streaming client and then inserted into MongoDB.
<br/>
1.Simulating real time data using Apache Kafka producers
<br/>
a. Event Producer 
<br/>
1: Write a python program that loads all the data from climate_streaming.csv and randomly feed the data to the stream every 5 seconds. You will need to append additional information such as sender_id and created_time. Save the file as Assignment_TaskC_Producer1.ipynb. 
<br/>b. Event Producer
<br/>2: Write a python program that loads all the data from hotspot_AQUA_streaming.csv and randomly feed the data to the stream every 10 - 30 seconds. AQUA is the satellite from NASA that reports latitude, longitude, confidence and surface temperature of a location. You will need to append additional information such as sender_id and created_time. Save the file as Assignment_TaskC_Producer2.ipynb. 
<br/>c. Event Producer 
<br/>3: Write a python program that loads all the data from hotspot_TERRA_streaming.csv and randomly feed the data to the stream every 10 - 30 seconds. TERRA is another satellite from NASA that reports latitude, longitude, confidence and surface temperature of a location. You will need to append additional information such as sender_id and created_time. Save the file as Assignment_TaskC_Producer3.ipynb. 2. Stream Processing using Apache Spark Streaming. 
a. Streaming Application: Write a streaming application in Apache Spark Streaming which has a local streaming context with two execution threads and a batch interval of 10 seconds. The streaming application will receive streaming data from all three producers. If the streaming application has data from all or at least two of the producers, do the processing as follows: - Join the streams based on the location (i,e, latitude and longitude) 
and create the data model developed in Task A. - Find if two locations are close to each other or not. You can do this by implementing the geo-hashing algorithm or find the library that does the job for you. Use precision 5. The precision determines the number of characters in the Geohash. 
