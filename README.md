# docker-spark
[![](https://images.microbadger.com/badges/version/p7hb/docker-spark.svg)](http://microbadger.com/images/p7hb/docker-spark) ![](https://img.shields.io/docker/automated/p7hb/docker-spark.svg) [![Docker Pulls](https://img.shields.io/docker/pulls/p7hb/docker-spark.svg)](https://hub.docker.com/r/p7hb/docker-spark/) [![Size](https://images.microbadger.com/badges/image/p7hb/docker-spark.svg)](https://microbadger.com/images/p7hb/docker-spark)

Dockerfiles for ***Apache Spark***.<br>
Apache Spark Docker image is available directly from [https://index.docker.io](https://hub.docker.com/u/p7hb/ "» Docker Hub").

This image contains the following softwares:

* OpenJDK 64-Bit v1.8.0_131
* Scala v2.12.2
* SBT v0.13.15
* Apache Spark v2.2.0


## Various versions of Spark Images
Depending on the version of the Spark Image you want, please run the corresponding command.<br>
Latest image is always the most recent version of Apache Spark available. As of 11th July, 2017 it is v2.2.0.

### Apache Spark latest [i.e. v2.2.0]
[Dockerfile for Apache Spark v2.2.0](https://github.com/P7h/docker-spark)

    docker pull p7hb/docker-spark

### Apache Spark v2.2.0
[Dockerfile for Apache Spark v2.2.0](https://github.com/P7h/docker-spark/tree/2.2.0)

    docker pull p7hb/docker-spark:2.2.0

### Apache Spark v2.1.1
[Dockerfile for Apache Spark v2.1.1](https://github.com/P7h/docker-spark/tree/2.1.1)

    docker pull p7hb/docker-spark:2.1.1

### Apache Spark v2.1.0
[Dockerfile for Apache Spark v2.1.0](https://github.com/P7h/docker-spark/tree/2.1.0)

    docker pull p7hb/docker-spark:2.1.0

### Apache Spark v2.0.2
[Dockerfile for Apache Spark v2.0.2](https://github.com/P7h/docker-spark/tree/2.0.2)

    docker pull p7hb/docker-spark:2.0.2

### Apache Spark v2.0.1
[Dockerfile for Apache Spark v2.0.1](https://github.com/P7h/docker-spark/tree/2.0.1)

    docker pull p7hb/docker-spark:2.0.1

### Apache Spark v2.0.0
[Dockerfile for Apache Spark v2.0.0](https://github.com/P7h/docker-spark/tree/2.0.0)

    docker pull p7hb/docker-spark:2.0.0

### Apache Spark v1.6.3
[Dockerfile for Apache Spark v1.6.3](https://github.com/P7h/docker-spark/tree/1.6.3)

    docker pull p7hb/docker-spark:1.6.3

### Apache Spark v1.6.2
[Dockerfile for Apache Spark v1.6.2](https://github.com/P7h/docker-spark/tree/1.6.2)

	docker pull p7hb/docker-spark:1.6.2


## Get the latest image
There are 2 ways of getting this image:

1. Build this image using [`Dockerfile`](Dockerfile) OR
2. Pull the image directly from DockerHub.

### Build the latest image
Copy the [`Dockerfile`](Dockerfile) to a folder on your local machine and then invoke the following command.

    docker build -t p7hb/docker-spark .

### Pull the latest image

    docker pull p7hb/docker-spark


## Run Spark image
### Run the latest image i.e. Apache Spark `2.2.0`
Spark latest version as on 11th July, 2017 is `2.2.0`.  So, `:latest` or `2.2.0` both refer to the same image.

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark

### Run images of previous versions
Other Spark image versions of this repository can be booted by suffixing the image with the Spark version. It can have values of `2.2.0`, `2.1.1`, `2.1.0`, `2.0.2`, `2.0.1`, `2.0.0`, `1.6.3` and `1.6.2`.

#### Apache Spark latest [i.e. v2.2.0]

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:2.2.0

#### Apache Spark v2.1.1

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:2.1.1

#### Apache Spark v2.1.0

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:2.1.0

#### Apache Spark v2.0.2

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:2.0.2

#### Apache Spark v2.0.1

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:2.0.1

#### Apache Spark v2.0.0

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:2.0.0

#### Apache Spark v1.6.3

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:1.6.3

#### Apache Spark v1.6.2

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark p7hb/docker-spark:1.6.2

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
    openjdk version "1.8.0_131"
    OpenJDK Runtime Environment (build 1.8.0_111-8u131-b11-2~bpo8+1-b11)
    OpenJDK 64-Bit Server VM (build 25.131-b11, mixed mode)

### Scala

    root@spark:~# scala -version
    Scala code runner version 2.12.2 -- Copyright 2002-2017, LAMP/EPFL and Lightbend, Inc.

### SBT

Running `sbt about` will download and setup SBT on the image.

### Spark

```
root@spark:~# spark-shell
Spark context Web UI available at http://172.17.0.2:4040
Spark context available as 'sc' (master = local[*], app id = local-1483032227786).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.1.1
      /_/

Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_111)
Type in expressions to have them evaluated.
Type :help for more information.

scala>
```

## Spark commands
All the required binaries have been added to the `PATH`.

### Start Spark Master

    start-master.sh

### Start Spark Slave

    start-slave.sh spark://spark:7077

### Execute Spark job for calculating `Pi` Value

    spark-submit --class org.apache.spark.examples.SparkPi --master spark://spark:7077 $SPARK_HOME/examples/jars/spark-examples*.jar 100
    .......
    .......
    Pi is roughly 3.140495114049511


OR even simpler

    $SPARK_HOME/bin/run-example SparkPi 100
    .......
    .......
    Pi is roughly 3.1413855141385514

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