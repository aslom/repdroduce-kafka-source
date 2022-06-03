# repdroduce-kafka-source


Reproducing test setup for https://github.com/knative-sandbox/eventing-kafka-broker/issues/2240

Required:
*  Strimzi https://strimzi.io/
* ko CLI https://github.com/google/ko - make sure to configure `export KO_DOCKER_REPO=...`
To run do
* knative eventing Kafka source https://github.com/knative-sandbox/eventing-kafka-broker/


To run scenario as provided:

```
ko apply -f scenario1
```

TO modify scenario copy `scenario1` folder and modify it.
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

