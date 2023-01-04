************************************
Add TA652FC-W to ThingsBoard
************************************

.. tip:: 

   - This section applies to the situation where you add TA652FC-W to ThingsBoard Server.
   - If you are adding the first Avantec HVAC device to ThingsBoard Server, please refer to :doc:`/intro/get-started`.

Step 1. Tenant Login
=====================

- Open ThingsBoard Web UI in browser, e.g. http://localhost:8080
- Tenant Administrator login ThingsBoard.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/tenant-login-1.png

The default user name and password are shown in the following table:

.. table::
   :widths: auto

   ==========  =======================
   Field       Value
   ==========  =======================
   Username    tenant@thingsboard.org
   Password    tenant
   ==========  =======================

Step 2. Import Device Profile
=============================

.. tip:: 
   *A Device Profile file* can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.


* Download :download:`ta652fc_w_thermostat.json </configuration-item/device-profiles/ta652fc_w_thermostat.json>`.

* **Profiles** --> **Device profiles** --> **+** --> **Popup dialog: Import device profile** --> Drag and drop *my deive profile File* --> **Import**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import-device-profile-1.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import-device-profile-2.png

Step 3. Import Dashboards
=========================

Step 3.1 Import Detail Dashboard
--------------------------------

.. tip:: 
   *A Dashboard file* can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.


* Download :download:`ta652fc_w_thermostat__for_mobile_app_.json </configuration-item/dashboards/ta652fc_w_thermostat__for_mobile_app_.json>`.

* **Dashboards** --> **+** --> **Popup dialog: Import dashboard** --> Drag and drop *detail dashboard File* --> **Import**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import-detail-dashboard-1.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import-detail-dashboard-2.png


Step 3.2 Modify Device Profile - Mobile dashboards
---------------------------------------------------

* **Profiles** --> **Device profiles** --> click *my deivce profile* --> **Toggle edit mode** (red icon)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-device-profile-mobile-dashboard-1.png

* Modify *Mobile dashboard* --> **Apply changes** (red icon)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-device-profile-mobile-dashboard-2.png

These values are shown in the following table:

.. table::
   :widths: auto

   ======================= ====================
   Field                   Value
   ======================= ====================
   Mobile dashboard        TA652FC-W Thermostat (For Mobile App)
   ======================= ====================

Step 3.3 Import List Dashboard
---------------------------------

.. tip:: 
   *A Dashboard file* can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.

* Download :download:`ta652fc_w_thermostat_list.json </configuration-item/dashboards/ta652fc_w_thermostat_list.json>`.

* **Dashboards** --> **+** --> **Popup dialog: Import dashboard** --> Drag and drop *list dashboard File* --> **Import**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import-list-dashboard-1.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import-list-dashboard-2.png


Step 3.4 Modify List Dashboard - Action Target dashboard
----------------------------------------------------------

* **Dashboards** --> Click *my list dashboard*

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-list-dashboard-1.png

* **Edit** (red icon on the bottom and right)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-list-dashboard-2.png

* Enter *Edit Dashboard Mode* --> **Edit Widget** (icon)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-list-dashboard-3.png

* **Action** --> **Edit Action** (icon)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-list-dashboard-4.png

* Modify **Target dashboard** --> modify **Target dashboard state** --> **Save**

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-list-dashboard-5.png

These values are shown in the following table:

.. table::
   :widths: auto

   ======================= ====================
   Field                   Value
   ======================= ====================
   Target dashboard        TA652FC-W Thermostat (For Mobile App)
   Target dashboard state  monitor
   ======================= ====================

* **Apply changes** (red icon)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-list-dashboard-6.png

* **Apply changes** (red icon on the bottom and right)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/modify-list-dashboard-7.png


Step 4. Provision device
========================

Step 4.1 Add device 
---------------------

* **Devices** --> **+** --> **Add new deivce** --> **Popup  Dialog** --> **Input**, select **device profile** --> **Add**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add-device-1.png

