*********************************
TA652FC-W MQTT API
*********************************

.. tip::

  - This section applies to both ``TA652FC-W`` and ``TA652FH-W``.
  - Unless otherwise specified, all specifications applicable to TA652FC-W are also applicable to TA652FH-W.


Overview
========

``TA652FC-W & TA652FH-W MQTT API`` is an implementation of :doc:`/thingsboard/thingsboard-mqtt-device-api` (MQTT is a lightweight publish/subscribe messaging protocol).

.. uml::

   node "\nThingsBoard Server\n" as TBSrv {
   }

   node "\nDevice\n" as TBDev {
   }

   node "\nServer-side Application\n" as TBApp {
   }

   TBSrv <-down-> TBDev : <color:#FF0000> **TA652FC-W / TA652FH-W MQTT API** </color>
   TBSrv <-down-> TBApp : REST API, Websocket API


Features
========

* MQTT protocol:

  * Support MQTT over TCP
  * **NOT support MQTT over SSL with mbedtls, MQTT over Websocket, MQTT over Websocket Secure**

* Base on :doc:`/thingsboard/thingsboard-mqtt-device-api`:

  * Support telemetry upload API
  * Support client-side & shared attributes, and attributes API:

    * Request attribute values from the server
    * Publish attribute update to the server
    * Subscribe to attribute updates from the server

  * Support PRC API:

    * Server-side RPC: one-way and two-way
    * Client-side RPC: one-way and two-way

  * Support Claiming devices API
  * Support Firmware API

  * **NOT support Device provisioning API**
 

MQTT Special
============

* Currently support ``mqtt`` schemes
* Currently **NOT** support ``mqtts``, ``ws``, ``wss`` schemes
* MQTT over TCP samples:

  * ``mqtt://mqtt.eclipse.org`` : MQTT over TCP, default port 1883:
  * ``mqtt://mqtt.eclipse.org:1884`` : MQTT over TCP, port 1884:


Flow Chart
==========

.. tip::

  The range of values for message fields is referred to in the following sections, see  `Telemetry (Time-series data)`_, `Shared attributes`_, `Client-side attributes`_ and `Server-side RPC`_.

TELE.01 Time-series Data Upload
-------------------------------

Chart:
  .. uml::

    caption  Time-series Data Upload

    participant "TA652FC-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20


    [-> TBDev: Timer(telemetry, period: **uploadFreq**)
    TBDev -> TBSrv: Telemetry upload (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/telemetry** \nPayload: {"roomTemp":26.2,"changeOverTemp":26.3}

    [-> TBDev: (telemetry, If temprature change \n exceeds **uploadThreshold**, \n upload immediately)
    TBDev -> TBSrv: Telemetry upload (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/telemetry** \nPayload: {"roomTemp":26.2,"changeOverTemp":26.3}

  .. uml::

    caption  Time-series Data Upload

    participant "TA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 


    [-> TBDev: Timer(telemetry, period: **uploadFreq**)
    TBDev -> TBSrv: Telemetry upload (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/telemetry** \nPayload: {"roomTemp":26.2,"floorTemp":26.3}

    [-> TBDev: (telemetry, If temprature change \n exceeds **uploadThreshold**, \n upload immediately)
    TBDev -> TBSrv: Telemetry upload (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/telemetry** \nPayload: {"roomTemp":26.2,"floorTemp":26.3}

Message:
  .. code:: javascript

    // Message Type:  Telemetry upload (MQTT, PUBLISH) 
    // Topic:         v1/devices/me/telemetry
    // Payload - TA652FC-W:
    {"roomTemp":26.2,"changeOverTemp":26.3}
    // Payload - TA652FH-W:
    {"roomTemp":26.2,"floorTemp":26.3}

See `roomTemp`_, `changeOverTemp`_ (only for TA652FC-W), `floorTemp`_ (only for TA652FH-W).

See `uploadFreq`_.

See `uploadThreshold`_.


CTRL.01 Control Mode
-----------------------

Chart:
  .. uml::

    caption  Control Mode

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    == local operate ==
    [-> TBDev 
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"controlMode":"On"}

    == remote operate ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetControlMode","params":"Off"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"controlMode":"Off"}

Message 1:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"controlMode":"On"}

Message 2:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetControlMode","params":"Off"}

See `controlMode`_ and `remoteSetControlMode`_. 


CTRL.02 Fan Mode & Fan Status (only for TA652FC-W)
----------------------------------------------------

Chart:
  .. uml::

    caption  Fan Mode & Fan Status

    participant "TA652FC-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    == local operate ==
    [-> TBDev 
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"fanMode":"Auto"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"fanStatus":"Low"}

    == remote operate ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetFanMode","params":"Med"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"fanMode":"Med"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"fanStatus":"Med"}

Message 1:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FC-W:
    {"fanMode":"Auto"}

Message 2:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FC-W:
    {"fanStatus":"Low"}

Message 3:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FC-W:
    {"method":"remoteSetFanMode","params":"Med"}

See `fanMode`_ (only for TA652FC-W), `fanStatus`_ (only for TA652FC-W) and `remoteSetFanMode`_ (only for TA652FC-W). 


CTRL.03 Set Point & Override Status
-------------------------------------

Chart:
  .. uml::

    caption  Setpoint & Override Status

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    == local adjust setpoint ==
    [-> TBDev 
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"spValue":27.5}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"overrideStatus":false}

    == remote adjust setpoint ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetSpValue","params":34}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"spValue":34}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"overrideStatus":true}

    == remote adjust to progrm setpoint ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetOverrideStatus","params":{}}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"overrideStatus":false}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"spValue":25.5}

Message 1:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"spValue":27.5}

Message 2:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"overrideStatus":false}

Message 3:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetSpValue","params":34}

Example 4:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetOverrideStatus","params":{}}

See `spValue`_, `overrideStatus`_, `remoteSetSpValue`_ and `remoteSetOverrideStatus`_ .


PRG.01 Program Mode & Program Status
---------------------------------------

Chart:
  .. uml::

    caption  Program Mode & Program Status

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    == local operate ==
    [-> TBDev 
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgMode":"Every-day"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextEnable":true}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextCtrlMode":"On"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextSetpoint":24.5}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextDaysTime":"Wed, 06:00 PM"}

    == remote operate ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetPrgMode","params":"Sun_mon-fri_sat"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgMode":"Sun_mon-fri_sat"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextEnable":true}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextCtrlMode":"On"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextSetpoint":25.5}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgNextDaysTime":"Mon, 10:00 PM"}

Message 1:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgMode":"Every-day"}

Message 2:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgNextEnable":true}

Message 3:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgNextCtrlMode":"On"} //{"prgNextCtrlMode":"Off"}

Message 4:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgNextSetpoint":24.5}

Message 5:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgNextDaysTime":"Wed, 06:00 PM"}

Message 6:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetPrgMode","params":"Sun_mon-fri_sat"}

See `prgMode`_, `prgNextEnable`_, `prgNextCtrlMode`_, `prgNextSetpoint`_, `prgNextDaysTime`_ and `remoteSetPrgMode`_. 


PRG.02 Program Setpoint & Time
---------------------------------

Chart:
  .. uml::

    caption  Program Setpoint & Time

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    == local operate ==
    [-> TBDev 
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgSpTime00":"10:00"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgCtrlMode00":"On"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgSpValue00":27.5}

    == remote operate ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetPrgSpTime27","params":"23:00"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgSpTime27":"23:00"}
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetPrgCtrlMode01","params":"Off"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgCtrlMode01":"Off"}
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetPrgSpValue14","params":21.5}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"prgSpValue14":21.5}

    note over TBDev, TBSrv
    prgSpTime00  ~ prgSpTime27
    prgCtrlMode00 ~ prgCtrlMode27
    prgSpValue00 ~ prgSpValue27
    remoteSetPrgSpTime00  ~ remoteSetPrgSpTime27
    remoteSetPrgCtrlMode00 ~ remoteSetPrgCtrlMode27
    remoteSetPrgSpValue00 ~ remoteSetPrgSpValue27
    end note

Message 1:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgSpTime00":"10:00"}

Message 2:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgCtrlMode00":"On"} //{"prgCtrlMode27":"Off"}

Message 3:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"prgSpValue00":27.5}

