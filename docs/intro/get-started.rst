**************
Get Started 
**************

.. tip:: 
   
   - This section applies to situations where there is no running instance of ThingBoard Server, or no Avantec HVAC device has been added to ThingBoard Server.
   - If you add some Avantec HVAC devies to ThingsBoard Server again, please refer to the instructions of each devies.

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
* Push notifications about new alarms over email, sms or other systems.


Prerequisites
================

You will need to have ThingsBoard server up and running. 

* The easiest way is to use `Live Demo server`_.
* Or `Thingsboard Cloud`_ for thingsboard cloud.
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

.. _Thingsboard Cloud: https://thingsboard.io/pricing/?section=thingsboard-pe-options&product=thingsboard-cloud


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


.. _Step 2. Import Avantec Widgets:

Step 2. Import Avantec Widgets
==============================

.. tip:: 
   Avantec_widgets.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.



* Download :download:`avantec_widgets.json </configuration-item/widgets/avantec_widgets.json>`.

* **Widgets Library** --> **+** --> **Import widgets bundle** --> **Popup dialog: Import widgets bundle** --> Drag and drop **avantec_widgets.json** --> **Import**.

.. image:: /_static/intro/get-started/import-avantec-widgets-1.png

* **Widgets Library** --> click **Avantec widgets**

.. image:: /_static/intro/get-started/import-avantec-widgets-2.png

* All Avantec widgets

.. image:: /_static/intro/get-started/import-avantec-widgets-3.png

See :doc:`/avantec/avantec-widgets`.

Step 3. Import device profile
=============================

* See :ref:`Step 2. Import Device Profile of TA652FC-W`.

Step 4. Import Dashboards
=========================

* See :ref:`Step 3. Import Dashboards of TA652FC-W`.

Step 5. Provision device
========================

* See :ref:`Step 4. Provision TA652FC-W device`.


Step 6. Connect device
=======================

* See :ref:`Step 5. Connect TA652FC-W device`.

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

See :ref:`Step 6.1 Assign dashboards of TA652FC-W to Customer`.


Step 7.3 Assign device to Customer
-----------------------------------

Let's assign device to the Customer. The Customer users will have ability to read and write telemetry and send commands to devices. 

See :ref:`Step 6.2 Assign TA652FC-W device to Customer`.


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

* See :ref:`Step 7. Open Dashboards of TA652FC-W`.


Next Steps
=============

* :doc:`/thingsboard/thingsboard-dashboards` - Customize your Dashboard & Widget.

* :doc:`/thingsboard/thingsboard-rule-engine` - Customize your event processing with Rule engine.

* :doc:`/thingsboard/thingsboard-white-labeling` - Customize your company or product logo with ThingsBoard PE.

* `Platform Integrations`_ - Connect existing NB IoT, LoRaWAN, SigFox and other devices with specific payload formats directly to ThingsBoard platform.

* `Trendz Analytics`_ - Converts the IoT dataset into insights and simplifies the decision-making process.

* `Getting started with ThingsBoard Mobile Application`_ or `Getting started with ThingsBoard PE Mobile Application`_ -  help you set up and run your first IoT mobile app, learn how to customize the app and publish it to Google Play or App Store.

* :doc:`/thingsboard/thingsboard-mqtt-device-api`, :doc:`/device/ta652fc-w/ta652fc-w-mqtt-api` & :doc:`/device/ta652fh-w/ta652fh-w-mqtt-api` - Connect Avantec HVAC device to your existing IoT platform.


.. _Getting started with ThingsBoard Mobile Application: https://thingsboard.io/docs/mobile/getting-started/
.. _Getting started with ThingsBoard PE Mobile Application: https://thingsboard.io/docs/pe/mobile/getting-started/
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
