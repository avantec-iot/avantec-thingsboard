TA65-FH --- Floor Heating Wi-Fi Thermostat
##############################################

CAUTION:
=========

1. Turn off all electrical devices (e.g. heater, cooler) that are connected to the unit before installation and maintenance.
2. The installer must be a trained service personnel
3. Disconnect the power supply before maintenance.
4. It must be mounted on a dry clean indoor place.
5. Do not expose this unit to moisture.
6. Do not expose this unit to dipping or splashing.


Introduction
=============

T65 is a controller that controls heater/cooler on or off to maintain room temperature at a desired level.  

When **Heat mode** is used, **Internal sensor**, **Floor sensor** and **combined sensor** can be selected for different application. 

When **Cool mode** is selected, Only **Internal sensor** will be used.


Feature List
=============

* Voltage supply: 230Vac
* Temperature display in oC or oF
* Temperature measurable range : 0 – 50 C 
* Selection of Heat/Cool
* Adaptive control
* 7days / 5+1+1days, 1day program, no program.
* EEPROM stores all settings
* Adjustable control span
* Short cycle protection for compressor


Wiring
=======

**NOTE:** Power supply of TA65 is 230Vac.

.. table::
    :widths: auto

    =========== ================
    Terminals	Device
    =========== ================
    L	        230Vac Live
    N	        230Vac Neutral
    LO	        Heater / Cooler
    T1	        Floor Sensor 1
    T2 	        Floor Sensor 2
    =========== ================

Pull all cables back into the wall beforehand to avoid trapping of wires.  Do not use any metal conduits or cables provided with metal sheaths.

Recommend adding fuse or protective device in the live circuit.

===========================================


.. image:: /_static/usage/ta65-fh/wiring-1.png
    :width: 54%

.. image:: /_static/usage/ta65-fh/wiring-2.png
    :width: 19%


Mounting
========

.. image:: /_static/usage/ta65-fh/mounting-1.png
    :width: 32%

.. image:: /_static/usage/ta65-fh/mounting-2.png
    :width: 32%

.. image:: /_static/usage/ta65-fh/mounting-3.png
    :width: 32%

1. Wiring the terminals.
2. Put into junction box.
3. Mount the bottom plate of LCD board into junction box.
4. Connect the wire to the LCD board.
5. Assemble the Top and bottom plate of LCD Board.


Dimension in mm:
================

.. image:: /_static/usage/ta65-fh/dimension-1.png
    :width: 50%

.. image:: /_static/usage/ta65-fh/dimension-2.png
    :width: 30%


LCD Interface
=============

LCD Indication
---------------

.. image:: /_static/usage/ta65-fh/lcd_indication.png
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
    8   Output is On (when appear)
    8   Wi-Fi (appear when connected to router)
    9   Mode Key: Press to **internal setting 1**. Long hold to **internal setting 2**.
    10  Clock Key: Press to **set clock**. Hold to **Program** the Schedule
    11  Short Press: Fan Key, Long Hold: On/Off Key
    12  Up/Down key: Adjust Set point or Value of setting.
    13  Blank: the area outside of the previous five keys
    === ===============================================================================


.. |icon_mode| image:: /_static/usage/ta65-fh/icon_mode.png
    :scale: 50%

.. |icon_clock| image:: /_static/usage/ta65-fh/icon_clock.png
    :scale: 50%

.. |icon_onoff| image:: /_static/usage/ta65-fh/icon_onoff.png
    :scale: 50%

.. |icon_up| image:: /_static/usage/ta65-fh/icon_up.png
    :scale: 50%

.. |icon_down| image:: /_static/usage/ta65-fh/icon_down.png
    :scale: 50%

.. |icon_blank| replace:: **[blank]**


Turn On/Off the thermostat
---------------------------

Hold |icon_onoff| to turn On / Off the thermostat. When the thermostat is Off. No Output will be activated.


Clock setting
-------------

** **Nomally the clock is automatically set once wifi is connected and synchronize for each day. So manual set is not ncecssary when it is online.**

* Press |icon_clock| to start the setting
* Press |icon_up| / |icon_down| to change the day of week
* Press |icon_clock| again to confirm day of week setting and start to adjust hour
* Press |icon_up| / |icon_down| to change the hour
* Press |icon_clock| again to confirm hour setting and start to adjust minutes
* Press |icon_up| / |icon_down| to change the minutes
* Press |icon_clock| again to confirm minutes setting and start to adjust day of week
* Press |icon_blank| to confirm or leave the clock setting. Or return after no key pressed for 20 seconds.

Clock synchronization
**********************

