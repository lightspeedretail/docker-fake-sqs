# ElasticMQ-Docker

Containerized [ElasticMQ](https://github.com/adamw/elasticmq)
Used for dev environments that [integrate with AWS SQS](http://labs.encoded.io/2013/02/03/testing-amazon-sqs-locally-with-elasticmq/)


## Basic usage

```
docker run -p "9324:9324" lightspeedretail/fake-sqs
```

By default, it creates a queue named "default" and with that command you will be able to access it at 
http://localhost:9324/queue/default

You can edit following environment variale to configure your queue :

* BRIDGE_HOST : Defaults to your container ip 
* QUEUE_NAME  : The name of the queue, defaults to "default"
* QUEUE_DEFAULT_VISIBILITY_TIMEOUT : (In seconds) Defaults to 10
* QUEUE_DELAY : (In seconds) Defaults to 5 seconds
* QUEUE_RECEIVE_MESSAGE_WAIT : (In seconds)

So to change the name of the queue to "myCustomName"

```
docker run -p "9324:9324" -e QUEUE_NAME=myCustomName lightspeedretail/fake-sqs
```


## Advance Usage

If you want to have more than on queues or want to change other setting, 
you can alternately provide it with the full config for elasticmq, like this :
```
docker run -p "9324:9324" lightspeedretail/fake-sqs $(< /path/to/my/config)
```

Tips: 
* Looks at the output of the logs of the container when it starts to see config it runs by default. 
* You can use either `localhost` or the name your container for the host. (In the logs you will se the ip of the container that you cant know in advance)
  

### Forked.

This is a fork from [behance/elasticmq-docker](https://github.com/behance/elasticmq-docker)
 
What we changed.
* Use Alpine as a base ditro to reduce the size
* Used version 0.10.0 of elasticmq
* Fixed it so you can kill it with ctrl+c
* Added a default queue.
* Added the ability to pass a config file
* added the ability to configure thre default queue