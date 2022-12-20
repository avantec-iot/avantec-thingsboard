ThingsBoard MQTT Device API reference
########################################


Introduction
============

See `ThingsBoard API reference`__.

.. __: https://thingsboard.io/docs/api/


ThingsBoard API consists of two main parts: **device API** and **server-side API**.


.. uml::

   interface "MQTT API" as MQTTAPI
   interface "CoAP API" as CoAPAPI
   interface "HTTP API" as HTTPAPI

   /'interface "Device API" as DeviceAPI'/
   interface "Websocket API" as WebsocketAPI
   interface "REST API" as RestAPI
   
   node "\nThingsBoard Server\n" as TBSrv {
   }

   node "Device" as TBDev {
   }

   node "Server-side Application" as TBApp {
      node "Web UI" as WebUI {
      }
   }

   /'TBSrv -left- DeviceAPI'/
   TBSrv -down-  MQTTAPI
   TBSrv -down-  CoAPAPI
   TBSrv -down-  HTTPAPI
   TBSrv -down- RestAPI
   TBSrv -down-  WebsocketAPI

   /'TBDev .up.> DeviceAPI'/
   TBDev .up.> MQTTAPI : **Device API**
   TBDev .up.> CoAPAPI : **Device API**
   TBDev .up.> HTTPAPI : **Device API**

   TBApp -up-> RestAPI : **Server-side API**
   WebUI -up-> WebsocketAPI : **Server-side API**

   note bottom of TBDev
      Switch one in MQTT API, 
      CoAP API and HTTP API
   end note


* **Server-side API** is available as *REST API* and *Websocket API*:
   * *REST API*:
      * `Administration REST API`__ - The server-side core APIs.
      * `Attributes query API`__ - The server-side APIs provided by `Telemetry Service`__.
      * `Timeseries query API`__ - The server-side APIs provided by `Telemetry Service`__.
      * `RPC API`__ - The server-side APIs provided by `RPC Service`__.
      * `REST Client`__ 
   * *Websocket API*:
      * `Websocket API`__ duplicates REST API functionality and provides the ability to subscribe to device data changes. 

.. __: https://thingsboard.io/docs/reference/rest-api
.. __: https://thingsboard.io/docs/user-guide/attributes/#data-query-api
.. __: https://thingsboard.io/docs/user-guide/attributes/
.. __: https://thingsboard.io/docs/user-guide/telemetry/#data-query-api
.. __: https://thingsboard.io/docs/user-guide/telemetry/
.. __: https://thingsboard.io/docs/user-guide/rpc/#server-side-rpc-api
.. __: https://thingsboard.io/docs/user-guide/rpc/
.. __: https://thingsboard.io/docs/reference/rest-client

.. __: https://thingsboard.io/docs/user-guide/telemetry/#websocket-api


* **Device API** is grouped by supported communication protocols:
   * `MQTT API`__
   * `CoAP API`__
   * `HTTP API`__

.. __: https://thingsboard.io/docs/reference/mqtt-api
.. __: https://thingsboard.io/docs/reference/coap-api
.. __: https://thingsboard.io/docs/reference/http-api


MQTT API 
========

See `MQTT Device API Reference`__.

.. __: https://thingsboard.io/docs/reference/mqtt-api/


Getting started
---------------

MQTT basics
***********

`MQTT`__ is a lightweight publish-subscribe messaging protocol which probably makes it the most suitable for various IoT devices. You can find more information about MQTT `here`__.

ThingsBoard server nodes act as an MQTT Broker that supports QoS levels 0 (at most once) and 1 (at least once) and a set of predefined topics.

.. __: https://en.wikipedia.org/wiki/MQTT
.. __: http://mqtt.org/


Client libraries setup
**********************

You can find a large number of MQTT client libraries on the web. Examples in this article will be based on Mosquitto and MQTT.js. In order to setup one of those tools, you can use instructions in our `Hello World`__ guide.

