# mdsm-dataset
# This is the dataset for the MDSM project

=========
Mobile device features collected during the (Mobiles device Dynamics Security Management (MDSM) project.


Description
-----------
The MDSM project took place at University of Granada (Spain) in order to monitorize mobile devices features (network traffic, permissions and apps, communication status, resources consuption, ...) to determine the security level [1,2].


The following tables provides database of the project.

a) Flows - WiFi network traffic of devices


-----------------+--------------+------+-----+----------------------+
| Field           | Type         | Description                       |
+-----------------+--------------+------+-----+----------------------+
| flowId          | int		 | Flow identification                     |
| macId           | int(11)      | Device identification             |
| packageName     | varchar      | Package name                      |
| time            | timestamp    | Flow timestamp (Reduced precision)|
| duration        | int          | Flow duration                     |
| protocol        | int          | Protocol (interval)               |
| saddr           | varchar      | Source IP (sustitution)           |
| sport           | int          | Source port (interval)            |
| daddr           | varchar      | Destination IP (sustitution)      |
| dport           | int          | Detaination port (inteval)        |
| sentBytes       | int          | Sent bytes                        |
| receivedBytes   | int          | Received bytes                    |
| sentPackets     | int          | Sent packets                      |
| receivedPackets | int          | REceives packets                  |
| tcpFlags        | int          | TCP flags (1)                     |
| ToS             | int          | ToS (2)                           |
| newFlow         | tinyint      | New Flow  (3)                     |
| finished        | tinyint      | Terminate (3)                     |   
+--------------------------------------------------------------------+                       


(1) TCP flags are 8 bits. I.e. 26 -> 0001 1010 -> ACK, PSH, SYN (https://en.wikipedia.org/wiki/Transmission_Control_Protocol#TCP_segment_structure) 

(2) ToS - Type of Service

(3) NewFlow and Finished identify the flow status. Flows are stored every 60 seconds, so is possible flow isn't finished.
                                            New Flow Finished

New flow                              		1       0
Transmiting 			                0       0
Closed                                          0       1
Less than 60 seconds                            1       1


b) Apps - Installed Apps and their persmissions

+-------------+----------------+------+-----+----------------------+-----------------------------+
| Field       | Type           | Description                                                     |
+-------------+----------------+------+-----+----------------------+-----------------------------+
| appId       | int            | App identification                                              |
| macId       | int            | Device identification                                           |
| name        | varchar        | Package name (masked)                                           |
| version     | varchar        | Packed version			                                 |
| permissions | varbinary      | Permission list (1 declared, 0 not declared)                    |
| autoStart   | tinyint        | App autostart active                                            |
| timestamp   | timestamp      | timestamp (Pression)                                            |
+-------------+----------------+------+-----+----------------------+----------------------------

c) Stat - 
+--------------+--------------+------+-----+----------------------+-----------------------------+
| Field        | Type         | Null |Description                                               |
+--------------+--------------+------+-----+----------------------+-----------------------------+
| statId       | int          | NO   | Status identification                                    |
| macId        | int          | NO   | Device indentification                                   |
| ramUsage     | int          | NO   | Ram usage                                                |
| batteryLevel | int          | NO   | Battery level                                            |
| cpuUsage     | int          | NO   | CPU usage                                                |
| timestamp    | timestamp    | NO   | Timestamp (Precission)                                   |
+--------------+--------------+------+-----+----------------------+-----------------------------+

d) Bluetooth - 
+-----------------+--------------+------+-----+----------------------+-----------------------------+
| Field           | Type         | Description                                                     |
+-----------------+--------------+------+-----+----------------------+-----------------------------+
| bluetoothId     | int          | Bluetooth identification                                        |
| macId           | int          | Device indentification                                          |
| bluetoothDevice | varchar      | Bluetooth device                                                |
| timestamp       | timestamp    | Timestamp                                                       |
+-----------------+--------------+------+-----+----------------------+-----------------------------+

e) Security

