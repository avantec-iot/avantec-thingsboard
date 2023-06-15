Connecting a gateway
======================

`Login <https://www.chirpstack.io/application-server/use/login/>`_ into the ChirpStack Application Server web-interface. The default credentials are:

* Username: admin
* Password: admin

Optional: Adding a Network Server
------------------------------------

Refer to `Network servers <https://www.chirpstack.io/application-server/use/network-servers/>`_.

ChirpStack Application Server is able to connect to one or multiple ChirpStack Network Server instances. Global admin users are able to add new Network Servers to the ChirpStack Application Server installation.

**Note:** once a Network Server is assigned to a `Service Profile <https://www.chirpstack.io/application-server/use/service-profiles/>`_ or `Device Profile <https://www.chirpstack.io/application-server/use/device-profiles/>`_, a Network Server can't be removed before deleting these entities, it will return an error.

When creating a new Network Server, ChirpStack Application Server will create a Routing Profile on the given Network Server, containing the ``hostname:ip`` of the ChirpStack Application Server installation. In case your ChirpStack Application Server installation is not reachable on ``localhost``, make sure this ``hostname:ip`` is configured correctly in your `ChirpStack Application Server Configuration <https://www.chirpstack.io/application-server/install/config/>`_. This Routing Profile is updated on Network Server updates and deleted on Network Server deletes.

#. Go to **Network-servers** -->  **+Add**.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/adding-a-network-server-1.png

#. Type some parameters --> **ADD NETWORK-SERVER**.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Network-server name
          - localhost network server
        * - Network-server server
          - llocalhost:8000
  
    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/adding-a-network-server-2.png

#. Show Network servers.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/adding-a-network-server-3.png



Optional: Creating a Service-profile
--------------------------------------

Refer to `Service profiles <https://www.chirpstack.io/application-server/use/service-profiles/>`_.

The Service Profile can be seen as the "contract" between an user and the network. It describes the features that are enabled for the user(s) of the Service Profile and the rate of messages that can be sent over the network.

When creating a Service Profile, ChirpStack Application Server will create the actual profile on the selected Network Server, and will keep a reference record so it knows to which organization it belongs.

#. Go to **Service-profiles** -->  **+Create**.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/creating-a-service-profile-1.png

#. Type some parameters --> **CREATE SERVICE-PROFILE**

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Service-profile name
          - localhost service profile
        * - Network-server name
          - localhost network server
        * - Add gateway meta-data
          - Enable

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/creating-a-service-profile-2.png

#. Show Service profiles.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/creating-a-service-profile-3.png


Adding a gateway
-----------------

Refer to `Connecting gateway <https://www.chirpstack.io/project/guides/connect-gateway/>`_.

This guide describes how to connect your gateway to ChirpStack and how to validate that it is successfully communicating with the ChirpStack Network Server. At this point it is expected that you have the ChirpStack Application Server and ChirpStack Network Server components up and running.


Requirements
^^^^^^^^^^^^^^^

Before continuing, please make sure that you have installed both a packet-forwarder and the `ChirpStack Gateway Bridge <https://www.chirpstack.io/gateway-bridge/>`_. The packet-forwarder that is installed on your gateway and the steps needed to install the ChirpStack Gateway Bridge vary per gateway vendor and model. In some cases you must also install the ChirpStack Gateway Bridge on the gateway. Please refer to the ChirpStack Gateway Bridge Gateway `installation documentation <https://www.chirpstack.io/gateway-bridge/gateway/>`_, which contains instructions for various gateway models.

Packet-forwarders
###################

There are different packet-forwarder implementations. The packet-forwarder that is installed on your gateway depends on the gateway vendor and model. The packet-forwarders that are compatible with ChirpStack:

* `ChirpStack Concentratord <https://www.chirpstack.io/concentratord/>`_
* `Semtech UDP Packet Forwarder <https://github.com/lora-net/packet_forwarder>`_
* `Semtech BasicStation <https://doc.sm.tc/station/>`_


Configuration
^^^^^^^^^^^^^^^

Packet-forwarder
###################

The packet-forwarder that is configured on your gateway must forward its data to the ChirpStack Gateway Bridge. As it controls the LoRa® chipset of the gateway, it also must be configured for the correct frequencies. A mismatch in frequencies means that the gateway will not receive uplinks sent by a device and / or is unable to send downlink payloads when the downlink frequency is outside the configured frequency range. Usually gateway vendors provide configuration examples for various bands. Please validate that the configuration matches the band and channels in the `ChirpStack Network Server Configuration <https://www.chirpstack.io/network-server/install/config/>`_.


Add gateway
^^^^^^^^^^^

.. tip:: 

    If you have not yet connected your `ChirpStack Application Server <https://www.chirpstack.io/project/application-server/>`_ instance with a `ChirpStack Network Server <https://www.chirpstack.io/project/network-server/>`_ instance, you must do this first. See `Optional: Adding a Network Server`_. Also you must connect the organization with the network-server by `Optional: Creating a Service-profile`_.

#. Go to **Gateways** in the web-interface, and click **+Create**.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/add-gateway-1.png

#. Complete the form. Make sure that the **Gateway ID** field is equal to the Gateway ID of your gateway. If this value is incorrectly configured, data received by your gateway will be rejected. Then click **Create Gateway**.

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Name
          - Headquarters-Gateway
        * - Description
          - MTCAP-868-041A<
        * - Gateway ID (EUI64)
          - *YOUR_GATEWAY_ID*, *eg:0080000000020e0b*
        * - Network-server name
          - localhost network server
        * - Service-profile name
          - localhost service profile

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/add-gateway-2.png

#. Show Gateways.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/add-gateway-3.png


Validate
^^^^^^^^^^^^^^

There are a few ways to validate if your gateway is correctly configured.

Last seen at
##################

Event when no LoRa(WAN) data is received by the gateway, it will send gateway statistics periodically. Usually this stats interval is configured to 30 seconds. As ChirpStack Application Server will update the gateway **Last seen at** timestamp when it receives statistics, this is the easiest way to validate that the gateway is correctly configured. 

**Note:** it might take a short while before statistics are sent by your gateway. You must refresh the page in order to see the (new) **Last seen at** value.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/validate-gateway-1.png


LoRaWAN frames
#################

After opening the overview page of your gateway, you will see a **LoRaWAN frames** tab. This will show all LoRaWAN frames that are received and sent by your gateway. In case of received frames, this means that you will also see received frames from devices that are not yours and / or that are not yet configured. Therefore this screen is useful to validate if your gateway is able to receive LoRaWAN frames and forward these to ChirpStack.

    .. image:: /_static/device/ta692fc-l-5/chirpstack-v3-connecting-a-gateway/validate-gateway-2.png


Troubleshooting
^^^^^^^^^^^^^^^^^^

See `Troubleshooting gateway <https://www.chirpstack.io/project/guides/connect-gateway/#troubleshooting>`_.