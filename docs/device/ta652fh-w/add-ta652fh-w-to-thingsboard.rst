************************************
Add TA652FH-W to ThingsBoard
************************************

.. tip:: 

   - This section applies to the situation where you add TA652FH-W to ThingsBoard Server.
   - If you are adding the first Avantec HVAC device to ThingsBoard Server, please refer to :doc:`/intro/get-started`.


Step 1. Tenant Login
=====================

- Open ThingsBoard Web UI in browser, e.g. http://localhost:8080
- Tenant Administrator login ThingsBoard.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/tenant-login-1.png

Tenant default username and password, refer to :ref:`Some important parameters`.


Step 2. Import Detail Dashboard of TA652FH-W
=================================================

See :ref:`Import TA652FH-W Detail Dashboard <Import TA652FH-W Detail Dashboard>`.


Step 3. Import List Dashboard of TA652FH-W
=================================================

See :ref:`Import TA652FH-W List Dashboard <Import TA652FH-W List Dashboard>`.



.. _Step 4. Provision TA652FH-W device:

Step 4. Provision TA652FH-W device
======================================

Step 4.1 Add device 
---------------------

* **Devices** --> **+** --> **Add new device** --> **Popup  Dialog** --> Input **Name, Label & Description**, select **device profile** --> **Add**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add-device-1.png

.. table::
   :widths: auto

   ===============  =============================================
   Field            Value                
   ===============  =============================================
   Name*            My device name, e.g. TA652FH-W-TB, A8:48:FA:57:D5:20
   Device profile*  **TA652FH-W Thermostat**
   Label            My device label, e.g. Avantec Manufacturing Plant
   Description      My device description, e.g. A Thermostat for floor-heating
   ===============  =============================================

.. note:: 
   The field with * must be filled in.

* Now my device should be listed first, since the table sort devices using the time of the creation by default.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add-device-2.png


.. _add-shared-attributes-of-ta652fh-w-cloudhost:

Step 4.2 Add shared attributes of new device
----------------------------------------------

* **Devices** --> Click *my device* --> **Attributes** --> **Shared attributes** --> **+** --> **Popup Dialog** --> Input Key, Value type & value --> **Add**。

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add-shared-attributes-1.png


Please add the following Shared attributes of **TA652FH-W**:

.. # define a hard line break for HTML
.. |br| raw:: html

   <br/>

.. list-table:: Add shared attributes of TA652FH-W
   :widths: 15, 10, 15, 50
   :header-rows: 1

   * - Key*
     - Value Type*
     - Value*
     - Memo

   * - :ref:`uploadFreq <ta652fc-w-uploadFreq>`
     - Integer
     - 300
     - 5*60. Telemetry per uploadFreq seconds

   * - :ref:`uploadThreshold <ta652fc-w-uploadThreshold>`
     - Double
     - 1.5
     - 1.5°C. If the temprature (Telemetry data) |br| change exceeds it, upload immediately!

   * - :ref:`syncTimeFreq <ta652fc-w-syncTimeFreq>`
     - Integer
     - 86400
     - 24*3600. Sync time per syncTimeFreq seconds

   * - :ref:`timezone <ta652fc-w-timezone>`
     - Integer
     - 480
     - **Please replace with your value**. |br| The time offset from UTC, minutes. |br| For example Hongkong is UTC+8:00 time |br| zone, this offset is 480 minutes (8*60)

   * - :ref:`timeNTPServer <ta652fc-w-timeNTPServer>`
     - String
     - pool.ntp.org
     - SNTP Server URL, e.g. pool.ntp.org, |br| 0.pool.ntp.org, 1.pool.ntp.org, |br| uk.pool.ntp.org, hk.pool.ntp.org, |br| time.nist.gov, …

.. note:: 
   The field with * must be filled in.

*  Now the shared attributes of my device is like:

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add-shared-attributes-2.png


