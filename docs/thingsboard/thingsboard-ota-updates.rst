******************************
Over-the-air firmware updates
******************************

Refer `here`_.

.. _here: https://thingsboard.io/docs/user-guide/ota-updates/


Overview
=========
Since ThingsBoard 3.3, ThingsBoard allows you to upload and distribute over-the-air(OTA) updates to devices. As a tenant administrator, you may upload firmware packages to the OTA repository. Once uploaded, you may assign them to `Device Profile`_ or `Device`_. ThingsBoard will notify devices about the available update and provide a protocol-specific API to download the firmware. The platform tracks status of the update and stores history of the updates. As a platform user, you may monitor the update process using the dashboard.

.. _Device Profile: https://thingsboard.io/docs/user-guide/device-profiles/
.. _Device: https://thingsboard.io/docs/user-guide/ui/devices/

.. image:: /_static/thingsboard/thingsboard-ota-updates/ota-updates-overview-1.png


.. _OTA updates Dashboard:

Dashboard
==========

ThingsBoard provides the summary of the firmware update to monitor and track the firmware update status of your device, such as which devices are updating right now, any boot issues, and which ones have already been updated.

Firmware update monitoring dashboard
-------------------------------------
The dashboard is created automatically for each new tenant that you add to ThingsBoard. You can also download the dashboard JSON `firmwre dashboard <https://github.com/thingsboard/thingsboard/blob/master/application/src/main/data/json/demo/dashboards/firmware.json>`_ and import it for existing tenants.


There you can see a list of all devices with full information about their firmware.

.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-dashboard-1.png
.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-dashboard-2.png

Click the “History of the firmware updates” button next to the device name to learn about the firmware update status of specific device.

.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-status-1.png
.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-status-2.png

Provision OTA package to ThingsBoard repository
================================================

Navigate to the “OTA Updates” menu item to list and upload OTA update packages. Each package consist of:

* Title - the name of your package. You can use different names for production and debug firmware.
* Version - the version of your package. Combination of the title and version must be unique in scope of a tenant.
* Device Profile - each package is compatible with one device profile. We track compatibility to prevent accidental updates of devices with incompatible firmware. Link to a device profile means that device that use this profile may be updated to the current package. However, the update is not triggered, until the user or script :ref:`assigns <Assign OTA package to device profile>` the package to the device profile or device.
* Type - can be either Firmware or Software.
* Checksum algorithm - optional parameter, it is a short name of the checksum algorithm to use.
* Checksum - optional parameter, it's a value of the file checksum. If no checksum provided by the user, server will use SHA-256 algorithm automatically.
* Description - optional text description of the firmware.

.. image:: /_static/thingsboard/thingsboard-ota-updates/ota-updates-provision-package-to-repository-1.png

You can browse the provisioned packages as well as search them by title. Also, you are able to download and delete packages. To open package details, click the table row. Package details allow you to copy package ID and checksum. Also, `Audit logs`_ track information about users who provisioned the firmware.

.. _Audit logs: https://thingsboard.io/docs/user-guide/audit-log/

.. image:: /_static/thingsboard/thingsboard-ota-updates/list-firmware-ce-1.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/list-firmware-ce-2.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/list-firmware-ce-3.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/list-firmware-ce-4.png


All actions listed are also available via `REST API`_.

.. _REST API: https://thingsboard.io/docs/reference/rest-api/


.. _Assign OTA package to device profile:

Assign OTA package to device profile
====================================

You may assign firmware to the device profile to automatically distribute the package to all devices that share the same profile. See screenshots below.

.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-deviceprofile-ce-1.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-deviceprofile-ce-2.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-deviceprofile-ce-3.png

The device profile details will let you choose only compatible OTA update packages (see `provisioning`_ for more info). Device profile may be used by thousands of devices. Assignment of the firmware triggers the :ref:`update process`.

.. _provisioning: https://thingsboard.io/docs/user-guide/ota-updates/?remoteintegrationdockerinstall=mqtt#provision-ota-package-to-thingsboard-repository


.. _Assign OTA package to device:

Assign OTA package to device
=============================

You may also assign firmware to specific device. See screenshots below.

.. image:: /_static/thingsboard/thingsboard-ota-updates/assign-package-to-device-1.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/assign-package-to-device-2.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/assign-package-to-device-3.png

