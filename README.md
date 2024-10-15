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
- Ubuntu Server 24.04

<h2>High-Level Steps</h2>

- Create a Windows 10 pro vm and a Linux (Ubuntu) vm
- Download Wireshark
- Observe various network protocols through Wireshark


<h2>Actions and Observations</h2>

![image](https://github.com/user-attachments/assets/9fba6210-24e0-419e-ace6-091df964d579)

Logged into the Windows 10 virtual machine and downloaded Wireshark. 
</p>
<br />

![image](https://github.com/user-attachments/assets/49467086-4910-47da-93f9-e33aefa6242a)

The first task with Wireshark is to start a packet capture and observe the traffic. We will then observe ICMP traffic through Wireshark. 
</p>
<br />

![image](https://github.com/user-attachments/assets/a0bd7db8-df35-4119-b3fe-2346985c7eba)

I sent a ping request through Powershell on the Linux virtual machine on its private IP address.

![image](https://github.com/user-attachments/assets/83fa71d5-d55f-4325-9598-387b8fbf757d)

I then observed the request from the Linux virtual machine (10.1.0.5) and the replies from the Windows virtual machine (10.1.0.4). 

![image](https://github.com/user-attachments/assets/d2349f15-4ad0-4130-81b4-da44d9268ac2)

I then pinged www.google.com from the Windows 10 virtual machine and observed the results. 
