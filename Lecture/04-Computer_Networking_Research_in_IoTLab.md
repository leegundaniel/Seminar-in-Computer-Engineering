# Computing Networking research in IoTLab
## Contents
- Introduction
    - Internet of Things (IoT)
    - Vehicular Internet of Things (VIoT)
- Research in IoTLab at SKKU
    - IoT
    - Vehicular Networking
    - Cloud-Based Security Services

## Internet of Things (IoT)
- Smart Factory
- Smart Farm
- Intelligent Transportation Systems
- Smart Building
- Smart Energy

### IoT-based Smart Era
- Smart Home
- Smart Wearable
- Smart Factory
- Smart Road

### Announcement of IoT Era
- Gartner's Hype Cycle in 2014
    - http://www.gartner.com/newsroom/id/2819918
    1. Innovation Trigger
    2. Peak of Inflated Expectations
    3. Trough of Disillusionment
    4. Slope of Enlightenment
    5. Plateau of Productivity

### Exponential Growth of IoT Devices
- 9 Billion IoT Devices by 2018

## Vehicular Internet of Things (VIoT)
### Smart Road Services in Vehicular Cloud
- Vehicular Cloud Services
    1. Intelligent Driving Services
    2. Online Diagnosis for Vehicle Safety
    3. Interaction with Mobile Devices for Remote Control, Safety and Entertainment

### Vehicular Networks
- Traffic Control Center (TCC)
- Road-Side Unit (RSU)
- Relay Node
- Router

### Smart Vehicle for VIoT
- Internal & External Camera
- DSRC/4G-LTE/3G/5G WiFi Devices
- Accelerometer / Gyroscope
- Mobile Devices (Smartphone/Tablet)
- Vehicle Computer

### Categories of VIoT Services
1. Safety & Regulation
    - Road Condition Monitoring
    - Driving Hazard Detection
    - Pedestrian Monitoring
2. Data Service
    - Location-Based Service (12V)
    - Data Upload (V2I)
    - Web Browsing, Email, etc.
3. Driving Efficiency
    - Smart Road Navigation
    - Smart Road Traffic Control
    - Green Vehicle Speed Control

### Proposed Solution & Challenges for VIoT
> Analysis of sensing data from a 3D acceleromenter.
> Integrated data from a crowd of taxis.

- Low Cost
    - 3G/4G-LTE/DSRC/WiFi Communications
- High Accuracy
    - Aggregated data from number of taxis
- Continuous Coverage
    - In both time and space

#### Road Condition Monitoring
#### Participatory Crowd Monitoring
- A driver can trigger the external camera to report the violations such as hit and run, crossing solid lines.

### Vehicular Communications for VIoT
1. Infrastructure-to-Vehicle Communications (I2V)
    - Vehicle requests to road network
    - road network send request to cloud
    - cloud provides response
    - road network gives data in the next network unit
2. Vehicle-to-Vehicle Communications (V2V)
    - Vehicle detects activity (e.g., aquaplaning)
    - send information to nearby vehicle
    - other vehicles nearby will receive information and data