when Wi-Fi is connected and time synronize is need. Plesae use the App for time synchronization.


Schedule Programming
---------------------

When **1 day** / **5+1+1 day** / **7day program** is selected in internal setting.

* Hold  |icon_clock| to start the setting.
* Press |icon_up| / |icon_down| to adjust the day of week
* Press |icon_clock| to confirm.
* Press |icon_up| / |icon_down| to adjust the time of schdule
* Press |icon_clock| to confirm.
* Press |icon_up| / |icon_down| to adjust the setpoint
* Press |icon_clock| to confirm.
* Press |icon_blank| to confirm return.


Override Temperature
---------------------

The Set point can be adjusted by |icon_up| / |icon_down|.

When it is in program mode, The set point will be overrided until the next time slot. 

|icon_clock| can be pressed to release the override status.


Internal parameter setting 1.
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
P08   Adaptvie Control              Enable / Disable	        Disable
P09   System Mode                   Heat / Cool	                Heat
P10   Sensor Mode                   | Internal Sensor /         Internal Sensor
                                    | External Sensor /
                                    | Combined mode
P11   Floor temperature limited     20-40°C, 68-104°F	        40°C
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
    Temperature unit in Celesius or Farenheit.

* Time Display Unit:
    12/24.

* Temperature offset:
    The temperature of internal sensor can be calibrated from -5°C - +5°C in case there is temperature difference between actual value and thermostat.

* Switching Differential:
    The difference between switching the heating or controller on and off

    .. image:: /_static/usage/ta65-fh/switching-differential-1.png
        :width: 49%

    .. image:: /_static/usage/ta65-fh/switching-differential-2.png
        :width: 49%

* Program Mode:
    * 0: **No Program** Mode, The thermostat control the temperature simply according to single setpoint.
    * 1: **1 day** program, The thermostat control the temperature according to single schedule.
    * 2: **5+1+1 day** program, The thermostat control the temperature according to 5 +1+1 schedule (Mon to Fri, Sat, Sun).
    * 3: **7 days** program, The thermostat control the temperature according to 7day program (individual program for each day).

* Adaptive control
    When this function is enable, the thermostat learns the time taken to reach the desired setpoint and turn on the heating / cooling earlier so that the room temperature will reach the setpoint at desired schedule. This is no effect when **No program** is selected.

* Heat / Cool Mode
    When **Heat mode** is selected, the thermostat control The room temperature with heating. **Room Sensor**, **Floor Sensor** or **Combined sensor** can be selected.

    When **Cool mode** is selected, the thermostat control The room temperature with cooling. Only **Room Sensor**, will be used.

* Sensor Mode
    There are 3 different settings of sensor control for Heat Mode. (For Cool Mode. Only Room sensor will be used)

    * Room sensor
        Thermostat control the room temperature based on Room Sensor

    * Floor sensor
        Thermostat controla the room temperature based on Floor Sensor
    * Combined Floor-/Room sensor
        Thermostat control the room temperature based on Room Sensor. And the output will be off if floor temperature above “floor temperature limited” for protection.

* Floor temperature limited
    It is the temperature limited for floor sensor. When the **Heat Mode** and **Combined Sensor** are selected. The output will turn off when floor sensor sense the temperature to be higher than **floor temperature limited**.


Internal parameter setting 2.
-----------------------------

* Operation:
    * Hold |icon_mode| key to start the setting
    * Press |icon_up| / |icon_down| to adjust the value
    * Press |icon_blank| to confirm and move to next setting

===== ============================================= =========== ====================
ID    Items	                                        Value	    Default Value
===== ============================================= =========== ====================
P19   Clear Wifi Configuration                      Yes or No   No
P20   Clear Parameter setting (restore default)     Yes or No   No
===== ============================================= =========== ====================

* Clear Wifi Configuration: 
    When set to yes,the SSID and Password stored in the thermostat will be clerared  so another SSID and Password can be set again.

* Clear Parameter setting: 
    When set to yes, all Internal parameter setting will be restored to default value in next power on (reset)


Minimum off time
-----------------

The minimum off time for Heat mode is 5 seconds and 4 minutes for Cool mode.



Technical Data
----------------

=========================   ==========================
Power supply:			    195-250 Vac
Relay Contact Voltage:		230Vac Max. 50/60 Hz
Relay Contact Current:		16A Max.
Sensing Element:			103AT
Terminals:				    2 sq. mm Cable 
Operating Temperature:		32 – 122 °F / 0 – 50 °C
Storage Temperature:		23 – 122 °F / -5 – 50 °C
Operating Humidity:		    5-95%RHnon-condensing
=========================   ==========================
