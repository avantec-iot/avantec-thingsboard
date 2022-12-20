ThingsBoard Overview
######################

Reprinted articles:  https://thingsboard.io/docs/

Introduction
============

See `What is ThingsBoard?`__

.. __: https://thingsboard.io/docs/getting-started-guides/what-is-thingsboard/

.. uml::

   node "\nThingsBoard Server\n" as TBSrv {
   }

   node "\nDevice\n" as TBDev {
   }

   node "\nServer-side Application\n" as TBApp {
   }

   TBSrv <-down-> TBDev : Device API
   TBSrv <-down-> TBApp : REST API, Websocket API


Features
========

Entities and relations
----------------------

See `Entities and relations`__ .

.. __: https://thingsboard.io/docs/user-guide/entities-and-relations/


Working with telemetry data
---------------------------

See `Working with telemetry data`__.

.. __: https://thingsboard.io/docs/user-guide/telemetry/


.. uml::

   title  Telemetry data

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 
   box "Server-side Application" #LightBlue
   participant "Server-side Application" as TBApp  order 30
   participant "Web UI" as WebUI  order 40
   end box

   == Telemetry Upload ==

   TBDev  ->  TBSrv: Telemetry upload API (**Device API**)

   == Timeseries data Query ==

   TBSrv  <-  TBApp: Timeseries data keys API (**REST API**)
   TBSrv  <-  TBApp: Timeseries data values API (**REST API**)
   ... other **Timeseries data Query API** ...

   == or Timeseries data Subscription ==

   TBSrv  <-  WebUI: subscription commands (**Websocket API**)
   TBSrv  ->  WebUI: subscription updates (**Websocket API**)



Working with IoT device attributes
----------------------------------

See `Working with IoT device attributes`__.

.. __: https://thingsboard.io/docs/user-guide/attributes/


Attributes are treated key-value pairs. Flexibility and simplicity of the key-value format allow easy and seamless integration with almost any IoT device on the market.

Device specific attributes are separated into two main groups:

* **client-side attributes** - attributes are reported and managed by the device application. For example current software/firmware version, hardware specification, etc.

* **shared attributes** - attributes are reported and managed by the server-side application. Visible to the device application. For example customer subscription plan, target software/firmware version.

.. uml::

   title  Device attributes

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 
   participant "Server-side Application" as TBApp  order 30

   == Request client-side and shared attributes from the server ==
   TBDev  ->  TBSrv: request attribute values from the server (**Device API**)
   TBDev <--  TBSrv: receive response (**Device API**)

   == Upload client-side attributes to the server ==
   TBDev ->  TBSrv: client-side attributes update to the server(**Device API**)

   == Subscribe to updates of shared attributes from the server ==
   TBDev ->  TBSrv: subscribe to updates of shared attributes (**Device API**)
   TBDev <-  TBSrv: updates of shared attributes (**Device API**)

   == Attribute Data Query ==
   TBSrv  <-  TBApp: Attribute keys API (**REST API**)
   TBSrv  <-  TBApp: Attribute values API (**REST API**)
   ... other **Attribute Data Query API** ...


Using RPC capabilities
----------------------

See `Using RPC capabilities`__.

.. __: https://thingsboard.io/docs/user-guide/rpc/


Thinsboard RPC feature can be divided into two types based on originator: device-originated and server-originated RPC calls. In order to use more familiar names, we will name device-originated RPC calls as a **client-side RPC** calls and server-originated RPC calls as **server-side RPC** calls.

Client-side RPC
***************

.. uml::

   title  Client-side RPC

   participant "Device" as TBDev order 10
   participant "ThingsBoard Server"  as TBSrv order 20 
   participant "Server-side Application" as TBApp  order 30

   TBDev   ->  TBSrv: Client-side RPC Request (**Device API**)
   TBSrv   ->  TBApp: Client-side RPC Request API (**REST API**)
   TBApp  -->  TBSrv: Client-side RPC response API (**REST API**)
   TBSrv  -->  TBDev: Client-side RPC Response (**Device API**)



Server-side RPC
***************

Server-side RPC calls can be divided into one-way and two-way:

* **One-way server-side RPC** request is sent to the device without delivery confirmation and obviously, does not provide any response from the device. RPC call may fail only if there is no active connection with the target device within a configurable timeout period.

   .. uml::

      title  One-way server-side RPC

      participant "Device" as TBDev order 10
      participant "ThingsBoard Server"  as TBSrv order 20 
      participant "Server-side Application" as TBApp  order 30

      TBSrv   <-  TBApp: Server-side RPC Request API (**REST API**)
      TBDev  <-  TBSrv: Server-side RPC Request (**Device API**)
      TBSrv  -->  TBApp: Server-side RPC **Empty** Response (**REST API**)


* **Two-way server-side RPC** request is sent to the device and expects to receive a response from the device within the certain timeout. The Server-side request is blocked until the target device replies to the request.

   .. uml::

      title  Two-way server-side RPC

      participant "Device" as TBDev order 10
      participant "ThingsBoard Server"  as TBSrv order 20 
      participant "Server-side Application" as TBApp  order 30

      TBSrv   <-  TBApp: Server-side RPC Request API (**REST API**)
      TBDev   <-  TBSrv: Server-side RPC Request (**Device API**)
      TBDev  -->  TBSrv: Server-side RPC response (**Device API**)
      TBSrv  -->  TBApp: Server-side RPC Response (**REST API**)


Claiming devices
----------------

See `Claiming devices`__.

.. __: https://thingsboard.io/docs/user-guide/claiming-devices/

**TODO**: Claiming devices.



Data Visualization
==================

ThingsBoard allows you to configure customizable IoT dashboards. Each IoT Dashboard may contain multiple dashboard widgets that visualize data from multiple IoT devices. Once IoT Dashboard is created, you may assign it to one of the customers of you IoT project.

IoT Dashboards are light-weight and you may have millions of dashboards. For example, you may automatically create a dashboard for each new customer based on data from registered customer IoT devices. Or you may modify dashboard via script when a new device is assigned to a customer. All these actions may be done manually or automated via REST API.

You can find useful links to get started below:

* `Dashboards`__
* `Widgets Library`__
    * **Digital** and **analog** gauges for latest real-time values visualization
    * Highly customizable Bar and Line **charts** for visualization of historical and sliding-window data points
    * **Map** widgets for tracking movement and latest positions of IoT devices on Google or OpenStreet maps.
    * **GPIO** control widgets that allow sending GPIO toggle commands to devices.
    * **Card** widgets to enhance your dashboards with flexible HTML labels based on static content or latest telemetry values from IoT devices.

.. __: https://thingsboard.io/docs/user-guide/ui/dashboards/
.. __: https://thingsboard.io/docs/user-guide/ui/widget-library/


Getting Started Guides
======================

These guides provide quick overview of main ThingsBoard features. Designed to be completed in 15-30 minutes.

* `Hello world`__ : Learn how to collect IoT device data using MQTT, HTTP or CoAP and visualize it on a simple dashboard. Provides variety of sample scripts that you can run on your PC or laptop to simulate the device.
* `End user IoT dashboards`__ : Learn how to perform basic operations over Devices, Customers, and Dashboards.
* `Device data management`__ : Learn how to perform basic operations over device attributes to implement practical device management use cases.

.. __: https://thingsboard.io/docs/getting-started-guides/helloworld/
.. __: https://thingsboard.io/docs/iot-video-tutorials/#working-with-users-devices-and-dashboards
.. __: https://thingsboard.io/docs/iot-video-tutorials/#device-data-management-using-thingsboard
