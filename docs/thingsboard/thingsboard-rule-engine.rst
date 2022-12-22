***********************************
Getting Started with Rule Engine
***********************************

What is ThingsBoard Rule Engine?
=====================================

Rule Engine is an easy to use framework for building event-based workflows. There are 3 main components:

* **Message** - any incoming event. It can be an incoming data from devices, device life-cycle event, REST API event, RPC request, etc.
* **Rule Node** - a function that is executed on an incoming message. There are many different Node types that can filter, transform or execute some action on incoming Message.
* **Rule Chain** - nodes are connected with each other with relations, so the outbound message from rule node is sent to next connected rule nodes.

Typical Use Cases
=====================================

ThingsBoard Rule Engine is a highly customizable framework for complex event processing. Here are some common use cases that one can configure via ThingsBoard Rule Chains:

* Data validation and modification for incoming telemetry or attributes before saving to the database.
* Copy telemetry or attributes from devices to related assets so you can aggregate telemetry. For example data from multiple devices can be aggregated in related Asset.
* Create/Update/Clear alarms based on defined conditions.
* Trigger actions based on device life-cycle events. For example, create alerts if Device is Online/Offline.
* Load additional data required for processing. For example, load temperature threshold value for a device that is defined in Device’s Customer or Tenant attribute.
* Trigger REST API calls to external systems.
* Send emails when complex event occurs and use attributes of other entities inside Email Template.
* Take into account User preferences during event processing.
* Make RPC calls based on defined condition.
* Integrate with external pipelines like Kafka, Spark, AWS services, etc.

See `Getting Started with Rule Engine`_.

.. _Getting Started with Rule Engine: https://thingsboard.io/docs/user-guide/rule-engine-2-0/re-getting-started/