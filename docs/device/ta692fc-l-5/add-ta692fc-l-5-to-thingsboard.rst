************************************
Add TA692FC-L-5 to ThingsBoard
************************************

.. tip:: 

   - This section applies to the situation where you add a TA692FC-L-5 to the ThingsBoard PE. It implement two-way communication between a TA692FC-L-5 and a ThingsBoard PE.
   - Only `ThingsBoard PE <https://thingsboard.io/products/thingsboard-pe/>`_ supports **Platform Integrations** feature.


.. tip:: 

    - If you only need one-way communication from TA692FC-L-5 to ThingsBoard, you can use **chirpstack v3** + **ThingsBoard CE** or **chirpstack v4** + **ThingsBoard CE**.
    - Refer to `ThingsBoard getting started for ChirpStack v3 <https://www.chirpstack.io/project/guides/thingsboard/>`_ and `ThingsBoard Integration for ChirpStack v3 <https://www.chirpstack.io/application-server/integrations/thingsboard/>`_ .
    - Refer to `ThingsBoard getting started for ChirpStack v4 <https://www.chirpstack.io/docs/guides/thingsboard.html>`_ and `ThingsBoard Integration for ChirpStack v4 <https://www.chirpstack.io/docs/chirpstack/integrations/thingsboard.html>`_.


Introduction
=============

.. note::
    The frequency of LoRaWAN device and gateway must match!

.. warning::
    ChirpStack v4, the latest version, doesn't handle downlink data from ThingsBoard PE v3.5.x.

The ChirpStack open-source LoRaWAN Network Server stack provides open-source components for LoRaWAN networks.
After integrating ChirpStack with ThingsBoard, you can connect, communicate, process and visualize data from TA692FC-L-5 thermostat in the ThingsBoard IoT platform.

.. uml::

  caption System Architecture\n\n

   node "\nThingsBoard IoT platform\n" as TBSrv {
   }

   node "\nLoRaWAN Network Server\n(ChirpStack)\n" as LoRaWanNS {
   }

   node "\nLoRaWAN Gateway\n(MTCAP)\n" as LoRaWanGateway {
   }

   node "\nLoRaWAN Device\n(TA692FC-L-5)\n" as LoRaWanDev {
   }

   node "\nServer-side Application\n" as TBApp {
      node "\nWeb UI\n" as TBWebUI {
      }
      node "\nMobile Application\n" as TBMobileApp {
      }
   }

   TBSrv <-left-> LoRaWanNS
   LoRaWanNS <-down-> LoRaWanGateway
   LoRaWanGateway <-down-> LoRaWanDev : LoRaWAN Device API

   TBSrv <-down-> TBApp : REST API, Websocket API


.. list-table::
   :widths: auto
   :header-rows: 1

   * - Item
     - Description
   * - LoRaWAN Device
     - TA692FC-L-5, Frequency 868 MHz*
   * - LoRaWAN Gateway
     - MTCAP-868-041A, Frequency 868 MHz*
   * - LoRaWAN Network Server
     - ChirpStack v3**
   * - LoRaWAN Application Server
     - ThingsBoard PE v3.5.x**


Prerequisites
==============

.. tip:: 

    You need a ChirpStack instance that can be accessed by your ThingsBoard PE instance. 

    - If your ThingsBoard PE instance is installed in a LAN, you may also install a ChirpStack instance in the same LAN. 
    - If your ThingsBoard PE instance is installed in the cloud, you may also install a ChirpStack instance on the corresponding cloud host.


* Obtain the following TA692FC-L-5 LoRaWAN Paramters from your equipment vendor.

    .. list-table:: 
      :widths: auto
      :header-rows: 1

      * - Item
        - Paramter
      * - Model
        - TA692FC-L-5, Frequency 868 MHz
      * - LoRaWAN
        - Class C
      * - EU868 band
        - 868.1MHz ~ 868.5MHz
      * - DevEUI/AppEUI/JoinEUI*
        - *YOUR_DEV_EUI*, *eg: 00:12:BD:FF:FE:02:AD:04*
      * - AppKey/Application Key/Network Key*
        - *YOUR_APP_KEY*, *eg: 72357538782F413F4428472B4B625065*

    **Note:** These parameters are different for every thermostat. 

* Setup the MTCAP-868-041A
    * :ref:`First-Time Setup of Gateway`
    * :ref:`Optional: Firmware Upgrade <MTCAP Firmware Upgrade>`

