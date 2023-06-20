*************************************************
TA692FC-L -- FCU Thermostat Series
*************************************************

.. table:: 
    :widths: 35, 65

    ============================ ===========================================================
    Operating Voltage		     230 VAC ±10%
    Measurable range		     0 - 40 °C, 0.1°C
    LoRaWAN			             Class C
    EU868 band                   868.1 MHz ~ 868.5 MHz
    AS923 band (Optional)        923.2 MHz ~ 923.4 MHz
    ============================ ===========================================================

Features
=========

* Wireless thermostats for fan coil units
* 1.5” VA TN with backlit - lite grey text on dark background
* Touch keys x 5
* Flush-mount installation in an 86 x 86 / British single-gang wall-box
* White gloss housing with light grey silk-printed keys
* Controls:
    * 3-speed fan
    * One DC 0…10V valve actuators
* Used in systems with:
    * Fan coil units
    * Heating and cooling appliances

Technical Specification
=========================

.. table::
    :widths: 35, 65

    ======================================= ===============================================
    Transmitting power						21.0dBm
    Receiving sensitivity					-140dBm
    Effective range outdoors				TBD  
    Measuring temperature					0 ~ 40°C
    Controlling temperature					5 ~ 35°C
    Adjustable span							1.0°C ~ 4.0°C
    Sensing Element							103AT
    Storage Temperature						-5 ~ 50°C
    Measuring accuracy/resolution			±0.5°C
    On/Off Relay Contact Rating				230VAC 2(1)A max
    AO Contact Rating						10VDC 1mA max
    Terminals								2 mm :sup:`2` cable
    Operating Temperature					0 ~ 50°C
    Operating Voltage						230VAC ±10%
    Operating Humidity						5 ~ 95%R.H. non-condensing            
    ======================================= ===============================================


Order Code
============

.. table::
    :widths: auto

    =========== =========== =================== =================== ======= =========================================
    Symbols     Fan Control Heating             Cooling             LoRa    Frequnecy
    =========== =========== =================== =================== ======= =========================================
    TA692FC-L-1 3-Speed     On/Off heater       On/Off valve        LoRoWAN endpoint 868.1M~868.5MHz, or 920M~925MHz
    TA692FC-L-2 0~10V       On/Off heater       On/Off valve        LoRoWAN endpoint 868.1M~868.5MHz, or 920M~925MHz
    TA692FC-L-3 0~10V       On/Off heater       0~10V modulating    LoRoWAN endpoint 868.1M~868.5MHz, or 920M~925MHz
    TA692FC-L-4 0~10V       0~10V modulating    0~10V modulating    LoRoWAN endpoint 868.1M~868.5MHz, or 920M~925MHz
    TA692FC-L-5 3-Speed     ---                 0~10V modulating    LoRoWAN endpoint 868.1M~868.5MHz, or 920M~925MHz
    =========== =========== =================== =================== ======= =========================================

Dimensions / Outline
======================

* Protruding part - 86.0mm(W) x 86.0mm(H) x 16.5mm(D)
* Concealed part - 64.0mm(W) x 66.5mm(H) x 26.6mm(D)

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/dimension-1.png
    :width: 40%

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/dimension-2.png
    :width: 18%

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/dimension-3.png
    :width: 35%

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/dimension-4.png
    :width: 38%


Product pictures
=======================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/product-picture-1.png
    :width: 30%

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/product-picture-2.png
    :width: 33%

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/product-picture-3.png
    :width: 30%



Wiring Example for TA692FC-L-1
==================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/wiring-example-for-ta692fc-l-1.png
    :width: 80%

.. table::
    :widths: auto

    ======= =========== 
    Symbols	Terminals
    ======= =========== 
    L	    Live
    N	    Neutral
    Q1	    Control output Fan speed 1, 230VAC
    Q2	    Control output Fan speed 2, 230VAC
    Q3	    Control output Fan speed 3, 230VAC
    Y1	    Control output for Cool Valve ON/OFF, 230VAC
    Y2	    Control output for Heater ON/OFF, 230VAC
    ======= =========== 

Terminal Labels on TA692FC-L-1
=================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/terminal-labels-on-ta692fc-l-1-1.png
    :width: 40%




Wiring Example for TA692FC-L-2
==================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/wiring-example-for-ta692fc-l-2.png
     :width: 80%

.. table::
    :widths: auto

    ======= =========== 
    Symbols	Terminals
    ======= =========== 
    L	    Live
    N	    Neutral
    G	    Control output to EC Fan 0...10VDC
    Y1	    Control output Cool valve ON/OFF. 230VAC
    Y2	    Control output Heater ON/OFF. 230VAC
    ======= =========== 

Terminal Labels on TA692FC-L-2
=================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/terminal-labels-on-ta692fc-l-2-1.png
    :width: 40%



Wiring Example for TA692FC-L-3
==================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/wiring-example-for-ta692fc-l-3.png
    :width: 80%

.. table::
    :widths: auto

    ======= =========== 
    Symbols	Terminals
    ======= =========== 
    L	    Live
    N	    Neutral
    G	    Control output to EC Fan 0...10VDC
    Y1	    Modulating control to Cool valve 0...10VDC 
    Y2	    Control output Heater ON/OFF. 230VAC
    ======= =========== 

Terminal Labels on TA692FC-L-3
=================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/terminal-labels-on-ta692fc-l-3-1.png
    :width: 40%



Wiring Example for TA692FC-L-4
==================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/wiring-example-for-ta692fc-l-4.png
    :width: 80%

