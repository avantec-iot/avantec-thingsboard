*************************************************
TA652FC-W -- 2 pipe Fan Coil Wi-Fi Thermostat
*************************************************

.. CAUTION::

    1. Turn off all electrical devices (e.g. heater, cooler) that are connected to the unit before installation and maintenance.
    2. The installer must be a trained service personnel.
    3. Disconnect the power supply before maintenance.
    4. It must be mounted on a dry clean indoor place.
    5. Do not expose this unit to moisture.
    6. Do not expose this unit to dipping or splashing.

Introduction
=============

TA652FC-W is a controller that controls fan coil system to maintain room temperature at a desired level. 
 
Changeover sensor is required to install when auto changeover is used.


Feature List
=============

* Voltage supply: 230Vac
* Temperature display in °C or °F
* Temperature measurable range : 0 - 50 °C
* 2-pipe system
* Manual changeover or Auto changeover can be selected 
* Selection of Heat/Cool
* 7days/5+1+1days, 1day program, no program.
* EEPROM stores all settings
* Adjustable control span


Wiring
=======

**NOTE:** Power supply of TA652FC-W is 230Vac.

.. table::
    :widths: auto

    =========== ================
    Terminals	Device
    =========== ================
    L	        230Vac Live
    N	        230Vac Neutral
    Qv	        Changeover valve
    Q1	        Fan Low
    Q2	        Fan Med
    Q3	        Fan High
    T1	        Floor Sensor
    T2 	        Floor Sensor
    =========== ================

Pull all cables back into the wall beforehand to avoid trapping of wires.  Do not use any metal conduits or cables provided with metal sheaths.

Recommend adding fuse or protective device in the live circuit.

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/wiring-1.png
    :width: 54%

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/wiring-2.png
    :width: 19%


Mounting
========

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/mounting-1.png
    :width: 32%

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/mounting-2.png
    :width: 32%

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/mounting-3.png
    :width: 32%

1. Wiring the terminals.
2. Put into junction box.
3. Mount the bottom plate of LCD board into junction box.
4. Connect the wire to the LCD board.
5. Assemble the Top and bottom plate of LCD Board.

Dimension in mm:
================

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/dimension-1.png
    :width: 50%

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/dimension-2.png
    :width: 30%


LCD Interface
=============

LCD Indication
---------------

.. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/lcd_indication.png
    :width: 40%

.. table::
    :widths: auto

    === ===============================================================================
    sn  item
    === ===============================================================================
    1   Time
    2   Room Temperature
    3   Current Set Point 
    4   Temperature Unit
    5   Current Program
    6   Heat / Cool Mode
    7   Auto Changeover
    8   Output is On (when appear)
    9   Fan Low/Med/High/Auto
    10  Wi-Fi (appear when connected to router)
    11  Mode Key: Press to **internal setting 1**. Long hold to **internal setting 2**.
    12  Clock Key: Press to **set clock**. Hold to **Program** the Schedule
    13  Short Press: Fan Key, Long Hold: On/Off Key
    14  Up/Down key: Adjust Set point or Value of setting.
    15  Blank: the area outside of the previous five keys
    === ===============================================================================


.. |icon_mode| image:: /_static/device/ta652fc-w/ta652fc-w-specifications/icon_mode.png
    :scale: 50%

.. |icon_clock| image:: /_static/device/ta652fc-w/ta652fc-w-specifications/icon_clock.png
    :scale: 50%

.. |icon_onoff| image:: /_static/device/ta652fc-w/ta652fc-w-specifications/icon_onoff.png
    :scale: 50%

.. |icon_up| image:: /_static/device/ta652fc-w/ta652fc-w-specifications/icon_up.png
    :scale: 50%

.. |icon_down| image:: /_static/device/ta652fc-w/ta652fc-w-specifications/icon_down.png
    :scale: 50%

.. |icon_blank| replace:: **[blank]**

Turn On/Off the thermostat
---------------------------

Hold |icon_onoff| to turn On / Off the thermostat. When the thermostat is Off. No Output will be activated.


Clock setting
-------------

**Normally the clock is automatically set once Wi-Fi is connected and synchronize for each day. So manual set is not necessary when it is online.**

* Press |icon_clock| to start the setting
* Press |icon_up| / |icon_down| to change the day of week
* Press |icon_clock| again to confirm day of week setting and start to adjust hour
* Press |icon_up| / |icon_down| to change the hour
* Press |icon_clock| again to confirm hour setting and start to adjust minutes
* Press |icon_up| / |icon_down| to change the minutes
* Press |icon_clock| again to confirm minutes setting and start to adjust day of week
* Press |icon_blank| to confirm or leave the clock setting. Or return after no key pressed for 20 seconds.

Clock synchronization
^^^^^^^^^^^^^^^^^^^^^^

When Wi-Fi is connected and time synchronization is need. Please use the App for time synchronization.


Schedule Programming
---------------------

When **1 day** / **5+1+1 day** / **7day program** is selected in internal setting.

