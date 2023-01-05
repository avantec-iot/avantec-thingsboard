********************************
Why Avantec + ThingsBoard?
********************************

Why Avantec?
================

**Avantec Manufacturing Limited** was founded in 1983. Avantec has been a trusted name in the original equipment and design manufacturing (OEM/ODM) industry. In early years, products manufactured and exported by Avantec were highly diversified, ranging from gaming, electronics dictionary, handheld timers, to corded and cordless telephones.

Over the past decade, we have evolved into product design and serve customers around the world with our branded products. Three major product lines are (1) Telecommunication, (2) Education and (3) HVAC (Heating, Ventilating, Air Conditioning and refrigeration).

Avantec's strength lies in delivering high-quality engineering solutions. We provide one-stop-shop service from product design, structural/mechanical engineering design, tooling maintenance, electronics circuit design, firmware and software coding, to quality control and optimization.

HVAC 
---------

* Device Type:
   * Thermostat
   * Humidistat
   * Sensor for smart city
   * DDC (Direct Digital Controller)
   * VAV (Variable Air Volume) Controller
   * ...

* Networking:
   * Classic
   * Modbus
   * BACnet
   * RF 433/868/915
   * Wi-Fi
   * LoRaWAN
   * ...

Why ThingsBoard?
====================

ThingsBoard IoT platform
--------------------------

`ThingsBoard`_ is an open-source IoT platform that enables rapid development, management and scaling of IoT projects. Their goal is to provide the out-of-the-box IoT cloud or on-premises solution that will enable server-side infrastructure for your IoT applications. 

.. _ThingsBoard: https://thingsboard.io/

* 100% Open-source
    ThingsBoard is licensed under Apache License 2.0, so **you can use any it in your commercial products for free**. You can even host it as a SaaS or PaaS solution.

* Telemetry Data Collection
    Collect and store telemetry data in reliable way, surviving network and hardware failures. Access collected data using customizable web dashboards or server-side APIs.

* IoT Rule Engine
    ThingsBoard allows you to create complex Rule Chains to process data from your devices and match your application specific use cases.

* Data Visualization
    Provides 30+ configurable widgets out-of-the-box and ability to create your own widgets using built-in editor. Built-in line-charts, digital and analog gauges, maps and much more.

* Multi-tenancy
    Support multi-tenant installations out-of-the-box. Single tenant may have multiple tenant administrators and millions of devices and customers.

* ThingsBoard Community Edition and ThingsBoard Professional Edition
   ThingsBoard includes ``ThingsBoard CE (Community Edition)`` and ``ThingsBoard PE (Professional Edition)``.

.. note::
   When we developed ``TA652FC-W`` and ``TA652FH-W`` Thermostats, we used ThingsBoard CE.


ThingsBoard IoT Gateway
---------------------------

The `ThingsBoard IoT Gateway`_ is an open-source solution that allows you to integrate devices connected to legacy and third-party systems with ThingsBoard.

.. _ThingsBoard IoT Gateway: https://thingsboard.io/docs/iot-gateway/what-is-iot-gateway/


ThingsBoard Mobile Application
-----------------------------------

The `ThingsBoard Mobile Application`_ is an open-source project based on Flutter. It allows you to build your own IoT mobile application with minimum coding efforts. It is powered by ThingsBoard CE IoT platform.

.. _ThingsBoard Mobile Application: https://thingsboard.io/docs/mobile/

The `ThingsBoard PE Mobile Application`_ is an open-source project based on Flutter. It allows you to build your own advanced IoT mobile application with minimum coding efforts. It is powered by ThingsBoard PE IoT platform.

.. _ThingsBoard PE Mobile Application: https://thingsboard.io/products/mobile-pe/


What is Avantec + ThingsBoard?
================================

Avantec Extension
-----------------

We provide :doc:`/avantec/avantec-widgets` and :doc:`/avantec/avantec-dashboards` based on ThingsBoard IoT platform for demonstration.

Of course, you can also customize your own Web UI and Mobile Application based on them.


Avantec Devices
-----------------

TA652FC-W
^^^^^^^^^^^

* 2 pipe Fan Coil Wi-Fi Thermostat. 
* Firmware ID: ``TA652FC-W-TB``.

.. image:: /_static/device/ta652fc-w/ta652fc-w.png
   :width: 30%
   :align: center


TA652FH-W
^^^^^^^^^^^

* Floor Heating Wi-Fi Thermostat. 
* Firmware ID: ``TA652FH-W-TB``.

  *Coming soon...*


HA652-W
^^^^^^^^^

   *Coming soon...*

TA640FC-W
^^^^^^^^^^

   *Coming soon...*

TA670-W
^^^^^^^^^

   *Coming soon...*


DL10-W
^^^^^^^^

   *Coming soon...*


CDT022-W
^^^^^^^^^

   *Coming soon...*


.. tip::
   Firmware ID - a hardware device may have several firmwares, which are respectively connected to different software platforms. Firmware ID are used to distinguish these firmwares.