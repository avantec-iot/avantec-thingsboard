Installing ThingsBoard CE on CentOS / RHEL
==========================================

This article from `ThingsBoard`__, has a new section called `Configure MQTT port`_. It has been made some cuts.

.. __: https://github.com/thingsboard/thingsboard.github.io

.. tip::

   In this article, We use **ThingsBoard CE V3.0.1**, a **PostgreSQL** database, and the **In Memory Message Queue Service**. To use other versions of ThingsBoard, other databases, or other message queue services, refer to `here`__.

.. __: https://thingsboard.io/docs/user-guide/install/rhel/

Prerequisites
-------------

This guide describes how to install ThingsBoard on RHEL/CentOS 7/8. Hardware requirements depend on chosen database and amount of devices connected to the system. To run ThingsBoard and PostgreSQL on a single machine you will need at least 1Gb of RAM. To run ThingsBoard and Cassandra on a single machine you will need at least 8Gb of RAM.

Before continue to installation execute the following commands in order to install necessary tools:

**For CentOS 7:** ::

   # Install wget
   sudo yum install -y nano wget
   # Add latest EPEL release for CentOS 7
   sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

**For CentOS 8:** ::

   # Install wget
   sudo yum install -y nano wget
   # Add latest EPEL release for CentOS 8
   sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm


Step 1. Install Java 8 (OpenJDK)
--------------------------------

ThingsBoard service is running on Java 8. Follow this instructions to install OpenJDK 8::

   sudo yum install java-1.8.0-openjdk

Please don't forget to configure your operating system to use OpenJDK 8 by default. You can configure which version is the default using the following command::

   sudo update-alternatives --config java

You can check the installation using the following command::

   java -version

Expected command output is::

   openjdk version "1.8.0_xxx"
   OpenJDK Runtime Environment (...)
   OpenJDK 64-Bit Server VM (build ...)


Step 2. ThingsBoard service installation
----------------------------------------

Download installation package::

   wget https://github.com/thingsboard/thingsboard/releases/download/v3.0.1/thingsboard-3.0.1.rpm

Install ThingsBoard as a service::

   sudo rpm -Uvh thingsboard-3.0.1.rpm


Step 3. Configure ThingsBoard database
--------------------------------------

ThingsBoard is able to use SQL or hybrid database approach. See corresponding architecture `page`__ for more details.

.. __: https://thingsboard.io/docs/reference/#sql-vs-nosql-vs-hybrid-database-approach

::

   PostgreSQL
   (recommended for < 5K msg/sec)

.. tip::

   ThingsBoard team recommends to use PostgreSQL for development and production environments with reasonable load (< 5000 msg/sec). Many cloud vendors support managed PostgreSQL servers which is a cost-effective solution for most of ThingsBoard instances.


PostgreSQL Installation
>>>>>>>>>>>>>>>>>>>>>>>

Instructions listed below will help you to install PostgreSQL::

   # Update your system
   sudo yum update

**For CentOS 7:** ::

   # Install the repository RPM (for CentOS 7):
   sudo yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
   # Install packages
   sudo yum -y install epel-release yum-utils
   sudo yum-config-manager --enable pgdg12
   sudo yum install postgresql12-server postgresql12
   # Initialize your PostgreSQL DB
   sudo /usr/pgsql-12/bin/postgresql-12-setup initdb
   sudo systemctl start postgresql-12
   # Optional: Configure PostgreSQL to start on boot
   sudo systemctl enable --now postgresql-12

**For CentOS 8:** ::

   # Install the repository RPM (for CentOS 8):
   sudo yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
   # Install packages
   sudo dnf -qy module disable postgresql
   sudo dnf -y install postgresql12 postgresql12-server
   # Initialize your PostgreSQL DB
   sudo /usr/pgsql-12/bin/postgresql-12-setup initdb
   sudo systemctl start postgresql-12
   # Optional: Configure PostgreSQL to start on boot
   sudo systemctl enable --now postgresql-12

Once PostgreSQL is installed you may want to create a new user or set the password for the the main user. 
The instructions below will help to set the password for main postgresql user::

   sudo su - postgres
   psql
   \password
   \q

Then, press “Ctrl+D” to return to main user console.

After configuring the password, edit the pg_hba.conf to use MD5 authentication with the postgres user.

Edit pg_hba.conf file::

   sudo nano /var/lib/pgsql/12/data/pg_hba.conf

Locate the following lines::

   # IPv4 local connections:
   host    all             all             127.0.0.1/32            ident

Replace **ident** with **md5**::

   host    all             all             127.0.0.1/32            md5

Finally, you should restart the PostgreSQL service to initialize the new configuration::

   sudo systemctl restart postgresql-12.service

Connect to the database to create thingsboard DB::

   psql -U postgres -d postgres -h 127.0.0.1 -W


Execute create database statement::

   CREATE DATABASE thingsboard;
   \q


ThingsBoard Configuration
>>>>>>>>>>>>>>>>>>>>>>>>>

Edit ThingsBoard configuration file::

   sudo nano /etc/thingsboard/conf/thingsboard.conf