.. __: https://thingsboard.io/docs/getting-started-guides/helloworld/

MQTT Connect
************

We will use access token device credentials in this article and they will be referred to later as **$ACCESS_TOKEN**. The application needs to send MQTT CONNECT message with username that contains **$ACCESS_TOKEN**. Possible return codes and their reasons during connect sequence:

* **0x00 Connected** - Successfully connected to ThingsBoard MQTT server.
* **0x04 Connection Refused, bad user name or password** - Username is empty.
* **0x05 Connection Refused, not authorized** - Username contains invalid **$ACCESS_TOKEN**.

Key-value format
----------------

By default, ThingsBoard supports key-value content in **JSON**. Key is always a string, while value can be either string, boolean, double, long or JSON. Using custom binary format or some serialization framework is also possible. See `Protocol customization`_ for more details. For example:

.. code:: json

   {
      "stringKey":"value1", 
      "booleanKey":true, 
      "doubleKey":42.0, 
      "longKey":73, 
      "jsonKey": {
         "someNumber": 42,
         "someArray": [1,2,3],
         "someNestedObject": {"key": "value"}
      }
   }


Telemetry upload API
--------------------

.. uml::

   title  Telemetry upload

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 

   TBDev  ->  TBSrv: Telemetry upload (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/telemetry** \nPayload: {"key1":"value1", "key2":"value2"} or \nPayload: [{"key1":"value1"}, {"key2":"value2"}] or \nPayload: {"ts":1451649600512, "values":{"key1":"value1", "key2":"value2"}}


In order to publish telemetry data to ThingsBoard server node, send PUBLISH message to the following topic::

   v1/devices/me/telemetry

The simplest supported data formats are:

.. code:: json

   {"key1":"value1", "key2":"value2"}

or

.. code:: json

   [{"key1":"value1"}, {"key2":"value2"}]

**Please note** that in this case, the server-side timestamp will be assigned to uploaded data!

In case your device is able to get the client-side timestamp, you can use following format:

.. code:: json

   {"ts":1451649600512, "values":{"key1":"value1", "key2":"value2"}}

In the example above, we assume that “1451649600512” is a `unix timestamp`__ with milliseconds precision. For example, the value "1451649600512" corresponds to "Fri, 01 Jan 2016 12:00:00.512 GMT"

.. __: https://en.wikipedia.org/wiki/Unix_time


Example
*******

+----------------+----------------------------+------------------------------------+
| Client library | Shell file                 | JSON file                          |
+================+============================+====================================+
| **Mosquitto**  | `mosquitto-telemetry.sh`_  | - `telemetry-data-as-object.json`_ |
+----------------+----------------------------+ - `telemetry-data-as-array.json`_  |
| **MQTT.js**    | `mqtt-js-telemetry.sh`_    | - `telemetry-data-with-ts.json`_   |
+----------------+----------------------------+------------------------------------+

mosquitto-telemetry.sh
++++++++++++++++++++++

.. code:: bash

   # Publish data as an object without timestamp (server-side timestamp will be used)
   mosquitto_pub -d -h "127.0.0.1" -t "v1/devices/me/telemetry" -u "$ACCESS_TOKEN" -f "telemetry-data-as-object.json"
   # Publish data as an array of objects without timestamp (server-side timestamp will be used)
   mosquitto_pub -d -h "127.0.0.1" -t "v1/devices/me/telemetry" -u "$ACCESS_TOKEN" -f "telemetry-data-as-array.json"
   # Publish data as an object with timestamp (server-side timestamp will be used)
   mosquitto_pub -d -h "127.0.0.1" -t "v1/devices/me/telemetry" -u "$ACCESS_TOKEN" -f "telemetry-data-with-ts.json"


mqtt-js-telemetry.sh
++++++++++++++++++++

.. code:: bash

   # Publish data as an object without timestamp (server-side timestamp will be used)
   cat telemetry-data-as-object.json | mqtt pub -v -h "127.0.0.1" -t "v1/devices/me/telemetry" -u '$ACCESS_TOKEN' -s
   # Publish data as an array of objects without timestamp (server-side timestamp will be used)
   cat telemetry-data-as-array.json | mqtt pub -v -h "127.0.0.1" -t "v1/devices/me/telemetry" -u '$ACCESS_TOKEN' -s
   # Publish data as an object with timestamp (server-side timestamp will be used)
   cat telemetry-data-with-ts.json | mqtt pub -v -h "127.0.0.1" -t "v1/devices/me/telemetry" -u '$ACCESS_TOKEN' -s


telemetry-data-as-object.json
+++++++++++++++++++++++++++++

.. code:: json
   
   {
      "stringKey": "value1",
      "booleanKey": true,
      "doubleKey": 42.0,
      "longKey": 73,
      "jsonKey": {
         "someNumber": 42,
         "someArray": [1,2,3],
         "someNestedObject": {"key": "value"}
      }
   }


telemetry-data-as-array.json
++++++++++++++++++++++++++++

.. code:: json
   
   [{"key1":"value1"}, {"key2":true}]


telemetry-data-with-ts.json
+++++++++++++++++++++++++++

.. code:: json
   
   {
      "ts": 1451649600512,
      "values": {
         "stringKey": "value1",
         "booleanKey": true,
         "doubleKey": 42.0,
         "longKey": 73,
         "jsonKey": {
            "someNumber": 42,
            "someArray": [1, 2, 3],
            "someNestedObject": {
            "key": "value"
            }
         }
      }
   }


Attributes API
--------------

ThingsBoard attributes API allows devices to

* Request `client-side`__ and `shared`__ device attributes from the server.
* Upload `client-side`__ device attributes to the server.
* Subscribe to `shared`__ device attributes from the server.

.. __: https://thingsboard.io/docs/user-guide/attributes/#attribute-types
.. __: https://thingsboard.io/docs/user-guide/attributes/#attribute-types
.. __: https://thingsboard.io/docs/user-guide/attributes/#attribute-types
.. __: https://thingsboard.io/docs/user-guide/attributes/#attribute-types


Request attribute values from the server
****************************************

.. uml::

   title  Request attribute values from the server

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 

   == Subscribe to client-side and shared attribute response from the server ==
   TBDev  ->  TBSrv: subscribe to attribute response (**MQTT, SUBSCRIBE**) \nTopic: **v1/devices/me/attributes/response/+**

   == Request client-side and shared attributes from the server ==
   TBDev  ->  TBSrv: request attribute values from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes/request/$request_id** \nPayload: {"clientKeys":"attribute1,attribute2", "sharedKeys":"shared1,shared2"}
   
   TBDev <--  TBSrv: receive response (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes/response/$request_id** \nPayload: {"client":{"attribute1":"value1","attribute2":"value2"},\n"shared":{"shared1":"value1","shared1":"value2"}}

Before sending PUBLISH message with the attributes request, client need to **subscribe** to::

   v1/devices/me/attributes/response/+

Once subscribed, the client may request client-side or shared device attributes to ThingsBoard server node, send **PUBLISH** message to the following topic::

   v1/devices/me/attributes/request/$request_id

where **$request_id** is your integer request identifier. 

The client should receive the response to the following topic::

   v1/devices/me/attributes/response/$request_id


Example
+++++++

The following example is written in javascript and is based on mqtt.js. Pure command-line examples are not available because subscribe and publish need to happen in the same mqtt session.

+----------------+-----------------------------------+------------------------------------+------------------------------+
| Client library | Shell file                        | JavaScript file                    |  Result (JSON file)          |
+================+===================================+====================================+==============================+
| **MQTT.js**    | `mqtt-js-attributes-request.sh`_  | `mqtt-js-attributes-request.js`_   | `attributes-response.json`_  |
+----------------+-----------------------------------+------------------------------------+------------------------------+

mqtt-js-attributes-request.sh
:::::::::::::::::::::::::::::

.. code:: bash

   export TOKEN=$ACCESS_TOKEN
   node mqtt-js-attributes-request.js


mqtt-js-attributes-request.js
:::::::::::::::::::::::::::::

.. code:: javascript

   var mqtt = require('mqtt')
   var client  = mqtt.connect('mqtt://127.0.0.1',{
      username: process.env.TOKEN
   })

   client.on('connect', function () {
      console.log('connected')
      client.subscribe('v1/devices/me/attributes/response/+')
      client.publish('v1/devices/me/attributes/request/1', '{"clientKeys":"attribute1,attribute2", "sharedKeys":"shared1,shared2"}')
   })

   client.on('message', function (topic, message) {
      console.log('response.topic: ' + topic)
      console.log('response.body: ' + message.toString())
      client.end()
   })


attributes-response.json
::::::::::::::::::::::::

.. code:: json

   {"key1":"value1"}


**Please note**, the intersection of client-side and shared device attribute keys is a **bad** practice! However, it is still possible to have same keys for client, shared or even server-side attributes.


Publish attribute update to the server
**************************************

.. uml::

   title  Publish attribute update to the server

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 

   TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"attribute1":"value1","attribute2":true}


In order to publish client-side device attributes to ThingsBoard server node, send **PUBLISH** message to the following topic::

   v1/devices/me/attributes

Example
+++++++

+----------------+-------------------------------------+------------------------------------+
| Client library | Shell file                          | JSON file                          |
+================+=====================================+====================================+
| **Mosquitto**  | `mosquitto-attributes-publish.sh`_  | `new-attributes-values.json`_      |
+----------------+-------------------------------------+                                    |
| **MQTT.js**    | `mqtt-js-attributes-publish.sh`_    |                                    |
+----------------+-------------------------------------+------------------------------------+

mosquitto-attributes-publish.sh
:::::::::::::::::::::::::::::::

.. code:: bash

   # Publish client-side attributes update
   mosquitto_pub -d -h "127.0.0.1" -t "v1/devices/me/attributes" -u "$ACCESS_TOKEN" -f "new-attributes-values.json"


mqtt-js-attributes-publish.sh
:::::::::::::::::::::::::::::

.. code:: bash
   
   # Publish client-side attributes update
   cat new-attributes-values.json | mqtt pub -d -h "127.0.0.1" -t "v1/devices/me/attributes" -u '$ACCESS_TOKEN' -s


new-attributes-values.json
::::::::::::::::::::::::::

.. code:: json
   
   {
      "stringKey": "value1",
      "booleanKey": true,
      "doubleKey": 42.0,
      "longKey": 73,
      "jsonKey": {
         "someNumber": 42,
         "someArray": [1,2,3],
         "someNestedObject": {"key": "value"}
      }
   }


Subscribe to attribute updates from the server
**********************************************

.. uml::

   title  Subscribe to attribute updates from the server

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 

   == Subscribe to attribute updates from the server ==
   TBDev  ->  TBSrv: subscribe to attribute response (**MQTT, SUBSCRIBE**) \nTopic: **v1/devices/me/attributes**

   == Receive the attribute update from the server ==
   TBDev  <-  TBSrv: receive attribute update from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"attribute1":"value1","attribute2":"value2"}


