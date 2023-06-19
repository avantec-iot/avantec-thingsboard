
Connecting a device
=========================

Refer to `Connecting device <https://www.chirpstack.io/project/guides/connect-device/>`_.

This guide describes how to connect your LoRaWAN device with ChirpStack and how to validate that it can successfully activate. At this point it is expected that you have the ChirpStack Network Server and ChirpStack Application Server components installed and that you have successfully connected a LoRa gateway to it.

Requirements
---------------

Before continuing, there are a couple things you need to know about your device. This information is usually provided by the device vendor.

* DevEUI
* LoRaWAN MAC version implemented by the device
* Regional Parameters revision implemented by the device
* OTAA: Device root-keys (when no external join-server is used)

Login
---------

Login into the ChirpStack Application Server web-interface. The default credentials are:

* Username: admin
* Password: admin


Optional: Creating a Device profile
-------------------------------------

Before you can add the device to ChirpStack, you have to create a `Device-profile <https://www.chirpstack.io/application-server/use/device-profiles/>`_ if you haven't done this already. In general it is a good practice to create separate device-profiles for different types of devices. A device-profile contains the capabilities of your device. For example if it uses ABP or OTAA for activation, which LoRaWAN version and Regional Parameters revision is implemented by the device, etc... It can also be configured with a function to decode the payloads sent by the devices using the device-profile.

#. Within the ChirpStack Application Server web-interface, click **Gateways** and then **Create**.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-profile-1.png

#. Under the **General** tab, fill in the required fields.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Name
          - TA692FC-L-5-868 Thermostat
        * - Network-server
          - localhost network server
        * - Region
          - EU868
        * - LoRaWAN MAC version
          - LoRaWAN 1.0.3
        * - LoRaWAN Regional parameters revision
          - A
        * - ADR algorithm
          - Default ADR algorithm (LoRa only)
        * - Uplink interval (seconds)
          - 1000
        * - Device-status request frequency (req/day)
          - 1

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-profile-2.png

#. Under the **Join (OTTA/ABP)** tab, fill in the required fields.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Join (OTAA / ABP)
          - yes, Device supports OTAA

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-profile-3.png

#. Under the **Class-B** tab, fill in the required fields.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Supports Class-B
          - no

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-profile-4.png

#. Under the **Class-C** tab, fill in the required fields.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Supports Class-C
          - yes
        * - Class-C confirmed downlink timeout (seconds)
          - 300

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-profile-5.png

#. Under the **Codec** tab, fill in the required fields. Then click **create device-profile**.

    **Note:** The data here may not be decoded. It's here just for debugging convenience.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Payload codec
          - Custom JavaScript codec functions

    .. code:: JavaScript

        // Decode decodes an array of bytes into an object.
        //  - fPort contains the LoRaWAN fPort number
        //  - bytes is an array of bytes, e.g. [225, 230, 255, 0]
        //  - variables contains the device variables e.g. {"calibration": "3.5"} (both the key / value are of type string)
        // The function must return an object, e.g. {"temperature": 22.5}
        function Decode(fPort, bytes, variables) {
            var dataX = {};
            var fanModeStateMeta = {
            0: "OFF",
            1: "LOW",
            2: "MED",
            3: "HIGH",
            4: "AUTO"
            };
            var systemModeMeta = {
            0: "OFF",
            1: "COOL",
            2: "FAN-ONLY"
            };
            if(fPort==10){
            dataX.roomTemperature = ((bytes[0] << 8) + bytes[1])/10;
            dataX.setTemperature = ((bytes[2] << 8) + bytes[3])/10;
            dataX.coolProportionalOutput = bytes[4]/100;
            dataX.fanMode = fanModeStateMeta[bytes[5]];
            dataX.fanState = fanModeStateMeta[bytes[6]];
            dataX.threshold = bytes[7]/10;
            dataX.systemMode = systemModeMeta[bytes[8]];
            dataX.coolPBand = bytes[9]/10;
            dataX.coolItime = (bytes[10] << 8) + bytes[11];
            dataX.kFactor = bytes[12];
            return {
                data: {
                roomTemperature: dataX.roomTemperature,
                setTemperature: dataX.setTemperature,
                coolProportionalOutput: dataX.coolProportionalOutput,
                fanMode: dataX.fanMode,
                fanState: dataX.fanState,
                threshold: dataX.threshold,
                systemMode: dataX.systemMode,
                coolPBand: dataX.coolPBand,
                coolItime: dataX.coolItime,
                kFactor: dataX.kFactor
                }
            };
            }
        }


    .. code:: JavaScript

        // Encode encodes the given object into an array of bytes.
        //  - fPort contains the LoRaWAN fPort number
        //  - obj is an object, e.g. {"temperature": 22.5}
        //  - variables contains the device variables e.g. {"calibration": "3.5"} (both the key / value are of type string)
        // The function must return an array of bytes, e.g. [225, 230, 255, 0]
        function Encode(fPort, obj, variables) {
        return [];
        }

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-profile-6.png

#. Show Device profiles.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-profile-7.png



Optional: Adding an Application
-----------------------------------

Devices are grouped by applications. For example you could group your temperature sensors under one application and weather stations under an other application.

#. If you haven't created an application yet to which you want to add the device, click **Applications**, then click **Create**. 

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-an-application-1.png

#. Fill in the required fields and **Create Application**.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Name
          - TA692FC-L-5-Application
        * - Description
          - TA692FC-L-5-868 Thermostat, TA692FC-L-5-915 Thermostat
        * - Service-profile name
          - localhost service profile

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-an-application-2.png

#. Show Applications.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-an-application-3.png


Creating a device
-------------------

#. Click the (newly created) **application** to which you want to add your device. 

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-0.png

#. Under the **Devices** tab, click **Create**. 

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-1.png

#. Fill in the required fields and select the device-profile that you want to associate with your device and save the device.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Name
          - Sales-Office
        * - Description
          - TA692FC-L-5-868 device
        * - Device EUI (EUI64)
          - *YOUR_DEVICE_EUI*, *eg:0012bdfffe02ad04*
        * - Device profile
          - TA692FC-L-5-868 Thermostat

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-2.png

#. Depending the device-profile is configured for OTAA or ABP, the next page will ask you to enter the device root-keys (OTAA) or device session-keys (ABP).

   In case your ChirpStack Network Server is configured with a join-server and your (OTAA) device will use this join-server for activation, then there is no need to enter the root-keys.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Application key
          - *YOUR_DEVICE_EUI*, *eg:72357538782F413F4428472B4B625065*

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-3.png

#. Show **Devices**.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/creating-a-device-4.png




Validate
----------

#. After adding your LoRaWAN device to ChirpStack, validate that your device is able activate (in case of OTAA) and send data. Clicking the device in the ChirpStack Application Server web-interface.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/validate-device-1.png

#. Open in one window the **Device data** and in an other window the **LoRaWAN frames** tab.
   Then turn on your device or trigger an uplink transmission. In case of an OTAA device you should first see a JoinRequest followed by a JoinAccept message in the **LoRaWAN frames** tab.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/validate-device-2.png


#. When the device sends its first data payload, you should also see a Join and Up event in the **Device data** tab.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-device/validate-device-3.png


Troubleshooting
-----------------

See `Troubleshooting device <https://www.chirpstack.io/project/guides/connect-device/#troubleshooting>`_.
