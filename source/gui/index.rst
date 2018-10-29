OpenKilda GUI
!!!!!!!!!!!!!

Accessing the GUI
@@@@@@@@@@@@@@@@@

OpenKilda includes a Graphical User Interface (GUI) to manually enter flows into the controller or display current status of different network elements. Using the default configuration, you can access the GUI at: http://localhost:1010/openkilda

Login Credentials
@@@@@@@@@@@@@@@@@

.. note:: Current version does not support individual user accounts. However, you need to use default login credentials to access system.

**ADMIN Credentials**

* username = admin
* password = admin

**USER Credentials**

* username = user
* password = user

GUI Features
@@@@@@@@@@@@

You will see login screen after launching GUI. By using default credentials, you will be able to login into system. On successful login, you will be redirected to home screen. On left, Different menu tabs will be shown like Home, Topology etc. User will be able to see default username on top right. On click, it will provide an option to logout from system.

Click on Topology tab will open default Topology View which is a cluster-wide view of the network topology.
Elements shown in base release are:

ISL Link Details: Provides source and destination switch details

* Speed
* Latency
* Available Bandwidth
* Graph: The Graph View provides ISL link traffic flow between ports connecting the two switches, choose options:

  * Start_datetime
  * End_datetime
  * Metric
  * Downsample
  * AutoReload(sec)

* Flow Link Details: The Flow view provides packet details with a known source and destination switch.

  * Flow Detail
  * Flow Name
  * Port
  * Switch
  * Vlan
  * Status
  * Maximum Bandwidth
  * Graph - The Graph view provides traffic flow between ports of connecting switches, choose options:

    * Start_datetime
    * End_datetime
    * Metric
    * Downsample
    * AutoReload(sec)

* Switch Details: Switch provide information of switch and number of ports. Click on Switch in topology view will show following details:

  * DPID
  * Address
  * Description
  * Controller
  * Port Details: Provides information of port with the following elements:

    * Interface Type
    * Port Name
    * Port Number
    * Status

OpenKilda Subsystem Web Interface
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

OpenKilda includes many sub-components that have web interfaces.  Here is a cheat sheet to access those web services:

.. list-table::
   :widths: 10,50

   * - **Storm**
     - http://127.0.0.1:8888

   * - **Neo4j**
     - http://127.0.0.1:7474

   * - **OpenTSDB**
     - http://127.0.0.1:4242

   * - **HBASE**
     - http://127.0.0.1:8070

   * - **Kibana**
     - http://127.0.0.1:5601

   * - **Swagger**
     - http://127.0.0.1:8088/api/v1/swagger-ui.html#/

   * - **OpenKilda GUI**
     - http://127.0.0.1:8010/openkilda

Loading the Kibana Dashboards
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

Default dashboards for Kibana have been added to the GitHub repository. To load these dashboards, OpenKilda has to be running. Navigate to the /tools/elk-dashboards folder:

.. code-block:: bash

   cd tools/elk-dashboards

Run the load.sh script to add the dashboards to Kibana:

.. code-block:: bash

   sudo ./load.sh
