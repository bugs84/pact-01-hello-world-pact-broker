# CDC - Consumer Driven Contract tests - Usage example of pact.io for test
This is example how to use "Pact Broker" in your pact.io tests.

## Associated projects:
- https://github.com/bugs84/pact-01-hello-world-01-consumer
- https://github.com/bugs84/pact-01-hello-world-02-producer
- https://github.com/bugs84/pact-01-hello-world-pact-broker

# pact-01-hello-world-pact-broker
Hello world example of pact.io test using [Pact Broker](https://github.com/pact-foundation/pact_broker)
for exchange of the artifacts.

## How to run example

- Run _Pact Broker_
  - using docker compose: `docker compose up`
    - then verify, that you can access it on port http://localhost:9292/ 
- Go to [Consumer application](https://github.com/bugs84/pact-01-hello-world-01-consumer)
  - run `gradlew test` - to generate pact files
  - run `gradlew pactPublish` - to upload contracts to Pact Broker
    - then verify, that contracts are uploaded to http://localhost:9292/
    - note: pactBrokerUrl can be changed in build.gradle.kts file
- Go to [Producer application](https://github.com/bugs84/pact-01-hello-world-02-producer)
  - run test e.g `gradlew test --tests "cz.vondr.pact.provider.ArticlesConsumerTest"`
  - note: pactBrokerUrl can be changed in the test


## Exercise
Change implementation. In a way, that Consumer do not list all articles, when need know "articlesCount"
It means: Change Application It will not call http method, which list all articles. But will call new http call, which will return only count of articles.
  1. Change ConsumerTest, that it will work in this new way 
  2. Consumer Implementation will not call http method, which list all articles. But will call new http call, which will return only count of articles. 
  3. Run Producer Test - it will fail
  4. Implement missing Producer Test according to contract
  5. Fix Producer implementation 
  6. Everything is working - new behaviour is implemented. 