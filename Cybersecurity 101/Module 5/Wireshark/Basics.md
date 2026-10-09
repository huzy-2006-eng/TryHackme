### Wireshark 
is one of the most potent traffic analyser tools available in the wild. There are multiple purposes for its use:

1. Detecting and troubleshooting network problems, such as network load failure points and congestion.
2. Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
3. Investigating and learning protocol details, such as response codes and payload data.

# Wireshark GUI:
1. #### Toolbar - 
The main toolbar contains multiple menus and shortcuts for packet sniffing and processing, including filtering, sorting, summarizing, exporting and merging.

2. #### Dislay Filter Bar -
The main query and filtering section.

3. #### Recent Files - 
List of the recently ivestigated files. You can recall listed files with a double-click.

4. #### Capture Filter and Interfaces -
Capture filters and available sniffing points (network interfaces). The network interface is the connection point between a computer and a network. The software connection (e.g.,lo,eth0 and ens33) enables networking hardware.

5. #### Status Bar -
Tool status, profile and numeric packet information.

# Loading PCAP Files:
Packet List Pane - Summary each packet (Source and destination addresses, protocol,and packet info).
You can click on the list to choose a packet for further investigation. Once u select a packet, the details will appear in the other panels.

Packet Details Panel - Detailed protocol breakdown of the selected packet.

Packet Bytes Pane - Hex and decoded ASCII representation of the selected packet. It highlights the packet field depending on the clicked section in the details pane.

### Packet Dissection -
Packet dissection is also known as protocol dissection, which investigates packet details by decoding available protocols and fields.
Wireshark also supports a long list of protocols for dissection, and u can also  write your dissection scripts. 