Message 4:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetPrgSpTime27","params":"23:00"}

Message 5:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetPrgCtrlMode27","params":"Off"} //{"method":"remoteSetPrgCtrlMode00","params":"On"}

Message 6:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetPrgSpValue14","params":21.5}

See `prgSpTimeXX`_, `prgCtrlModeXX`_, `prgSpValueXX`_, `remoteSetPrgSpTimeXX`_, `remoteSetPrgCtrlModeXX`_ and `remoteSetPrgSpValueXX`_. 


SET.01 Upload Device Attributes when the device is started
-------------------------------------------------------------

Chart:
  .. uml::

    caption  Upload Device Attributes when the device is started

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    [-> TBDev : power on

    == Upload  Device Fixed attributes ==
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"model":"TA652FC-W-TB","mac":"24:0A:C4:2C:EB:C8",\n"wifiFWVersion":"1.5.4.0","mcuFWVersion":"1.4.4.1",\n"wifiRSSIMin":0,"wifiRssiMax":255,"wifiRssiResolution":1,\n"uploadFreqMin":2,"uploadFreqMax":2592000,"uploadFreqStep":1,\n"syncTimeFreqMin":1800,"syncTimeFreqMax":2592000,"syncTimeFreqStep":1}

    note over TBDev, TBSrv
    send these attributes only once when the device is started
    end note

    == Upload  temperature unit related attributes ==
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"supportCtrlModeInSchedule":"Yes",\n"currentTempUnit":"°C",\n"envirTempMin":0,"envirTempMax":50,"envirTempStep":0.1,\n"spValueMin":5,"spValueMax":40,"spValueStep":0.5,\n"internalOffsetMin":-5,"internalOffsetMax":5,"internalOffsetStep":0.5,\n"uploadThresholdMin":0.2,"uploadThresholdMax":5,"uploadThresholdStep":0.1}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"floorTempLimitedMin":20,"floorTempLimitedMax":40,"floorTempLimitedStep":0.5,\n"switchingDiffHeatingMin":1,"switchingDiffHeatingMax":4,"switchingDiffHeatingStep":0.5,\n"switchingDiffCoolingMin":1,"switchingDiffCoolingMax":4,"switchingDiffCoolingStep":0.5,\n"changeOverTempHeatingMin":27,"changeOverTempHeatingMax":40,"changeOverTempHeatingStep":0.5,\n"changeOverTempCoolingMin":10,"changeOverTempCoolingMax":25,"changeOverTempCoolingStep":0.5}

    note over TBDev, TBSrv
    send these attributes only once when the device is started
    end note

Message 1:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"model":"TA652FC-W-TB","mac":"24:0A:C4:2C:EB:C8",
    "wifiFWVersion":"1.5.4.0","mcuFWVersion":"1.4.4.1",
    "wifiRSSIMin":0,"wifiRssiMax":255,"wifiRssiStep":1,
    "uploadFreqMin":2,"uploadFreqMax":2592000,"uploadFreqStep":1,
    "syncTimeFreqMin":1800,"syncTimeFreqMax":2592000,"syncTimeFreqStep":1}

Message 2:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"supportCtrlModeInSchedule":"Yes",
    "currentTempUnit":"°C",
    "envirTempMin":0,"envirTempMax":50,"envirTempStep":0.1,
    "spValueMin":5,"spValueMax":40,"spValueStep":0.5,
    "internalOffsetMin":-5,"internalOffsetMax":5,"internalOffsetStep":0.5,
    "uploadThresholdMin":0.2,"uploadThresholdMax":5,"uploadThresholdStep":0.1}

Message 3 - TA652FC-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FC-W:
    {"switchingDiffHeatingMin":1,"switchingDiffHeatingMax":4,"switchingDiffHeatingStep":0.5,
    "switchingDiffCoolingMin":1,"switchingDiffCoolingMax":4,"switchingDiffCoolingStep":0.5,
    "changeOverTempHeatingMin":27,"changeOverTempHeatingMax":40,"changeOverTempHeatingStep":0.5,
    "changeOverTempCoolingMin":10,"changeOverTempCoolingMax":25,"changeOverTempCoolingStep":0.5}

Message 3 - TA652FH-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FH-W:
    {"floorTempLimitedMin":20,"floorTempLimitedMax":40,"floorTempLimitedStep":0.5,
    "switchingDiffHeatingMin":1,"switchingDiffHeatingMax":4,"switchingDiffHeatingStep":0.5,
    "switchingDiffCoolingMin":1,"switchingDiffCoolingMax":4,"switchingDiffCoolingStep":0.5}

See `model`_, `mac`_, 
`wifiFWVersion`_, `mcuFWVersion`_, 
`wifiRSSIMin`_, `wifiRssiMax`_, `wifiRssiStep`_, 
`uploadFreqMin`_, `uploadFreqMax`_, `uploadFreqStep`_, 
`syncTimeFreqMin`_, `syncTimeFreqMax`_ and `syncTimeFreqStep`_.

See `supportCtrlModeInSchedule`_, `currentTempUnit`_,
`envirTempMin`_, `envirTempMax`_, `envirTempStep`_,
`spValueMin`_, `spValueMax`_, `spValueStep`_,
`internalOffsetMin`_, `internalOffsetMax`_ and `internalOffsetStep`_,
`uploadThresholdMin`_, `uploadThresholdMax`_ and `uploadThresholdStep`_.

See `floorTempLimitedMin`_ (only for TA652FH-W), `floorTempLimitedMax`_ (only for TA652FH-W), `floorTempLimitedStep`_ (only for TA652FH-W),
`switchingDiffHeatingMin`_, `switchingDiffHeatingMax`_, `switchingDiffHeatingStep`_,
`switchingDiffCoolingMin`_, `switchingDiffCoolingMax`_, `switchingDiffCoolingStep`_,
`changeOverTempHeatingMin`_ (only for TA652FC-W), `changeOverTempHeatingMax`_ (only for TA652FC-W), `changeOverTempHeatingStep`_ (only for TA652FC-W),
`changeOverTempCoolingMin`_ (only for TA652FC-W), `changeOverTempCoolingMax`_ (only for TA652FC-W) and `changeOverTempCoolingStep`_ (only for TA652FC-W).


SET.02 Settings
--------------------

