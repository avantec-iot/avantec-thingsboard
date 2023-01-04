*********************************
Connect TA652FC-W to ThingsBoard
*********************************

.. tip::

  - This section applies to both ``TA652FC-W`` and ``TA652FH-W``.
  - Unless otherwise specified, all specifications applicable to TA652FC-W are also applicable to TA652FH-W.

This section describes the process of connecting TA652FC-W to ThingsBoard via Wi-Fi. This process applies to all models of thermostats in this series.

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


Prerequisites. Clear Wi-Fi Configuration
=========================================

.. tip::
    If your TA652FC-W is used for the first time, or your TA652FC-W has never been connected to any Wi-Fi router, you can skip this step.

If your TA652FC-W has been connected to a Wi-Fi router before, when you need to connect to a new Wi-Fi router, you need to clear the Wi-Fi configuration of the TA652FC-W first.

- Press and hold |icon_mode| and |icon_onoff| simultaneously for 10 seconds on the TA652FC-W.

   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/clear_wifi_config_a.png
      :width: 60 %

- Enter Wi-Fi parameter clearing mode P19.
   
   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/clear_wifi_config_b.png
      :width: 60 %

- Press |icon_up| or |icon_down| to select `YES`.

   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/clear_wifi_config_c.png
      :width: 60 %

- Press |icon_mode| to return to the normal interface, and the Wi-Fi parameters are cleared.


Step 1. Get Access-Token
==========================

Get a access-token of TA652FC-W from ThingsBoard. 
See :ref:`Step 5.1 Copy credentials of new TA652FC-W device`.


Step 2. Power On
==================

When you first power up, TA652FC-W will enter Wi-Fi AP mode without any Wi-Fi parameters. At this point, you can configure the parameters through the web page.

.. tip::
   TA652FC-W has a different Wi-Fi Hotspot name every time it's powered on.


Step 3. Configure
===================

- Connect to TA652FC-W's Wi-Fi hotspot on your computer or phone. It's like ``EasyStat-XXXXX``.

   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/connect_ta65_ap.png
      :width: 50 %

- Open your browser, type ``http://192.168.4.1`` .
- Input your configuration, then ``Apply``.

   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/configure_ta65.png


   .. table::
      :widths: auto

      ============  =====================================================================
      Field         Description
      ============  =====================================================================
      Wi-Fi SSID    SSID of your Wi-Fi router
      Password      password of your Wi-Fi router
      Auth Token    Access Token of your TA652FC-W. See `Step 1. Get Access-Token`_
      Host          | This ThingsBoard Server's MQTT URL.
                    | It must begin with "MQTT ://", such as mqtt://192.168.21.206
                    | **Please replace 192.168.21.206 with your Thingsboard IP Address**.
                    | See :ref:`add-shared-attributes-of-ta652fc-w-cloudhost`
      ============  =====================================================================

   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/configure_ta65_connting.png

- If the configuration is successful, the following screen *may be* displayed. 

   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/configure_ta65_result.png


Step 4. Check
================

Check if TA652FC-W is connected to ThingsBoard correctly. If connected correctly, there will be a Wi-Fi icon in the upper right corner of the Thermostat, and the time will no longer be **00:00**. If you do not set the Tonezone relationship on ThingsBoard correctly, the time displayed by TA652FC-W may be slightly off.
 
   .. image:: /_static/device/ta652fc-w/connect-ta652fc-w-to-thingsboard/check_connection.png
      :width: 60%


Troubleshooting
================

Thermostat TA652FC-W cann't connect to Wi-Fi:

- If the Thermostat has never been connected to any Wi-Fi router since leaving the factory, it will enter Soft-AP mode. You can search for Wi-Fi SSID similar to "EasyStat-xxxx" through your mobile phone or computer.
- Make sure the Wi-Fi router supports and turns on the 2.4G signal. Currently, some dual-band (2.4G & 5G) Wi-Fi routers can turn off the 2.4G signal. Please turn it on in your router settings.
- Make sure your Wi-Fi SSID and Password are correct, and they are related parameters of 2.4G Wi-Fi signal.
- Confirm that the Token is normal.

   - Confirm that the Token corresponds to the actual model (the Token of TA652FH-W-TB can only be connected to the Thermostat of TA652FH-W-TB. The same is true for TA652FC-W-TB).
   - Confirm that the Token did not fail during the copying process.
   - Confirm that the Token has no special characters. Token can only contain A-Z, a~z, 0~9. Illegal characters such as "-" will appear in the case of product end. You can edit and get a new Token in `Step 1. Get Access-Token`_.

- Confirm that the `Host` parameter is correct. Host must start with "mqtt://", followed by IP address or domain name of Thingsboard.
- If the above parameters are confirmed to be correct, you can start from `Step 2. Power On`_ and try several times.
