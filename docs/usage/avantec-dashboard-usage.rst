Avantec Dashboard Usage
=======================


Default State
-------------

.. image:: /_static/usage/avantec_usage/default_state.png

*  Dashboard bar:
    * |Dashboard name| : Click here to skip to **root State**. Since **default State** is *root state*, click here and there is no response.
    * |Dashboard expand to fullscreen| : Click the two ICONS in the upper left corner to display the page in full screen.
    * |Dashboard edit timewindow| : Edit timewindow.

.. |Dashboard name| image:: /_static/usage/avantec_usage/dashboard_name_icon.png
.. |Dashboard expand to fullscreen| image:: /_static/usage/avantec_usage/dashboard_fullname_icon.png
.. |Dashboard edit timewindow| image:: /_static/usage/avantec_usage/dashboard_timewindow_icon.png

*  Thermostats widget:
    * Field: 
        * Entity name，Entity type: device name, type.
        * Model, Room temp, Unit: see `TA65-FC_Control State`_.
    *  State Operate:
        * |default_control| : skip to `TA65-FC_Control State`_。
        * |default_program| : skip to `TA65-FC_Program State`_。
        * |default_settings| : skip to `TA65-FC_Settings State`_。
        * |default_admin| : skip to `TA65-FC_Admin State`_。

.. |default_control| image:: /_static/usage/avantec_usage/default_control_icon.png
.. |default_program| image:: /_static/usage/avantec_usage/default_program_icon.png
.. |default_settings| image:: /_static/usage/avantec_usage/default_settings_icon.png
.. |default_admin| image:: /_static/usage/avantec_usage/default_admin_icon.png


TA65-FC States
--------------

TA65-FC_Control State
>>>>>>>>>>>>>>>>>>>>>

.. image:: /_static/usage/avantec_usage/ta65_fc_control_state.png

*  Dashboard bar:
    See `Default State`_.

* Widgets:
    .. table:: 
        :widths: 20, 80

        ======================= ========================================================
        Widget                  Description
        ======================= ========================================================
        Room Temp               room temperature
        Change Over Sensor Temp change over sensor temperature
        Temp Unit               temperature unit, "°C" or "°F"
        Fan Status              "Off", "Low", "Med" or "High"
        PRG Enabled             program enabled, true or false
        PRG Next Time           next program time
        PRG Next SP             next program set point
        Control Mode            "Off" or "On"
        Fan Mode                "Auto", "Low", "Med" or "High"
        Set Point               If you adjust *set point*, *override status* is YES(true)
        Override Status         "YES"(true) or "NO"(false)
        Temperature history     | Room Temp & Change Over Sensor Temp history. Click \
                                | |Dashboard edit timewindow| to edit this timewindow. \
                                | See `Default State`_
        ======================= ========================================================


TA65-FC_Program State
>>>>>>>>>>>>>>>>>>>>>>

.. image:: /_static/usage/avantec_usage/ta65_fc_program_state.png

*  Dashboard bar:
    See `Default State`_.

* Widgets:
    * Programe Mode: 

    .. table:: 
        :widths: 20, 80

        ======================= ===================================================
        Program Mode            Description
        ======================= ===================================================
        NO PROGRAM              Program disabled
        1 DAY (MON)             Using 4 set points of Monday every day
        1+5+1 (SUN+MON+SAT)     Using 4 set points of Monday from Monday to Friday
        7 DAYS (SUN~SAT)        Using 4 set points every day
        ======================= ===================================================

    * Set Points:

    .. table:: 
        :widths: 20, 80

        =========================== ======================================================
        Widget                      Description
        =========================== ======================================================
        prgSpTime00 ~ prgSpTime27   time, hour:minute
        prgSpValue00 ~ prgSpValue27 set point value, temperature
        =========================== ======================================================

TA65-FC_Settings State
>>>>>>>>>>>>>>>>>>>>>>>

.. image:: /_static/usage/avantec_usage/ta65_fc_settings_state.png

*  Dashboard bar:
    See `Default State`_.

* Widgets:
    .. table:: 
        :widths: 30, 70

        ============================ ===========================================================
        Widget                       Description
        ============================ ===========================================================
        Time Format                  "12 Hours" or "24 Hours"
        Timezone                     See :ref:`add-shared-attributes-of-new-device-cloudhost`
        NTP Server                   | SNTP protocol server URL, eg: pool.ntp.org, 
                                     | 0.pool.ntp.org, 1.pool.ntp.org, 
                                     | time.nist.gov, …
                                     | see :ref:`add-shared-attributes-of-new-device-cloudhost`

        Sync Time                    If you change *Timezone* or *NTP Server*, you have to do it
        Temp Unit                    "°C" or "°F". **Reboot the device to take effect**
        Change Over Mode             "Heat", "Cool" or "Auto"
        Force Ventialation           Used in automatic *Fan Mode*
        Temp Offset(Internal Sensor) Internal sensor temperture offset
        Change Over Temp Heating     Change over temperature heating
        Change Over Temp Cooling     Change over temperature cooling
        Switching Diff Heating       Switching differential heating
        Switching Diff Cooling       Switching differential cooling
        WI-FI RSSI                   Wi-Fi Received Signal Strength Indicator
        ============================ ===========================================================


TA65-FC_Admin State
>>>>>>>>>>>>>>>>>>>>

.. image:: /_static/usage/avantec_usage/ta65_fc_admin_state.png

*  Dashboard bar:
    See `Default State`_.

* Widgets:
    .. table:: 
        :widths: 30, 70

        =================== ===========================================================
        Widget                       Description
        =================== ===========================================================
        Cloud Host          | This ThingsBoard Server's MQTT URL. 
                            | It must begin with “MQTT ://”, such as
                            | mqtt://192.168.21.222
                            | **Please replace 192.168.21.222 with your value.**
                            | See :ref:`add-shared-attributes-of-new-device-cloudhost`

        Telemetry Upload    | Telemetry per uploadFreq seconds 
                            | See :ref:`add-shared-attributes-of-new-device-cloudhost`

        Sync Time           | Sync time per syncTimeFreq seconds 
                            | See :ref:`add-shared-attributes-of-new-device-cloudhost`

        Memory Usage        byte, iram: internal RAM, spiram: external SPI RAM
        Wi-Fi FUOTA         | First input a HTTP URL of Wi-Fi module F/W, 
                            | then click this button

        MCU FUOTA           | First input a HTTP URL of main MCU F/W, 
                            | then click this button

        Clear Wi-Fi Config  Clear device's Wi-Fi configuration
        Reboot              Reboot device
        Device attributes   | Device model, device mac, 
                            | device Wi-Fi Module F/W version
                            | device Main MCU F/W version

        =================== ===========================================================
