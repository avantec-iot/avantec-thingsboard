Add TA65 to ThingsBoard
==========================

Add devices (TA65 thermostat) to ThingsBoard.

.. tip:: 
   Two devices are added in this section, TA652FC-W-TB and TA652FH-W-TB. You may add only one device, such as TA652FC-W-TB.


Step 1. Login
-------------

- Open your ThingsBoard website in your browser.
- Tenant Administrator login ThingsBoard: tenant@thingsboard.org / tenant.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/tenant_login.png
   :width: 50 %
   
The default user name and password are shown in the following table:

.. table::
   :widths: auto

   ==========  ===========
   Field       Value
   ==========  ===========
   Username    tenant@thingsboard.org
   Password    tenant
   ==========  ===========


Step 2. Add device
------------------

**Devices** --> **+** --> **Add new deivce** --> **Popup  Dialog** --> **Input** --> **Add**.

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

.. _copy-credentials-of-new-device:

Step 3. Copy credentials of new device
--------------------------------------

**Devices** --> **Manage credentials (icon)** --> **Popup Dialog** --> **Copy Access Token** --> **Select Access Token** --> Ctrl + C.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/copy_credentials.png

.. tip:: 
   The Credentials (Access Token), which you need to use when you're configuring your hardware, for example, j9JiCkID9E7uE1WhKxnc, lMTQLZ7VSRQSD7ls.


Step 4. Add shared attributes of new device
-------------------------------------------

**Devices** --> **New device(TA652FC-W-TB or TA652FH-W-TB)** --> **Attributes** --> **Shared attributes** --> **+** --> **Popup Dialog** --> **Inpug Key, Value type & value** --> **Add**。

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add_shared_attributes_of_device.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/shared_attributes_list.png

The following Shared attributes of the two devices, TA652FC-W-TB and TA652FH-W-TB, are identical.

.. _add-shared-attributes-of-new-device-cloudhost:

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


Step 5. Add asset
-----------------

**Note**: You can skip this step if your asset already in ThingsBoard.

**Assets** --> **+** --> **Add new asset** --> **Popup dialog** --> **Input name & asset type** --> **Add**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add_asset.png

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


Step 6. Add device to asset
---------------------------

Add two devices to the Building X: **Assets** --> **Building X** --> **Relations** --> **Direction: From** --> **+** --> **Popup dialog** --> **Input relation type, to entity type & entity list** --> **Add**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add_device_to_asset_a.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/add_device_to_asset_b.png

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


Step 7. Import Avantec Widgets
------------------------------

.. tip:: 
   Avantec_widgets.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported it, you can skip this step.


**Widgets Library** --> **+** --> **Popup dialog** --> **Select File: avantec_widgets.json** --> **Import**.

See :download:`avantec_widgets.json </_static/thingsboard/thingsboard_extension/avantec_widgets.json>`.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/import_widgets_bundle.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/avantec_widgets.png


Step 8. Avantec Dashboard
-------------------------

Step 8.1. Import Avantec Dashboard (Option)
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

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

Step 8.2. Edit Avantec Dashboard
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

.. tip:: 
   Avantec_dashboard.json can only be imported once. If you have already imported it, you do not need and cannot repeat the import.

   If you have already imported avantec_dashboard.json, you may skip this step.

   We can modify it, for example we can modify alias to add a new device.

**Dashboards** --> **Open dashboard(icon)** --> **New Dashboard: Avantec Dashboard** --> **Edit (red icon on the bottom and right)** --> **Edit Dashboard Mode** --> **Entity aliases(icon on the top and right)** --> **Popup dialog: Entity aliases** --> **Edit alias(icon)** --> **Popup dialog: Edit alias** --> **Modify Fileds : ...** --> **Save**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_a.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_b.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_c.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/edit_dashboard_d.png


Step 9. Open Avantec Dashboard
------------------------------

**Dashboards** --> **Open dashboard(icon) in the line of  Avantec Dashboard** --> **New Dashboard: Avantec Dashboard** --> **Click this line of TA652FC-W-TB**.

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/open_dashboard_a.png

.. image:: /_static/device/ta652fc-w/add-ta652fc-w-to-thingsboard/open_dashboard_b.png