.. table::
   :widths: auto

   ===============  =============================================
   Field            Device A                 
   ===============  =============================================
   Name*            My device name, e.g. TA652FC-W-TB             
   Device profile*  **TA652FC-W Thermostat**
   Label            My device label, e.g. AVANTEC Headquaters       
   Description      My device descript, e.g. A Thermostat for fan-coil
   ===============  =============================================

.. note:: 
   The field with * must be filled in.

* Now my device should be listed first, since the table sort devices using the time of the creation by default.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add-device-2.png


Step 4.2 Add shared attributes of new device
----------------------------------------------

* **Devices** --> Click *my device* --> **Attributes** --> **Shared attributes** --> **+** --> **Popup Dialog** --> Input Key, Value type & value --> **Add**。

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add-shared-attributes-1.png


Please add the following Shared attributes of **TA652FC-W**:

.. _add-shared-attributes-of-ta652fc-w-cloudhost:

.. table:: Add shared attributes of TA652FC-W
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
                                               | uk.pool.ntp.org, hk.pool.ntp.org, 
                                               | time.nist.gov, …
   ============= ===========  ================ =========================================

.. note:: 
   The field with * must be filled in.

*  Now the shared attributes of my device is like:

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add-shared-attributes-2.png


You may also use:
 * `Bulk provisioning`_ to provision multiple devices from a CSV file using UI.
 * `Device provisioning`_ to allow device firmware to automatically provision the device, so you don't need to configure each device manually.
 * `REST API`_ to provision devices and other entities programmatically.

.. _Bulk provisioning: https://thingsboard.io/docs/user-guide/bulk-provisioning
.. _Device provisioning: https://thingsboard.io/docs/user-guide/device-provisioning
.. _REST API: https://thingsboard.io/docs/api

Step 5. Connect device
=======================

Step 5.1 Copy credentials of new device
-----------------------------------------

**Devices** --> **Manage credentials (icon)** --> **Popup Dialog** --> **Select Access Token**, ``Ctrl + C``.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/copy-credentials.png

.. tip:: 
   The Credentials (Access Token), which you need to use when you're configuring your hardware, for example, *j9JiCkID9E7uE1WhKxnc*, *lMTQLZ7VSRQSD7ls*.


Step 5.2 Connect device to ThingsBoard
---------------------------------------

Refer to :doc:`/device/ta652fc-w/connect-ta652fc-w-to-thingsboard`.


Step 5.3 Publish data to ThingsBoard
---------------------------------------

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/publish-data-to-thingsboard-1.png


Step 6. Assign Device and Dashboards to Customer
=================================================

One of the most important ThingsBoard features is the ability to assign Dashboards to Customers. 
You may assign different devices to different customers. Then, you may create a Dashboard(s) and assign it to multiple customers.
Each customer user will see his own devices and will not be able to see devices or any other data that belongs to a different customer.

Step 6.1 Create customers
--------------------------

//same										Y				R


Step 6.2 Assign dashboards to Customer
--------------------------------------

//步骤一样，不同的型号参数不同		   Y				R(device profile first)


Step 6.3 Assign device to Customer
-----------------------------------

//步骤一样，不同的型号参数不同		   Y				R


Step 6.4 Create customer user
------------------------------

//same										Y				R


Step 6.5 Activate customer user
--------------------------------

//same										Y				R


Step 7. Open Dashboards
=========================

* **Dashboards** --> click *my list dashboard*

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/open-dashboard-1.png

* Select my device --> **Settings** (icon)

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/open-dashboard-2.png

* Switch page --> Operation

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/open-dashboard-3.png

See :doc:`/device/ta652fc-w/ta652fc-w-demo-dashboards-usage`.

Your feedback
==============

Don't hesitate to star Avante on `github`_ to help us spread the word.

.. _github: https://github.com/avantec-iot/avantec-thingsboard
