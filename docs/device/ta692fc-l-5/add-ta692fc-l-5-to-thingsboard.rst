************************************
Add TA692FC-L-5 to ThingsBoard
************************************

.. tip:: 

   - This section applies to the situation where you add TA692FC-L-5 to ThingsBoard PE.
   - Only `ThingsBoard PE <https://thingsboard.io/products/thingsboard-pe/>`_ supports **Platform Integrations** feature.
   - Use `ThingsBoard Cloud <https://thingsboard.cloud/signup>`_ or `install <https://thingsboard.io/docs/user-guide/install/pe/installation-options/>`_ your own ThingsBoard PE platform instance.


Introduction
=============

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

.. note::
    The frequency of LoRaWAN device and gateway must match!

.. warning::
    ChirpStack v4, the latest version, doesn't handle downlink data from ThingsBoard PE v3.5.x.


Prerequisites
-------------

* MTCAP upgrade -------------------------------------------------------------------
* Install ChirpStack v3
* Subscribe or install ThingsBoard PE 


MTCAP configuration
====================

TA692FC-L-5 thermostat 上电......



ChirpStack configuration
=========================

xxxx
------

Connect device to ChirpStack
-----------------------------


Check data on ChirpStack
------------------------


Integrating ChirpStack with ThingsBoard PE
==========================================

xxxx
------

Check data on ThingsBoard
--------------------------

Synchronize device state using client and shared attribute requests (Optional)
------------------------------------------------------------------------------

Control device using shared attributes (Optional)
--------------------------------------------------

Dashboard
==========

Conclusion
==========


adfasd
===========




LoRaWAN Device - TA692FC-L-5
=============================

This article takes ``TA692FC-L-5`` as an example to illustrate.

Obtain the following parameters from your equipment vendor.

.. # define a hard line break for HTML
.. |br| raw:: html

   <br/>

.. list-table:: TA692FC-L-5 LoRaWAN Paramters
   :widths: auto
   :header-rows: 1

   * - Item
     - Paramter
   * - Model
     - TA692FC-L-5-868
   * - LoRaWAN
     - Class C
   * - EU868 band
     - 868.1MHz ~ 868.5MHz
   * - DevEUI/AppEUI/JoinEUI*
     - *YOUR_DEV_EUI*, *eg: 00:12:BD:FF:FE:02:AD:04*
   * - AppKey/Application Key/Network Key*
     - *YOUR_APP_KEY*, *eg: 72357538782F413F4428472B4B625065*

**Note:** These parameters are different for every thermostat. 


LoRaWAN Gateway - MultiTech Conduit AP (MTCAP)
==============================================


Configuration
---------------

.. list-table:: MTCAP Paramters
   :widths: auto
   :header-rows: 1

   * - Item
     - Paramter
   * - Model
     - MTCAP-868-041A
   * - IteGateway ID (EUI64)*
     - *YOUR_GATEWAY_ID*, *eg: 0080000000020E0B*
   * - LoRa Mode
     - Packet-forwarder
   * - Channel Plan
     - EU868
   * - 
     - 
   * - Server Address
     - *YOUR_CHIRPSTACK_SERVER_IP, eg: 13.48.187.149*

**Note:** These parameters are different for every gateway.


基它操作见 《Application Note - Configuring mDot with Conduit AP using LoRa - S000812》 



LoRaWAN Network Server - ChirpStack v3
======================================

Prerequisites - Only for AWS EC2
--------------------------------------

* Application and OS Images (Amazon Machine Image)

  * Amazon Machine Image (AMI): Ubuntu Server 20.04 LTS (HVM), SSD Volume Type
  * Architecture: 64-bit (x86)

* Instance type : t3.micro, Family: t3, 2 vCPU, 1 GiB Memory, Current generation: true
* Key pair: ...
* Network settings

  * VPC: ...
  * Subnet: ...
  * Auto-assign public IP: Enable
  * Firewall (security groups): Create security group

    * Security group: ...
    * Inbound security groups rules:

      * ssh
      * https
      * 8080, tcp, http
      * 1700, udp, LoRaWAN uplink

* Configure storage

  * 1 x 8 GiB, Volume type: gp2, Root volume (Not encrypted)


Install ChirpStack Gateway Bridge & ChirpStack v3 - Quickstart Debian / Ubuntu
-------------------------------------------------------------------------------

Refer `Quickstart Debian or Ubuntu <https://www.chirpstack.io/project/guides/debian-ubuntu/>`_.

Install dependencies
^^^^^^^^^^^^^^^^^^^^^

