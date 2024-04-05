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

<h2>High-Level Steps</h2>

- Create VMs and Install Wireshark
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic (Pop quiz!)

<h2>Actions and Observations</h2>

![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/52bffc93-266a-4f01-a876-8b896f19165c)
![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/89a5586e-df74-4319-acb9-93594fb37cd7)
![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/b029c69e-9903-4400-b07e-aeef616add1b)


Part 1 (Create our Resources)
- Create a Resource Group
- Create a Windows 10 Virtual Machine (VM)
- While creating the VM, select the previously created Resource Group
- While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
- Create a Linux (Ubuntu) VM
- While create the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher


![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/63c84621-6a55-471b-9879-840f763447f2)


Part 2 (Observe ICMP Traffic)
- Use Remote Desktop to connect to your Windows 10 Virtual Machine
- Within your Windows 10 Virtual Machine, Install Wireshark
- Open Wireshark and filter for ICMP traffic only
- Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
- Observe ping requests and replies within WireShark
- From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/e2e9b5c7-96dc-4bd8-89d2-7b1a43bef192)

- Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
- Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/d68e3125-e138-4ca7-aab8-6cf8109e5f56)

- Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity

![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/c080643e-9f25-43ae-8b29-ff76b54dfb54)

- Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
- Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
- Stop the ping activity

Part 3 (Observe SSH Traffic)
- Back in Wireshark, filter for SSH traffic only
- From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
- Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
- Exit the SSH connection by typing ‘exit’ and pressing [Enter]

![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/f3332e0f-6bf9-4c53-bf7e-0d387e1232b3)


Part 4 (Observe DHCP Traffic)
- Back in Wireshark, filter for DHCP traffic only
- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark
![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/6168b085-fee8-4c6e-8cc4-b88bec787d24)

Part 5 (Observe DNS Traffic)
- Back in Wireshark, filter for DNS traffic only
- From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
- Observe the DNS traffic being show in WireShark

![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/c2250f00-c212-4aa4-b303-118504a9b3d5)

Part 6 (Observe RDP Traffic)
- Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
- <b>Pop Quiz!</b> Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
![image](https://github.com/kphillip1/azure-network-protocols/assets/165929885/eacd07fd-54a1-464f-b10c-89c9914064aa)

- Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

<h2 align="center"> Nice work! We now know how to observe various forms of network traffic with Wireshark as well as some basics with Network Security Groups </h2>