+------------------+--------------+------+-----+----------------------+-----------------------------+
| Field            | Type         | Description                    |
+------------------+--------------+------+-----+----------------------+-----------------------------+
| securityId       | int          | Protection features identification                              |
| macId            | int          | Device identification                                           |
| unknownSources   | tinyint      | Can install software from unkown sources                        |
| developerOptions | tinyint      | Developper option is activated                                  |
| secure           | tinyint      | Device with a locking mechanism                             |
| rooted           | tinyint      | Device rooted                                                   |
| timestamp        | timestamp    | timestamp                                                       |
+------------------+--------------+------+-----+----------------------+-----------------------------+

f) WiFI

+-----------+--------------+------+-----+----------------------+-----------------------------+
| Field     | Type         | Description (anonymization type)                                |
+-----------+--------------+------+-----+----------------------+-----------------------------+
| wifiId    | int          | WiFi identification                                             |
| macId     | int          | Device indentification                                          |
| ssid      | varchar      | SSID (masked)                                                   |
| security  | varchar      | Security type                                                   |
| timestamp | timestamp    | Timestamp                                                       |
+-----------+--------------+------+-----+----------------------+-----------------------------+

g) Devices - Device mobile characteristics of the project volunteers  

+--------------+--------------+------+-----+-------------------------+-----------------------------+
| Field        | Type     | Description (anomynization type)            |
+--------------+--------------+------+-----+-------------------------+-----------------------------+
| macId        | int      |             |
| mac          | varchar  |                             |
| manufacturer | varchar  |                              |
| brand        | varchar  |                              |
| model        | varchar  |                              |
| board        | varchar  |                                                 |
| hardware     | varchar  |                              |
| bootloader   | varchar  |                              |
| user         | varchar  |                              |
| host         | varchar  |                              |
| sdk          | tinyint  |                              |
| id           | varchar  |                            |
| fingerprint  | varchar  |                     |                             |
| time         | timestamp| NO   |     | CURRENT_TIMESTAMP(3)    | on update CURRENT_TIMESTAMP |
| cpuCores     | tinyint  |                             |
| ramTotal     | int      |                              |
| batteryTotal | int      |                            |
| timestamp    | timestamp| NO   |     | 0000-00-00 00:00:00.000 |                             |
+--------------+--------------+------+-----+-------------------------+-----------------------------+

h) Connectivity - Connectivity types activated in the devices

+----------------+--------------+------+-----+----------------------+-----------------------------+
| Field          | Type         | Description                                                     |
+----------------+--------------+------+-----+----------------------+-----------------------------+
| connectivityId | int(11)      |             |
| macId          | int(11)      |                             |
| data           | tinyint(4)   |                              |
| wifi           | tinyint(4)   |                              |
| airplane       | tinyint(4)   |                              |
| bluetooth      | tinyint(4)   |                              |
| gps            | tinyint(4)   |                             |
| timestamp      | timestamp(3) |  |
+----------------+--------------+------+-----+----------------------+-----------------------------+

Contributors
------------
J. A. Gómez-Hernández, jagomez@ugr.es
P. García-Teodoro, pgteodor@ugr.es
J.A. Holgado-Terriza, jaholgado@ugr.es
G. Maciá-Fernández, gmacia@ugr.es
J. Camacho-Páez, josecamacho@ugr.es
M. Robles-Carrillo, mrobles@ugr.es


References
----------
[1] https://nesg.ugr.es/mdsm/
[2] J.A. Gómez-Hernández, et al., "AMon: A Monitoring Multidimensional Feature Android Application to Secure Mobile Environments", 6th International Workshop on Traffic Measurements for Cybersecurity (WTMC) 2021.
[3] F. Prasser, F. Kohlmayer, "Putting Statistical Disclosure Control Into Practice: The ARX Data Anonymization Tool", in Gkoulalas-Divanis, Aris, Loukides, Grigorios (Eds.): Medical Data Privacy Handbook, Springer, November 2015. ISBN: 978-3-319-23632-2.