* Install a ChirpStack v3 instance on
    * :ref:`Amazon AWS <Quick start Amazon AWS Cloud>`, or
    * `Microsoft Azure <https://www.chirpstack.io/project/guides/microsoft-azure/>`_, or
    * `Google Cloud <https://www.chirpstack.io/project/guides/google-cloud-platform/>`_, or
    * `Debian/Ubuntu <https://www.chirpstack.io/project/guides/debian-ubuntu/>`_, or
    * `Docker Compose <https://www.chirpstack.io/project/guides/docker-compose/>`_

* Subscribe or install a ThingsBoard PE instance
    * `Use ThingsBoard Cloud <https://thingsboard.cloud/signup>`_, or
    * `Install your own ThingsBoard PE instance <https://thingsboard.io/docs/user-guide/install/pe/installation-options/>`_


MTCAP configuration
====================

* :ref:`Configuring LoRa Packet Forwarder`.


ChirpStack configuration
=========================

* :ref:`Connect gateway to ChirpStack <Connecting a Gateway>`.

* :ref:`Connect device to ChirpStack <Connecting a Device>`.


Integrating ChirpStack with ThingsBoard PE
==========================================

Refer to `ChirpStack Integration <https://thingsboard.io/docs/user-guide/integrations/chirpstack/>`_.


Importing uplink Converter
--------------------------

**TA692FC-L-5 uplink from ChirpStack** :

.. code:: javascript

  // TODO:...


Importing downlink Converter
----------------------------


.. code:: javascript

  // TODO:...


Get Application API key from ChirpStack
----------------------------------------

* ChirpStack

  * Org.API keys -- Create a API key:

    * API key name: <u>Thingsboard integration</u>
    * API key id: 32aafe54-c268-492b-9157-30903f200859
    * API Key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcGlfa2V5X2lkIjoiMzJhYWZlNTQtYzI2OC00OTJiLTkxNTctMzA5MDNmMjAwODU5IiwiYXVkIjoiYXMiLCJpc3MiOiJhcyIsIm5iZiI6MTY4NjIwMjU5OSwic3ViIjoiYXBpX2tleSJ9.Od17K2ZlAdpN7188jmePAO6TjSZ1GscAReo30rRAmRI

Creating ChirpStack intergration
---------------------------------

* ThingsBoard Server:

  * Integrations +

    * Type: ChirpStack
    * Name: <u>TA692FC-L-5 ChirpStack integration</u>
    * Enable integration: v
    * Debug mode: v (only for debug)
    * Allow create devices or assets
    * Uplink data converter: <u>TA692FC-L-5 uplink from ChirpStack</u>
    * Downlink data converter: <u>TA692FC-L-5 downlink to ChirpStack</u>
    * Base URL: <u>https://thingsboard.cloud</u>
    * HTTP endpoint URL: *https://thingsboard.cloud/api/v1/integrations/chirpstack/127834db-ff11-8a6e-edc6-30da3828f2d7*
    * Application server URL: <u>http://13.48.187.149:8080</u>
    * Applicattion server API Token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcGlfa2V5X2lkIjoiMzJhYWZlNTQtYzI2OC00OTJiLTkxNTctMzA5MDNmMjAwODU5IiwiYXVkIjoiYXMiLCJpc3MiOiJhcyIsIm5iZiI6MTY4NjIwMjU5OSwic3ViIjoiYXBpX2tleSJ9.Od17K2ZlAdpN7188jmePAO6TjSZ1GscAReo30rRAmRI


Importing rule chain to process shared attribute update
--------------------------------------------------------

In order to send Downlink, we use the rule chain to process shared attribute update.
To get fPort and DevEUI from device we have to import rule-chain.

*TODO:....*


Modify the root rule-chain
------------------------------

*TODO:....*


Create integration on ChirpStack Network server stack
-------------------------------------------------------

To create integration on ChirpStack Network server stack, we need to do the following steps:

1. Login to ChirpStack Network server stack user interface (Default login/password - **admin/admin**).
2. We go to the tab **Applications** in the left menu and open our application (our application is named Application).
3. Open the **Integrations** tab and create a **HTTP** integration.
4. Let`s go to the **Integrations** tab in ThingsBoard. Find your ChirpStack integration and click on it. There you can find the HTTP endpoint URL. Click on the icon to copy the url.
5. Fill the fields with endpoint url from ThingsBoard integration: <u>https://thingsboard.cloud/api/v1/integrations/chirpstack/127834db-ff11-8a6e-edc6-30da3828f2d7</u>


validate data
--------------


Synchronize device state using client and shared attribute requests (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*TODO:....*

Control device using shared attributes (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*TODO:....*

visiual data
--------------

Updating Avantec Widgets
^^^^^^^^^^^^^^^^^^^^^^^^

*TODO:....*

Importing Dashboard
^^^^^^^^^^^^^^^^^^^

*TODO:....*

Modify Dashboard
^^^^^^^^^^^^^^^^

*TODO:....*
