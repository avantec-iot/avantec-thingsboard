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

We will connect and visualize data from the ``TA652FC-W`` to keep it simple.

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

Please remember the following important parameters, which will be used frequently in the following work:

.. list-table:: Some important parameters
   :widths: auto
   :header-rows: 1

   * - ThingsBoard server
     - Web URI
     - MQTT URI / Cloud Host
     - Default tenant account

   * - Live Demo server
     - https://demo.thingsboard.io/
     - mqtt://demo.thingsboard.io
     -

   * -  ThingsBoard Cloud |br| (Subscription plans)
     - https://thingsboard.cloud/
     - mqtt://mqtt.thingsboard.cloud
     -

   * - Installation
     - local: http://localhost:8080 |br| remote: http://your_server_ip:8080
     - mqtt://your_server_ip
     - username: tenant@thingsboard.org |br| password: tenant |br| See `demo accounts`_

.. # define a hard line break for HTML
.. |br| raw:: html

   <br/>


Step 1. Tenant Login
=====================

- Open your ThingsBoard Web UI in your browser.
- Tenant Administrator login ThingsBoard.

.. image:: /_static/intro/get-started/get-started-step-1-item-1.png

The default user name and password are shown in the following table:

.. table::
   :widths: auto

   ==========  =======================
   Field       Value
   ==========  =======================
   Username    tenant@thingsboard.org
   Password    tenant
   ==========  =======================


Step 2. Import Avantec Widgets
==============================

.. tip:: 
   Avantec_widgets.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.


**Widgets Library** --> **+** --> **Popup dialog** --> **Select File: avantec_widgets.json** --> **Import**.

See :download:`avantec_widgets.json </_static/thingsboard/thingsboard_extension/avantec_widgets.json>`.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import_widgets_bundle.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/avantec_widgets.png

See :doc:`/avantec/avantec-widgets`.


Step 3. Create device profile
==============================


Step 4. Import Dashboards
=========================

Step 4.1 Import Dashboards
---------------------------

.. tip:: 
   Avantec_dashboard.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.

**Dashboards** --> **+** --> **Popup dialog: Import dashboard** --> **Select File: avantec_dashboard.json** --> **Import** --> **Popup dialog: Configure aliases used by imported dashboard** --> **Edit alias(icon)** --> **Popup dialog: Edit alias** --> **Input Fileds : ...** --> **Save**.

See :download:`avantec_dashboard.json </_static/thingsboard/thingsboard_extension/avantec_dashboard.json>`.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import_dashboard_a.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import_dashboard_b.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import_dashboard_c.png

.. table::
   :widths: auto

   ============================== =====================
   Field                          Value
   ============================== =====================
   Alias name*:                   Thermostats
   Resolve as multiple entities*  TRUE
   Filter type*                   Device search query
   Type*                          Asset
   Asset*                         Building X
   Relation type*                 Contains
   Device types*                  TA652FC-W-TB, TA652FH-W-TB
   ============================== =====================

Step 4.2 Edit Dashboards
--------------------------

.. tip:: 
   Avantec_dashboard.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported avantec_dashboard.json, you may skip this step.

   We can modify it, for example we can modify alias to add a new device.

**Dashboards** --> **Open dashboard(icon)** --> **New Dashboard: Avantec Dashboard** --> **Edit (red icon on the bottom and right)** --> **Edit Dashboard Mode** --> **Entity aliases(icon on the top and right)** --> **Popup dialog: Entity aliases** --> **Edit alias(icon)** --> **Popup dialog: Edit alias** --> **Modify Fileds : ...** --> **Save**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_a.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_b.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_c.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_d.png

See :doc:`/avantec/avantec-dashboards`.


Step 5. Provision device
========================

Step 5.1 Add device
---------------------

For simplicity, we will provision the device manually using the UI.

* Open the Devices page.

.. image:: /_static/intro/get-started/get-started-step-2-item-1.png

* Click on the "+" icon in the top right corner of the table and then select "Add new device".

.. image:: /_static/intro/get-started/get-started-step-2-item-2.png