## Research Projects in IoTLab at SKKU
- [IoT](#research-on-iot)
    - [DNS Naming and Control for IoT Devices](#dns-naming-and-control-for-iot-devices)
    - [Secure DNS Naming for IoT Devices](#secure-dns-naming-for-iot-devices)
    - [Indoor Positioning System (IPS)](#indoor-positioning-systems-ips)
    - [Smartphone-Assisted Localization Algorithm](#smartphone-assisted-localization-algorithm-sala)
    - [Device-Free Human Localization](#device-free-human-counting-indoors)
- [VIoT](#research-on-viot)
    - [V2X Communications with IEEE 802.11-OCB](#v2x-communcations-with-ieee-80211-ocb)
    - [Context-Aware Navigator for Driving Safety](#context-aware-navigator-for-driving-safety)
    - Smartphone App for Pedestrian Protection
- [Cloud-Based Services](#research-on-cloud-based-security-services)
    - [Internet-Based Networking for Cloud-Based Security](#intent-based-networking-for-cloud-based-security)
    - [Cloud-Based IoT Device Management](#cloud-based-iot-device-management)

### Research on IoT
#### DNS Naming and Control for IoT Devices
- Keuntae Lee, Seokhwa Kim, Jaehoon (Paul) Jeong, Sejun Lee, Hyoungshick Kim, and Jung-Soo Park, "A Framework for DNS Naming Services for Internet-of-Things Devices", Elsevier Future Generation Computer Systems, Vol. 92, pp.617-627, March 2019

- Time sequence diagram of DNS Name Autoconfiguration (DNSNA)
    1. DNS Name Generation
    2. DNS Name Collection
    3. DNS Name Registration
    4. IoT Device List Retrieval

#### Secure DNS Naming for IoT Devices
- Keuntae Lee, Seokhwa Kim, Jaehoon (Paul) Jeong, Sejun Lee, Hyoungshick Kim, and Jung-Soo Park, "A Framework for DNS Naming Services for Internet-of-Things Devices", Elsevier Future Generation Computer Systems, Vol. 92, pp.617-627, March 2019
1. Smartphone interacts with Authentication server to get private key
2. Authentication key: Security Information Generation
3. Authentication Server gives public key back to smartphone; Authentication server gives verification key to Router (DHCPv6 Server)
4. Smartphone sends the signing key to IPv6 IoT Device
5. Router sends RA or DHCP Option (DNS Search List) to IPv6 IoT Device
6. IPv6 IoT Device: DNS Name & Signature Generation
7. IPv6 IoT Device sends Duplicate Address Detection (DAD) to Router
8. Router sends NI Query (DNS Name Collection) back to IPv6 IoT Device
9. IPv6 IoT Device sends NI Reply (DNS Name & IPv6 Address & Signature) to Router
10. Router does NI Verification
11. Router can access DNS Server and match DNS name

#### Indoor Positioning Systems (IPS)
- Yiwen Shen, Beom Hwang, Jaehoon (Paul) Jeong, "Particle Filtering-Based Indoor Positioning System for Beacon Tag Tracking", IEEE Access, December 2020.

- System for tracking BLE

1. Indoor Environment Beacons to Anchor Points
2. AP sends Wireless signal data (RSSI, CSI) to the server
3. Server Preprocess to develop smoothed RSSI data
4. Wireless signal data calibration; constructing mapping function
5. Particle Filter
6. Positioning
7. Visualization

- RSSI measurement and curve fitting
- Raw RSSI data smoothed by the Kalman Filter

#### Smartphone-Assisted Localization Algorithm (SALA)
- Jaehoon (Paul) Jeon, Solchan Yeon, Taemoon Kim, Hyunsoo Lee, Song Min Kim, and Sang-Chul Kim, "SALA: Smartphone-Assisted Localization Algorithm for Positioning Indoor IoT Devices", Springer Wireless Networks, Vol. 24, No. 1, January 2018.
- Localize IoT Device using smartphone as anchors

- Procedure of SALA
    1. Detection of IoT Device: smartphone sends to Repository
    2. Position of Smartphone send to SALA server
    3. IoT Device Detection Trace Data goes through RSSI-Centroid
    4. Wall-Corner Handling
    5. Power-Distance Table
    6. Grid-Weight Map
    7. Position Notification sent from SALA server back to Smartphone

#### Device-Free Human Counting Indoors
- Jaehoon (Paul) Jeong, Yiwen (Chris) Shen, Seokhwa Kim, Daegeun Choe, Keuntae Lee, and Yongserk Kim, "DFC: Device-Free Human Counting through Wi-Fi Fine-Grained Subcarrier Information", IET Communications, Vol.15, Issue 3, pp.337-350, January 2021.

- Smart Building to find how many people are in the rooms based on IoT Devices
    - Meeting Area
    - Rest Area
    - Working Area
    
- Training and Testing Procedure for Device-Free Human Counting
    - Two Features
        - CSI Average Attenuation
        - CSI Average Variation

1. Collect Training Data
2. Data Processing
3. Feature Extraction
4. Probability Distribution
5. Collect Input Data
6. Data Processing
7. Input Data into Probability Distribution
8. Probabilitic Estimation of the Number of People

### Research on VIoT
#### Use Cases of Vehicular Networking in Intelligent Transportation Systems (ITS)
- Vehicle Traffic Release
- City Road Emergency
- Road Intersection Passing
- Navigation
- Connected Automated Vehicles
- Vehicle Data Forwarding Services

#### Vehicular Networking for Vehicles
- Vehicular Cloud connected to Traffic Control Center (TCC)
- Road-Side Unit (RSU) deployed on the roadway connected to Vehicular Cloud
- V2I: Vehicle-to-Infrastructure Communication
- V2V: Vehichle-to-Vehicle Communication

#### V2X Communcations with IEEE 802.11-OCB
- Yiwen (Chris) Shen, Bien Aime Mugabarigira and Jaehoon (Paul) Jeong, "IPv6 Vehicular Communications over IEEE 802.11-OCB Wireless Link", KICS-2020-Winter, February 2020.
1. WAVE Protocol Stack
2. Video Data Delivery with IPv6 over IEEE 802.11-OCB

#### Web-Based Car Control and Monitoring
- Junhee Kwon, Bien Aime Mugabarigira, and Jaehoon (Paul) Jeong, "Web-Based Car Control and Monitoring for Safe Driving Autonomous Vehicles", International Conference on Information Networking (ICOIN), Jeju, Korea, January 12-15, 2022.
- Robotic Cars communicating using WiFi

- Implemented V2V and V2I by utilizing an R1 AION robot car to check the delay of each communication method
- A robot car issues its own data (e.g., position and speed) and stores issued data as a file in VSS format

- VSS: GENIVI Vehicle Signal Specification
- VISS: W3C Vehicle Information Service Specification

#### Context-Aware Navigator for Driving Safety
- Bien Aime Mugabarigira, Yiwen (Chris) Shen, Daegeun Choe and Jaehoon (Paul) Jeong, "Context-Aware Navigator for Road Safety in Vehicular Cyber-Physical Systems" The Third International Conference On Consumer Electronics (ICCE) Asia, Jeju, Korea, June 24-26, 2018.
- Context Awareness in IP based Network Via lightweight messages
    - when accident occurs, beacon detects situation and sends signal to nearby vehicles
    - Cooperative context messages (CCM)
    - Emergency Context Message (ECM)

##### Internet Standardization in IETF
- SKKU IoTLab is leading the Standardization for Vehicular Networking at IETF IPWAVE Working Group
- SKKU students are participating in IETF Hackathon for IPWAVE standardization

- https://www.youtube.com/watch?v=E2BpQ0V oJA
    - DOESNT WORK

### Research on Cloud-Based Security Services
#### Intent-Based Networking for Cloud-Based Security
- Jinyoung (Tim) Kim et al., "IBCS: Intent-Based Cloud Services for Security Applications", IEEE Communications Magazine, Vol. 58, No. 4, April 2020.

- Administrator delivers policy to cloud (Security Service Provider Server)
    - I2NSF Framework in Logical View

- I2NSF: Interface to Network Security Functions
    - can detect a DoS attack for NSF A and automatically set up a new security policy for this attack
    - can log monitoring data from NSFs with a Distributed Network (e.g., Blockchain)
    - can visualize monitoring data in the web for security attack detection

##### Internet Standardization in IETF
- SKKU IoTLab is leading the Standardization for Cloud-Based Security Systems at IETF I2NSF Working Group.
- SKKU students are participating in IETF Hackahon for I2NSF standardization.

- github: https://github.com/jaehoonpaul/i2nsf-framework
- youtube: https://youtu.be/g7T928Gea58

#### Cloud-Based IoT Device Management
- IoT Devices (e.g., digital healthcare devices) are registered and managed with Cloud-Based IoT System

1. Healthcare Devices monitored using 5G communications to the edge cloud
2. SDN Network forwards data to healthcare servers

## Vision: IoT-based Digital World
- develop Cloud Infrastructure to provide
    1. Safety & Security
    2. Efficiency
    3. Data Services

## Conclusion
- IoT
- VIoT
- Research Projects in IoT Lab
    - IoT
    - Vehicular Networking
    - Cloud-Based Security
- IoT will be one of key technologies in Internet-based Digital World
    - IoT is a bridge of Physical and Cyber Worlds
    - IoT technology is key power of IT competition