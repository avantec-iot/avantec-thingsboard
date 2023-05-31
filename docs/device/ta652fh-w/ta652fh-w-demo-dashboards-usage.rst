**********************************
TA652FH-W Demo Dashboards Usage
**********************************

Overview
=========

There are some dashboards related to TA652FH-W, namely ``TA652FH-W Thermostat List``, ``TA652FH-W Thermostat (For Mobile App)`` and ``Office center - TA652FH-W Thermostats``. We open the former to start operating TA652FH-W.

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-overview-1.png

.. list-table:: TA652FH-W Demo Dashboards
   :widths: 10 5 5 5 5
   :header-rows: 1

   * - Dashboard
     - Description
     - For Web UI
     - For Mobile App
     - Entry*
   * - TA652FH-W Thermostat List*
     - list
     - Yes
     - No
     - Yes
   * - TA652FH-W Thermostat (For Mobile App)
     - details
     - Yes
     - Yes
     - No
   * - 
     - 
     - 
     - 
     - 
   * - Office center - TA652FH-W Thermostats**
     - list & details
     - Yes
     - Yes
     - Yes

.. hint::

    - If *Entry* is *Yes*, then directly enter the Dashboard and there will be data displayed.
    - If *Entry* is *No*, there will be no data display when entering this Dashboard directly, and you need to jump to this Dashboard from other Dashboards.
    - 
    - ``TA652FH-W Thermostat List`` depends on ``TA652FH-W Thermostat (For Mobile App)``.
    - ``Office center - TA652FH-W Thermostats`` can be used independently.


.. _TA652FH-W Thermostat List:

TA652FH-W Thermostat List
==========================

Dashboard states
------------------

Default state
^^^^^^^^^^^^^^^^^^^

``Default state`` is root state.

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-1.png

*  Dashboard bar:
    * |Dashboard name| : Click here to skip to **root state**. Since **default state** is *root state*, click here and there is no response.
    * |Dashboard expand to fullscreen| : Click the two ICONS in the upper left corner to display the page in full screen.
    * |Dashboard edit timewindow| : Edit time window.

.. |Dashboard name| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-2.png
.. |Dashboard expand to fullscreen| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-3.png
.. |Dashboard edit timewindow| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-4.png

*  Thermostats widgets:
    * Fields: 
        * Device name, Label, Type, active.
        * Room temperature, Floor Temperature, Setpoint, Unit: Refer to `Monitor state`_.
    * Actions:
        * |detail_dashboard| : skip to `TA652FH-W Thermostat (For Mobile App)`_.
        * |edit_device| : Popup dialog to editing a device's label.

.. |detail_dashboard| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-5.png
.. |edit_device| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-6.png


.. _Import TA652FH-W List Dashboard:

Import List Dashboard
----------------------

.. include:: ta652fh-w-demo-list-dashboard-import.rst



.. _Update TA652FH-W List Dashboard:

Update List Dashboard
----------------------

.. include:: ta652fh-w-demo-list-dashboard-update.rst




.. _TA652FH-W Thermostat (For Mobile App):

TA652FH-W Thermostat (For Mobile App)
======================================

Dashboard states
------------------

Monitor state
^^^^^^^^^^^^^^^^^^^

``Monitor state`` is root state.

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-monitor-1.png

