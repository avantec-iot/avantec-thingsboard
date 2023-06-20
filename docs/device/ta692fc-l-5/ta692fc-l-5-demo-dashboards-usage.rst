**********************************
TA692FC-L-5 Demo Dashboards Usage
**********************************

Overview
=========

There are two dashboards related to TA692FC-L-5, namely ``TA692FC-L-5 Thermostat List`` and ``TA692FC-L-5 Thermostat (For Mobile App)``. We open the former to start operating TA692FC-L-5.

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-overview-1.png

.. list-table:: TA692FC-L-5 Demo Dashboards
   :widths: 10 5 5 5 5
   :header-rows: 1

   * - Dashboard
     - Description
     - For Web UI
     - For Mobile App
     - Entry*
   * - TA692FC-L-5 Thermostat List
     - list
     - Yes
     - No
     - Yes
   * - TA692FC-L-5 Thermostat (For Mobile App)
     - details
     - Yes
     - Yes
     - No

.. hint::

    - If *Entry* is *Yes*, then directly enter the Dashboard and there will be data displayed.
    - If *Entry* is *No*, there will be no data display when entering this Dashboard directly, and you need to jump to this Dashboard from other Dashboards.

.. _TA692FC-L-5 Thermostat List:

TA692FC-L-5 Thermostat List
=============================

Dashboard states
------------------

Default state
^^^^^^^^^^^^^^^^^^^

``Default state`` is root state.

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-list-1.png

*  Dashboard bar:
    * |Dashboard name| : Click here to skip to **root state**. Since **default state** is *root state*, click here and there is no response.
    * |Dashboard expand to fullscreen| : Click the two ICONS in the upper left corner to display the page in full screen.
    * |Dashboard edit timewindow| : Edit time window.

.. |Dashboard name| image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-list-2.png
.. |Dashboard expand to fullscreen| image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-list-3.png
.. |Dashboard edit timewindow| image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-list-4.png

*  Thermostats widgets:
    * Fields: 
        * Device name, Label, Type, active.
        * Room temperature, Set Temperature, System Mode, Fan status: Refer to `Monitor state`_.
    * Actions:
        * |detail_dashboard| : skip to `TA692FC-L-5 Thermostat (For Mobile App)`_.
        * |edit_device| : Popup dialog to editing a device's label.

.. |detail_dashboard| image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-list-5.png
.. |edit_device| image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-list-6.png



.. _Import TA692FC-L-5 List Dashboard:

Import List Dashboard
----------------------

.. include:: ta692fc-l-5-demo-list-dashboard-import.rst


.. _Update TA692FC-L-5 List Dashboard:

Update List Dashboard
----------------------

.. include:: ta692fc-l-5-demo-list-dashboard-update.rst


.. _TA692FC-L-5 Thermostat (For Mobile App):

TA692FC-L-5 Thermostat (For Mobile App)
=========================================

Dashboard states
------------------

Monitor state
^^^^^^^^^^^^^^^

``Monitor state`` is root state.

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-detail-monitor-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =============================== ============================================================
        Widget                          Description
        =============================== ============================================================
        MONITOR                         skip to `Monitor state`_
        CONTROL                         skip to `Control state`_
        SETTINGS                        skip to `Settings state`_

        Room Temperature                room temperature
        Set Temperature                 current setpoint value
        System Mode                     "OFF", "OFF", "COOL" or "FAN-ONLY"
        Fan Mode                        "OFF", "LOW", "MED", "HIGH" or "AUTO"
        Fan Status                      "OFF", "LOW", "MED" or "HIGH"
        Cool Proportional Output        0 ~ 100%

        Temperature history             | Room temperature history. Click 
                                        | |Temperature history edit timewindow| \
                                        | to edit this timewindow. Refer to `Default state`_
        =============================== ============================================================

.. |Temperature history edit timewindow| image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-detail-monitor-2.png

Control state
^^^^^^^^^^^^^^^

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-detail-control-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        =============================== ============================================================
        Widget                          Description
        =============================== ============================================================
        Set Temperature                 current setpoint value
        Set Fan Mode                    change fan mode
        Set System Mode                 change system mode
        =============================== ============================================================


Settings state
^^^^^^^^^^^^^^^^^^^

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-demo-dashboards-usage/ta692fc-l-5-demo-dashboards-usage-detail-settings-1.png

*  Dashboard bar:
    Hidden.
    Refer to `Default state`_.

* Widgets:
    .. table:: 
        :widths: 35, 65

        ============================ ===========================================================
        Widget                       Description
        ============================ ===========================================================
        Set P-Band for Cool          1.0 ~ 4.0 °C
        Set I-Time for Cool          5 ~ 180 seconds
        Set K-Factor                 1 ~ 9

        Set Threshold                0.2 ~ 5.0 °C
        ============================ ===========================================================



.. _Import TA692FC-L-5 Detail Dashboard:

Import Detail Dashboard
------------------------

.. include:: ta692fc-l-5-demo-detail-dashboard-import.rst



.. _Update TA692FC-L-5 Detail Dashboard:

Update Detail Dashboard
---------------------------

.. include:: ta692fc-l-5-demo-detail-dashboard-update.rst