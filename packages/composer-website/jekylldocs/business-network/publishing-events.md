---
layout: default
title: Publishing Events
category: tasks
sidebar: sidebars/businessnetworks.md
excerpt: Publishing Events Using Transactions
---

# Publishing Events

Events can be published by {{site.data.conrefs.composer_full}} and subscribed to by applications. Events are defined in the model file of a business network definition, and are emitted by transaction JavaScript in the transaction processor functions file.

## Before you begin

Before you begin adding events to your business network, you should have a good understanding of the modelling language for business networks, and what makes up a full business network definition.

## Procedure

1. Events are defined in the model file (`.cto`) of your business network definition, in the same way as assets and participants. Events use the following format:

        ```
        event BasicEvent identified by eventId {
        o String eventId
        }
        ```

2. In order for the event to be published the transaction which creates the event must include three functions, the first is the `getFactory` function. The `getFactory` allows events to be created as part of a transaction. Next, an event must be created by using `factory.newEvent('org.namespace', 'BasicEvent')`. This creates a `BasicEvent` from the business network model file in the defined organisation namespace. Lastly, the event must be emitted by using `emit(BasicEvent)`. A simple transaction which calls this event would look like this:

        ```JavaScript
        /**
         * @param {org.namespace.BasicEventTransaction} basicEventTransaction
         * @transaction
         */
        function basicEventTransaction(basicEventTransaction) {
            var factory = getFactory();

            var basicEvent = factory.newEvent('org.namespace', 'BasicEvent');
            emit(basicEvent);
        }
        ```

This transaction would create and publish an event of the `BasicEvent` type as defined in the business network's model file. For more information on the getFactory function, see the [{{site.data.conrefs.composer_short}} API documentation](https://hyperledger.github.io/composer/jsdoc/module-composer-runtime.html#getFactory).

## What next?

* [Subscribing to events](../applications/subscribing-to-events.html)
* [Creating an application](../applications/genapp.html)

---
