[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/_lZVuyYO)
# Homework Assignment 3

Submission Deadline: March 27, 2024

This assignment comprises two parts. This is an individual assignment to be conducted individually by each student.

## Part 1: Implement Hotel Map Microservices

In this part, you will implement the microservices for the Hotel Map application. We provide you with a partial implementation that you can use as a starting point. You can find the code in the directory `hotelapp`. The parts you need to fill in are marked with `TODO` comments. 

You should establish that your web app is running correctly. You can test your application by sending to it search queries through the web interface, for example, using your web browser or the `curl` utility, as described in the [lab notes](https://github.com/ucy-coast/cs452-sp24/blob/main/labs/06-hotelapp/README.md#testing).

## Part 2: Evaluate Hotel Map Microservices

In this part, you will conduct a characterization and analysis of the Hotel Map microservices. You can use either your microservices container images (from part 1) or the ones available from DockerHub. You should evaluate how throughput and latency performance scales with increasing number of nodes (machines) and service instances.

You will use the [wrk2](https://github.com/giltene/wrk2) HTTP benchmarking tool described in the [lab notes](https://github.com/ucy-coast/cs452-sp24/blob/main/labs/06-hotelapp/README.md#benchmarking). You can find the code for `wrk2` in the directory `hotelapp/wrk2`.

### Single node

Use [Docker Compose](https://docs.docker.com/compose/) to deploy the [monolithic implementation](https://github.com/ucy-coast/cs452-sp24/tree/main/labs/06-hotelapp#deploying-web-applications-with-docker) and the microservices-based implementation on a single machine.

Evaluate the throughput and latency performance of the monolithic and microservices-based implementations when deployed on a single machine.

Using jaeger, [trace the RPC call chains](https://github.com/ucy-coast/cs452-sp24/tree/main/labs/07-microservices#tracing-requests) and identify any bottlenecks. 

### Multiple nodes

Use [Docker Swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/) to deploy the microservices-based implementation on multiple machines. Deploy each microservice on a separate machine.

Evaluate the throughput and latency performance of the microservices-based implementation when deployed on multiple machines. Compare its performance to that of the monolithic implementation and the microservices-based implementations when deployed on a single machine.

Using jaeger, [trace the RPC call chains](https://github.com/ucy-coast/cs452-sp24/tree/main/labs/07-microservices#tracing-requests) and identify any bottlenecks. 

### Hints:

There are a few notable things that need to happen in your `docker-compose.yml` file.

#### Let your containers grow

Make sure you remove any `container_name` from a service you want to scale, otherwise you will get a warning.

This is important because docker will need to name your containers individually when you want to have more than one of them running.

#### Don’t port clash

We need to make sure that if you are mapping ports, you use the correct format. The standard host port mapping in short syntax is `HOST:CONTAINER` which will lead to port clashes when you attempt to spin up more than one container. We will use ephemeral host ports instead.

Instead of:

```
   ports:
     - "8081:8081"
```

Do this:

```
   ports:
     - "8081"
```     

Doing it this way, Docker will auto-”magic”-ly grab unused ports from the host to map to the container and you won’t know what these are ahead of time. You can see what they ended up being after you bring your service up.

#### Bring it up

To scale the service with [Docker Swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/scale-service/), you run the following command:

```
docker service scale profile=3
```

To scale the service with Docker Compose, you need to pass an additional argument `--scale <serviceName>:<number of instances>`.

```
docker-compose up --scale profile=3
```

### Submission

Now you need to submit your assignment. Commit your change and push it to the remote repository by doing the following:

```
$ git commit -am "[you fill me in]"
$ git push -u origin main
```

You may push you code as many times you like, grading and submission time will be based on your last push.
# hw3
# hw3
