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

- Open Powershell and Ping VM2 (Linux) from within VM1 (Windows 10 Pro) Observations: you will need to find VM2 Private IP address from the Azure Portal in order to continue. Connection will be established successfully after pinging.

![Screenshot 2024-07-03 205001](https://github.com/erik-salgado/Azure-Networking/assets/173113320/4d8fd403-3808-4416-830b-c78fde4f1206)

![Screenshot 2024-07-03 205054](https://github.com/erik-salgado/Azure-Networking/assets/173113320/66a87a67-b483-402c-9b73-c04bc8c36e20)

![Screenshot 2024-07-03 205128](https://github.com/erik-salgado/Azure-Networking/assets/173113320/139457f2-7950-4608-98ec-1e46a9edfb4a)

- Ping "www.google.com -4" Observations: This will force it to use IP4 Address

![Screenshot 2024-07-03 205304](https://github.com/erik-salgado/Azure-Networking/assets/173113320/2bf4893e-466d-4422-b075-7e4c5330f0c6)

![Screenshot 2024-07-03 205405](https://github.com/erik-salgado/Azure-Networking/assets/173113320/e73a0d80-4723-4b61-9c1d-fb0a283fa72d)

- Clear Data and initiate a perpetual ping. Observations: This will be a non-stop ping.

![Screenshot 2024-07-03 205456](https://github.com/erik-salgado/Azure-Networking/assets/173113320/b6c18cce-e78b-4d01-a631-7e9525722fee)

![Screenshot 2024-07-04 110338](https://github.com/erik-salgado/Azure-Networking/assets/173113320/b9ed386f-c093-45b1-90af-63d842daa31c)

- On the Azure Portal go to VM2 Security Groups and create a rule that will blocks ICMP traffic. Observations: On the inbound rule, change the protocol to ICMPv4. Change Action to deny. Set Priority to 200. Name the Rule. Click Add. You will notice in Powershell that the connection well timed out as a result of the new security rule.

![Screenshot 2024-07-04 083725](https://github.com/erik-salgado/Azure-Networking/assets/173113320/e7e876af-a87f-4d27-8d20-4cb96bbe61e6)
![Screenshot 2024-07-04 083900](https://github.com/erik-salgado/Azure-Networking/assets/173113320/53d2d1ff-de04-4942-885f-e700ba01f57d)
![Screenshot 2024-07-04 083916](https://github.com/erik-salgado/Azure-Networking/assets/173113320/6cdfb06e-b2db-42d6-8f6d-c1cbf480e8ec)
![Screenshot 2024-07-04 084148](https://github.com/erik-salgado/Azure-Networking/assets/173113320/f93c4302-c6c5-4b5e-8d18-0b6a19dfd8ce)
![Screenshot 2024-07-04 084213](https://github.com/erik-salgado/Azure-Networking/assets/173113320/9086595b-ceb2-49d7-97d9-754f76e38860)