.. code:: bash

  # Install dependencies
  sudo apt update
  sudo apt install mosquitto mosquitto-clients redis-server redis-tools postgresql


Setup PostgreSQL databases and users
######################################

.. code:: bash

  # Setup PostgreSQL databases and users
  sudo -u postgres psql


.. code:: psql

  -- psql operation

  -- set up the users and the passwords
  -- (note that it is important to use single quotes and a semicolon at the end!)
  create role chirpstack_as with login password 'dbpassword';
  create role chirpstack_ns with login password 'dbpassword';

  -- create the database for the servers
  create database chirpstack_as with owner chirpstack_as;
  create database chirpstack_ns with owner chirpstack_ns;

  -- change to the ChirpStack Application Server database
  \c chirpstack_as

  -- enable the pq_trgm and hstore extensions
  -- (this is needed to facilitate the search feature)
  create extension pg_trgm;
  -- (this is needed to store additional k/v meta-data)
  create extension hstore;

  -- exit psql
  \q



Setup ChirpStack software repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: bash

  # Setup ChirpStack software repository
  sudo apt install apt-transport-https dirmngr
  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00
  sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list
  sudo apt update


Install ChirpStack Gateway Bridge
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: bash

  # Install ChirpStack Gateway Bridge
  sudo apt install chirpstack-gateway-bridge


log output:


.. code::

  ----------------------------------------------------------
  The configuration file is located at:
  /etc/chirpstack-gateway-bridge/chirpstack-gateway-bridge.toml

  Some helpful commands for chirpstack-gateway-bridge:
  Start:
  $ sudo systemctl start chirpstack-gateway-bridge
  
  Restart:
  $ sudo systemctl restart chirpstack-gateway-bridge

  Stop:
  $ sudo systemctl stop chirpstack-gateway-bridge

  Display logs:
  $ sudo journalctl -f -n 100 -u chirpstack-gateway-bridge
  ----------------------------------------------------------

The configuration file is located at ``/etc/chirpstack-gateway-bridge/chirpstack-gateway-bridge.toml``. The default configuration is sufficient for this guide.

.. code:: bash

  # start chirpstack-gateway-bridge
  sudo systemctl start chirpstack-gateway-bridge

  # start chirpstack-gateway-bridge on boot
  sudo systemctl enable chirpstack-gateway-bridge


Install ChirpStack Network Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: bash
  
  # Installing the ChirpStack Network Server
  sudo apt install chirpstack-network-server


log output:


.. code::

  -----------------------------------------------------
  The configuration file is located at:
  /etc/chirpstack-network-server/chirpstack-network-server.toml

  Some helpful commands for chirpstack-network-server:
  Start:
  $ sudo systemctl start chirpstack-network-server

  Restart:
  $ sudo systemctl restart chirpstack-network-server

  Stop:
  $ sudo systemctl stop chirpstack-network-server
  
  Display logs:
  $ sudo journalctl -f -n 100 -u chirpstack-network-server
  -------------------------------------------------------


The configuration file is located at ``/etc/chirpstack-network-server/chirpstack-network-server.toml`` and must be updated to match the database and band configuration. See below two examples for the EU868 and US915 band.  For more information about all the ChirpStack Network Server configuration options, see `here <https://www.chirpstack.io/project/guides/debian-ubuntu/#installing-the-chirpstack-network-server>`_ or `ChirpStack Network Server configuration <https://www.chirpstack.io/network-server/install/config/>`_.


.. code:: bash
  
  # start chirpstack-network-server
  sudo systemctl start chirpstack-network-server

  # start chirpstack-network-server on boot
  sudo systemctl enable chirpstack-network-server

  # Print the ChirpStack Network Server log-output:
  # sudo journalctl -f -n 100 -u chirpstack-network-server




EU868 configuration example
############################

.. code:: toml

  [general]
  log_level=4

  [postgresql]
  dsn="postgres://chirpstack_ns:dbpassword@localhost/chirpstack_ns?sslmode=disable"

  [network_server]
  net_id="000000"

    [network_server.band]
    # name="EU_863_870"
    name="EU868"

    [[network_server.network_settings.extra_channels]]
    frequency=867100000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867300000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867500000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867700000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867900000
    min_dr=0
    max_dr=5



Installing ChirpStack Application Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: bash

  # Installing ChirpStack Application Server
  sudo apt install chirpstack-application-server


log output:


.. code::

  -------------------------------------------------------
  The configuration file is located at:
  /etc/chirpstack-application-server/chirpstack-application-server.toml

  Some helpful commands for chirpstack-application-server:
  Start:
  $ sudo systemctl start chirpstack-application-server

  Restart:
  $ sudo systemctl restart chirpstack-application-server

  Stop:
  $ sudo systemctl stop chirpstack-application-server

  Display logs:
  $ sudo journalctl -f -n 100 -u chirpstack-application-server
  -------------------------------------------------------

The configuration file is located at ``/etc/chirpstack-application-server/chirpstack-application-server.toml`` and must be updated to match the database configuration. See below a configuration example which matches the database which we have created in one of the previous steps. 

.. code:: toml

  [general]
  log_level=4

  [postgresql]
  dsn="postgres://chirpstack_as:dbpassword@localhost/chirpstack_as?sslmode=disable"

    [application_server.external_api]
    jwt_secret="M9LoHX3wPQlcB2ziakV6qs/F2vLOvkAtrRv1yTu5Kks="


Note: you must replace the ``jwt_secret`` with a secure secret! You could use the command ``openssl rand -base64 32`` to generate a random secret.


.. code:: bash

  # start chirpstack-application-server
  sudo systemctl start chirpstack-application-server

  # start chirpstack-application-server on boot
  sudo systemctl enable chirpstack-application-server

  # Print the ChirpStack Application Server log-output:
  # sudo journalctl -f -n 100 -u chirpstack-application-server


Connecting a Gateway
--------------------

<https://www.chirpstack.io/project/guides/connect-gateway/>


Option: Adding a Network Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Network-servers** -->  **+Add**  --> Type some parameters --> **ADD NETWORK-SERVER**

* General

  * Network-server name: localhost network server
  * Network-server server: localhost:8000



Option: Creating a Service-profile
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Service-profiles** -->  **+Create**  --> Type some parameters --> **CREATE SERVICE-PROFILE**

* General

  * Service-profile name: localhost service profile 
  * Network-server name: localhost network server
  * Add gateway meta-data: Enable


Adding a gateway
^^^^^^^^^^^^^^^^^

**Service-profiles** -->  **+Create**  --> Type some parameters --> **CREATE SERVICE-PROFILE**

Navigate to **Gateways** in the web-interface, and click **+Create** and complete the form. Make sure that the **Gateway ID** field is equal to the Gateway ID of your gateway. If this value is incorrectly configured, data received by your gateway will be rejected.

* General

  * Name: <u>Headquarters-Gateway</u>
  * Description: <u>MTCAP-868-041A</u>
  * Gateway ID (EUI64): <u>`0080000000020E0B`</u> (Device surface)
  * Network-server name: localhost network server
  * Service-profile name: localhost service profile 
  * Stats interval (secs): 30


Connecting a device
------------------------

<https://www.chirpstack.io/project/guides/connect-device/>

Option: Adding a Device profile
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


* Name: <u>TA692FC-L-5-868 Thermostat</u>
* Network-server: localhost network server
* Region: EU868
* LoRaWAN MAC version: LoRaWAN 1.0.3
* LoRaWAN Regional parameters revision: A
* ADR algorithm: Default ADR algorithm (LoRa only)
* Uplink interval (seconds):  1000
* Device-status request frequency (req/day): 1
* Join (OTAA / ABP): yes, Device supports OTAA
* Supports Class-B: no
* Supports Class-C: yes
* Class-C confirmed downlink timeout (seconds): 300
* Codec:

  * Payload codec: JavaScript functions
  * Codec functions:

  .. code:: JavaScript

    // Decode decodes an array of bytes into an object.
    //  - fPort contains the LoRaWAN fPort number
    //  - bytes is an array of bytes, e.g. [225, 230, 255, 0]
    //  - variables contains the device variables e.g. {"calibration": "3.5"} (both the key / value are of type string)
    // The function must return an object, e.g. {"temperature": 22.5}
    function Decode(fPort, bytes, variables) {
      var dataX = {};
      var fanModeStateMeta = {
        0: "OFF",
        1: "LOW",
        2: "MED",
        3: "HIGH",
        4: "AUTO"
      };
      var systemModeMeta = {
        0: "OFF",
        1: "COOL",
        2: "FAN-ONLY"
      };
      if(fPort==10){
      dataX.roomTemperature = ((bytes[0] << 8) + bytes[1])/10;
      dataX.setTemperature = ((bytes[2] << 8) + bytes[3])/10;
      dataX.coolProportionalOutput = bytes[4]/100;
      dataX.fanMode = fanModeStateMeta[bytes[5]];
      dataX.fanState = fanModeStateMeta[bytes[6]];
      dataX.threshold = bytes[7]/10;
      dataX.systemMode = systemModeMeta[bytes[8]];
      dataX.coolPBand = bytes[9]/10;
      dataX.coolItime = (bytes[10] << 8) + bytes[11];
      dataX.kFactor = bytes[12];
        return {
          data: {
            roomTemperature: dataX.roomTemperature,
            setTemperature: dataX.setTemperature,
            coolProportionalOutput: dataX.coolProportionalOutput,
            fanMode: dataX.fanMode,
            fanState: dataX.fanState,
            threshold: dataX.threshold,
            systemMode: dataX.systemMode,
            coolPBand: dataX.coolPBand,
            coolItime: dataX.coolItime,
            kFactor: dataX.kFactor
          }
        };
      }
    }

  
    // Encode encodes the given object into an array of bytes.
    //  - fPort contains the LoRaWAN fPort number
    //  - obj is an object, e.g. {"temperature": 22.5}
    //  - variables contains the device variables e.g. {"calibration": "3.5"} (both the key / value are of type string)
    // The function must return an array of bytes, e.g. [225, 230, 255, 0]
    function Encode(fPort, obj, variables) {
      return [];
    }