You may also use:
 * `Bulk provisioning`_ to provision multiple devices from a CSV file using UI.
 * `Device provisioning`_ to allow device firmware to automatically provision the device, so you don't need to configure each device manually.
 * `REST API`_ to provision devices and other entities programmatically.

.. _Bulk provisioning: https://thingsboard.io/docs/user-guide/bulk-provisioning
.. _Device provisioning: https://thingsboard.io/docs/user-guide/device-provisioning
.. _REST API: https://thingsboard.io/docs/api


.. _Step 5. Connect TA652FH-W device:

Step 5. Connect TA652FH-W device
=================================

.. _Step 5.1 Copy credentials of new TA652FH-W device:

Step 5.1 Copy credentials of new device
-----------------------------------------

To connect the device you need to get the device credentials first. ThingsBoard supports various device credentials. We recommend using default auto-generated credentials which is access token for this guide.

* **Devices** --> **Manage credentials (icon)** --> **Popup Dialog** --> **Select Access Token**, ``Ctrl + C``.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/copy-credentials.png

.. tip:: 
   The Credentials (Access Token), which you need to use when you're configuring your hardware, for example, *j9JiCkID9E7uE1WhKxnc*, *lMTQLZ7VSRQSD7ls*.


Step 5.2 Connect device to ThingsBoard
---------------------------------------

See :doc:`/device/ta652fh-w/connect-ta652fh-w-to-thingsboard`.


Step 5.3 Publish data to ThingsBoard
---------------------------------------

Now your device has already published telemetry data to ThingsBoard. You should immediately see them in the Device Telemetry Tab:

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/publish-data-to-thingsboard-1.png


Step 6. Assign Device and Dashboards to Customer
=================================================

One of the most important ThingsBoard features is the ability to assign Dashboards to Customers. 
You may assign different devices to different customers. Then, you may create a Dashboard(s) and assign it to multiple customers.
Each customer user will see his own devices and will not be able to see devices or any other data that belongs to a different customer.

Refer to :ref:`Step 7.1 Create customers`, :ref:`Step 7.4 Create customer user` & :ref:`Step 7.5 Activate customer user`.

.. _Step 6.1 Assign dashboards of TA652FH-W to Customer:

Step 6.1 Assign dashboards of TA652FH-W to Customer
----------------------------------------------------

* Assign *Detail dashboard* to Customer: **Dashboards** --> Click **Manage assigned customers** (icon) in *Detail dashboard* line --> **Popup Dialog** --> Select *My New Customer* --> **Update**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/assign-dashboards-to-customer-1.png

* Assign *List dashboard* to Customer: **Dashboards** --> Click **Manage assigned customers** (icon) in *List dashboard* line --> **Popup Dialog** --> Select *My New Customer* --> **Update**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/assign-dashboards-to-customer-2.png

* It's like this now.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/assign-dashboards-to-customer-3.png


.. _Step 6.2 Assign TA652FH-W device to Customer:

Step 6.2 Assign TA652FH-W device to Customer
---------------------------------------------

* **Devices** --> Click **Assign to customers** (icon) in *My New Device* line --> **Popup Dialog** --> Select *My New Customer* --> **Assign**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/assign-device-to-customer-1.png

* It's like this now.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/assign-device-to-customer-2.png


.. _Step 7. Open Dashboards of TA652FH-W:

Step 7. Open Dashboards of TA652FH-W
=====================================

* You are logged in as a Customer User or a Tenant user.

* **Dashboards** --> click *my list dashboard*

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/open-dashboard-1.png

* Select my device --> **Settings** (icon)

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/open-dashboard-2.png

* Switch page --> Operation

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/open-dashboard-3.png

See :doc:`/device/ta652fh-w/ta652fh-w-demo-dashboards-usage`.

Your feedback
==============

Don't hesitate to star Avantec on `github`_ to help us spread the word.

.. _github: https://github.com/avantec-iot/avantec-thingsboard
