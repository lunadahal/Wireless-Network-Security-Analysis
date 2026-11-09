# Wireless Network Security Analysis

### IEEE 802.11 Traffic Capture and Analysis

## Overview

This project examines wireless network communication through passive IEEE 802.11 traffic capture and packet analysis in an authorized environment.

The objective was to identify wireless network characteristics, observe traffic associated with selected access points and an authorized client, and assess the visibility and limitations of wireless monitoring.

## Environment and Tools

| Component | Technology |
|---|---|
| Operating System | Kali Linux (VirtualBox) |
| Wireless Adapter | ALFA, MediaTek MT7612U |
| Wireless Monitoring | Airodump-ng |
| Packet Analysis | Wireshark |
| Network Security | WPA2, CCMP |

## Assessment Approach

The assessment involved wireless network discovery, targeted traffic capture, IEEE 802.11 frame inspection, and client-specific traffic analysis.

Airodump-ng was used to identify nearby wireless networks and capture traffic. Wireshark was used to examine management, control, and data frames, including filtering traffic associated with an authorized test device.

## Key Findings

- Identified wireless networks with different advertised security configurations, including WPA2-protected and open networks.
- Successfully captured and analyzed wireless traffic associated with selected access points.
- Identified 3,285 IEEE 802.11 data frames in the analyzed capture.
- Isolated traffic involving an authorized wireless client using Wireshark display filters.
- Established that wireless traffic visibility does not automatically provide access to encrypted application data.

## Technical Documentation and Evidence

The testing methodology, individual observations, Wireshark filters, and supporting screenshots are documented in:

**[Wireless Traffic Analysis Observations](observations.md)**

## Scope and Limitations

Testing was limited to passive wireless discovery and traffic analysis within an authorized environment.

No credential recovery, WPA2 cracking, unauthorized network access, or decryption of protected application traffic was performed.
