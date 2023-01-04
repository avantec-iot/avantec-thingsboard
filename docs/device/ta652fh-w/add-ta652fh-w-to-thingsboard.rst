************************************
Add TA652FH-W to ThingsBoard
************************************

.. tip:: 

   - This section applies to the situation where you add TA652FH-W to ThingsBoard Server.
   - If you are adding the first Avantec HVAC device to ThingsBoard Server, please refer to :doc:`/intro/get-started`.



.. tip:: 
   Two devices are added in this section, TA652FC-W-TB and TA652FH-W-TB. You may add only one device, such as TA652FC-W-TB.


Step 1. Tenant Login
=====================

- Open your ThingsBoard Web UI in your browser.
- Tenant Administrator login ThingsBoard.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/tenant-login-1.png

The default user name and password are shown in the following table:

.. table::
   :widths: auto

   ==========  =======================
   Field       Value
   ==========  =======================
   Username    tenant@thingsboard.org
   Password    tenant
   ==========  =======================


Step 2. Create device profile
==============================

Step 3. Import Device Profile & Dashboards
==========================================

Step 3.1 Import Detail Dashboard
--------------------------------

Step 3.2 Import Device Profile
------------------------------

Step 3.2.1 Import Device Profile
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 3.2.2 Modify Device Profile - Mobile dashboards
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 3.3 Import List Dashboard
------------------------------

Step 3.3.1 Import List Dashboard
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 3.3.2 Modify List Dashboard
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 3. Import Dashboards
=========================

Step 3.1 Import Dashboards
---------------------------

.. tip:: 
   Avantec_dashboard.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.

**Dashboards** --> **+** --> **Popup dialog: Import dashboard** --> **Select File: avantec_dashboard.json** --> **Import** --> **Popup dialog: Configure aliases used by imported dashboard** --> **Edit alias(icon)** --> **Popup dialog: Edit alias** --> **Input Fileds : ...** --> **Save**.

See :download:`avantec_dashboard.json </_static/thingsboard/thingsboard_extension/avantec_dashboard.json>`.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/import_dashboard_a.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/import_dashboard_b.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/import_dashboard_c.png

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

Step 3.2 Edit Dashboards
--------------------------

.. tip:: 
   Avantec_dashboard.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported avantec_dashboard.json, you may skip this step.

   We can modify it, for example we can modify alias to add a new device.

**Dashboards** --> **Open dashboard(icon)** --> **New Dashboard: Avantec Dashboard** --> **Edit (red icon on the bottom and right)** --> **Edit Dashboard Mode** --> **Entity aliases(icon on the top and right)** --> **Popup dialog: Entity aliases** --> **Edit alias(icon)** --> **Popup dialog: Edit alias** --> **Modify Fileds : ...** --> **Save**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/edit_dashboard_a.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/edit_dashboard_b.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/edit_dashboard_c.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/edit_dashboard_d.png

See :doc:`/avantec/avantec-dashboards`.

Step 4. Provision device
========================

Step 4.1 Add device 
---------------------

**Devices** --> **+** --> **Add new deivce** --> **Popup  Dialog** --> **Input** --> **Add**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add_devices_a.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add_devices_b.png

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


You may also use:
 * `Bulk provisioning`_ to provision multiple devices from a CSV file using UI.
 * `Device provisioning`_ to allow device firmware to automatically provision the device, so you don't need to configure each device manually.
 * `REST API`_ to provision devices and other entities programmatically.

.. _Bulk provisioning: https://thingsboard.io/docs/user-guide/bulk-provisioning
.. _Device provisioning: https://thingsboard.io/docs/user-guide/device-provisioning
.. _REST API: https://thingsboard.io/docs/api

Step 4.2 Add shared attributes of new device
----------------------------------------------

**Devices** --> **New device(TA652FC-W-TB or TA652FH-W-TB)** --> **Attributes** --> **Shared attributes** --> **+** --> **Popup Dialog** --> **Inpug Key, Value type & value** --> **Add**。

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add_shared_attributes_of_device.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/shared_attributes_list.png

The following Shared attributes of the two devices, TA652FC-W-TB and TA652FH-W-TB, are identical.

.. _add-shared-attributes-of-ta652fh-w-cloudhost:

.. table:: Add shared attributes of TA652FH-W
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


Step 5. Connect device
=======================

Step 5.1 Copy credentials of new device
-----------------------------------------

**Devices** --> **Manage credentials (icon)** --> **Popup Dialog** --> **Copy Access Token** --> **Select Access Token** --> Ctrl + C.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/copy_credentials.png

.. tip:: 
   The Credentials (Access Token), which you need to use when you're configuring your hardware, for example, *j9JiCkID9E7uE1WhKxnc*, *lMTQLZ7VSRQSD7ls*.


Step 5.2 Connect device to ThingsBoard
---------------------------------------

Refer to :doc:`/device/ta652fc-w/connect-ta652fc-w-to-thingsboard`.


Step 5.3 Publish data to ThingsBoard
---------------------------------------

*TODO:*


Step 5.A Add asset
--------------------------

**Note**: You can skip this step if your asset already in ThingsBoard.

**Assets** --> **+** --> **Add new asset** --> **Popup dialog** --> **Input name & asset type** --> **Add**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add_asset.png

.. table::
   :widths: auto

   ============ ============
   Type         Assets
   ============ ============
   Name*        Building X
   Asset type*  building
   Label
   Description
   ============ ============

.. note:: 
   The field with * must be filled in.


Step 5.B Add device to asset
--------------------------------

Add two devices to the Building X: **Assets** --> **Building X** --> **Relations** --> **Direction: From** --> **+** --> **Popup dialog** --> **Input relation type, to entity type & entity list** --> **Add**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add_device_to_asset_a.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/add_device_to_asset_b.png

.. table::
   :widths: auto

   ========== ============== ============== ========
   Direction* Relation Type* To entityType* Device*
   ========== ============== ============== ========
   From       Contains       Device         TA652FC-W-TB
   From       Contains       Device         TA652FH-W-TB
   ========== ============== ============== ========

.. note:: 
   The field with * must be filled in.

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

**Dashboards** --> **Open dashboard(icon) in the line of  Avantec Dashboard** --> **New Dashboard: Avantec Dashboard** --> **Click this line of TA652FC-W-TB**.

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/open_dashboard_a.png

.. image:: /_static/device/ta652fh-w/add-ta652fh-w-to-thingsboard/open_dashboard_b.png

Your feedback
==============

Don't hesitate to star Avante on `github`_ to help us spread the word.

.. _github: https://github.com/avantec-iot/avantec-thingsboard