*  Dashboard bar:
    Hidden.
    Refer  `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =============================== ============================================================
        Widget                          Description
        =============================== ============================================================
        MONITOR                         skip to `Monitor state`_
        CONTROL                         skip to `Control state`_
        PROGRAM                         skip to `Program state`_
        SETTINGS                        skip to `Settings state`_
        ADMIN                           skip to `Admin state`_

        Room Temperature                room temperature
        Floor Temperature               floor temperature
        Setpoint                        current setpoint value
        Temperature history             | Room temperature & Change Over Sensor temperature \
                                        | history. Click |Temperature history edit timewindow| \
                                        | to edit this timewindow. Refer to `Default state`_
        =============================== ============================================================

.. |Temperature history edit timewindow| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-monitor-2.png

Control state
^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-control-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =============================== ============================================================
        Widget                          Description
        =============================== ============================================================
        Setpoint                        If you adjust *setpoint*, *override program status* is YES (true)
        Program                         program on or off
        PRG next setpoint               next program time & setpoint
        Override program status         "YES"(true) or "NO"(false)

        Control Mode                    "Off" or "On"
        =============================== ============================================================

Program state
^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-program-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        ======================= ===================================================
        Program Mode            Description
        ======================= ===================================================
        NO PROGRAM              Program disabled
        1 DAY (MON)             Using 4 set points of Monday every day
        1+5+1 (SUN+MON+SAT)     Using 4 set points of Monday from Monday to Friday
        7 DAYS (SUN~SAT)        Using 4 set points every day
        Sunday, ...             Skip to `Program_setpoints state`_
        ======================= ===================================================

Program_setpoints state
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-program-setpoints-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =========================== ======================================================
        Widget                      Description
        =========================== ======================================================
        Program 1 ~ Program 4       time, hour:minute
        Setpoint 1 ~ Setpoint 4     setpoint value, temperature
        =========================== ======================================================


Settings state
^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-settings-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        ============================ ===========================================================
        Widget                       Description
        ============================ ===========================================================
        Temp Unit                    "°C" or "°F". **Reboot the device to take effect**
        Adaptive control             Enabled or disabled

        System Mode                  "Heat" or "Cool"
        Sensor Mode                  | "Internal" / "External" / "Combined" senosr can be selected 
                                     | when it is in "Heat" mode.
                                     | Only "Internal" Sensor will be used when it is in "Cool" mode.

        Floor temperature limited    external sensor temperature offset
        Temp Offset(Internal Sensor) Internal sensor temperature offset

        Switching Diff Heating       Switching differential heating
        Switching Diff Cooling       Switching differential cooling
        ============================ ===========================================================


Admin state
^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-admin-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =================== ===========================================================
        Widget                       Description
        =================== ===========================================================
        Time Format         "12 Hours" or "24 Hours"
        Timezone            See :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`
        NTP Server          | SNTP protocol server URL, e.g. pool.ntp.org, 
                            | 0.pool.ntp.org, 1.pool.ntp.org, 
                            | time.nist.gov, …
                            | see :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`
        Sync Time           | Sync time per syncTimeFreq seconds.
                            | If you change *Timezone* or *NTP Server*, you have to do it.
                            | See :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`

        Device attributes   | Device name, device profile (type), device label, 
                            | model, MAC, device Wi-Fi Module F/W version,
                            | device Main MCU F/W version

        Reboot              Reboot device
        Clear Wi-Fi Config  Clear device's Wi-Fi configuration
        =================== ===========================================================


.. _Import TA652FH-W Detail Dashboard:

Import Detail Dashboard
------------------------

.. include:: ta652fh-w-demo-detail-dashboard-import.rst



.. _Update TA652FH-W Detail Dashboard:

Update Detail Dashboard
---------------------------

.. include:: ta652fh-w-demo-detail-dashboard-update.rst






.. _Office center - TA652FH-W Thermostats:

Office center - TA652FH-W Thermostats
======================================

Dashboard states
------------------

Office state
^^^^^^^^^^^^^^^^^^^^^^^

``Office state`` is root state.

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-1.png

*  Dashboard bar:
    * |office state root state| : Click here to skip to **root state**. Since **default state** is *root state*, click here and there is no response.

.. |office state root state| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-2.png

*  Thermostats List:
    * Fields: 
        * Thermostat name, Label, active.
        * Room temperature, Floor Temperature, Setpoint, Unit, xPos, yPos.
    * Actions:
        * |Edit Location| : Skip to `Map state`_.
        * |Add Thermostat| : Open a dialog, to add a new thermostat.
        * |Thermostat chart| : Skip to `Chart state`_.
        * |Edit Thermostat| : Open a dialog, to edit a thermostat.
        * |Delete Thermostat| : Open a dialog, to edit a thermostat.

.. |Edit Location| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-3.png
.. |Add Thermostat| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-4.png
.. |Thermostat chart| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-5.png
.. |Edit Thermostat| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-6.png
.. |Delete Thermostat| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-7.png

* Map widget:
    * |Anchor Thermostat| : Open a box, to show some text.
    * |Thermostat link| : Skip to `Chart state`_.

.. |Anchor Thermostat| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-8.png
.. |Thermostat link| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-office-state-9.png


Map state
^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-map-state-1.png

* Map widget:
    * |Drag-drop mode| : Click to enter drag-drop mode, you can modify the position of the thermostat. Click again to save the modification and exit drag-drop mode.


.. |Drag-drop mode| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-map-state-2.png


Chart state
^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/office-center-dashboard-chart-state-1.png



.. _Import Office Center Dashboard:

Import Office Center Dashboard
---------------------------------

.. include:: ta652fh-w-demo-office-center-dashboard-import.rst


.. _Update Office Center Dashboard:

Update Office Center Dashboard
--------------------------------

.. include:: ta652fh-w-demo-office-center-dashboard-update.rst