* Input device name. For example, "My New Device". No other changes required at this time. Click "Add" to add the device.

.. image:: /_static/intro/get-started/get-started-step-2-item-3.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add_devices_a.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add_devices_b.png

.. table::
   :widths: auto

   ============  =========================     ==========
   Field         Device A                      Device B
   ============  =========================     ==========
   Name*         TA652FC-W-TB                    TA652FH-W-TB
   Device type*  TA652FC-W-TB                    TA652FH-W-TB
   Label         AVANTEC Headquaters           Avantec Manufacturing Plant
   Description   A Thermostat for fan-coil     A Thermostat for floor-heating
   ============  =========================     ==========

.. note:: 
   The field with * must be filled in.


* Now your device should be listed first, since the table sort devices using the time of the creation by default.

.. image:: /_static/intro/get-started/get-started-step-2-item-4.png

You may also use:
 * `Bulk provisioning`_ to provision multiple devices from a CSV file using UI.
 * `Device provisioning`_ to allow device firmware to automatically provision the device, so you don't need to configure each device manually.
 * `REST API`_ to provision devices and other entities programmatically.

.. _Bulk provisioning: https://thingsboard.io/docs/user-guide/bulk-provisioning
.. _Device provisioning: https://thingsboard.io/docs/user-guide/device-provisioning
.. _REST API: https://thingsboard.io/docs/api

Step 5.2 Add shared attributes of new device
----------------------------------------------

**Devices** --> **New device(TA652FC-W-TB or TA652FH-W-TB)** --> **Attributes** --> **Shared attributes** --> **+** --> **Popup Dialog** --> **Inpug Key, Value type & value** --> **Add**。

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add_shared_attributes_of_device.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/shared_attributes_list.png

The following Shared attributes of the two devices, TA652FC-W-TB and TA652FH-W-TB, are identical.

.. .. _add-shared-attributes-of-new-device-cloudhost:

.. table:: Add shared attributes of new device
   :widths: 15, 10, 15, 50

   ============= ===========  ================ =========================================
   Key*          Value Type*  Value*                     Memo
   ============= ===========  ================ =========================================
   cloudHost     String       | mqtt://\       | **Please replace THINGSBOARD_IP** 
                              | THINGSBOARD_IP | **with your value**.
                                               | This ThingsBoard Server's MQTT URL, 
                                               | It must begin with "MQTT ://", such as
                                               | mqtt://192.168.21.222
   uploadFreq    Integer      120              Telemetry per uploadFreq seconds
   syncTimeFreq  Integer      1800             Sync time per syncTimeFreq seconds
   timezone      Integer      480              | **Please replace with your value**.
                                               | The time offset from UTC, minutes.
                                               | For example Hongkong is UTC+8:00 time 
                                               | zone, this offset is 480 minutes (8*60)
   timeNTPServer String       pool.ntp.org     | SNTP Server URL, eg: pool.ntp.org, 
                                               | 0.pool.ntp.org, 1.pool.ntp.org, 
                                               | time.nist.gov, …
   ============= ===========  ================ =========================================

.. note:: 
   The field with * must be filled in.


Step 6. Connect device
=======================

.. _copy-credentials-of-new-device:

Step 6.1 Copy credentials of new device
-----------------------------------------

To connect the device you need to get the device credentials first. ThingsBoard supports various device credentials. We recommend using default auto-generated credentials which is access token for this guide.

* Click on the device row in the table to open device details

.. image:: /_static/intro/get-started/get-started-step-3-2-item-1.png

* Click "Copy access token". Token will be copied to your clipboard. Save it to a safe place.

.. image:: /_static/intro/get-started/get-started-step-3-2-item-2.png
.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/copy_credentials.png

.. tip:: 
   The Credentials (Access Token), which you need to use when you're configuring your hardware, for example, *j9JiCkID9E7uE1WhKxnc*, *lMTQLZ7VSRQSD7ls*.


Step 6.2 Connect device to ThingsBoard
---------------------------------------

Refer to :doc:`/device/ta652fc-w/connect-ta652fc-w-to-thingsboard`.


