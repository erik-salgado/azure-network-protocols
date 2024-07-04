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
![Screenshot 2024-07-04 084329](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/8640f002-7f3e-4ce9-991e-72acef15ae44)
![Screenshot 2024-07-04 084420](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/924dd1ab-660c-4380-b7fa-2e62b57392f9)


- Go back to the Azure Portal for VM2 and allow IMCP traffic to go through. Observations: You will start receiving replys back as a result of the new rule change.

![Screenshot 2024-07-04 084513](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/42e523a2-5c0d-4403-8c6f-3da423d77e86)
![Screenshot 2024-07-04 084610](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/7b1dc3a8-bb65-42b2-baa9-fa47d2be83b5)
![Screenshot 2024-07-04 084652](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/eacc8cc5-533a-4cd0-927f-6aecb9f0a364)

- Filter traffic by SSH. Observations/Notes: SSH (is a secure way to remotely access and manage computers over an internet connection. It encrypts data sent between computers, ensuring that sensitive information remains private and secure. It's commonly used by administrators and developers to securely log in to servers and execute commands or transfer files). Instead of pinging, we're gonna connect from VM1 into VM2 via secure shell (SSH)

![Screenshot 2024-07-04 084951](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/0ce22c84-3d75-4bf0-8d84-2afd1a89e5e5)

- Open Powershell and type "ssh [username]@[IP Address of VM2]" Observations/Notes: say yes to continue. Type the password. Connection will be established between VM1 and VM2. VM2 is currently on linux so we're gonna use a few linux commands. Another way to filter traffic is by using port number 22 by typing "tcp.port == 22"

![Screenshot 2024-07-04 085123](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/3aa2aa8c-56c9-4de3-ac1a-87863e08e645)
![Screenshot 2024-07-04 085145](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/61823a41-7a56-4d04-b2fe-b56af8339d86)
![Screenshot 2024-07-04 085235](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/a5e69151-ca19-4f75-a56d-5ca39a734560)
![Screenshot 2024-07-04 085258](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/278b70c7-c7e9-475d-b157-04a344877b83)

![Screenshot 2024-07-04 090305](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/f5783c34-4f94-417c-8929-429f53f72fcc)

![Screenshot 2024-07-04 090005](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/4786f414-538d-4324-99c1-8ba50e56b525)
![Screenshot 2024-07-04 090114](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/c5596485-7337-41f3-8c2f-07218a14bef1)

- Renew IP Address by typing "ipconfig /renew". Observations/Notes: VM1 will broadcast on the Virtual Network and will ask for a new IP Address. Azure has a DCHP (Dynamic Host Configuration Protocol) server inside of the Virtual Network, what this server does is that it assigns/reissues IP addresses.

![Screenshot 2024-07-04 090443](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/00217ba2-aba8-4fbf-9d8b-b97164a380b1)

- Filter traffic by DCHP.

![Screenshot 2024-07-04 090504](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/13faa395-43bc-4c13-9d2c-54a02a27e283)

- Filter traffic by DNS. Observations/Notes: Use the nslookup command to ask the DNS (Domain Name System) server what the IP address is for any given host name for example www.google.com. Traffic will come through. Another way to filter traffic by DNS is by using the port number 53 or "udp.port == 53"

![Screenshot 2024-07-04 090716](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/48a450c4-5ab6-460f-b4d4-82dabb409d07)
![Screenshot 2024-07-04 090845](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/3cd6298e-3b37-4242-b02a-2429a623f494)
![Screenshot 2024-07-04 090912](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/560dbc6b-98e0-46e2-a127-a0292bb54ff6)
![Screenshot 2024-07-04 091006](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/d52cdd92-7f40-45d4-8f73-68c8d33dc635)


- Filter traffic by RDP. Observation/Notes: RDP (Remote Desktop Protocol) another way to filter traffic by RDP is using the port number or "tcp.port == 3389). This will spam non-stop because there is a live RDP traffic from our actual host computer.

![Screenshot 2024-07-04 091058](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/7d7cde17-0b29-4246-be7c-5647a569adb9)
![Screenshot 2024-07-04 091435](https://github.com/erik-salgado/azure-network-protocols/assets/173113320/050d7999-27dd-4829-95f7-d4c231fe105f)

This brings the conclusion to this tutorial. Thanks for watching! :)


