# repdroduce-kafka-source

Reproducing test setup for https://github.com/knative-sandbox/eventing-kafka-broker/issues/2240

Required:
*  Strimzi https://strimzi.io/ (Strimzi setup used is described later if you want to reproduce it)
* ko CLI https://github.com/google/ko - make sure to configure `export KO_DOCKER_REPO=...`
To run do
* knative eventing Kafka source https://github.com/knative-sandbox/eventing-kafka-broker/


To run scenario as provided:

```
ko apply -f scenario1
```

TO run scenario again make sure to delete previous job:

```
 kubectl delete job scenario1-kafkaproduce-job1
```

THen you can run `ko apply` again and see new results.

To modify scenario copy `scenario1` folder and modify it.
In particular edit `scenario2/600-kafkaproducer-job.yaml` to set your workload parameters. You may also want to modify

Run

```
cp -r scenario1 scenario2
ko apply -f scenario2
```

## Running workload from CLI

If you make Strimzi Kafka available wih external endpoint you can eun

```
export BROKERS=my-cluster-kafka-bootstrap-kafka.o7-111a9c...appdomain.cloud:443

TOPIC=topic30 EVENTCT=1 go run ./KafkaProducer
````

## NOTES

Copied lcoally KafkaScraper/KafkaScraper.go from https://github.com/steven0711dong/KafkaScraper and customizeEventDisplay/evendisplay.go from https://github.com/steven0711dong/customizeEventDisplay otherwise `ko://` works otherwise getting `error: no objects passed to apply Error: error processing import paths in "config1/300-kafkascraper.yaml": error resolving image references: found strict reference but ko://KafkaScraper is not a valid import path: importpath is not package main`


## Strimzi setup

Install Strimzi ephemeral

https://strimzi.io/quickstarts/minikube/

https://github.com/aslom/knative-kafka-notes/blob/master/ibm-event-streams/StrimziIKS.md

```
kubectl create namespace kafka

kubectl apply -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka

kubectl get pod -n kafka --watch

kubectl logs deployment/strimzi-cluster-operator -n kafka -f
```

And create cluster


```
kubectl apply -f strimzi/my-cluster-ephemeral-triple-with-route.yaml

```

