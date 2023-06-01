*************************************************
Release Notes
*************************************************

v2.2 (June 1, 2023)
===================

* TA652FC-W MQTT API/Protocol
    * New feature: support (control mode) on/off in schdule.
        * New client-side attributes: ``supportCtrlModeInSchedule`` (string), ``prgNextCtrlMode`` (string),  ``prgCtrlModeXX`` (string).
        * New Server-side RPC: ``remoteSetPrgCtrlModeXX``.

* Avantec Widgets
    * New widget for on/off in schdule - ``Styled button of string value with pattern key``.
    * Fixed bug: primary color of some widgets about button can't be used in ThingsBoard v3.5.1.
    * Fixed bug: Setting list is not disyplayed properly in ThingsBoard v3.5.1.

* TA652FC-W Dashboards
    * TA652FC-W List Dashboard
        * New feature: support for modifying device label.
    * TA652FC-W Detail Dashboard
        * New feature: support (control mode) on/off in schdule.

* TA652FH-W Dashboards
    * TA652FH-W List Dashboard
        * New feature: support for modifying device label.
    * New dashboard - Office Center Dashboard


v2.1 (Apr 18, 2023)
===================

* TA652FC-W/TA652FH-W MQTT API/Protocol
	* New shared attributes: ``uploadThreshold`` (double).
	* New client-side attributes: ``uploadThresholdMin``, ``uploadThresholdMax``,  ``uploadThresholdStep`` (double).

* Refactor all documentation
* Refactor all widgets
* Refactor all dashboards


v1.0 (Jul 24, 2020 / Dec 20, 2022)
=====================================

Inital version.