.. image:: /_static/thingsboard/thingsboard-ota-updates/assign-package-to-device-4.png

The firmware version assigned to the device will automatically overwrite firmware version that is assigned to the device profile.

For example, let's assume you have Devices D1 and D2 that has Profile P1:

* If you assign package F1 to Profile P1 (via :ref:`profile details UI <Assign OTA package to device profile>` or REST API), Devices D1 and D2 will be updated to F1.
* If you assign package F2 to Device D1 (via :ref:`device details UI <Assign OTA package to device>` or REST API), Device D1 will be updated to F2.
* Subsequent assignment of the package F3 to the Profile P1 will affect only D2, since it has no specific firmware version assigned on the device level. So, D2 will be updated to F3, while D1 will continue to use F2.

Customers may choose available firmware and assign it to the devices that belong to them. However, customers can't provision or manage firmware packages.

.. tips:
    Deletion of the firmware packages that is assigned to at least one device or device profile is prohibited.

.. _Update process:

Update process
===============

Assignment of the firmware to the device or device profile triggers the update process. ThingsBoard tracks the progress of the update and persists it to the device attributes.

Update progress may have one of the following states. The state of the update is stored as an attribute of the device and is used to visualize the update process on the :ref:`dashboard <OTA updates Dashboard>`.

QUEUED state
------------

The very first state of the firmware update. Means that the notification about new firmware is queued but not yet pushed to the device. ThingsBoard queues the update notifications to avoid peak loads. The queue is processed with the constant pace. By default, it is configured to notify up to 100 device per minute. See :ref:`configuration properties <ota update queue processing pace>` for more details.

INITIATED state
----------------

Means that the notification about firmware is fetched from queue and pushed to device. Under the hood, ThingsBoard converts notification to the update of the following :ref:`shared attributes <Working with IoT device attributes>`:

* fw_title - name of the firmware.
* fw_version - version of the firmware.
* fw_size - size of the firmware file in bytes.
* fw_checksum - attribute that is used to verify integrity of the received file.
* fw_checksum_algorithm - the algorithm used to calculate file checksum.

.. image:: /_static/thingsboard/thingsboard-ota-updates/fw-attributes-ce.png

Device is able to subscribe to shared attribute update using :doc:`MQTT API </thingsboard/thingsboard-mqtt-device-api>`.

Update states reported by the device
-------------------------------------

The remaining states are reported by the device firmware that is currently processing the update. We have prepared description of those states and sample applications for the most popular protocols written in python. Sample applications simulate behavior of the device firmware and may used as a reference for the implementation.

* DOWNLOADING - notification about new firmware update was received and device started downloading the update package.
* DOWNLOADED - device completed downloading of the update package.
* VERIFIED - device verified the checksum of the downloaded package.
* UPDATING - device started the firmware update. Typically is sent before reboot of the device or restart of the service.
* UPDATED - the firmware was successfully updated to the next version.
* FAILED - checksum wasn’t verified, or the device failed to update. See “Device failed” tab on the Firmware dashboard for more details.
* Once the firmware is updated, ThingsBoard expect the device to send the following telemetry:

for firmware:

.. code:: json

    {"current_fw_title": "TA652FC-W-TB", "current_fw_version": "1.6.3", "fw_state": "UPDATED"}

If the firmware update failed, ThingsBoard expect the device to send the following telemetry:

for firmware:


.. code:: json

    {"fw_state": "FAILED", "fw_error":  "the human readable message about the cause of the error"}

Firmware of the device is updated. To see its status, you should go to the firmware dashboard as it shows in the following paragraph.

To find out about the firmware update, you need to :ref:`make a request and subscribe to attributes <Firmware_API>`.


Configuration
==============

.. _ota update queue processing pace:

Queue processing pace
----------------------

To set the max number of devices that will be notified in the chosen time period using the following `configuration <https://thingsboard.io/docs/user-guide/install/config/>`_ properties:

.. code:: shell

    export TB_QUEUE_CORE_FW_PACK_INTERVAL_MS=60000
    export TB_QUEUE_CORE_FW_PACK_SIZE=100


Max size setting
-----------------

By default, the maximum size of firmware that we can save in database is 2 gb. It can not be configured.