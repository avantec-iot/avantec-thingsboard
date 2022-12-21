.. Using Avantec HVAC device with ThingsBoard documentation master file, created by
   sphinx-quickstart on Tue Dec 20 10:31:29 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

************************************************
Using Avantec HVAC device with ThingsBoard
************************************************

`Avantec`_ provides some HVAC networking solutions.  A series of HVAC networked devices in these solutions are connected to `ThingsBoard`_ IoT platform through `MQTT`_ protocol.

.. _Avantec: http://www.avantec.com.hk/
.. _ThingsBoard: https://thingsboard.io/
.. _MQTT: https://mqtt.org/

.. uml::
   :align: center

   node "\nThingsBoard IoT platform\n" as TBSrv {
   }

   node "\nAvantec HVAC devices\n" as TBDev {
   }

   node "\nWeb UI\n" as TBWebUI {
   }

   node "\nMobile Application\n" as TBApp {
   }

   TBSrv <-down-> TBDev : MQTT
   TBSrv <-down-> TBWebUI
   TBSrv <-down-> TBApp


.. You can find out more about our all the :doc:`/features` in these pages.


First steps
============

Are you new to Avantec Thermostats or ThingsBoard IoT platform?
Learn about them to help you create fantastic project.

.. toctree::
   :maxdepth: 3
   :caption: First steps

   Why ThingsBoard? </intro/why-thingsboard>
   Why Avantec? </intro/why-avantec>
   What is Avantec + ThingsBoard? </intro/what-is-avantec-thingsboard>
   Get Started </intro/get-started>
   

..   :hidden:


ThingsBoard
=============

Here is an overview about ThingsBoard.

.. toctree::
   :maxdepth: 5
   :caption: ThingsBoard

   Overview </thingsboard/thingsboard-overview>
   Installation </thingsboard/thingsboard-install>
   Customize </thingsboard/thingsboard-customization>
   MQTT Device API </thingsboard/thingsboard-mqtt-device-api>

..   :hidden:

Avantec Extension
==================

Here is an overview about Avantec Customization.

.. toctree::
   :maxdepth: 5
   :caption: Avantec Extension

   Avantec Widgets </avantec/avantec-widgets.rst>
   Avantec Dashboards </avantec/avantec-dashboards.rst>


TA652FC-W Wi-Fi Thermostat
==============================

These references will help you learn more about TA652FC-W Wi-Fi Thermostat, operate it, and even realize your personalized DashBoard.

.. toctree::
   :maxdepth: 5
   :caption: TA652FC-W Wi-Fi Thermostat

   Specification </device/ta652fc-w/ta652fc-w-specification>
   Add to ThingsBoard </device/ta652fc-w/add-ta652fc-w-to-thingsboard>
   Connect to ThingsBoard </device/ta652fc-w/connect-ta652fc-w-to-thingsboard>
   Demo Dashboard </device/ta652fc-w/ta652fc-w-demo-dashboard-usage>
   MQTT Device API </device/ta652fc-w/ta652fc-w-mqtt-api>

..   :hidden:

TA652FH-W Wi-Fi Thermostat
============================

These references will help you learn more about TA652FH-W Wi-Fi Thermostat, operate it, and even realize your personalized DashBoard.

.. toctree::
   :maxdepth: 5
   :caption: TA652FH-W Wi-Fi Thermostat

   Specification </device/ta652fh-w/ta652fh-w-specification>

..   :hidden:

Avantec and the project
=============================

Learn about the project and the company.

.. toctree::
   :maxdepth: 3
   :caption: About Avantec

   avantec
   copyright

..   :hidden:

.. Indices and tables
.. ==================

.. * :ref:`genindex`
.. * :ref:`search`

.. * :ref:`modindex`
