

# Ingest App
##Problem
fetch the 50 most recent commits from the public github events api
publish each event as an individual message to a messaging system such as kafka or rabbitmq

This Project will fetch the recent events from Github and pushed them to kafka topic

### Start Zookeeper
- `bin/zookeeper-server-start.sh config/zookeeper.properties`

### Start Kafka Server
- `bin/kafka-server-start.sh config/server.properties`

### Create Kafka Topic
- `bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic eventmetrics`

After all the above steps, start the application. 
There is a scheduler job running for every 24 hours to 
fetch data from Github.
If you want to change the frequency of the scheduler, 
navigate to **Producer** class and try changing fixedRated value.
    `@Scheduled(fixedRate = 864000000)`
 
 ### Run the Application
 `mvn spring-boot:run`