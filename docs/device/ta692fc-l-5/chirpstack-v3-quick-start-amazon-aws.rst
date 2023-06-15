Quick start Amazon AWS
==============================

Refer  to `Quickstart Debian or Ubuntu <https://www.chirpstack.io/project/guides/debian-ubuntu/>`_.

This section describes the steps needed to setup the ChirpStack stack including all requirements on a single machine. It has been tested on the following distributions (but with non or minimal modifications it will work on other versions too):

* Ubuntu 20.04 LTS

Please refer to the other install pages for more generic installation instructions.

Assumptions
---------------

Many configurations of these packages are possible. Dependent software packages could be installed on any number of remote servers, and the packages themselves could be on their own servers. However, in order to simplify the initial installation, we will assume the following deployment architecture:

* All ChirpStack components and their dependencies will be installed on a single server instance.
* The `ChirpStack Gateway Bridge <https://www.chirpstack.io/gateway-bridge/>`_ component will be installed on the server, but can also be installed on the gateway itself.
* No firewall rules are setup.

Of course, optimizations may need to be made depending on the performance of your systems. You may opt to move the PostgreSQL database to another server. Or you may decide to put your MQTT broker on a different system, or even use a different server than the one recommended in this document. These and other installation changes are beyond the scope of this document. However, you should be able to find the information here that would make these changes relatively straight-forward.


Prerequisites
-------------

#. Launch an Amazon EC2 instance:

    .. list-table::
        :widths: auto
        :header-rows: 1

        * - Item
          - Description
        * - Software Image (AMI)
          - Ubuntu Server 20.04 LTS (HVM), SSD Volume Type, |br|  64-bit (x86)
        * - Virtual server type (instance type)
          - t3.micro, |br| Family: t3, 2 vCPU, 1 GiB Memory, Current generation: true
        * - Firewall (security group)
          - ssh; |br| https; |br| 8080, tcp, http;  |br| 1700, udp, LoRaWAN uplink
        * - Configure storage
          - 1 x 8 GiB, Volume type: gp2, Root volume (Not encrypted)

#. Allocate Elastic IP address.

#. Associate Elastic IP address with the EC2 instance.

.. # define a hard line break for HTML
.. |br| raw:: html

   <br/>


Install dependencies
--------------------

* **MQTT broker** - A publish/subscribe protocol that allows users to publish information under topics that others can subscribe to. A popular implementation of the MQTT protocol is `Mosquitto <https://mosquitto.org/>`_.
* **Redis** - An in-memory database used to store relatively transient data.
* **PostgreSQL** - The long-term storage database used by the open source packages.

Use the package manager apt to install these dependencies:

.. code:: bash

  sudo apt update
  sudo apt install mosquitto mosquitto-clients redis-server redis-tools postgresql


Setup PostgreSQL databases and users
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To enter the command line utility for PostgreSQL:

.. code:: bash

  sudo -u postgres psql


Inside this prompt, execute the following queries to set up the databases that are used by the ChirpStack stack components. It is recommended to change the usernames and passwords. Just remember to use these other values when updating the ``chirpstack-network-server.toml`` and ``chirpstack-application-server.toml`` configuration files. Since these two applications both use the same table to track database upgrades, they must have separate databases.


.. code:: psql

  -- set up the users and the passwords
  -- (note that it is important to use single quotes and a semicolon at the end!)
  create role chirpstack_as with login password 'dbpassword';
  create role chirpstack_ns with login password 'dbpassword';

  -- create the database for the servers
  create database chirpstack_as with owner chirpstack_as;
  create database chirpstack_ns with owner chirpstack_ns;

  -- change to the ChirpStack Application Server database
  \c chirpstack_as

  -- enable the pq_trgm and hstore extensions
  -- (this is needed to facilitate the search feature)
  create extension pg_trgm;
  -- (this is needed to store additional k/v meta-data)
  create extension hstore;

  -- exit psql
  \q



Setup ChirpStack software repository
------------------------------------

ChirpStack provides a repository that is compatible with the Ubuntu apt package system. First make sure that both ``dirmngr`` and ``apt-transport-https`` are installed:

.. code:: bash

   sudo apt install apt-transport-https dirmngr


Set up the key for this new repository:

.. code:: bash

  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1CE2AFD36DBCCA00


Add the repository to the repository list by creating a new file:

.. code:: bash

  sudo echo "deb https://artifacts.chirpstack.io/packages/3.x/deb stable main" | sudo tee /etc/apt/sources.list.d/chirpstack.list


Update the apt package cache:

.. code:: bash

  sudo apt update



Install ChirpStack Gateway Bridge
----------------------------------

Note: If you intend to run the `ChirpStack Gateway Bridge <https://www.chirpstack.io/gateway-bridge/>`_ only on gateway(s) themselves, you can skip this step.

Install the package using ``apt``:

.. code:: bash

  sudo apt install chirpstack-gateway-bridge


log output:

.. code::

  ----------------------------------------------------------
  The configuration file is located at:
  /etc/chirpstack-gateway-bridge/chirpstack-gateway-bridge.toml

  Some helpful commands for chirpstack-gateway-bridge:
  Start:
  $ sudo systemctl start chirpstack-gateway-bridge
  
  Restart:
  $ sudo systemctl restart chirpstack-gateway-bridge

  Stop:
  $ sudo systemctl stop chirpstack-gateway-bridge

  Display logs:
  $ sudo journalctl -f -n 100 -u chirpstack-gateway-bridge
  ----------------------------------------------------------

