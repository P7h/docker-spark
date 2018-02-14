# docker-spark
[![](https://images.microbadger.com/badges/version/p7hb/docker-spark.svg)](http://microbadger.com/images/p7hb/docker-spark) ![](https://img.shields.io/docker/automated/p7hb/docker-spark.svg) [![Docker Pulls](https://img.shields.io/docker/pulls/p7hb/docker-spark.svg)](https://hub.docker.com/r/p7hb/docker-spark/) [![Size](https://images.microbadger.com/badges/image/p7hb/docker-spark.svg)](https://microbadger.com/images/p7hb/docker-spark)

This repo contains Dockerfiles for ***Apache Spark*** for running in *standalone* mode. Standalone mode is the easiest to set up and will provide almost all the same features as the other cluster managers if you are only running Spark. 

Apache Spark Docker image is available directly from [docker](https://hub.docker.com/u/p7hb/ "» Docker Hub").

# Quickstart
 - [Docker-Compose Start](#docker-compose-start)
 - [Manual Start](#manual-start)

## Docker Compose Start
Copy the [`docker-compose.yml`](docker-compose.yml) file and run the following command.

    docker-compose up

This should run a spark cluster on your host machine at `localhost:7077`. You can connect to it remotely
from any spark shell. A short pyspark example is provided below that will work with the juypter notebook
running at `localhost:8888`.


```
    from pyspark import SparkConf, SparkContext
    import random

    conf = SparkConf().setAppName('test').setMaster('spark://master:7077')
    sc = SparkContext(conf=conf)

    NUM_SAMPLES = 100000

    def inside(p):
        x, y = random.random(), random.random()
        return x*x + y*y < 1

    count = sc.parallelize(xrange(0, NUM_SAMPLES)) \
                 .filter(inside).count()
    print "Pi is roughly %f" % (4.0 * count / NUM_SAMPLES)
```

Be sure that your worker is using the desired amount of cores and memory. These can be set directly
in the [`docker-compose.yml`](docker-compose.yml) file.

    SPARK_WORKER_CORES: 4
    SPARK_WORKER_MEMORY: 2g


## Manual Start
### Step 1: Get the latest image
There are 2 ways of getting this image:

1. Build this image using [`Dockerfile`](Dockerfile) OR
2. Pull the image directly from DockerHub.

#### Build the latest image
Copy the [`Dockerfile`](Dockerfile) to a folder on your local machine and then invoke the following command.

    git clone https://github.com/Ouwen/docker-spark.git && cd docker-spark
    docker build -t p7hb/docker-spark .

#### Pull the latest image

    docker pull p7hb/docker-spark


### Step 2: Run Spark image
#### Run the latest image i.e. Apache Spark `2.2.0`
Spark latest version as on 11th July, 2017 is `2.2.0`.  So, `:latest` or `2.2.0` both refer to the same image.

    docker run -it -p 7077:7077 -p 4040:4040 -p 8080:8080 -p 8081:8081 p7hb/docker-spark

The above step will launch and run the bash shell into the latest image. We preset a couple ports for the following purposes:
 * `7077` is the port bind for spark master process
 * `8080` is the port bind for the spark master webui
 * `8081` is the port bind for the spark worker webui
 * `4040` is the port bind the spark 

### Sanity Check
All the required binaries have been added to the `PATH`. Run the following in a running container.

#### Start Spark Master

    start-master.sh

#### Start Spark Slave

    start-slave.sh spark://0.0.0.0:7077

#### Execute Spark job for calculating `Pi` Value

    spark-submit --class org.apache.spark.examples.SparkPi --master spark://0.0.0.0:7077 $SPARK_HOME/examples/jars/spark-examples*.jar 100
    .......
    .......
    Pi is roughly 3.140495114049511

#### Start Spark Shell

    spark-shell --master spark://0.0.0.0:7077

#### View Spark Master WebUI console

[`http://localhost:8080/`](http://localhost:8080/)

#### View Spark Worker WebUI console

[`http://localhost:8081/`](http://localhost:8081/)

#### View Spark WebUI console
Only available for the duration of the application.

[`http://localhost:4040/`](http://localhost:4040/)


# Further documentation
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


## Various versions of Spark Images
Depending on the version of the Spark Image you want, please run the corresponding command.<br>
Latest image is always the most recent version of Apache Spark available. As of 11th July, 2017 it is v2.2.0.

#### Apache Spark latest [i.e. v2.2.0]
[Dockerfile for Apache Spark v2.2.0](https://github.com/P7h/docker-spark)

    docker pull p7hb/docker-spark

#### Apache Spark v2.2.0
[Dockerfile for Apache Spark v2.2.0](https://github.com/P7h/docker-spark/tree/2.2.0)

    docker pull p7hb/docker-spark:2.2.0

#### Apache Spark v2.1.1
[Dockerfile for Apache Spark v2.1.1](https://github.com/P7h/docker-spark/tree/2.1.1)

    docker pull p7hb/docker-spark:2.1.1

#### Apache Spark v2.1.0
[Dockerfile for Apache Spark v2.1.0](https://github.com/P7h/docker-spark/tree/2.1.0)

    docker pull p7hb/docker-spark:2.1.0

#### Apache Spark v2.0.2
[Dockerfile for Apache Spark v2.0.2](https://github.com/P7h/docker-spark/tree/2.0.2)

    docker pull p7hb/docker-spark:2.0.2

#### Apache Spark v2.0.1
[Dockerfile for Apache Spark v2.0.1](https://github.com/P7h/docker-spark/tree/2.0.1)

    docker pull p7hb/docker-spark:2.0.1

#### Apache Spark v2.0.0
[Dockerfile for Apache Spark v2.0.0](https://github.com/P7h/docker-spark/tree/2.0.0)

    docker pull p7hb/docker-spark:2.0.0

#### Apache Spark v1.6.3
[Dockerfile for Apache Spark v1.6.3](https://github.com/P7h/docker-spark/tree/1.6.3)

    docker pull p7hb/docker-spark:1.6.3

#### Apache Spark v1.6.2
[Dockerfile for Apache Spark v1.6.2](https://github.com/P7h/docker-spark/tree/1.6.2)

    docker pull p7hb/docker-spark:1.6.2

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

## Check softwares and versions
This image contains the following softwares:
* OpenJDK 64-Bit v1.8.0_131
* Scala v2.12.2
* SBT v0.13.15
* Apache Spark v2.2.0

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

### Spark Scala

```
root@spark:~# spark-shell
Spark context Web UI available at http://localhost:4040
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

## Problems? Questions? Contributions? [![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](http://p7h.org/contact/)
If you find any issues or would like to discuss further, please ping me on my Twitter handle [@P7h](http://twitter.com/P7h "» @P7h") or drop me an [email](http://p7h.org/contact/ "» Contact me").


## License [![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)
Copyright &copy; 2016 Prashanth Babu.

Modified work Copyright &copy; 2018 Ouwen Huang.

Licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).