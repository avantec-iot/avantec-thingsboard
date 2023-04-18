**********************************
TA652FH-W Demo Dashboards Usage
**********************************

Overview
=========

There are two dashboards related to TA652FH-W, namely ``TA652FH-W Thermostat List`` and ``TA652FH-W Thermostat (For Mobile App)``. We open the former to start operating TA652FH-W.

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-overview-1.png

.. list-table:: TA652FH-W Demo Dashboards
   :widths: 10 5 5 5 5
   :header-rows: 1

   * - Dashboard
     - Description
     - For Web UI
     - For Mobile App
     - Entry*
   * - TA652FH-W Thermostat List
     - list
     - Yes
     - No
     - Yes
   * - TA652FH-W Thermostat (For Mobile App)
     - details
     - Yes
     - Yes
     - No

.. hint::

    - If *Entry* is *Yes*, then directly enter the Dashboard and there will be data displayed.
    - If *Entry* is *No*, there will be no data display when entering this Dashboard directly, and you need to jump to this Dashboard from other Dashboards.

.. _TA652FH-W Thermostat List:

TA652FH-W Thermostat List
==========================

*Default State* is root state.

Default State
----------------

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-1.png

*  Dashboard bar:
    * |Dashboard name| : Click here to skip to **root State**. Since **default State** is *root state*, click here and there is no response.
    * |Dashboard expand to fullscreen| : Click the two ICONS in the upper left corner to display the page in full screen.
    * |Dashboard edit timewindow| : Edit time window.

.. |Dashboard name| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-2.png
.. |Dashboard expand to fullscreen| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-3.png
.. |Dashboard edit timewindow| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-4.png

*  Thermostats widgets:
    * Fields: 
        * Entity name, Entity type, Type, active.
        * Room temperature, Floor Temperature, Setpoint, Unit: Refer to `Monitor State`_.
    * Actions:
        * |detail_dashboard| : skip to `TA652FH-W Thermostat (For Mobile App)`_。

.. |detail_dashboard| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-list-5.png


.. _TA652FH-W Thermostat (For Mobile App):

TA652FH-W Thermostat (For Mobile App)
======================================

*Monitor State* is root state.

Monitor State
-------------------------

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-monitor-1.png

*  Dashboard bar:
    Hidden.
    Refer  `Default State`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =============================== ============================================================
        Widget                          Description
        =============================== ============================================================
        MONITOR                         skip to `Monitor State`_
        CONTROL                         skip to `Control State`_
        PROGRAM                         skip to `Program State`_
        SETTINGS                        skip to `Settings State`_
        ADMIN                           skip to `Admin State`_

        Room Temperature                room temperature
        Floor Temperature               floor temperature
        Setpoint                        current setpoint value
        Temperature history             | Room temperature & Change Over Sensor temperature \
                                        | history. Click |Temperature history edit timewindow| \
                                        | to edit this timewindow. Refer to `Default State`_
        =============================== ============================================================

.. |Temperature history edit timewindow| image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-monitor-2.png

Control State
-------------------------

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-control-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default State`_.

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

Program State
------------------------

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-program-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default State`_.

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
        Sunday, ...             Skip to `Program_Setpoints State`_
        ======================= ===================================================

Program_Setpoints State
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-program-setpoints-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default State`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =========================== ======================================================
        Widget                      Description
        =========================== ======================================================
        Program 1 ~ Program 4       time, hour:minute
        Setpoint 1 ~ Setpoint 4     setpoint value, temperature
        =========================== ======================================================


Settings State
-------------------------

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-settings-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default State`_.

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


Admin State
----------------------

.. image:: /_static/device/ta652fh-w/ta652fh-w-demo-dashboards-usage/ta652fh-w-demo-dashboards-usage-detail-admin-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default State`_.

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
