**************
Get Started 
**************

.. tip:: 
   
   - This section applies when no Avantec HVAC device is added to the ThingBoard server.
   - If you add some Avantec HVAC devices to ThingsBoard Server again, please refer to the instructions of each device.
      - :doc:`Add TA652FC-W to ThingsBoard </device/ta652fc-w/add-ta652fc-w-to-thingsboard>`
      - :doc:`Add TA652FH-W to ThingsBoard </device/ta652fh-w/add-ta652fh-w-to-thingsboard>`

Reprinted this article from `Getting Started with ThingsBoard`_, slightly modified.

.. _Getting Started with ThingsBoard: https://thingsboard.io/docs/getting-started-guides/helloworld/


Introduction
==============

The goal of this tutorial is to demonstrate the basic usage of the most popular Avantec HVAC device and ThingsBoard features. 
You will learn how to:

* Connect devices to ThingsBoard;
* Import real-time end-user dashboards.

We will connect and visualize data from a Avantec HVAC device to keep it simple.

Refer to `Getting Started with ThingsBoard`_ to get support for the following features:

* Define thresholds and trigger alarms;
* Push notifications about new alarms over email, SMS or other systems.


Prerequisites
================

You will need to have ThingsBoard server up and running. 

* The easiest way is to use `Live Demo server`_.
* Or `ThingsBoard Cloud`_.
* The alternative option is to install ThingsBoard using :doc:`/thingsboard/thingsboard-installation-options`. 
   * **Windows** users should follow this `guide`_. 
   * **Linux** users that have docker installed should execute the following commands:

   .. code:: bash

      mkdir -p ~/.mytb-data && sudo chown -R 799:799 ~/.mytb-data
      mkdir -p ~/.mytb-logs && sudo chown -R 799:799 ~/.mytb-logs
      docker run -it -p 9090:9090 -p 7070:7070 -p 1883:1883 -p 5683-5688:5683-5688/udp -v ~/.mytb-data:/data \
      -v ~/.mytb-logs:/var/log/thingsboard --name mytb --restart always thingsboard/tb-postgres

   These commands install ThingsBoard and load demo data and accounts.
   ThingsBoard UI will be available using the URL: http://localhost:8080 . You may use username **tenant@thingsboard.org** and password **tenant**. More info about `demo accounts`_ is available.

.. _Live Demo server: https://demo.thingsboard.io/signup
.. _guide: https://thingsboard.io/docs/user-guide/install/docker-windows/
.. _demo accounts: https://thingsboard.io/docs/samples/demo-account/

.. _ThingsBoard Cloud: https://thingsboard.io/pricing/?section=thingsboard-pe-options&product=thingsboard-cloud


.. _Some important parameters:

Some important parameters
---------------------------

Please remember the following important parameters, which will be used frequently in the following work:

.. list-table:: Some important parameters
   :widths: auto
   :header-rows: 1

   * - ThingsBoard |br| server
     - Web URI
     - Default Tenant Account
     - MQTT URI / Cloud Host

   * - Live Demo |br| server
     - https://demo.thingsboard.io
     -
     - mqtt://demo.thingsboard.io

   * -  ThingsBoard |br| Cloud |br| (Subscription |br| plans)
     - https://thingsboard.cloud
     -
     - mqtt://mqtt.thingsboard.cloud

   * - Installation
     - local:  |br|  http://localhost:8080 |br| remote:  |br|  http://your_server_ip:8080
     - username:  |br|  tenant@thingsboard.org |br| password: tenant |br| See `demo accounts`_
     - mqtt://your_server_ip

.. # define a hard line break for HTML
.. |br| raw:: html

   <br/>


Step 1. Tenant Login
=====================

- Open ThingsBoard Web UI in browser, e.g. http://localhost:8080
- Tenant Administrator login ThingsBoard.

.. image:: /_static/intro/get-started/tenant-login-1.png

Tenant default username and password, refer to :ref:`Some important parameters`.


Step 2. Import Avantec Widgets
==============================

* See :ref:`Import Avantec Widgets <Import Avantec Widgets>`.

Step 3. Import device profile
=============================

* See :ref:`Import Device Profile of TA652FC-W Thermostat <Import Device Profile of TA652FC-W Thermostat>`, or
* See :ref:`Import Device Profile of TA652FH-W Thermostat <Import Device Profile of TA652FH-W Thermostat>`.


Step 4. Import Dashboards
=========================

* See :ref:`Import TA652FC-W Detail Dashboard <Import TA652FC-W Detail Dashboard>` and :ref:`Import TA652FC-W List Dashboard <Import TA652FC-W List Dashboard>` , or
* See :ref:`Import TA652FH-W Detail Dashboard <Import TA652FH-W Detail Dashboard>` and :ref:`Import TA652FH-W List Dashboard <Import TA652FH-W List Dashboard>`.

Step 5. Provision device
========================

* See :ref:`Step 4. Provision TA652FC-W device`, or
* See :ref:`Step 4. Provision TA652FH-W device`.

Step 6. Connect device
=======================

* See :ref:`Step 5. Connect TA652FC-W device`, or
* See :ref:`Step 5. Connect TA652FH-W device`.

Step 7. Assign Device and Dashboards to Customer
================================================

One of the most important ThingsBoard features is the ability to assign Dashboards to Customers. 
You may assign different devices to different customers. Then, you may create a Dashboard(s) and assign it to multiple customers.
Each customer user will see his own devices and will not be able to see devices or any other data that belongs to a different customer.

