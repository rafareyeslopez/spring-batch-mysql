# Spring Batch reading from MySQL a large dataset and publish to RabbitMQ

In this example will be shown how to read a large dataset from MySQL database table and publish items to a RabbitMQ instance.


## RabbitMQ

First of all lets start a RabbitMQ container using docker

    docker run -d  -p 5672:5672 -p 15672:15672 --name rabbit rabbitmq:management-alpine

Next lets start a MySQL container

    docker run --name mysql -e MYSQL_ROOT_PASSWORD=rootpass -e MYSQL_DATABASE=my_schema -e MYSQL_USER=user -e MYSQL_PASSWORD=pass -p 3306:3306 -d mysql
    
Now we have our environment ready.

In the startup of the project data is  loaded via the component *UserLoader*. It loads 10 million rows into our table.

There is a cron scheduled job running at certain time which executes the job. This job what is does is read the rows from the desired table and publish to a RabbitMQ queue.

To tune the performance the size of the chunk can be modified to satisfy the requirements. See: 




References:
[https://www.baeldung.com/spring-batch-start-stop-job](https://www.baeldung.com/spring-batch-start-stop-job)