In order to subscribe to shared device attribute changes, send **SUBSCRIBE** message to the following topic::

   v1/devices/me/attributes

When a shared attribute is changed by one of the server-side components (such as the REST API or the Rule Chain), the client will **receive** the following update:

.. code:: json

   {"key1":"value1"}


Example
+++++++

+----------------+---------------------------------------+
| Client library | Shell file                            |
+================+=======================================+
| **Mosquitto**  | `mosquitto-attributes-subscribe.sh`_  |
+----------------+---------------------------------------+
| **MQTT.js**    | `mqtt-js-attributes-subscribe.sh`_    |
+----------------+---------------------------------------+

mosquitto-attributes-subscribe.sh
:::::::::::::::::::::::::::::::::

.. code:: bash

   # Subscribes to attribute updates
   mosquitto_sub -d -h "127.0.0.1" -t "v1/devices/me/attributes" -u "$ACCESS_TOKEN"

mqtt-js-attributes-subscribe.sh
:::::::::::::::::::::::::::::::

.. code:: bash
   
   # Subscribes to attribute updates
   mqtt sub -v "127.0.0.1" -t "v1/devices/me/attributes" -u '$ACCESS_TOKEN'


PRC API
-------

Server-side RPC
***************

.. uml::

   title  Server-side RPC

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 

   == Subscribe to sever-side RPC request from the server ==
   TBDev  ->  TBSrv: subscribe to sever-side RPC request (**MQTT, SUBSCRIBE**) \nTopic: **v1/devices/me/rpc/request/+**

   == Receive two-way sever-side RPC request from the server ==
   TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteOTA","params":"http://192.168.xx.xxx/abc.bin"}
   
   TBDev -->  TBSrv: send response (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/response/$request_id** \nPayload: {"method":"remoteOTA","results":{"result":"success"}}

   == Receive one-way sever-side RPC request from the server ==
   TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"setSpValue","params":14.5}


