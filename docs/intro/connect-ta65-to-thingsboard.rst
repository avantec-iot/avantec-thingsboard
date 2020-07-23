Connect TA65 to ThingsBoard
===========================

本节描述 TA65 通过 Wi-Fi 连接 ThingsBoard 的过程。适用于本系列的所有型号恒温器。

Prerequisites. Clear Wi-Fi Configuration
----------------------------------------

.. tip::
    如果您的 TA65 是第一次使用，或者您的 TA65 从来没有连接上任何 Wi-Fi 路由器， 可以跳过这一步。

如果您的 TA65 连接上 Wi-Fi 路由器使用过，当您需要连接新的 Wi-Fi 路由器时，需要首先清除 TA65 的 Wi-Fi 配置。

- 在 TA65 上同时长按 Mode、Power 两个按键 10 秒钟。

   .. image:: /_static/intro/connect_ta65_to_thingsboard/clear_wifi_config_a.png
      :width: 60 %

- 进入 Wi-Fi 参数清除模式 P19。
   
   .. image:: /_static/intro/connect_ta65_to_thingsboard/clear_wifi_config_b.png
      :width: 60 %

- 按 Up 或 Down, 选择 Yes。

   .. image:: /_static/intro/connect_ta65_to_thingsboard/clear_wifi_config_c.png
      :width: 60 %

- 按 Mode 返回至正常界面，则 Wi-Fi 参数清除。


Step 1. Get Access-Token
------------------------

Get a access-token of TA65 from ThingsBoard. 
See :ref:`copy-credentials-of-new-device`.


Step 2. Power On
------------------

When you first power up, TA65 will enter Wi-Fi AP mode without any Wi-Fi parameters. At this point, you can configure the parameters through the web page.

.. tip::
   TA65 has a different Wi-Fi Hotspot name every time it's powered on.


Step 3. Configure
-----------------

- Connect to TA65's Wi-Fi hotspot on your computer or phone.

   .. image:: /_static/intro/connect_ta65_to_thingsboard/connect_ta65_ap.png
      :width: 50 %

- Open your browser, type ``http://192.168.4.1`` .
- Input your configuration, then ``Apply``.

   .. image:: /_static/intro/connect_ta65_to_thingsboard/configure_ta65.png

   .. table::
      :widths: auto

      ============  =====================================================================
      Field         Description
      ============  =====================================================================
      Wi-Fi SSID    SSID of your Wi-Fi router
      Password      password of your Wi-Fi router
      Auth Token    Access Token of your TA65. See `Step 1. Get Access-Token`_
      Host          | This ThingsBoard Server's MQTT URL.
                    | It must begin with "MQTT ://", such as
                    | mqtt://192.168.21.222
                    | **Please replace 192.168.21.222 with your Thingsboard IP Address**.
                    | See :ref:`add-shared-attributes-of-new-device-cloudhost`
      ============  =====================================================================

- If saved successfully, the following will be displayed.

   .. image:: /_static/intro/connect_ta65_to_thingsboard/configure_ta65_result.png


Step 4. Check
-------------

检查 TA65 是否正确连上 ThingsBoard。若正确连上，Thermostat右上角会有 Wi-Fi 图标，时间也不再是 **00:00**。
如果你没有在 ThingsBoard 上正确设置时区 Tonezone 的关系，TA65 显示的时间可能有些偏差。
 
   .. image:: /_static/intro/connect_ta65_to_thingsboard/check_connection.png
      :width: 60%


Troubleshooting
---------------

Thermostat TA65 连不上 Wi-Fi:

- 如果 Thermostat 出厂后从来没有连上任何的 Wi-Fi 路由器，那它会进入 Soft-AP 模式。\
  你能通过手机或电脑，搜索到类似 “Thermostat-xxxx”的Wi-Fi信号。
- 确认 Wi-Fi 路由器支持且开启了 2.4G 信号。目前有部分双频（2.4G&5G）Wi-Fi 路由器\
  可以关闭 2.4G 信号。请在路由器设置中打开它。
- 确认你的 Wi-Fi SSID、Password 正确，而且是 2.4G Wi-Fi 信号的相关参数。
- 确认 Token 正常。

   - 确认 Token 与实物的型号对应正确（TA65-FH-TB 的 Token 只能连 TA65-FH-TB 的 \
     Thermostat. TA65-FC-TB 也是如此）。
   - 确认 Token 没有在复制过程出错。
   - 确认 Token 没有特殊字符。Token 只能包含 A-Z、a~z、0~9。在积端情况下会出现 “-” \
     等非法字符。你可以在 `Step 1. Get Access-Token`_ 编辑获取一个新的 Token。

- 确认 Host 参数正确。Host必须是以"mqtt://"开头，后面带上 Thingsboard 的 IP 地址或域名。
- 若以上参数确认无误，你可以从 `Step 2. Power On`_ 开始，多次尝试。