Chart:
  .. uml::

    caption  Settings

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    == local operate temperature unit ==
    [-> TBDev 
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \n{"tempUnit":"°C}

    note over TBDev
    take effect after it reboots
    end note

    == remote operate temperature unit ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetTempUnit","params":"°F"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"tempUnit":"°F"}

    note over TBDev
    take effect after it reboots
    end note

    == local operate time format ==
    [-> TBDev 
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \n{"timeFormat":"12hours"}

    == remote operate time format ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteSetTimeFormat","params":"24hours"}
    TBDev  ->  TBSrv: publish client-side attributes update to the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"timeFormat":"24hours"}

    note over TBDev, TBSrv
    internalOffset, remoteSetInternalOffset
    switchingDiffHeating, remoteSetSwitchingDiffHeating
    switchingDiffCooling, remoteSetSwitchingDiffCooling

    systemMode, remoteSetSystemMode (only for TA652FH-W)
    sensorMode, remoteSetSensorMode (only for TA652FH-W)
    floorTempLimited, remoteSetFloorTempLimited (only for TA652FH-W)
    adaptiveControl, remoteSetAdaptiveControl (only for TA652FH-W)

    forceVent, remoteSetForceVent (only for TA652FC-W)
    changeOverMode, remoteSetChangeOverMode (only for TA652FC-W)
    changeOverTempHeating, remoteSetChangeOverTempHeating (only for TA652FC-W)
    changeOverTempCooling, remoteSetChangeOverTempCooling (only for TA652FC-W)
    end note

Message 1a:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"tempUnit":"°C"}

Message 1b:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetTempUnit","params":"°F"}

Message 2a:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"timeFormat":"12hours"}

Message 2b:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetTimeFormat","params":"24hours"}

Message 3a:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"method":"remoteSetInternalOffset","params":-3.5}

Message 3b:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"internalOffset":-3.5}

Message 4a:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"switchingDiffHeating":3.5}

Message 4b:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetSwitchingDiffHeating","params":3.5}

Message 5a:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"switchingDiffCooling":2.5}

Message 5b:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSetSwitchingDiffCooling","params":2.5}

Message 6a - TA652FH-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FH-W:
    {"systemMode":"Cool"}

Message 6b - TA652FH-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FH-W:
    {"method":"remoteSetSystemMode","params":"Heat"}

Message 7a - TA652FH-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FH-W:
    {"sensorMode":"Internal"}

Message 7b - TA652FH-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FH-W:
    {"method":"remoteSetSensorMode","params":"External"}

Message 8a - TA652FH-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FH-W:
    {"floorTempLimited":29.5}

Message 8b - TA652FH-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FH-W: 
    {"method":"remoteSetFloorTempLimited","params":29.5}

Message 9a - TA652FH-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FH-W:
    {"adaptiveControl":false}

Message 9b - TA652FH-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FH-W:
    {"method":"remoteSetAdaptiveControl","params":true}

Message 10a - TA652FC-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FC-W:
    {"forceVent":true}

Message 10b - TA652FC-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FC-W:
    {"method":"remoteSetForceVent","params":false}

Message 11a - TA652FC-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FC-W:
    {"changeOverMode":"Heat"}

Message 11b - TA652FC-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FC-W:
    {"method":"remoteSetChangeOverMode","params":"Auto"}

Message 12a - TA652FC-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FC-W:
    {"changeOverTempHeating":27}

Message 12b - TA652FC-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FC-W:
    {"method":"remoteSetChangeOverTempHeating","params":27}

Message 13a - TA652FC-W:
  .. code:: javascript

    // Message Type:  publish client-side attributes update to the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload - TA652FC-W:
    {"changeOverTempCooling":11.5}

Message 13b - TA652FC-W:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload - TA652FC-W:
    {"method":"remoteSetChangeOverTempCooling","params":10}

See `tempUnit`_ and `remoteSetTempUnit`_, `timeFormat`_ and `remoteSetTimeFormat`_,
`internalOffset`_ and `remoteSetInternalOffset`_, 
`switchingDiffHeating`_ and `remoteSetSwitchingDiffHeating`_,
`switchingDiffCooling`_ and `remoteSetSwitchingDiffCooling`_. 

See `systemMode`_ and `remoteSetSystemMode`_, `sensorMode`_ and `remoteSetSensorMode`_,
`floorTempLimited`_ and `remoteSetFloorTempLimited`_, `adaptiveControl`_ and `remoteSetAdaptiveControl`_.(only for TA652FH-W)

See `forceVent`_ and `remoteSetForceVent`_, `changeOverMode`_ and `remoteSetChangeOverMode`_,
`changeOverTempHeating`_ and `remoteSetChangeOverTempHeating`_, `changeOverTempCooling`_ and `remoteSetChangeOverTempCooling`_.(only for TA652FC-W)


ADM.01 Request all remote parameters when the device is started
-------------------------------------------------------------------

Chart:
  .. uml::

    caption  Request all remote parameters when the device is started

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    TBDev  ->  TBSrv: request attribute values from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes/request/$request_id** \nPayload: {"sharedKeys":"uploadFreq,uploadThreshold,\nsyncTimeFreq,timezone,timeNTPServer"}
    
    TBDev <--  TBSrv: receive response (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes/response/$request_id** \nPayload: {"shared":{"uploadFreq":300,"uploadThreshold":1.5,\n"syncTimeFreq":86400,timezone":480,\n"timeNTPServer":"pool.ntp.org"}}

Message 1:
  .. code:: javascript

    // Message Type:  request attribute values from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes/request/$request_id
    // Payload: 
    {"sharedKeys":"uploadFreq,uploadThreshold,syncTimeFreq,timezone,timeNTPServer"}

Message 2:
  .. code:: javascript

    // Message Type:  receive response (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes/response/$request_id
    // Payload: 
    {"shared":{"uploadFreq":300,"uploadThreshold":1.5,"syncTimeFreq":86400,
    "timezone":480,"timeNTPServer":"pool.ntp.org"}}

See `uploadFreq`_, `uploadThreshold`_, `syncTimeFreq`_, `timezone`_ and `timeNTPServer`_.


ADM.02 Timer Parameters & upload threshold
-----------------------------------------------

Chart:
  .. uml::

    caption  Timer Parameters

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 

    == Modify Timer Parameters ==
    TBDev  <-  TBSrv: receive attribute update from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"uploadFreq":300}
    TBDev  <-  TBSrv: receive attribute update from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"uploadThreshold":1.5}
    TBDev  <-  TBSrv: receive attribute update from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"syncTimeFreq":86400}

Message 1:
  .. code:: javascript

    // Message Type:  receive attribute update from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload:
    {"uploadFreq":300}

Message 2:
  .. code:: javascript

    // Message Type:  receive attribute update from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload:
    {"uploadThreshold":1.5}

Message 3:
  .. code:: javascript

    // Message Type:  receive attribute update from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"syncTimeFreq":86400}

See `uploadFreq`_, `uploadThreshold`_  and `syncTimeFreq`_.


ADM.03 Remote Sync Time
----------------------------

