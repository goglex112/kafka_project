# Realtime Data Processing using Apache Kafka in Confluent and Spark Streaming

## 1. Set up Confluent Account
  - Create free Confluent account
  - Create cluster
  - After that grab this information: bootstrap.servers, security.protocol, sasl.username, sasl.password
  - Copy and paste that information to this file credentials.ini 

## 2. Set up Docker Container
  - Create Image for the container:** docker build -t kafka_project .**
  - Create the container: **docker run -it -d --name kafka_project_container kafka_project**
  - After that the container should be running and ready to use
    ![image](https://github.com/goglex112/kafka_project/assets/92841420/cd5901b0-da0f-4831-8666-c72d0b8fff4b)
  - After that we can enter our container using this command: **docker exec -it kafka_project_container bash**

## 3. Creating Topics
  - Create topic using this command, for this project we need 2 topic, therefore you should one topic for raw-data and one topic for clean-data.
    **docker exec -it kafka_project_container python /project/run_topic.py /project/credentials.ini <your-topic-name>**
    ![image](https://github.com/goglex112/kafka_project/assets/92841420/aa58a444-8041-4124-82d7-d56311429d11)
    We can check our topic we just created in Confluent.

## 4. After that we can run our code inside our container to push data using Kafka
  - **docker exec -it kafka_project_container python /project/hands-on/push_kafka.py /project/credentials.ini ronald-data-raw**
    ![image](https://github.com/goglex112/kafka_project/assets/92841420/fb07f3ff-608f-41b0-a2ef-5bd4c1d2aae8)
  - We can check if our data is streaming using this command: **docker exec -it kafka_project_container python /project/run_consumer.py /project/credentials.ini ronald-data-raw**

# 5. Next we will try to use Spark for transforming data on the fly:
  - We can run this command: **sudo docker exec -it kafka_project_container spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.0.3 /project/hands-on/clean_data.py**
  - To check if our data is streaming we can use this command: **sudo docker exec -it kafka_project_container python /project/run_consumer.py /project/credentials.ini ronald-data-clean**
  - Next we can open confluent to see our data
    ![image](https://github.com/goglex112/kafka_project/assets/92841420/11563f7b-8f21-4f33-b344-465f7f4ad898)