Step 6.3 publish data to ThingsBoard 
---------------------------------------

Now your device has already published telemetry data to thingsboard. You should immediately see them in the Device Telemetry Tab:

* Click on the device row in the table to open device details

.. image:: /_static/intro/get-started/get-started-step-3-4-item-1.png

* Navigate to the telemetry tab.

.. image:: /_static/intro/get-started/get-started-step-3-4-item-2.png


Step 7. Assign Device and Dashboards to Customer
================================================

One of the most important ThingsBoard features is the ability to assign Dashboards to Customers. 
You may assign different devices to different customers. Then, you may create a Dashboard(s) and assign it to multiple customers.
Each customer user will see his own devices and will not be able to see devices or any other data that belongs to a different customer.

Step 7.1 Create customers
--------------------------

Let's create a customer with title "My New Customer". Please see instruction below:

* Navigate to the Customers page.

.. image:: /_static/intro/get-started/get-started-step-6-1-item-1.png

* Click the "+" sign to add a customer.

.. image:: /_static/intro/get-started/get-started-step-6-1-item-2.png

* Add customer title and click "Add".

.. image:: /_static/intro/get-started/get-started-step-6-1-item-3.png

Step 7.2 Assign dashboards to Customer
--------------------------------------

Let's share our dashboard with the Customer. The Customer users will have read-only access to the Dashboard. 

* Open Dashboards. Click "Manage assigned customers".

.. image:: /_static/intro/get-started/get-started-step-6-3-item-1.png

* Select "My New Customer" and click "Update".

.. image:: /_static/intro/get-started/get-started-step-6-3-item-2.png

Step 7.3 Assign device to Customer
-----------------------------------

Let's assign device to the Customer. The Customer users will have ability to read and write telemetry and send commands to devices. 

* Open Devices page. Click "Assign to customer" for *"My New Device"*.

.. image:: /_static/intro/get-started/get-started-step-6-2-item-1.png

* Select *"My New Customer"* and click "Assign".

.. image:: /_static/intro/get-started/get-started-step-6-2-item-2.png

Step 7.4 Create customer user
------------------------------

Finally, let's create a user that will belong to the customer and will have read-only access to the dashboard and the device.
You may optionally configure the dashboard to appear just after user login to the platform web UI.

* Navigate back to the "Customers" page and click the "manage customer users" icon.

.. image:: /_static/intro/get-started/get-started-step-6-4-item-1.png

* Click the "Add user" icon.

.. image:: /_static/intro/get-started/get-started-step-6-4-item-2.png

* Specify email that you will use to login as a customer user and click "Add".

.. image:: /_static/intro/get-started/get-started-step-6-4-item-3.png

* Copy the activation link and save it to a safe place. You will use it later to set the password.

.. image:: /_static/intro/get-started/get-started-step-6-4-item-4.png

* Open user details.

.. image:: /_static/intro/get-started/get-started-step-6-4-item-5.png

* Toggle edit mode.

.. image:: /_static/intro/get-started/get-started-step-6-4-item-6.png

* Select default dashboard and check "Always fullscreen". Apply changes.

.. image:: /_static/intro/get-started/get-started-step-6-4-item-7.png


Step 7.5 Activate customer user
--------------------------------

* Use the activation link to set the password. Click "Create Password". You will automatically login as a customer user.

.. image:: /_static/intro/get-started/get-started-step-6-5-item-1.png

* You have logged in as a Customer User. You may browse the data and acknowledge/clear alarms.

.. image:: /_static/intro/get-started/get-started-step-6-5-item-1.png



Step 8. Open Dashboards
=========================

**Dashboards** --> **Open dashboard(icon) in the line of  Avantec Dashboard** --> **New Dashboard: Avantec Dashboard** --> **Click this line of TA652FC-W-TB**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/open_dashboard_a.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/open_dashboard_b.png


Next steps
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

Don't hesitate to star Avante on `github`_ to help us spread the word.

.. _github: https://github.com/avantec-iot/avantec-thingsboard