Option: Adding an Application
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Name: <u>TA692FC-L-5-Application</u>
* Description: <u>TA692FC-L-5-868 Thermostat, TA692FC-L-5-915 Thermostat</u>
* Service-profile name: localhost service profile 


Creating a device
^^^^^^^^^^^^^^^^^^^

* Name: <u>Sales-Office</u>
* Description: <u>TA692FC-L-5-868 device</u>
* Device EUI (EUI64): <u>`0012bdfffe02ad04`</u> (Your manufacturer)
* Device profile: <u>*TA692FC-L-5-868 Thermostat*</u>

* Application key: <u>`72357538782F413F4428472B4B625065`</u>  (Your manufacturer)


ThingsBoard integration - only uplink
======================================

<https://www.chirpstack.io/docs/guides/thingsboard.html#thingsboard-integration>

<https://www.chirpstack.io/docs/chirpstack/integrations/thingsboard.html>

* ThingsBoard Server:
  
  * Add a device

    * Device Name:  Sale Office
    * Device Label:  TA692FC-L-5-868 device

  * **Copy access token** of this device.

* ChirpStack

  * Applications/TA692FC-L-5 Appliction/Integrations

    *  ThingsBoard +

       * ThingsBoard server: http://192.168.21.206:8080

  * Applications/TA692FC-L-5 Appliction/Devices

    * <u>Sale Office</u>

      * Configuration

        * Variables + 

          * ``ThingsBoardAccessToken``/*YOUR_ACCESS_TOKEN*


ThingsBoard integration - uplink and downlink
==============================================

<https://thingsboard.io/docs/user-guide/integrations/chirpstack/>


Create Uplink Converter
-----------------------

Importing uplink Converter
--------------------------

**TA692FC-L-5 uplink from ChirpStack** :

.. code:: javascript

  // TODO:...


Create Downlink Converter
---------------------------

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


Create Integration on ThingsBoard Server
----------------------------------------

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

Importing Rule Chain
---------------------

In order to send Downlink, we use the rule chain to process shared attribute update.
To get fPort and DevEUI from device we have to import rule-chain.

**TODO:....**


Configure the root rule-chain
------------------------------

**TODO:....**


Create integration on ChirpStack Network server stack
-------------------------------------------------------

To create integration on ChirpStack Network server stack, we need to do the following steps:

1. Login to ChirpStack Network server stack user interface (Default login/password - **admin/admin**).
1. We go to the tab **Applications** in the left menu and open our application (our application is named Application).
1. Open the **Integrations** tab and create a **HTTP** integration.
1. Let`s go to the **Integrations** tab in ThingsBoard. Find your ChirpStack integration and click on it. There you can find the HTTP endpoint URL. Click on the icon to copy the url.
1. Fill the fields with endpoint url from ThingsBoard integration: <u>https://thingsboard.cloud/api/v1/integrations/chirpstack/127834db-ff11-8a6e-edc6-30da3828f2d7</u>


validate data
--------------

visiual data
--------------

Updating Avantec Widgets
^^^^^^^^^^^^^^^^^^^^^^^^

Importing Dashboard
^^^^^^^^^^^^^^^^^^^

Modify Dashboard
^^^^^^^^^^^^^^^^