* Hold  |icon_clock| to start the setting.
* Press |icon_up| / |icon_down| to adjust the day of week
* Press |icon_clock| to confirm.
* Press |icon_up| / |icon_down| to adjust the time of schedule
* Press |icon_clock| to confirm.
* Press |icon_up| / |icon_down| to adjust the setpoint
* Press |icon_clock| to confirm.
* Press |icon_blank| to confirm return.


Override Temperature
---------------------

The Set point can be adjusted by |icon_up| / |icon_down|.

When it is in program mode, the set point will be overwritten until the next time slot. 

|icon_clock| can be pressed to release the override status.


Internal parameter setting 1
-----------------------------

* Operation:
    * Press |icon_mode| key to start the setting
    * Press |icon_up| / |icon_down| to adjust the value
    * Press |icon_blank| to confirm and move to next setting

===== ============================= =========================== =====================
ID    Items	                        Value	                    Default Value
===== ============================= =========================== =====================
P00   User Interface Screen Saver   0-3	                        0
P01   Screen Saver Count  down      0-120	                    20
P02   Display unit                  °C / °F	                    °C
P03   Time Display unit             12/24	                    12
P04   Temperature Offset            -5°C - 5°C, -10°F-10°F	    0°C
P05   Switching Differential Heat   2 - 4°C, 4 - 8°F 	        2°C
P06   Switching Differential Cool   2 - 4°C, 4 - 8°F 	        2°C
P07   Program mode                  | No program (0) /          3
                                    | 1day program (1) / 
                                    | 5+1+1 program (2) /
                                    | 7day program (3)	
P12   Force Ventilation             Disable, Enable	            Disable
P13   Changeover Mode               Heat, Cool, Auto	        Heat
P14   Changeover temperature Heat   27 - 40°C	                27°C
P15   Changeover temperature Cool   10-25°C	                    10°C
===== ============================= =========================== =====================

* User Interface Screen Saver:
    The thermostat will go to screen saver mode after no key for certain period.

    * **Mode 0**: Nothing will be displayed in screen saver mode.
    * **Mode 1**: Only room temperature will be displayed in screen saver mode.
    * **Mode 2**: Room temperature and Time will be displayed in screen saver mode.
    * **Mode 3**: Display all in screen saver mode.

* Screen Saver Count Down:
    The count down time (in seconds) to screen saver mode.

* Display Unit:
    Temperature unit in Celsius or Fahrenheit.

* Time Display Unit:
    12/24.

* Temperature offset:
    The temperature of internal sensor can be calibrated from -5°C - +5°C in case there is temperature difference between actual value and thermostat.

* Switching Differential:
    The difference between switching the heating or controller on and off

    .. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/switching-differential-1.png
        :width: 49%

    .. image:: /_static/device/ta652fc-w/ta652fc-w-specifications/switching-differential-2.png
        :width: 49%

* Program Mode:
    * 0: **No Program** Mode, the thermostat control the temperature simply according to single setpoint.
    * 1: **1 day** program, the thermostat control the temperature according to single schedule.
    * 2: **5+1+1 day** program, the thermostat control the temperature according to 5 +1+1 schedule (Mon to Fri, Sat, Sun).
    * 3: **7 days** program, the thermostat control the temperature according to 7day program (individual program for each day).

* Forced Ventilation:
    * **Disable**: Fan will turn on only when heat/cool is on.
    * **Enable**: Fan keeps on (low) even heat / cool is off.

* Changeover mode:
    * 0: **Heat mode**
    * 1: **Cool mode**
    * 2: **Auto Changeover**: When changeover sensor detect the temperature above changeover heat set point. Heat mode will be activated.
        When changeover sensor detect the temperature below changeover cool set point. Cool mode will be activated.

* Changeover heating setpoint:
    Parameter for Auto Changeover mode.

* Changeover cooling setpoint:
    Parameter for Auto Changeover mode.


Internal parameter setting 2
-----------------------------

* Operation:
    * Hold |icon_mode| key to start the setting
    * Press |icon_up| / |icon_down| to adjust the value
    * Press |icon_blank| to confirm and move to next setting

===== ============================================= =========== ====================
ID    Items	                                        Value	    Default Value
===== ============================================= =========== ====================
P19   Clear Wi-Fi Configuration                     Yes or No   No
P20   Clear Parameter setting (restore default)     Yes or No   No
Adr   Address                                       ...         Read only, eg: 75C68
===== ============================================= =========== ====================

* Clear Wi-Fi Configuration: 
    When set to yes, the SSID and Password stored in the thermostat will be cleared  so another SSID and Password can be set again.

* Clear Parameter setting: 
    When set to yes, all internal parameter setting will be restored to default value in next power on (reset)

* Address: 
    The last 5 characters of the MAC address

Technical Data
----------------

=========================   ==========================
Power supply:			    195-250 Vac
Relay Contact Voltage:		230Vac Max. 50/60 Hz
Relay Contact Current:		2A Max. for each
Sensing Element:			103AT
Terminals:				    2 sq. mm Cable 
Operating Temperature:		32 - 122 °F / 0 - 50 °C
Storage Temperature:		23 - 122 °F / -5 - 50 °C
Operating Humidity:		    5-95%RHnon-condensing
=========================   ==========================
