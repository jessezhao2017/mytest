Start the containers:

1) export DOCKER_KAFKA_HOST=$(ipconfig getifaddr en0)
2) docker-compose up -d kafka

Create a topic:
docker exec  kafka  kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic test

Produce messages:
docker exec -it kafka /opt/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --top
ic test

Receive messages:
docker exec  kafka opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-
beginning --topic test


Run application in Mac, for instance, in python:

pip install kafka-python
 
Run python terminal
>>>from kafka import KafkaConsumer
>>>consumer = KafkaConsumer('test', bootstrap_servers='192.168.2.191:19092')  
    // please replace 192.168.2.191 with $DOCKER_KAFKA_HOST
>>>for msg in consumer: print msg
… Enter return key here

For more examples,please refer: http://kafka-python.readthedocs.io/en/master/usage.html


