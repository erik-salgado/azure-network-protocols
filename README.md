<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

# Steps:

- Download/Install Wireshark on Windows 10 (VM1)

![Screenshot 2024-07-03 203907](https://github.com/erik-salgado/Azure-Networking/assets/173113320/4b2a8ec0-e9a3-458e-89a0-b677c3ef195e)
![Screenshot 2024-07-03 204013](https://github.com/erik-salgado/Azure-Networking/assets/173113320/d06b4d7a-9ab9-409b-b874-b5d65cd38738)

![Screenshot 2024-07-03 204308](https://github.com/erik-salgado/Azure-Networking/assets/173113320/47c91c90-2f8b-4154-b492-20d336c712bf)

- Open Wireshark and select the Ethernet Adapter. Observations: This will lets us see the live traffic that's happening on the VM. You will notice spam traffic as well, that's because there is so much going in the background even when we are not doing anything.

![Screenshot 2024-07-03 204535](https://github.com/erik-salgado/Azure-Networking/assets/173113320/477e0675-2555-423f-b26e-ebd2c8c0cf0d)
![Screenshot 2024-07-03 204556](https://github.com/erik-salgado/Azure-Networking/assets/173113320/3238e9fc-e3b0-468e-be7f-d059ad60cb39)

- Filter traffic by "icmp". Observations/notes: This will stop spam traffic and will only filter out ICMP traffic. ICMP (Internet Control Messaging Protocol) This is the protocol that ping uses. Ping is used to test connectivity to different hosts on the internet, on the network and between VMs.

![Screenshot 2024-07-03 204708](https://github.com/erik-salgado/Azure-Networking/assets/173113320/393c929c-8670-4ae6-98af-384643684a23)
