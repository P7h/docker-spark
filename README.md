# docker-spark 
[![](https://images.microbadger.com/badges/version/p7hb/docker-spark.svg)](http://microbadger.com/images/p7hb/docker-spark) ![](https://img.shields.io/docker/automated/p7hb/docker-spark.svg) [![Docker Pulls](https://img.shields.io/docker/pulls/p7hb/docker-spark.svg)](https://hub.docker.com/r/p7hb/docker-spark/) [![Size](https://images.microbadger.com/badges/image/p7hb/docker-spark.svg)](https://microbadger.com/images/p7hb/docker-spark) [![HitCount](https://hitt.herokuapp.com/P7h/docker-spark.svg)](https://github.com/P7h/docker-spark)

Dockerfiles for ***Apache Spark***.<br>
The image is available directly from [https://index.docker.io](https://hub.docker.com/u/p7hb/ "» Docker Hub").

This image contains the following softwares:

* OpenJDK 64-Bit v1.8.0_102
* Scala v2.11.8
* SBT v0.13.12
* Apache Spark v2.0.0 

## Get this image
There are 2 ways of getting this image:

1. Build this image using [`Dockerfile`](Dockerfile) OR
2. Pull the image directly from DockerHub.

### Build this image
Copy the [`Dockerfile`](Dockerfile) to a folder on your local machine and then invoke the following command.

    docker build -t p7hb/docker-spark .

### Pull the image

    docker pull p7hb/docker-spark


## Run the image

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark


The above step will launch and run the image with:

* `root` is the user we logged into.
 * `spark` is the container name.
 * `spark` is host name of this container. 
 	* This is very important as Spark Slaves are started using this host name as the master.
 * The container exposes ports 4040, 8080, 8081 for Spark Web UI console(s).

## Check softwares and versions

### Host name

    root@spark:~# hostname
    spark

### Java

    root@spark:~# java -version
    openjdk version "1.8.0_102"
    OpenJDK Runtime Environment (build 1.8.0_102-8u102-b14.1-1~bpo8+1-b14)
    OpenJDK 64-Bit Server VM (build 25.102-b14, mixed mode)

### Scala

    root@spark:~# scala -version
    Scala code runner version 2.11.8 -- Copyright 2002-2016, LAMP/EPFL

### SBT

Running `sbt about` will download and setup SBT on the image.

### Spark

```
root@spark:~# spark-shell
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.0.0
      /_/

Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_102)
Type in expressions to have them evaluated.
Type :help for more information.
Spark context available as sc.
SQL context available as sqlContext.

scala>
```

## Spark commands
All the required binaries have been added to the `PATH`.

### Start Spark Master

    start-master.sh

### Start Spark Slave

    start-slave.sh spark://spark:7077

### Execute Spark job for calculating `Pi` Value

    spark-submit --class org.apache.spark.examples.SparkPi --master spark://spark:7077 $SPARK_HOME/lib/spark-examples*.jar 100

OR even simpler

    $SPARK_HOME/bin/run-example SparkPi 100

Please note the first command above expects Spark Master and Slave to be running. And we can even check the Spark Web UI after executing this command. But with the second command, this is not possible.

### Start Spark Shell

    spark-shell --master spark://spark:7077

### View Spark Master WebUI console

[`http://192.168.99.100:8080/`](http://192.168.99.100:8080/)

### View Spark Worker WebUI console

[`http://192.168.99.100:8081/`](http://192.168.99.100:8081/)

### View Spark WebUI console
Only available for the duration of the application.

[`http://192.168.99.100:4040/`](http://192.168.99.100:4040/)

## Misc Docker commands

### Find IP Address of the Docker machine
This is the IP Address which needs to be used to look upto for all the exposed ports of our Docker container.

    docker-machine ip default

### Find all the running containers

    docker ps

### Find all the running and stopped containers

	docker ps -a

### Show running list of containers

	docker stats --all shows a running list of containers.

### Find IP Address of a specific container

    docker inspect <<Container_Name>> | grep IPAddress

### Open new terminal to a Docker container
We can open new terminal with new instance of container's shell with the following command.

    docker exec -it <<Container_ID>> /bin/bash #by Container ID

OR

    docker exec -it <<Container_Name>> /bin/bash #by Container Name


## Problems? Questions? Contributions? [![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](http://p7h.org/contact/)
If you find any issues or would like to discuss further, please ping me on my Twitter handle [@P7h](http://twitter.com/P7h "» @P7h") or drop me an [email](http://p7h.org/contact/ "» Contact me").


## License [![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)
Copyright &copy; 2016 Prashanth Babu.<br>
Licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).