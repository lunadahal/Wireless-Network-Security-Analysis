# Wireless Network Security Analysis Observations
This lab documents wireless network discovery and IEEE 802.11 traffic analysis using an ALFA MT7612U WiFi adapter, Airodump-ng, and Wireshark in an authorized environment.

## Screenshot 1: Wireless Environment Discovery

### WIRESTAR.NET SECURE
BSSID: A8:0B:FB:7C:DA:80  
Encryption: WPA2  
Cipher: CCMP  
Authentication: PSK  
PWR: -55  

### WIRESTAR.NET GUEST
BSSID: A8:0B:FB:7C:DA:81  
Channel: 1  
Encryption: WPA2  
Cipher: CCMP  
Authentication: PSK  
PWR: -53  

### WIRESTAR.NET REGISTER
BSSID: A8:0B:FB:7C:DA:82  
Channel: 1  
Encryption: OPN  
Cipher: None  
Authentication: None  
PWR: -53  

### Observation

The wireless scan identified multiple WIRESTAR.NET networks and BSSIDs.

SECURE and GUEST used WPA2 with CCMP encryption and PSK authentication, while REGISTER was open and did not use WiFi link layer encryption.

The scan also shows that the wireless environment used multiple access point radios with different BSSIDs and signal levels.

## Screenshot 2: Targeted Wireless Capture

Target SSID: WIRESTAR.NET GUEST  
Target BSSID: A8:0B:FB:7C:DA:81  
Channel: 1  
Security: WPA2, CCMP, PSK  
Capture: `guest_capture-01.cap`

### Observation

Airodump-ng was configured to monitor one specific access point using its BSSID and channel.

This capture mainly contained wireless management and control traffic and was saved for analysis in Wireshark.

## Screenshot 3: IEEE 802.11 Frame Analysis

Tool: Wireshark  
Capture: `guest_capture-01.cap`

### Observation

Wireshark identified several IEEE 802.11 frame types, including:

* Beacon frames
* Probe responses
* Acknowledgement frames

Beacon frames advertise the wireless network. Probe responses are sent by an access point in response to wireless discovery requests. Acknowledgement frames confirm successful frame reception at the wireless MAC layer.

This demonstrates the workflow:

`ALFA adapter → Airodump-ng capture → Wireshark analysis`

## Screenshot 4: Beacon Frame Inspection

Frame Type: IEEE 802.11 Beacon  
Destination: Broadcast  
SSID: WIRESTAR.NET GUEST

### Observation

A beacon frame was inspected in Wireshark. It showed the access point advertising WIRESTAR.NET GUEST to nearby wireless devices.

Wireshark also provided access to the frame structure and raw packet bytes.

## Screenshot 5: Targeted Client Traffic Capture

SSID: WIRESTAR.NET SECURE  
BSSID: A8:0B:FB:BC:DA:80  
Channel: 36  
Security: WPA2, CCMP, PSK  
Airodump-ng #Data Counter: 2857

### Observation

The BSSID and channel used by the Windows test laptop were identified and used for a targeted capture.

The laptop appeared in the STATION list, confirming that traffic involving the authorized client was being observed. The increasing #Data counter showed active wireless data communication associated with the access point.

## Screenshot 6: Wireless Data Frame Analysis

Tool: Wireshark  
Filter: `wlan.fc.type == 2`

### Observation

The filter displayed 3,285 IEEE 802.11 data frames from the targeted capture.

The Windows test laptop was visible through its wireless MAC address, confirming that the capture contained active client data frames in addition to management and control traffic.

### Security Relevance

Monitor mode provides visibility into wireless client activity.

However, capturing wireless frames does not automatically reveal protected application content. WPA2 protects the wireless link, while protocols such as HTTPS can provide additional encryption at higher layers.

## Screenshot 7: Client Specific Wireless Traffic

Tool: Wireshark  
Filter: `wlan.addr == 0c:54:15:xx:xx:xx && wlan.fc.type == 2`

### Observation

The filter isolated IEEE 802.11 data frames involving the authorized Windows test laptop.

This demonstrated how a wireless capture can be narrowed to traffic associated with a specific client during an investigation.

## Key Takeaways

* Used monitor mode to observe IEEE 802.11 wireless traffic
* Identified SSIDs, BSSIDs, channels, security settings, and PWR values
* Performed targeted captures using BSSID and channel information
* Distinguished management, control, and data frames
* Analyzed wireless captures using Wireshark
* Identified an authorized wireless client
* Filtered traffic associated with a specific device

## Scope

This project focused on passive wireless discovery and traffic analysis in an authorized environment.
It did not attempt to crack WPA2, recover credentials, decrypt protected application traffic, or access private communications.