Chart:
  .. uml::

    caption  Remote Sync Time

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 
    participant "SNTP Server"  as SNTPSrv order 30 

    == Set Device Timezone, SNTP Server ==
    TBDev  <-  TBSrv: receive attribute update from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"timezone":480}
    TBDev  <-  TBSrv: receive attribute update from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/attributes** \nPayload: {"timeNTPServer":"pool.ntp.org"}
    TBDev  --> SNTPSrv: (get datetime)

    == Remote Sync Time ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \n{"method":"remoteSyncTimeRequest","params":{}}
    TBDev  -> TBDev: (refresh datetime)

Message 1:
  .. code:: javascript

    // Message Type:  receive attribute update from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"timezone":480}

Message 2:
  .. code:: javascript

    // Message Type:  receive attribute update from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/attributes
    // Payload: 
    {"timeNTPServer":"pool.ntp.org"}

Message 3:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteSyncTimeRequest","params":{}}

See `timezone`_, `timeNTPServer`_  and `remoteSyncTimeRequest`_. 


ADM.04 FUOTA (firmware update over the air) 
--------------------------------------------------

The flow is to download the firmware from your HTTP server. For the flow of downloading firmware from ThingsBoard server, please refer to :ref:`Firmware_API`.

Chart:
  .. uml::

    caption  FUOTA (firmware update over the air)

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20 
    participant "HTTP Server"  as HTTPSrv order 30 

    == Wi-Fi FUOTA ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteWiFiFUOTA","params":\n"http://192.168.1.106/TA652FC-W_WiFi.ino.bin"}
    TBDev -->  TBSrv: send response (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/response/$request_id** \nPayload: {"method":"remoteWiFiFUOTA","results":{"result":"success"}}
    TBDev  --> HTTPSrv: (get Wi-Fi module firmware)
    TBDev  ->  TBDev: reboot

    == MCU FUOTA (NOT implemented) ==
    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteMcuFUOTA","params":\n"http://192.168.1.106/TA652FC-W-MCU.bin"}
    TBDev -->  TBSrv: send response (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/response/$request_id** \nPayload: {"method":"remoteMcuFUOTA","results":{"result":"success"}}
    TBDev  --> HTTPSrv: (get MCU firmware)
    TBDev  ->  TBDev: reboot

Message 1a:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteWiFiFUOTA",
    "params":"http://192.168.1.106/TA652FC-W_WiFi.ino.bin"}

Message 1b:
  .. code:: javascript

    // Message Type:  send response (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/response/$request_id
    // Payload: 
    {"method":"remoteWiFiFUOTA","results":{"result":"success"}}

Message 2a (NOT implemented):
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
     {"method":"remoteMcuFUOTA",
     "params":"http://192.168.1.106/TA652FC-W_MCU.bin"}

Message 2b (NOT implemented):
  .. code:: javascript

    // Message Type:  send response (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/response/$request_id
    // Payload: 
    {"method":"remoteMcuFUOTA","results":{"result":"success"}}

See `remoteWiFiFUOTA`_ and `remoteMcuFUOTA`_. 


ADM.05 Remote Get Memeory Usage
------------------------------------

Chart:
  .. uml::

    caption  Remote Get Memeory Usage

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20

    TBDev  <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteGetMemoryUsage"}
    TBDev -->  TBSrv: send response (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/response/$request_id** \nPayload: {"iram":162592,"spiram":4194252}

Message 1a:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteGetMemoryUsage"}

Message 1b:
  .. code:: javascript

    // Message Type:  send response (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/response/$request_id
    // Payload: 
   {"iram":162592,"spiram":4194252}

See `remoteGetMemoryUsage`_. 


ADM.06 Remote Reboot Device
------------------------------

Chart:
  .. uml::

    caption  Remote Reboot Device

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20

    TBDev <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteRebootDevice","params":{}}
    TBDev ->  TBDev: (reboot)

Message 1:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteRebootDevice","params":{}}

See `remoteRebootDevice`_. 


ADM.07 Remote Clear Wi-Fi Config
------------------------------------

Chart:
  .. uml::

    caption  Remote Clear Wi-Fi Config

    participant "TA652FC-W\nTA652FH-W" as TBDev order 10
    participant "ThingsBoard Server"  as TBSrv order 20

    TBDev <-  TBSrv: receive server-side RPC request from the server (**MQTT, PUBLISH**) \nTopic: **v1/devices/me/rpc/request/$request_id** \nPayload: {"method":"remoteClearWiFiConfig","params":{}}
    TBDev ->  TBDev: (clear Wi-Fi config)
    TBDev ->  TBDev: (reboot)

Message 1:
  .. code:: javascript

    // Message Type:  receive server-side RPC request from the server (MQTT, PUBLISH)
    // Topic:         v1/devices/me/rpc/request/$request_id
    // Payload: 
    {"method":"remoteClearWiFiConfig","params":{}}

See `remoteClearWiFiConfig`_. 

Claiming 
--------------

Refer to :ref:`Claiming_API`.

Firmware update with ThingsBoard Server
------------------------------------------

Refer to :ref:`Firmware_API`.


Telemetry (Time-series data)
============================

.. tip::
    * All of these telemetry (timeseries data) is uploaded every `uploadFreq`_ seconds.
    * If these telemetry (timeseries data) change exceeds `uploadThreshold`_, upload immediately.

roomTemp
----------

changeOverTemp
-----------------

floorTemp
-----------

wifiRssi
----------

.. list-table:: Telemetry (Time-series data)
   :widths: auto
   :header-rows: 1

   * - Time-series
     - Type
     - Unit
     - Min
     - Max
     - Step/Precision
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - roomTemp
     - float
     - `currentTempUnit`_
     - `envirTempMin`_
     - `envirTempMax`_
     - `envirTempStep`_
     - 
     - ●
     - ●
     - Room temperature

   * - changeOverTemp
     - float
     - `currentTempUnit`_
     - `envirTempMin`_
     - `envirTempMax`_
     - `envirTempStep`_
     - 
     - ●
     - 
     - Change Over |br| Temperatue

   * - floorTemp
     - float
     - `currentTempUnit`_
     - `envirTempMin`_
     - `envirTempMax`_
     - `envirTempStep`_
     - 
     - 
     - ●
     - Floor Temperatue

   * - wifiRssi (deprecated)*
     - int
     - 
     - `wifiRssiMin`_
     - `wifiRssiMax`_
     - `wifiRssiStep`_
     - 
     - ●
     - ●
     - Received Signal |br| Strength Indicator

.. # define a hard line break for HTML
.. |br| raw:: html

   <br/>

.. tip::
    In order to reduce the load on ThingsBoard server, `wifiRssi` is no longer sent.

Shared attributes
=================

.. tip::
    All of these shared attributes may be obtained 
    from your ThingsBoard server.

.. _ta652fc-w-uploadFreq:

uploadFreq
------------

.. _ta652fc-w-uploadThreshold:

uploadThreshold
-------------------

.. _ta652fc-w-syncTimeFreq:

syncTimeFreq
---------------

.. _ta652fc-w-timezone:

timezone
---------

.. _ta652fc-w-timeNTPServer:

timeNTPServer
----------------

.. list-table:: Shared attributes
   :widths: auto
   :header-rows: 1

   * - Shared |br| attribute
     - Type
     - Unit
     - Min
     - Max
     - Step/Precision
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - uploadFreq
     - int
     - second
     - `uploadFreqMin`_
     - `uploadFreqMax`_
     - `uploadFreqStep`_
     - Default: 300
     - ●
     - ●
     - Time-series (Telemetry) |br| upload Frequency. see |br| :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`.

   * - uploadThreshold
     - double
     - temperature
     - `uploadThresholdMin`_
     - `uploadThresholdMax`_
     - `uploadThresholdStep`_
     - Default: 1.5
     - ●
     - ●
     - Time-series (Telemetry) |br| upload Threshold. see |br| :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`.

   * - syncTimeFreq
     - int
     - second
     - `syncTimeFreqMin`_
     - `syncTimeFreqMax`_
     - `syncTimeFreqStep`_
     - Default: |br| 86400 (24*3600)
     - ●
     - ●
     - timer period of |br| sync datetime. see |br| :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`.

   * - timezone
     - int
     - minute
     - 
     - 
     - 
     - Default: |br| 480 (8*60)
     - ●
     - ●
     - offset UTC. see |br| :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`.

   * - timeNTPServer
     - string
     - 
     - 
     - 
     - 
     - Default: |br| pool.ntp.org |br| (127 char+'\0')
     - ●
     - ●
     - SNTP server, eg: |br| pool.ntp.org . see |br| :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`.



Client-side attributes
======================

Client-side attribute (static/fixed)
--------------------------------------

model
^^^^^

mac
^^^^^

wifiFWVersion
^^^^^^^^^^^^^^^

mcuFWVersion
^^^^^^^^^^^^^^^

.. list-table:: Client-side attribute (static/fixed)
   :widths: auto
   :header-rows: 1

   * - Client-side |br| attribute |br| (static/fixed)
     - Type
     - Unit
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - model
     - string
     - 
     - "TA652FC-W-TB", |br| "TA652FH-W-TB"
     - ●
     - ●
     - Product Model

   * - mac
     - string
     - 
     - eg: |br| "34:02:86:5F:23:A9"
     - ●
     - ●
     - Mac Address

   * - wifiFWVersion
     - string
     - 
     - eg: |br| "1.5.5"
     - ●
     - ●
     - WiFi Module |br| F/W version

   * - mcuFWVersion
     - string
     - 
     - eg: |br| "1.5.4"
     - ●
     - ●
     - Main MCU |br| F/W version


Client-side attribute (static/fixed, metadata)
--------------------------------------------------

wifiRssiMin
^^^^^^^^^^^^^

wifiRssiMax
^^^^^^^^^^^^^

wifiRssiStep
^^^^^^^^^^^^^

uploadFreqMin
^^^^^^^^^^^^^^^

uploadFreqMax
^^^^^^^^^^^^^

uploadFreqStep
^^^^^^^^^^^^^^

syncTimeFreqMin
^^^^^^^^^^^^^^^

syncTimeFreqMax
^^^^^^^^^^^^^^^

syncTimeFreqStep
^^^^^^^^^^^^^^^^^

.. list-table:: Client-side attribute (static/fixed, metadata)
   :widths: auto
   :header-rows: 1

   * - Client-side |br| attribute |br| (static/fixed, |br| metadata)
     - Type
     - Unit
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - wifiRssiMin
     - int
     - 
     - 0
     - ●
     - ●
     - the minimum value |br| of `wifiRssi`_
   * - wifiRssiMax
     - int
     - 
     - 255
     - ●
     - ●
     - the maximum value |br| of `wifiRssi`_
   * - wifiRssiStep
     - int
     - 
     - 1
     - ●
     - ●
     - the step value |br| of `wifiRssi`_

   * - uploadFreqMin
     - int
     - second
     - 2
     - ●
     - ●
     - the minimum value |br| of `uploadFreq`_
   * - uploadFreqMax
     - int
     - second
     - 30*24*3600 (2592000)
     - ●
     - ●
     - the maximum value |br| of `uploadFreq`_
   * - uploadFreqStep
     - int
     - second
     - 1
     - ●
     - ●
     - the step value |br| of `uploadFreq`_

   * - syncTimeFreqMin
     - int
     - second
     - 30*60
     - ●
     - ●
     - the minimum value |br| of `syncTimeFreq`_
   * - syncTimeFreqMax
     - int
     - second
     - 30*24*3600
     - ●
     - ●
     - the maximum value |br| of `syncTimeFreq`_
   * - syncTimeFreqStep
     - int
     - second
     - 1
     - ●
     - ●
     - the step value |br| of `syncTimeFreq`_


Client-side attribute (semi-static)
---------------------------------------

supportCtrlModeInSchedule
^^^^^^^^^^^^^^^^^^^^^^^^^^

currentTempUnit
^^^^^^^^^^^^^^^

tempResolution
^^^^^^^^^^^^^^^^

envirTempMin
^^^^^^^^^^^^

envirTempMax
^^^^^^^^^^^^^

envirTempStep
^^^^^^^^^^^^^^

spValueMin
^^^^^^^^^^

spValueMax
^^^^^^^^^^

spValueStep
^^^^^^^^^^^^

internalOffsetMin
^^^^^^^^^^^^^^^^^

internalOffsetMax
^^^^^^^^^^^^^^^^^^

internalOffsetStep
^^^^^^^^^^^^^^^^^^

uploadThresholdMin
^^^^^^^^^^^^^^^^^^

uploadThresholdMax
^^^^^^^^^^^^^^^^^^^

uploadThresholdStep
^^^^^^^^^^^^^^^^^^^^^

floorTempLimitedMin
^^^^^^^^^^^^^^^^^^^

floorTempLimitedMax
^^^^^^^^^^^^^^^^^^^

floorTempLimitedStep
^^^^^^^^^^^^^^^^^^^^

switchingDiffHeatingMin
^^^^^^^^^^^^^^^^^^^^^^^

switchingDiffHeatingMax
^^^^^^^^^^^^^^^^^^^^^^^^^^^

switchingDiffHeatingStep
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

switchingDiffCoolingMin
^^^^^^^^^^^^^^^^^^^^^^^^^^^

switchingDiffCoolingMax
^^^^^^^^^^^^^^^^^^^^^^^

switchingDiffCoolingStep
^^^^^^^^^^^^^^^^^^^^^^^^^

changeOverTempHeatingMin
^^^^^^^^^^^^^^^^^^^^^^^^^

changeOverTempHeatingMax
^^^^^^^^^^^^^^^^^^^^^^^^^

changeOverTempHeatingStep
^^^^^^^^^^^^^^^^^^^^^^^^^

changeOverTempCoolingMin
^^^^^^^^^^^^^^^^^^^^^^^^^

changeOverTempCoolingMax
^^^^^^^^^^^^^^^^^^^^^^^^^

changeOverTempCoolingStep
^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table:: Client-side attribute (semi-static)
   :widths: auto
   :header-rows: 1

   * - Client-side |br| attribute |br| (semi-static)
     - Type
     - Unit
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - supportCtrlModeInSchedule
     - string
     - 
     - "Yes" / "No"
     - ●
     - ●
     - Control On/Off |br| in schedule

   * - currentTempUnit
     - string
     - 
     - "°C" / "°F"
     - ●
     - ●
     - Centigrade, |br| Fahrenheit

   * - envirTempMin
     - float
     - `currentTempUnit`_
     - 0.0 (°C) / 32 (°F)
     - ●
     - ●
     - the minimum value of |br| `roomTemp`_ |br| `changeOverTemp`_, |br| `floorTemp`_
   * - envirTempMax
     - float
     - `currentTempUnit`_
     - 50.0 (°C) / 120 (°F)
     - ●
     - ●
     - the maximum value of |br| `roomTemp`_ |br| `changeOverTemp`_, |br| `floorTemp`_
   * - envirTempStep
     - float
     - `currentTempUnit`_
     - 0.1 (°C) / 0.5 (°F)
     - ●
     - ●
     - the step value of |br| `roomTemp`_ |br| `changeOverTemp`_, |br| `floorTemp`_

   * - spValueMin
     - float
     - `currentTempUnit`_
     - 5.0 (°C) /  40 (°F)
     - ●
     - ●
     - the minimum value of |br| `spValue`_ |br| `prgSpValueXX`_
   * - spValueMax
     - float
     - `currentTempUnit`_
     - 40.0 (°C) / 104 (°F)
     - ●
     - ●
     - the maximum value of |br| `spValue`_ |br| `prgSpValueXX`_
   * - spValueStep
     - float
     - `currentTempUnit`_
     - 0.5 (°C) / 1.0 (°F)
     - ●
     - ●
     - the step value of |br| `spValue`_ |br| `prgSpValueXX`_

   * - internalOffsetMin
     - float
     - `currentTempUnit`_
     - -5.0 (°C) / -10 (°F)
     - ●
     - ●
     - the minimum value of |br| `internalOffset`_
   * - internalOffsetMax
     - float
     - `currentTempUnit`_
     - 5.0 (°C) /  10 (°F)
     - ●
     - ●
     - the maximum value of |br| `internalOffset`_
   * - internalOffsetStep
     - float
     - `currentTempUnit`_
     - 0.1 (°C) / 0.5 (°F)
     - ●
     - ●
     - the step value of |br| `internalOffset`_

   * - uploadThresholdMin
     - float
     - `currentTempUnit`_
     - 0.2 (°C) / 32 (°F)
     - ●
     - ●
     - the minimum value of |br| `uploadThreshold`_
   * - uploadThresholdMax
     - float
     - `currentTempUnit`_
     - 5.0 (°C) /  41 (°F)
     - ●
     - ●
     - the maximum value of |br| `uploadThreshold`_
   * - uploadThresholdtep
     - float
     - `currentTempUnit`_
     - 0.1 (°C) / 0.5 (°F)
     - ●
     - ●
     - the step value of |br| `uploadThreshold`_

   * - floorTempLimitedMin
     - float
     - `currentTempUnit`_
     - 20.0 (°C) /  68 (°F)
     - 
     - ●
     - the minimum value of |br| `floorTempLimited`_
   * - floorTempLimitedMax
     - float
     - `currentTempUnit`_
     - 5.0 (°C) /  10 (°F)
     - 
     - ●
     - the maximum value of |br| `floorTempLimited`_
   * - floorTempLimitedStep
     - float
     - `currentTempUnit`_
     - 40.0 (°C) / 104 (°F)
     - 
     - ●
     - the step value of |br| `floorTempLimited`_

   * - switchingDiffHeatingMin
     - float
     - `currentTempUnit`_
     - 0.5 (°C) / 1 (°F)
     - ●
     - ●
     - the minimum value of |br| `switchingDiffHeating`_
   * - switchingDiffHeatingMax
     - float
     - `currentTempUnit`_
     - 4.0 (°C) / 8 (°F)
     - ●
     - ●
     - the maximum value of |br| `switchingDiffHeating`_
   * - switchingDiffHeatingStep
     - float
     - `currentTempUnit`_
     - 0.5 (°C) / 1 (°F)
     - ●
     - ●
     - the step value of |br| `switchingDiffHeating`_

   * - switchingDiffCoolingMin
     - float
     - `currentTempUnit`_
     - 0.5 (°C) / 1 (°F)
     - ●
     - ●
     - the minimum value of |br| `switchingDiffCooling`_
   * - switchingDiffCoolingMax
     - float
     - `currentTempUnit`_
     - 4.0 (°C) / 8 (°F)
     - ●
     - ●
     - the maximum value of |br| `switchingDiffCooling`_
   * - switchingDiffCoolingStep
     - float
     - `currentTempUnit`_
     - 0.5 (°C) / 1 (°F)
     - ●
     - ●
     - the step value of |br| `switchingDiffCooling`_

   * - changeOverTempHeatingMin
     - float
     - `currentTempUnit`_
     - 27.0 (°C) / 80 (°F)
     - ●
     - 
     - the minimum value of |br| `changeOverTempHeating`_
   * - changeOverTempHeatingMax
     - float
     - `currentTempUnit`_
     - 40.0 (°C) / 104 (°F)
     - ●
     - 
     - the maximum value of |br| `changeOverTempHeating`_
   * - changeOverTempHeatingStep
     - float
     - `currentTempUnit`_
     - 0.5 (°C) / 1 (°F)
     - ●
     - 
     - the step value of |br| `changeOverTempHeating`_

   * - changeOverTempCoolingMin
     - float
     - `currentTempUnit`_
     - 10.0 (°C) / 50 (°F)
     - ●
     - 
     - the minimum value of |br| `changeOverTempCooling`_
   * - changeOverTempCoolingMax
     - float
     - `currentTempUnit`_
     - 25.0 (°C) / 77 (°F)
     - ●
     - 
     - the maximum value of |br| `changeOverTempCooling`_
   * - changeOverTempCoolingStep
     - float
     - `currentTempUnit`_
     - 0.5 (°C) / 1 (°F)
     - ●
     - 
     - the step value of |br| `changeOverTempCooling`_


Client-side attribute (application state)
-------------------------------------------------

fanStatus
^^^^^^^^^^

overrideStatus
^^^^^^^^^^^^^^^

prgNextEnable
^^^^^^^^^^^^^^^

prgNextCtrlMode
^^^^^^^^^^^^^^^^

prgNextDaysTime
^^^^^^^^^^^^^^^

prgNextSetpoint
^^^^^^^^^^^^^^^


.. list-table:: Client-side attribute (application state)
   :widths: auto
   :header-rows: 1

   * - Client-side |br| attribute |br| (application |br| state)
     - Type
     - Unit
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - fanStatus
     - string
     - 
     - "Off", |br| "Low", |br| "Med", |br| "High"
     - ●
     - 
     - 

   * - overrideStatus
     - bool
     - 
     - true, |br| false
     - ●
     - ●
     - see `spValue`_

   * - prgNextEnable
     - bool
     - 
     - true, |br| false
     - ●
     - ●
     - Next program |br| enabled

   * - prgNextCtrlMode
     - string
     - 
     - "On", |br| "Off"
     - ●
     - ●
     - Next program |br| control On/Off

   * - prgNextDaysTime
     - float
     - 
     - 
     - ●
     - ●
     - Next program |br| weekday |br| & time

   * - prgNextSetpoint
     - float
     - `currentTempUnit`_
     - 
     - ●
     - ●
     - Next program |br| set point


Client-side attribute (change by server-side RPC, settings)
------------------------------------------------------------------

tempUnit
^^^^^^^^^^

timeFormat
^^^^^^^^^^

systemMode
^^^^^^^^^^

sensorMode
^^^^^^^^^^

internalOffset
^^^^^^^^^^^^^^^

floorTempLimited
^^^^^^^^^^^^^^^^^

switchingDiffHeating
^^^^^^^^^^^^^^^^^^^^

switchingDiffCooling
^^^^^^^^^^^^^^^^^^^^

adaptiveControl
^^^^^^^^^^^^^^^

forceVent
^^^^^^^^^^

changeOverMode
^^^^^^^^^^^^^^^

changeOverTempHeating
^^^^^^^^^^^^^^^^^^^^^^

changeOverTempCooling
^^^^^^^^^^^^^^^^^^^^^^

.. list-table:: Client-side attribute (change by server-side RPC, settings)
   :widths: auto
   :header-rows: 1

   * - Client-side |br| attribute 
     - Type
     - Unit
     - Min
     - Max
     - Step/ |br| Precision
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - tempUnit
     - string
     - 
     - 
     - 
     - 
     - "°C" / "°F"
     - ●
     - ●
     - Centigrade, Fahrenheit, see |br| `remoteSetTempUnit`_

   * - timeFormat
     - string
     - 
     - 
     - 
     - 
     - "12hours", |br| "24hours"
     - ●
     - ●
     - see `remoteSetTimeFormat`_

   * - systemMode
     - string
     - 
     - 
     - 
     - 
     - "Heat", |br| "Cool"
     - 
     - ●
     - see `remoteSetSystemMode`_

   * - sensorMode
     - string
     - 
     - 
     - 
     - 
     - "Internal", |br| "External", |br| "Combined"
     - 
     - ●
     - see `remoteSetSensorMode`_

   * - internalOffset
     - float
     - `currentTempUnit`_
     - `internalOffsetMin`_
     - `internalOffsetMax`_
     - `internalOffsetStep`_
     - 
     - ●
     - ●
     - Internal Sensor |br| Temperture Offset, see |br| `remoteSetInternalOffset`_

   * - floorTempLimited
     - float
     - `currentTempUnit`_
     - `floorTempLimitedMin`_
     - `floorTempLimitedMax`_
     - `floorTempLimitedStep`_
     - 
     - 
     - ●
     -  floor temperature limited |br| (combined mode), see |br| `remoteSetFloorTempLimited`_

   * - switchingDiffHeating
     - float
     - `currentTempUnit`_
     - `switchingDiffHeatingMin`_
     - `switchingDiffHeatingMax`_
     - `switchingDiffHeatingStep`_
     - 
     - ●
     - ●
     - Switching Differential Heating, see |br| `remoteSetSwitchingDiffHeating`_
   * - switchingDiffCooling
     - float
     - `currentTempUnit`_
     - `switchingDiffCoolingMin`_
     - `switchingDiffCoolingMax`_
     - `switchingDiffCoolingStep`_
     - 
     - ●
     - ●
     - Switching Differential Cooling, see |br| `remoteSetSwitchingDiffCooling`_

   * - adaptiveControl
     - bool
     - 
     - 
     - 
     - 
     - true, |br| false
     - 
     - ●
     - see `remoteSetAdaptiveControl`_

   * - forceVent
     - bool
     - 
     - 
     - 
     - 
     - true, |br| false
     - ●
     - 
     - Force Ventialation, see |br| `remoteSetForceVent`_

   * - changeOverMode
     - string
     - 
     - 
     - 
     - 
     - "Heat", |br| "Cool", |br| "Auto"
     - ●
     - 
     - see `remoteSetChangeOverMode`_

   * - changeOverTempHeating
     - float
     - `currentTempUnit`_
     - `changeOverTempHeatingMin`_
     - `changeOverTempHeatingMax`_
     - `changeOverTempHeatingStep`_
     - 
     - ●
     - 
     - Change Over Temp Heating, see |br| `remoteSetChangeOverTempHeating`_
   * - changeOverTempCooling
     - float
     - `currentTempUnit`_
     - `changeOverTempCoolingMin`_
     - `changeOverTempCoolingMax`_
     - `changeOverTempCoolingStep`_
     - 
     - ●
     - 
     - Change Over Temp Cooling, see |br| `remoteSetChangeOverTempCooling`_



Client-side attribute (change by server-side RPC, control & program)
------------------------------------------------------------------------------

controlMode
^^^^^^^^^^^^

fanMode
^^^^^^^^^

spValue
^^^^^^^^

prgMode
^^^^^^^^^

prgSpTimeXX 
^^^^^^^^^^^^

0 <= XX <= 27, prgSpTime00 ~ prgSpTime27

prgCtrlModeXX 
^^^^^^^^^^^^^^^^

0 <= XX <= 27, prgCtrlMode00 ~ prgCtrlMode27

prgSpValueXX
^^^^^^^^^^^^^

0 <= XX <= 27,  prgSpValue00 ~ prgSpValue27

.. list-table:: Client-side attribute (change by server-side RPC, control & program)
   :widths: auto
   :header-rows: 1

   * - Client-side |br| attribute 
     - Type
     - Unit
     - Min
     - Max
     - Step/ |br| Precision
     - Value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - controlMode
     - string
     - 
     - 
     - 
     - 
     - "Off", |br| "On"
     - ●
     - ●
     - see `remoteSetControlMode`_

   * - fanMode
     - string
     - 
     - 
     - 
     - 
     - "Auto", |br| "Low", |br| "Med", |br| "High"
     - ●
     - 
     - see `remoteSetFanMode`_

   * - spValue
     - float
     - `currentTempUnit`_
     - `spValueMin`_
     - `spValueMax`_
     - `spValueStep`_
     - 
     - ●
     - ●
     - see `remoteSetSpValue`_, |br| see `overrideStatus`_

   * - prgMode
     - string
     - 
     - 
     - 
     - 
     - "No-program", |br| "One-day", |br| "Sun_mon-fri_sat", |br| "Every-day"
     - ●
     - ●
     - see `remoteSetPrgMode`_

   * - prgSpTimeXX
     - string
     - 
     - 
     - 
     - 
     - "hh:mm", |br| eg: "23:50"
     - ●
     - ●
     - see `remoteSetPrgSpTimeXX`_

   * - prgCtrlModeXX
     - string
     - 
     - 
     - 
     - 
     - "On", |br| "Off"
     - ●
     - ●
     - see `remoteSetPrgCtrlModeXX`_

   * - prgSpValueXX
     - float
     - `currentTempUnit`_
     - `spValueMin`_
     - `spValueMax`_
     - `spValueStep`_
     - 
     - ●
     - ●
     - see `remoteSetPrgSpValueXX`_


Server-side RPC
===============

Server-side RPC (remote change client-side attribute)
----------------------------------------------------------------

.. tip::
    * All of these server-side RPC are **one-way**, no response
    * Request format of these server-side RPC: {"**method**":"remoteSetTempUnit", "**params**":"°F"}
    * **params** value see `Client-side attribute (change by server-side RPC, settings)`_ & `Client-side attribute (change by server-side RPC, control & program)`_

remoteSetTempUnit
^^^^^^^^^^^^^^^^^^

remoteSetTimeFormat
^^^^^^^^^^^^^^^^^^^^

remoteSetSystemMode
^^^^^^^^^^^^^^^^^^^

remoteSetSensorMode
^^^^^^^^^^^^^^^^^^^

remoteSetInternalOffset
^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetFloorTempLimited
^^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetSwitchingDiffHeating
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetSwitchingDiffCooling
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetAdaptiveControl
^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetForceVent
^^^^^^^^^^^^^^^^^^

remoteSetChangeOverMode
^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetChangeOverTempHeating
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetChangeOverTempCooling
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

remoteSetControlMode
^^^^^^^^^^^^^^^^^^^^

remoteSetFanMode
^^^^^^^^^^^^^^^^^^

remoteSetSpValue
^^^^^^^^^^^^^^^^^

remoteSetPrgMode
^^^^^^^^^^^^^^^^^^

remoteSetPrgSpTimeXX
^^^^^^^^^^^^^^^^^^^^

 0 <= XX <= 27, remoteSetPrgSpTime00 ~ remoteSetPrgSpTime27

remoteSetPrgCtrlModeXX
^^^^^^^^^^^^^^^^^^^^^^

 0 <= XX <= 27, remoteSetPrgCtrlMode00 ~ remoteSetPrgCtrlMode27

remoteSetPrgSpValueXX
^^^^^^^^^^^^^^^^^^^^^^

 0 <= XX <= 27, remoteSetPrgSpValue00 ~ remoteSetPrgSpValue27


.. list-table:: Server-side RPC (remote change client-side attribute)
   :widths: auto
   :header-rows: 1

   * - Server-side RPC |br| (remote change |br| client-side attribute)
     - params |br| value |br| type
     - params |br| value
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - remoteSetTempUnit
     - string
     - "°C" / "°F"
     - ●
     - ●
     - `tempUnit`_

   * - remoteSetTimeFormat
     - string
     - "12hours" |br| "24hours"
     - ●
     - ●
     - `timeFormat`_

   * - remoteSetSystemMode
     - string
     - "Heat" |br| "Cool"
     - 
     - ●
     - `systemMode`_

   * - remoteSetSensorMode
     - string
     - "Internal" |br| "External" |br| "Combined"
     - 
     - ●
     - `sensorMode`_

   * - remoteSetInternalOffset
     - float
     - 
     - ●
     - ●
     - `internalOffset`_

   * - remoteSetFloorTempLimited
     - float
     - 
     - 
     - ●
     - `floorTempLimited`_

   * - remoteSetSwitchingDiffHeating
     - float
     - 
     - ●
     - ●
     - `switchingDiffHeating`_
   * - remoteSetSwitchingDiffCooling
     - float
     - 
     - ●
     - ●
     - `switchingDiffCooling`_

   * - remoteSetAdaptiveControl
     - bool
     - true |br| false
     - 
     - ●
     - `adaptiveControl`_

   * - remoteSetForceVent
     - bool
     - true |br| false
     - ●
     - 
     - `forceVent`_

   * - remoteSetChangeOverMode
     - string
     - "Heat" |br| "Cool" |br| "Auto"
     - ●
     - 
     - `changeOverMode`_

   * - remoteSetChangeOverTempHeating
     - float
     - 
     - ●
     - 
     - `changeOverTempHeating`_
   * - remoteSetChangeOverTempCooling
     - float
     - 
     - ●
     - 
     - `changeOverTempCooling`_


   * - remoteSetControlMode
     - string
     - "Off" |br| "On"
     - ●
     - ●
     - `controlMode`_
   * - remoteSetFanMode
     - string
     - "Auto" |br| "Low" |br| "Med" |br| "High"
     - ●
     - 
     - `fanMode`_
   * - remoteSetSpValue
     - float
     - 
     - ●
     - ●
     - `spValue`_
   * - remoteSetPrgMode
     - string
     - "No-program" |br| "One-day" |br| "Sun_mon-fri_sat" |br| "Every-day"
     - ●
     - ●
     - `prgMode`_
   * - remoteSetPrgSpTimeXX
     - string
     - "hh:mm", |br| eg: "23:50"
     - ●
     - ●
     - remoteSetPrgSpTime00 ~ |br| remoteSetPrgSpTime27, |br| see `prgSpTimeXX`_
   * - remoteSetPrgCtrlModeXX
     - string
     - "On" |br| "Off"
     - ●
     - ●
     - remoteSetPrgCtrlMode00 ~ |br| remoteSetPrgCtrlMode27, |br| see `prgCtrlModeXX`_
   * - remoteSetPrgSpValueXX
     - float
     - 
     - ●
     - ●
     - remoteSetPrgSpValue00 ~ |br| remoteSetPrgSpValue27, |br| see `prgSpValueXX`_


Server-side RPC (remote control)
-------------------------------------------

remoteSetOverrideStatus
^^^^^^^^^^^^^^^^^^^^^^^^

remoteSyncTimeRequest
^^^^^^^^^^^^^^^^^^^^^^^

remoteClearWiFiConfig
^^^^^^^^^^^^^^^^^^^^^^

remoteRebootDevice
^^^^^^^^^^^^^^^^^^^

remoteWiFiFUOTA
^^^^^^^^^^^^^^^

remoteMcuFUOTA
^^^^^^^^^^^^^^

remoteGetMemoryUsage
^^^^^^^^^^^^^^^^^^^^

.. list-table:: Server-side RPC (remote control)
   :widths: auto
   :header-rows: 1

   * - Server-side RPC
     - one-way | |br| two-way
     - Request
     - Response
     - TA652 |br| FC-W
     - TA652 |br| FH-W
     - Memo

   * - remoteSetOverrideStatus
     - one-way
     - {"method":"remoteSetOverrideStatus", |br| "params":{}}
     - 
     - ●
     - ●
     - Assign a `prgSpValueXX` to |br| `spValue`, 0 <= XX <= 27

   * - remoteSyncTimeRequest
     - one-way
     - {"method":"remoteSyncTimeRequest", |br| "params":{}}
     - 
     - ●
     - ●
     -

   * - remoteClearWiFiConfig
     - one-way
     - {"method":"remoteClearWiFiConfig", |br| "params":{}}
     - 
     - ●
     - ●
     -		

   * - remoteRebootDevice
     - one-way
     - {"method":"remoteRebootDevice", |br| "params":{}}
     - 
     - ●
     - ●
     -
				
   * - remoteWiFiFUOTA
     - two-way
     - {"method":"remoteWiFiFUOTA", |br| "params":"http://192.168.1.2/x.img"}
     - {"method":"remoteWiFiFUOTA", |br| "results":{"result":"success"}}, or |br| {"method":"remoteWiFiFUOTA", |br| "results":{"result":"failure", "description":"xxx"}}
     - ●
     - ●
     -		

   * - remoteMcuFUOTA |br| *(NOT implemented)*
     - two-way
     - {"method":"remoteMcuFUOTA", |br| "params":"http://192.168.1.1/y.img"}
     - {"method":"remoteMcuFUOTA", |br| "results":{"result":"success"}}, or |br| {"method":"remoteMcuFUOTA", |br| "results":{"result":"failure", "description":"xxx"}}
     - ●
     - ●
     -

   * - remoteGetMemoryUsage
     - two-way
     - {"method":"remoteGetMemoryUsage", |br| "params":{}}
     - {"method":"remoteGetMemoryUsage", |br| "results":{"iram":123123, "spiram":2345678}}
     - ●
     - ●
     -
