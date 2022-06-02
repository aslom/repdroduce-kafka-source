# repdroduce-kafka-source


Reproducing test setup for https://github.com/knative-sandbox/eventing-kafka-broker/issues/2240

Required:
*  Strimzi https://strimzi.io/
* ko CLI https://github.com/google/ko - make sure to configure `export KO_DOCKER_REPO=...`
To run do
* knative eventing Kafka source https://github.com/knative-sandbox/eventing-kafka-broker/

Run 

```
ko apply -f scenario1
```

Copied lcoally KafkaScraper/KafkaScraper.go from https://github.com/steven0711dong/KafkaScraper and customizeEventDisplay/evendisplay.go from https://github.com/steven0711dong/customizeEventDisplay otherwise `ko://` works otherwise getting `error: no objects passed to apply Error: error processing import paths in "config1/300-kafkascraper.yaml": error resolving image references: found strict reference but ko://KafkaScraper is not a valid import path: importpath is not package main`