.. table::
    :widths: auto

    ======= =========== 
    Symbols	Terminals
    ======= =========== 
    L	    Live
    N	    Neutral
    G	    Control output to EC Fan 0...10VDC
    Y1	    Modulating control to Cooling valve 0...10VDC
    Y2	    Modulating control to Heating valve 0...10VDC
    ======= =========== 

Terminal Labels on TA692FC-L-4
=================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/terminal-labels-on-ta692fc-l-4-1.png
    :width: 40%



Wiring Example for TA692FC-L-5
==================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/wiring-example-for-ta692fc-l-5.png
    :width: 80%

.. table::
    :widths: auto

    ======= =========== 
    Symbols	Terminals
    ======= =========== 
    L	    Live
    N	    Neutral
    Q1	    Control output Fan speed 1, 230VAC
    Q2	    Control output Fan speed 2, 230VAC
    Q3	    Control output Fan speed 3, 230VAC
    Y1	    Control output to Cooling valve 0...10VDC
    ======= =========== 

Terminal Labels on TA692FC-L-5
=================================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/terminal-labels-on-ta692fc-l-5-1.png
    :width: 40%



Output diagrams 
================

* **Fan controls** - Q :sub:`1` Q :sub:`2` Q :sub:`3` - in **Auto Fan Mode**. Applicable to TA692FC-L-1, TA692FC-L-5 Except when Power Off, TA692FC-L is always running at low-fan (Q :sub:`1`  On).

    .. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/output-diagrams-1.png

* Cooling Valve (Y :sub:`1`)
   PI control of Cooling Valve (Y :sub:`1`) in Cool Mode. 

   Applicable to TA692FC-L-3, TA692FC-L-4, TA692FC-L-5.

   TA692FC-L employs proportional-integrative modulating control (PI). 

   Diagram shows changing in temperature difference versus Y1 voltage level over time.

   Ion |icon-valve| blinks when output power is under 70%; persistently on at 100%; disppears at 0%. 

   Refer to subsequent sections for K-Factor, P-band and I-time settings.

    .. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/output-diagrams-2.png

* Cooling Valve (Y1) in Fan-Only Mode
   Applicable to TA692FC-L-3, TA692FC-L-4, TA692FC-L-5.
   
   If Fan-Only Mode is selected, Y1 simply shuts off. |icon-valve|  disappears.


    .. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/output-diagrams-3.png

.. |icon-valve|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-valve.png


LCD Display Content
====================

.. image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/lcd-display-content-1.png


Icons
^^^^^^^


.. table::
    :widths: auto

    =============== ========================== 
    Label	        Description
    =============== ========================== 
    6	            Room temperature 
    7	            Temperature Setpoint
    9	            | System Mode icon 
                    | |icon-cool| Cool mode
                    | |icon-heat| Heat mode 

                    no icon - **Fan-Only mode**

    12	            Y1 output status indicator  
    13	            Y2 output status indicator
    14              | Fan status indictor
                    | |icon-auto| Auto Fan Mode

                    no icon - Manual Fan Mode

    |icon-fan-high| High Fan Speed indicator
    |icon-fan-med|  Med Fan speed indicator
    |icon-fan-low|  Low Fan speed indicator
    =============== ========================== 

.. |icon-cool|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-cool.png

.. |icon-heat|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-heat.png

.. |icon-auto|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-auto.png

.. |icon-fan-high|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-fan-high.png

.. |icon-fan-med|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-fan-med.png

.. |icon-fan-low|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-fan-low.png



Buttons
^^^^^^^^^^

.. table::
    :widths: auto

    =================== ===================== 
    Keys	            Function
    =================== ===================== 
    |icon-menu|         | Menu Key 
                        | Short press: change mode
                        | Press-n-hold: Internal setting    
    |icon-fan-speed|    | Fan Speed
                        | Short press: cycle-through
                        | L->M->H->Auto->L
    |icon-power|        Power On/Off Key    
    |icon-up|           Traverse Up in Setting Menu    
    |icon-down|         Traverse Down in Setting Menu
    =================== =====================  

.. |icon-menu|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-menu.png

.. |icon-fan-speed|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-fan-speed.png

.. |icon-power|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-power.png

.. |icon-up|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-up.png

.. |icon-down|  image:: /_static/device/ta692fc-l-5/ta692fc-l-5-specifications/icon-down.png



Internal Parameter Menu in TA692FC-L-5
===============================================

.. table::
    :widths: auto

    =================== =========================== ========== 
    Items	            Selection	                Default 
    =================== =========================== ========== 
    System Mode (P00)	Cool / Fan-only (CL/FAN)	Cool (CL)
    Calibration (P04)	-4°C ~ 4°C 	                0°C 
    Span for Cool (P09)	1.0°C ~ 4.0°C	            1.0°C 
    K-Factor(1/K) (P10)	1 ~ 9	                    3
    P-band Cool (P12)	1.0oC ~ 4.0°C	            4.0°C
    I-Time Cool (P14)	5 ~ 180 sec	                30 sec
    =================== =========================== ========== 

Advanced Parameter Menu in TA692FC-L-5
============================================

.. table::
    :widths: auto

    =============================================== =========================== ================
    Items	                                        Selection	                Default
    =============================================== =========================== ================
    Restore Default on the next power-cycle (P20)   Disabled/Enabled (DIS/EN)	Disabled(DIS)
    LoRa status (P36)	                            Active/disconnect (on/dis)	Active (on)
    Dev EUI (P37 ~ P44)	                            HEX. Read-only	            --
    =============================================== =========================== ================