.. _Step 7.1 Create customers:

Step 7.1 Create customers
--------------------------

Let's create a customer with title "My New Customer". Please see instruction below:

* Navigate to the Customers page.

.. image:: /_static/intro/get-started/create-customers-1.png

* Click the "+" sign to add a customer.

.. image:: /_static/intro/get-started/create-customers-2.png

* Add customer title and click "Add".

.. image:: /_static/intro/get-started/create-customers-3.png

Step 7.2 Assign dashboards to Customer
--------------------------------------

Let's share our dashboard with the Customer. The Customer users will have read-only access to the Dashboard. 

* See :ref:`Step 6.1 Assign dashboards of TA652FC-W to Customer`, or
* See :ref:`Step 6.1 Assign dashboards of TA652FH-W to Customer`.

Step 7.3 Assign device to Customer
-----------------------------------

Let's assign device to the Customer. The Customer users will have ability to read and write telemetry and send commands to devices. 

* See :ref:`Step 6.2 Assign TA652FC-W device to Customer`, or
* See :ref:`Step 6.2 Assign TA652FH-W device to Customer`

.. _Step 7.4 Create customer user:

Step 7.4 Create customer user
------------------------------

Finally, let's create a user that will belong to the customer and will have read-only access to the dashboard and the device.
You may optionally configure the dashboard to appear just after user login to the platform web UI.

* Navigate back to the "Customers" page and click the "manage customer users" icon.

.. image:: /_static/intro/get-started/create-customer-user-1.png

* Click the "Add user" icon.

.. image:: /_static/intro/get-started/create-customer-user-2.png

* Specify email that you will use to login as a customer user and click "Add".

.. image:: /_static/intro/get-started/create-customer-user-3.png

* Copy the activation link and save it to a safe place. You will use it later to set the password.

.. image:: /_static/intro/get-started/create-customer-user-4.png

* Open user details.

.. image:: /_static/intro/get-started/create-customer-user-5.png

* (Option) Toggle edit mode.

.. image:: /_static/intro/get-started/create-customer-user-6.png

* (Option) Select default dashboard and check "Always fullscreen". Apply changes.

.. image:: /_static/intro/get-started/create-customer-user-7.png

.. _Step 7.5 Activate customer user:

Step 7.5 Activate customer user
--------------------------------

* Use the activation link to set the password. Click "Create Password". You will automatically login as a customer user.

.. image:: /_static/intro/get-started/activate-customer-user-1.png

* You have logged in as a Customer User. You may browse the data and acknowledge/clear alarms.

.. image:: /_static/intro/get-started/activate-customer-user-2.png


Step 8. Open Dashboards
=========================

* See :ref:`Step 7. Open Dashboards of TA652FC-W`, or
* See :ref:`Step 7. Open Dashboards of TA652FH-W`.

Next Steps
=============

* :doc:`/thingsboard/thingsboard-dashboards` - Customize your Dashboard & Widget.

* :doc:`/thingsboard/thingsboard-rule-engine` - Customize your event processing with Rule engine.

* :doc:`/thingsboard/thingsboard-white-labeling` - Customize your company or product logo with ThingsBoard PE.

* `Platform Integrations`_ - Connect existing NB IoT, LoRaWAN, SigFox and other devices with specific payload formats directly to ThingsBoard platform.

* `Trendz Analytics`_ - Converts the IoT dataset into insights and simplifies the decision-making process.

* :doc:`/thingsboard/thingsboard-mobile-application` - learn how to customize the mobile application.

* :doc:`/thingsboard/thingsboard-mqtt-device-api` | :doc:`/device/ta652fc-w/ta652fc-w-mqtt-api` | :doc:`/device/ta652fh-w/ta652fh-w-mqtt-api` - Connect Avantec HVAC device to your existing IoT platform.

.. _Platform Integrations: https://thingsboard.io/docs/user-guide/integrations/
.. _Trendz Analytics: https://thingsboard.io/docs/trendz/


See also
===========

* `Installation guides`_ - Learn how to setup ThingsBoard on various available operating systems.

* `Connect your device`_ - Learn how to connect devices based on your connectivity technology or solution.

* `Data visualization`_ - These guides contain instructions how to configure complex ThingsBoard dashboards.

* `Data processing & actions`_ - Learn how to use ThingsBoard Rule Engine.

* `IoT Data analytics`_ - Learn how to use rule engine to perform basic analytics tasks.

* `Hardware samples`_ - Learn how to connect various hardware platforms to ThingsBoard.

* `Advanced features`_ - Learn about advanced ThingsBoard features.

.. _Installation guides: https://thingsboard.io/docs/user-guide/install/installation-options
.. _Connect your device: https://thingsboard.io/docs/guides#AnchorIDConnectYourDevice
.. _Data visualization: https://thingsboard.io/docs/guides#AnchorIDDataVisualization
.. _Data processing & actions: https://thingsboard.io/docs/guides#AnchorIDDataProcessing
.. _IoT Data analytics: https://thingsboard.io/docs/guides#AnchorIDDataAnalytics
.. _Hardware samples: https://thingsboard.io/docs/guides#AnchorIDHardwareSamples
.. _Advanced features: https://thingsboard.io/docs/guides#AnchorIDAdvancedFeatures

Your feedback
==============

Don't hesitate to star Avantec on `github`_ to help us spread the word.

.. _github: https://github.com/avantec-iot/avantec-thingsboard
