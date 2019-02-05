# IBM MQ Remote Queue connection Demo

#### This is demo application to show how to queue manager can exchange the messages using remote queue connection.

This Demo uses two Queue Managers EARTH (Running on QMS1 docker container) and MOON (Running on QMS2 docker container). There are remote MQ and Sender and recvr Channel defination from EARTH to MOON and vise versa.

## Requirement 
- Should have docker verion `Docker version 18.03.1-ce, build 9ee9f40` or higher.
- Should have docker-compose version `docker-compose version 1.13.0, build 1719ceb`  or higher
## Setup
### Clone the github repo 
 ```sh
 git clone git@github.com:amarm85/remote-mq-connection-demo.git
 ```
### CD to the folder where you downloaded the github repo and run
```sh
docker-compose up -d
```
### You will see two containers running.
```sh
docker ps

CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                            NAMES
0a6d40e31888        remoteqmdemo_mqs1     "runmqdevserver"         46 seconds ago      Up 43 seconds       0.0.0.0:1414->1414/tcp, 0.0.0.0:9443->9443/tcp   MQS1
30fa84e902cd        remoteqmdemo_mqs2     "runmqdevserver"         46 seconds ago      Up 44 seconds       0.0.0.0:1415->1414/tcp, 0.0.0.0:9444->9443/tcp   MQS2

```
### Get into MQS1 with bash and put some messages 
```sh
docker exec -ti MQS1 /bin/bash

(mq:9.0.5.0)root@0a6d40e31888:/# dspmq
QMNAME(EARTH)                                             STATUS(Running)
(mq:9.0.5.0)root@0a6d40e31888:/# amqsput RQ1.TO.MOON
Sample AMQSPUT0 start
target queue is RQ1.TO.MOON
hello mooners 
greetings from earth
```

### Start another terminal to get into MQS2 and get those messages
```sh
docker exec -ti MQS2 /bin/bash

(mq:9.0.5.0)root@30fa84e902cd:/# amqsget LQ1 
Sample AMQSGET0 start
message <hello mooners >
message <greetings from earth>

```
License
----

MIT