In order to subscribe to RPC commands from the server, send **SUBSCRIBE** message to the following topic::

   v1/devices/me/rpc/request/+

Once subscribed, the client will receive individual commands as a **PUBLISH** message to the corresponding topic::

   v1/devices/me/rpc/request/$request_id

where **$request_id** is an integer request identifier.

The client should publish the response to the following topic::

   v1/devices/me/rpc/response/$request_id


Example
+++++++

The following example is written in javascript and is based on mqtt.js. Pure command-line examples are not available because subscribe and publish need to happen in the same mqtt session.

+----------------+-----------------------------------+------------------------------------+
| Client library | Shell file                        | JavaScript file                    |
+================+===================================+====================================+
| **MQTT.js**    | `mqtt-js-rpc-from-server.sh`_     | `mqtt-js-rpc-from-server.js`_      |
+----------------+-----------------------------------+------------------------------------+

mqtt-js-rpc-from-server.sh
::::::::::::::::::::::::::

.. code:: bash

   export TOKEN=$ACCESS_TOKEN
   node mqtt-js-rpc-from-server.js

mqtt-js-rpc-from-server.js
:::::::::::::::::::::::::::::::

.. code:: javascript
   
   var mqtt = require('mqtt');
   var client  = mqtt.connect('mqtt://127.0.0.1',{
      username: process.env.TOKEN
   });

   client.on('connect', function () {
      console.log('connected');
      client.subscribe('v1/devices/me/rpc/request/+')
   });

   client.on('message', function (topic, message) {
      console.log('request.topic: ' + topic);
      console.log('request.body: ' + message.toString());
      var requestId = topic.slice('v1/devices/me/rpc/request/'.length);
      //client acts as an echo service
      client.publish('v1/devices/me/rpc/response/' + requestId, message);
   });