Add the following lines to the configuration file. Don't forget **to replace** 
“PUT_YOUR_POSTGRESQL_PASSWORD_HERE” with **your real postgres user password**::

   # DB Configuration
   export DATABASE_ENTITIES_TYPE=sql
   export DATABASE_TS_TYPE=sql
   export SPRING_JPA_DATABASE_PLATFORM=org.hibernate.dialect.PostgreSQLDialect
   export SPRING_DRIVER_CLASS_NAME=org.postgresql.Driver
   export SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/thingsboard
   export SPRING_DATASOURCE_USERNAME=postgres
   export SPRING_DATASOURCE_PASSWORD=PUT_YOUR_POSTGRESQL_PASSWORD_HERE
   export SPRING_DATASOURCE_MAXIMUM_POOL_SIZE=5
   # Specify partitioning size for timestamp key-value storage. Allowed values: DAYS, MONTHS, YEARS, INDEFINITE.
   export SQL_POSTGRES_TS_KV_PARTITIONING=MONTHS


Step 4. Choose ThingsBoard queue service
----------------------------------------

ThingsBoard is able to use various messaging systems/brokers for storing the messages and communication between ThingsBoard services. How to choose the right queue implementation?

- **In Memory** queue implementation is built-in and default. It is useful for development(PoC) environments and is not suitable for production deployments or any sort of cluster deployments.
- **Kafka** is recommended for production deployments. This queue is used on the most of ThingsBoard production environments now. It is useful for both on-prem and private cloud deployments. It is also useful if you like to stay independent from your cloud provider. However, some providers also have managed services for Kafka. See AWS `MSK`__ for example.
- **RabbitMQ** is recommended if you don't have much load and you already have experience with this messaging system.
- **AWS SQS** is a fully managed message queuing service from AWS. Useful if you plan to deploy ThingsBoard on AWS.
- **Google Pub/Sub** is a fully managed message queuing service from Google. Useful if you plan to deploy ThingsBoard on Google Cloud.
- **Azure Service Bus** is a fully managed message queuing service from Azure. Useful if you plan to deploy ThingsBoard on Azure.

.. __: https://aws.amazon.com/msk/

See corresponding architecture `page`__ and rule engine `page`__ for more details.

.. __: https://thingsboard.io/docs/reference/#message-queues-are-awesome

.. __: https://thingsboard.io/docs/user-guide/rule-engine-2-0/overview/#rule-engine-queue

::

   In Memory
   (built-in and default)


In Memory queue is built-in and enabled by default. No additional configuration steps required.

Step 5. [Optional] Memory update for slow machines (1GB of RAM)
---------------------------------------------------------------

Edit ThingsBoard configuration file::

  sudo nano /etc/thingsboard/conf/thingsboard.conf

Add the following lines to the configuration file::

  # Update ThingsBoard memory usage and restrict it to 256MB in /etc/thingsboard/conf/thingsboard.conf
  export JAVA_OPTS="$JAVA_OPTS -Xms256M -Xmx256M"


Step 6. Run installation script
-------------------------------

Once ThingsBoard service is installed and DB configuration is updated, you can execute the following script::

   # --loadDemo option will load demo data: users, devices, assets, rules, widgets.
   sudo /usr/share/thingsboard/bin/install/install.sh --loadDemo


Step 7. Start ThingsBoard service
---------------------------------

ThingsBoard UI is accessible on 8080 port by default. Make sure that your 8080 port is accessible via firewall. In order to open 8080 port execute the following command::

   sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent
   sudo firewall-cmd --reload

Execute the following command to start ThingsBoard::

   sudo service thingsboard start

Once started, you will be able to open Web UI using the following link::

   http://localhost:8080/

The following default credentials are available if you have specified - loadDemo during execution of the installation script:

- **Systen Administrator**: sysadmin@thingsboard.org / sysadmin
- **Tenant Administrator**: tenant@thingsboard.org / tenant
- **Customer User**: customer@thingsboard.org / customer

You can always change passwords for each account in account profile page.

.. tip::

   Please allow up to 90 seconds for the Web UI to start. This is applicable only for slow machines with 1-2 CPUs or 1-2 GB RAM.


Post-installation steps
-----------------------

Configure MQTT port
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

ThingsBoard MQTT is accessible on 1883 port by default. Make sure that your 1883 port is accessible via firewall. In order to open 1883 port execute the following command::

   sudo firewall-cmd --zone=public --add-port=1883/tcp --permanent
   sudo firewall-cmd --reload

Configure HAProxy to enable HTTPS
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

You may want to configure HTTPS access using HAProxy. This is possible in case you are hosting ThingsBoard in the cloud and have a valid DNS name assigned to your instance. Please follow this `guide`__ to install HAProxy and generate valid SSL certificate using Let's Encrypt.

.. __: https://thingsboard.io/docs/user-guide/install/pe/add-haproxy-rhel


Troubleshooting
---------------

ThingsBoard logs are stored in the following directory::

   /var/log/thingsboard

You can issue the following command in order to check if there are any errors on the backend side::

   cat /var/log/thingsboard/thingsboard.log | grep ERROR