The configuration file is located at ``/etc/chirpstack-gateway-bridge/chirpstack-gateway-bridge.toml``. The default configuration is sufficient for this guide.

Start the ChirpStack Gateway Bridge service:

.. code:: bash

  # start chirpstack-gateway-bridge
  sudo systemctl start chirpstack-gateway-bridge

  # start chirpstack-gateway-bridge on boot
  sudo systemctl enable chirpstack-gateway-bridge


Install ChirpStack Network Server
----------------------------------

Install the package using apt:

.. code:: bash
  
  sudo apt install chirpstack-network-server


log output:

.. code::

  -----------------------------------------------------
  The configuration file is located at:
  /etc/chirpstack-network-server/chirpstack-network-server.toml

  Some helpful commands for chirpstack-network-server:
  Start:
  $ sudo systemctl start chirpstack-network-server

  Restart:
  $ sudo systemctl restart chirpstack-network-server

  Stop:
  $ sudo systemctl stop chirpstack-network-server
  
  Display logs:
  $ sudo journalctl -f -n 100 -u chirpstack-network-server
  -------------------------------------------------------


The configuration file is located at ``/etc/chirpstack-network-server/chirpstack-network-server.toml`` and must be updated to match the database and band configuration. See below two examples for the **EU868** and **US915** band.  For more information about all the ChirpStack Network Server configuration options, see `here <https://www.chirpstack.io/project/guides/debian-ubuntu/#installing-the-chirpstack-network-server>`_ or `ChirpStack Network Server configuration <https://www.chirpstack.io/network-server/install/config/>`_.

After updating the configuration, you need to restart the ChirpStack Network Server and validate that there are no errors.

Start the ChirpStack Network Server service:

.. code:: bash
  
  # start chirpstack-network-server
  sudo systemctl start chirpstack-network-server

  # start chirpstack-network-server on boot
  sudo systemctl enable chirpstack-network-server


Print the ChirpStack Network Server log-output:

.. code:: bash

  sudo journalctl -f -n 100 -u chirpstack-network-server



EU868 configuration example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: toml

  [general]
  log_level=4

  [postgresql]
  dsn="postgres://chirpstack_ns:dbpassword@localhost/chirpstack_ns?sslmode=disable"

  [network_server]
  net_id="000000"

    [network_server.band]
    # name="EU_863_870"
    name="EU868"

    [[network_server.network_settings.extra_channels]]
    frequency=867100000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867300000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867500000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867700000
    min_dr=0
    max_dr=5

    [[network_server.network_settings.extra_channels]]
    frequency=867900000
    min_dr=0
    max_dr=5



US915 configuration example sub-band 1 (125kHz channels 0 - 7 & 500kHz channel 64)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: toml

  [general]
  log_level=4

  [postgresql]
  dsn="postgres://chirpstack_ns:dbpassword@localhost/chirpstack_ns?sslmode=disable"

  [network_server]
  net_id="000000"

  [network_server.band]
  # name="US_902_928"
  name="US915"

  [network_server.network_settings]
  enabled_uplink_channels=[0, 1, 2, 3, 4, 5, 6, 7, 64]


US915 configuration example sub-band 2 (125kHz channels 8 - 15 & 500kHz channel 65)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is the same channel-plan as used by The Things Network.

.. code:: toml

  [general]
  log_level=4

  [postgresql]
  dsn="postgres://chirpstack_ns:dbpassword@localhost/chirpstack_ns?sslmode=disable"

  [network_server]
  net_id="000000"

  [network_server.band]
  # name="US_902_928"
  name="US915"

  [network_server.network_settings]
  enabled_uplink_channels=[8, 9, 10, 11, 12, 13, 14, 15, 65]



Install ChirpStack Application Server
-------------------------------------

Install the package using apt:

.. code:: bash

  sudo apt install chirpstack-application-server

log output:

.. code::

  -------------------------------------------------------
  The configuration file is located at:
  /etc/chirpstack-application-server/chirpstack-application-server.toml

  Some helpful commands for chirpstack-application-server:
  Start:
  $ sudo systemctl start chirpstack-application-server

  Restart:
  $ sudo systemctl restart chirpstack-application-server

  Stop:
  $ sudo systemctl stop chirpstack-application-server

  Display logs:
  $ sudo journalctl -f -n 100 -u chirpstack-application-server
  -------------------------------------------------------

The configuration file is located at ``/etc/chirpstack-application-server/chirpstack-application-server.toml`` and must be updated to match the database configuration. See below a configuration example which matches the database which we have created in one of the previous steps. For more information about the ChirpStack Application Server configuration options, see `ChirpStack Application Server configuration <https://www.chirpstack.io/application-server/install/config/>`_.

.. code:: toml

  [general]
  log_level=4

  [postgresql]
  dsn="postgres://chirpstack_as:dbpassword@localhost/chirpstack_as?sslmode=disable"

    [application_server.external_api]
    jwt_secret="M9LoHX3wPQlcB2ziakV6qs/F2vLOvkAtrRv1yTu5Kks="


Note: you must replace the ``jwt_secret`` with a secure secret! You could use the command ``openssl rand -base64 32`` to generate a random secret.


Start the ChirpStack Application Server service:

.. code:: bash

  # start chirpstack-application-server
  sudo systemctl start chirpstack-application-server

  # start chirpstack-application-server on boot
  sudo systemctl enable chirpstack-application-server

Print the ChirpStack Application Server log-output:

.. code:: bash

  sudo journalctl -f -n 100 -u chirpstack-application-server