![Travis build status](https://travis-ci.org/pousse-cafe/pousse-cafe-spring-pulsar.svg?branch=master)
![Maven status](https://maven-badges.herokuapp.com/maven-central/org.pousse-cafe-framework/pousse-cafe-spring-pulsar/badge.svg)

# Pousse-Café Spring Pulsar

This projects enables a smooth integration of [Pousse-Café Pulsar](https://github.com/pousse-cafe/pousse-cafe-pulsar) in
a Spring application.

Your Spring configuration class should look like this (do not forget to include `poussecafe.spring` in your
package scan):

    @Configuration
    @ComponentScan(basePackages = { "poussecafe.spring" })
    public class AppConfiguration {
    
        @Bean
        public Bundles bundles(
                PulsarMessaging messaging,
                Storage storage) {
            MessagingAndStorage messagingAndStorage = new MessagingAndStorage(messaging, storage);
            return new Bundles.Builder()
                // Register your bundles here using withBundle and use messagingAndStorage
                // when building them
                .build();
        }
    }

## Properties

- `poussecafe.spring.pulsar.broker`: the URL of Pulsar broken (default is `pulsar://localhost:6650`)
- `poussecafe.spring.pulsar.subscriptionTopics`: a comma-separated list of topics (default is `pousse-cafe`)
- `poussecafe.spring.pulsar.subscriptionName`: the subscription name (default is `pousse-cafe`)
- `poussecafe.spring.pulsar.defaultPublicationTopic`: the topic used when publishing messages if none is
    explicitly provided (default is `pousse-cafe`)
- `poussecafe.spring.pulsar.subscriptionType`: the subscription type (default is `Shared`)
- `poussecafe.spring.pulsar.statsIntervalInS`: the stats publication interval (in s); a negative value disables
    stats reporting (default is `-1`)
- `poussecafe.spring.pulsar.sendAsynchronously`: messages are sent using the asynchronous API of Pulsar client
    (default is `false`)


## Configure your Maven project

Add the following snippet to your POM:

    <dependency>
        <groupId>org.pousse-cafe-framework</groupId>
        <artifactId>pousse-cafe-spring-pulsar</artifactId>
        <version>${poussecafe.spring.pulsar.version}</version>
    </dependency>
    <dependency>
        <groupId>org.apache.pulsar</groupId>
        <artifactId>pulsar-client</artifactId>
        <version>${pulsar.version}</version>
    </dependency>
