
******************
Get Started
******************

Reprinted articles:  https://thingsboard.io/docs/getting-started-guides/helloworld/

Introduction
==============

The goal of this tutorial is to demonstrate the basic usage of the most popular ThingsBoard features. You will learn how to:

* Connect devices to ThingsBoard;
* Import real-time end-user dashboards.

We will connect and visualize data from the ``TA652FC-W`` to keep it simple.

Refer to `Here`_ to get support for the following features:

* Define thresholds and trigger alarms;
* Push notifications about new alarms over email, sms or other systems.

.. _Here: https://thingsboard.io/docs/getting-started-guides/helloworld/


Prerequisites
================

You will need to have ThingsBoard server up and running. 

* The easiest way is to use `Live Demo server`_.
* The alternative option is to install ThingsBoard using `Installation Guide`_. 
* **Windows** users should follow this `guide`_. 
* **Linux** users that have docker installed should execute the following commands:

.. code:: bash

    mkdir -p ~/.mytb-data && sudo chown -R 799:799 ~/.mytb-data
    mkdir -p ~/.mytb-logs && sudo chown -R 799:799 ~/.mytb-logs
    docker run -it -p 9090:9090 -p 7070:7070 -p 1883:1883 -p 5683-5688:5683-5688/udp -v ~/.mytb-data:/data \
    -v ~/.mytb-logs:/var/log/thingsboard --name mytb --restart always thingsboard/tb-postgres

These commands install ThingsBoard and load demo data and accounts.

ThingsBoard UI will be available using the URL: http://localhost:8080 . You may use username **tenant@thingsboard.org** and password **tenant**. More info about `demo accounts`_ is available.

.. _Live Demo server: https://demo.thingsboard.io/signup
.. _Installation Guide: https://thingsboard.io/docs/user-guide/install/installation-options/
.. _guide: https://thingsboard.io/docs/user-guide/install/docker-windows/
.. _demo accounts: https://thingsboard.io/docs/samples/demo-account/

Step 1. Provison device
========================


step 2. Connect device
=======================


Step 3. Import Avantec Widget
==============================


Step 4. Import Avantec Dashboard
=================================

Step 4.1 Import Avantec dashboard
-----------------------------------

Step 4.2 Modify entity alias
-----------------------------


Step 5. Share dashboard with customers
=======================================

Step 5.1 Create customers
--------------------------

Step 5.2 Assign device to Customer
-----------------------------------

Step 5.3 Assign dashboard to Customer
--------------------------------------

Step 5.4 Create customer user
------------------------------

Step 5.5 Activate customer user
--------------------------------


Next steps
===========


Step 2: Import Avantec Widget to ThingsBoard
Step 3: Import Avantec Dashboard to ThingsBoard
Step 4: Add asset
Step 5: Add devices to ThingsBoard
1. add device
2. Copy credentials of new device
3. Add shared attributes of new device
4. Add device to asset

Step 6: Connect device to ThingsBoard
1. Clear Wi-Fi configuration
2. Get Access-Token
3. Power On
4. Configure
5. Check

Troubleshooting
Step 7: Operate it
Setp 8: Customize

*TODO:...*