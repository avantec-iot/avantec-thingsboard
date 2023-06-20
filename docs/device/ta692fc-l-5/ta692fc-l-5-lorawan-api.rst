*********************************
TA692FC-L-5 LoRaWAN API
*********************************

.. tip::

  - This section applies to ``TA692FC-L-5``.


Overview
========

.. uml::

   node "\nThingsBoard IoT platform\n" as TBSrv {
   }

   node "\nLoRaWAN Network Server\n" as LoRaWanNS {
   }

   node "\nLoRaWAN Gateway\n" as LoRaWanGateway {
   }

   node "\nTA692FC-L-5\n" as LoRaWanDev {
   }

   node "\nServer-side Application\n" as TBApp {
      node "\nWeb UI\n" as TBWebUI {
      }
      node "\nMobile Application\n" as TBMobileApp {
      }
   }

   TBSrv <-left-> LoRaWanNS
   LoRaWanNS <-down-> LoRaWanGateway
   LoRaWanGateway <-down-> LoRaWanDev : <color:#FF0000> **TA692FC-L-5 LoRaWAN Device API** </color>

   TBSrv <-down-> TBApp : REST API, Websocket API


Payload format in LoRA packet used by TA692FC-L-5
==================================================

Uplink | port 10
-----------------

.. table::
    :widths: auto

    ===== ================================= =============================================== ===========
    Byte	Data	                            Content	                                        Range
    ===== ================================= =============================================== ===========
    0     data.RoomTemperature (High Byte)  Room Temperature(°C) = D_Room_Temperature/10    0 ~ 400
    1     data.RoomTemperature (Low Byte)
    2     data.SetTemperature (High Byte)   Set Temperature(°C) = D_Set_Temperature/10	    50 ~ 350
    3     data.SetTemperature (Low Byte)
    4	    data.CoolProportionalOutput	      Cool Proportional Output : 0-100% 	            0 ~ 100
    5 	  data.FanMode	                    0:OFF 1:LOW 2:MED 3:HIGH 4: AUTO	              0 ~ 4
    6	    data.FanState	                    0:OFF 1:LOW 2:MED 3:HIGH 	                      0 ~ 3
    7	    data.threshold (*)	              Temperature change: 0.2°C ~ 5.0°C	              2 ~ 50
    8	    data.SystemMode	                  0:OFF 1:COOL 2:FAN-ONLY	                        0 ~ 2
    9	    Data.CoolPBand	                  P-Band for Cool : 1.0°C ~ 4.0°C	                10 ~ 40
    10	  Data.CoolItime (High Byte)	        I-Time for Cool : 5 ~ 180	                      5 ~ 180
    11	  Data.CoolItime (Low Byte)		
    12	  Data.Kfactor	                    K-Factor : 1 ~ 9	                              1 ~ 9
    ===== ================================= =============================================== ===========

Downlink | port 90
-------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     data.SetTemperature (High Byte) Set Temperature(°C) = D_Set_Temperature/10  50 ~ 350
    1     data.SetTemperature (Low Byte)		
    2     data.FanMode	                  0:OFF 1:LOW 2:MED 3:HIGH 4:AUTO             0 ~ 4
    3     data.threshold [#f1]_           Temperature change: 0.2°C ~ 5.0°C           2 ~ 50
    4     data.SystemMode	                0:OFF 1:COOL 2:FAN-ONLY                     0 ~ 2
    5     Data.CoolPBand                  P-Band for Cool : 1.0°C ~ 4.0°C             10 ~ 40
    6     Data.CoolItime (High Byte)      I-Time for Cool : 5 ~ 180                   5 ~ 180
    7     Data.CoolItime (Low Byte)		
    8     Data.Kfactor                    K-Factor : 1 ~ 9                            1 ~ 9
    ===== =============================== =========================================== ===========

.. rubric:: Footnotes

.. [#f1] D_update_threshold determines the minimum change in ambient room temp required to trigger a send event i.e. uplink. The range is from 0.2 to 5 centigrade. However, this parameter is limited by another named, “sending interval”, hardcoded 15 seconds.
  
  e.g. if change in temp > 0.2°C, or, fan status change, or user press a button etc., sends uplink immediately


Downlink | port 91
--------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     data.SetTemperature (High Byte) Set Temperature(°C) = D_Set_Temperature/10  50 ~ 350
    1     data.SetTemperature (Low Byte)
    ===== =============================== =========================================== ===========


Downlink | port 92
--------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     data.FanMode	                  0:OFF 1:LOW 2:MED 3:HIGH 4:AUTO             0 ~ 4
    ===== =============================== =========================================== ===========


Downlink | port 93
--------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     data.threshold [#f2]_           Temperature change: 0.2°C ~ 5.0°C           2 ~ 50
    ===== =============================== =========================================== ===========

.. rubric:: Footnotes

.. [#f2] D_update_threshold determines the minimum change in ambient room temp required to trigger a send event i.e. uplink. The range is from 0.2 to 5 centigrade. However, this parameter is limited by another named, “sending interval”, hardcoded 15 seconds.

  e.g. if change in temp > 0.2°C, or, fan status change, or user press a button etc., sends uplink immediately


Downlink | port 94
--------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     data.SystemMode	                0:OFF 1:COOL 2:FAN-ONLY                     0 ~ 2
    ===== =============================== =========================================== ===========


Downlink | port 95
--------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     Data.CoolPBand                  P-Band for Cool : 1.0°C ~ 4.0°C             10 ~ 40
    ===== =============================== =========================================== ===========


Downlink | port 97
--------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     Data.CoolItime (High Byte)      I-Time for Cool : 5 ~ 180                   5 ~ 180
    1     Data.CoolItime (Low Byte)		
    ===== =============================== =========================================== ===========



Downlink | port 95
--------------------

.. table::
    :widths: auto

    ===== =============================== =========================================== ===========
    Byte	Data	                          Content	                                    Range
    ===== =============================== =========================================== ===========
    0     Data.Kfactor                    K-Factor : 1 ~ 9                            1 ~ 9
    ===== =============================== =========================================== ===========