Client-side RPC
***************

.. uml::

   title  Client-side RPC

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 

   == Subscribe to client-side RPC response from the server ==
   TBDev  ->  TBSrv: subscribe to client-side RPC response (**MQTT, SUBSCRIBE**) \nTopic: **v1/devices/me/rpc/response/+**

   == Publish client-side RPC request ==
   TBDev  ->  TBSrv: publish client-side RPC request (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"getTime","params":{}}
   
   TBDev <--  TBSrv: receive response (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/response/$request_id** \n{"method":"getTime","results":{"utcDateime":"2020-06-18T09:16:59Z"}}


In order to subscribe to client-side RPC response from the server, send **SUBSCRIBE** message to the following topic::

   v1/devices/me/rpc/response/+

Once subscribed, the client may send **PUBLISH** message to the following topic::

   v1/devices/me/rpc/request/$request_id

where **$request_id** is an integer request identifier. The response from server will be published to the following topic::

   v1/devices/me/rpc/response/$request_id


Example
+++++++

The following example is written in javascript and is based on mqtt.js. Pure command-line examples are not available because subscribe and publish need to happen in the same mqtt session.

+----------------+-----------------------------------+------------------------------------+
| Client library | Shell file                        | JavaScript file                    |
+================+===================================+====================================+
| **MQTT.js**    | `mqtt-js-rpc-from-client.sh`_     | `mqtt-js-rpc-from-client.js`_      |
+----------------+-----------------------------------+------------------------------------+


mqtt-js-rpc-from-client.sh
::::::::::::::::::::::::::

.. code:: bash

   export TOKEN=$ACCESS_TOKEN
   node mqtt-js-rpc-from-client.js


mqtt-js-rpc-from-client.js
::::::::::::::::::::::::::

.. code:: javascript
   
   var mqtt = require('mqtt');
   var client = mqtt.connect('mqtt://127.0.0.1', {
      username: process.env.TOKEN
   });

   client.on('connect', function () {
      console.log('connected');
      client.subscribe('v1/devices/me/rpc/response/+');
      var requestId = 1;
      var request = {
         "method": "getTime",
         "params": {}
      };
      client.publish('v1/devices/me/rpc/request/' + requestId, JSON.stringify(request));
   });

   client.on('message', function (topic, message) {
      console.log('response.topic: ' + topic);
      console.log('response.body: ' + message.toString());
   });


Claiming API
------------

Please see the corresponding article to get more information about the `Claiming devices`__ feature.

.. __: https://thingsboard.io/docs/user-guide/claiming-devices

In order to initiate claiming device, send PUBLISH message to the following topic::

   v1/devices/me/claim

The supported data format is:

.. code:: json
   
   {"secretKey":"value", "durationMs":60000}

**Please note** that the above fields are optional. In case the **secretKey** is not specified, the empty string as a default value is used. In case the **durationMs** is not specified, the system parameter **device.claim.duration** is used (in the file **/etc/thingsboard/conf/thingsboard.yml** ).


Protocol customization
----------------------

MQTT transport can be fully customized for specific use-case by changing the corresponding `module`__.

.. __: https://github.com/thingsboard/thingsboard/tree/master/transport/mqtt



Device MQTT Topic 
-----------------

.. role:: strike
    :class: strike

.. list-table:: Device MQTT Topic 
   :widths: auto
   :header-rows: 1

   * - Function \ Topic
     - Subscribe
     - Tx
     - Rx

   * - Telemetry
     - 
     - ① v1/devices/me/telemetry
     - 

   * - 
     - 
     - 
     - 
   * - Request attributes
     - ① v1/devices/me/attributes/response/+
     - ② v1/devices/me/attributes/request/$request_id
     - ③ v1/devices/me/attributes/response/$request_id
   * - Publish attributes
     - 
     - ① v1/devices/me/attributes
     - 
   * - Subscribe attributes update
     - ① v1/devices/me/attributes
     - 
     - ② v1/devices/me/attributes

   * - 
     - 
     - 
     - 
   * - Server-Side RPC
     - ① v1/devices/me/rpc/request/+
     - ③ v1/devices/me/rpc/response/$request_id
     - ② v1/devices/me/rpc/request/$request_id
   * - Client-Side RPC
     - ① v1/devices/me/rpc/response/+
     - ② v1/devices/me/rpc/request/$request_id
     - ③ v1/devices/me/rpc/response/$request_id

   * - 
     - 
     - 
     - 
   * - Claiming device
     - 
     - :strike:`① v1/devices/me/claim`
     - 


**Note**: ①②③ The order in which topics are performed.