 ## PySpark en AWS EMR

# Apache Spark for a Machine Learning Engineer

This git repo is a collection of introductory tutorials and code samples on
Apache Spark. The code samples are in python, so essentially we are using pySpark.

The goal is to

- Build expertise in Spark Dataframe
- Read/Write from/to AWS S3
- Apply Feature Engineering on the data read from AWS S3 on Spark
- Write features back to AWS S3
- Learn to use AWS EMR to execute all the above steps
- Be familiar with Spark MLLib
- Be familiar with Spark Structured Streaming with Kafka

### Tools used:
- Apache Spark 2.4 with pySpark
- AWS S3 for data storage
- AWS EMR (Elastic Map Reduce)
- Spark Dataframe
- Spark MLLib (low priority)
- Spark Structured Streaming with Kafka

## Reference

### Spark Structured Streaming with Kafka
Please follow this [Databricks tutorial](https://databricks.com/blog/2017/04/04/real-time-end-to-end-integration-with-apache-kafka-in-apache-sparks-structured-streaming.html) if you are interested in Spark
Structured Streaming with Kafka. Although the tutorial is written in Scala, you
can easily do it in python if you have completed the above steps in python.

### Install python dependencies :

Create requirements.txt file with all depencies and upload to S3 Bucket.


Create depencies.sh file :
```
#!/bin/bash
sudo pip-3.4 install -r https://s3.amazonaws.com/bucket/requirements.txt
``` 

Use EMR’s bootstrap


### Configure EMR with python :

Create configuration.js
```
[
    {
        "Classification": "spark-env",
        "Properties": {},
        "Configurations": [
            {
                "Classification": "export",
                "Properties": {
                    "PYSPARK_PYTHON": "python34"
                },
                "Configurations": []
            }
        ]
    }
]
``` 



### Create cluster with configuration 

Example : 
```
aws emr create-cluster [..config..] --region eu-central-1 --configurations file://configurations.json --bootstrap-action Path="s3://bucket/dependencies.sh"
``` 


### Add step : 

![alt text](https://i1.wp.com/blog.sqreen.io/wp-content/uploads/2017/05/word-image-4.png)


### Acces log 

Go SSH on instance : 
```
ssh -i xxxp.em hadoop@xxxxxx.eu-central-1.compute.amazonaws.com
``` 


Display logs :
```
yarn logs -applicationId <applicationID>
``` 



