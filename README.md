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

I Logged into the Windows 10 virtual machine that we created earlier and downloaded Wireshark. Wireshark is an open-source network protocol analyzer.
</p>
<br />

![image](https://github.com/user-attachments/assets/49467086-4910-47da-93f9-e33aefa6242a)

The first thing we want to do with Wireshark is to start a packet capture and observe the normal traffic that a computer uses. The first type of traffic that we are going to capture is ICMP traffic. ICMP (ping) is used to test the connectivity of a host on a network.
</p>
<br />

![image](https://github.com/user-attachments/assets/a0bd7db8-df35-4119-b3fe-2346985c7eba)

I sent a ping request through Powershell onto the Linux virtual machine on its private IP address (10.1.0.5).

![image](https://github.com/user-attachments/assets/83fa71d5-d55f-4325-9598-387b8fbf757d)

I then observed the request from the Linux virtual machine (10.1.0.5) and the replies from the Windows virtual machine (10.1.0.4). Seeing the request and replies tells me that I have network connectivity. 

![image](https://github.com/user-attachments/assets/d2349f15-4ad0-4130-81b4-da44d9268ac2)

I then pinged www.google.com from the Windows 10 virtual machine and observed the results of the request and reply. This shows me that I have network connectivity which is what ICMP(ping) looks for. 

![image](https://github.com/user-attachments/assets/719195c0-154d-4c43-8919-8071878e1929)

I initiated a continuous ping from Powershell to the Ubuntu virtual machine and observed the traffic in Wireshark. A continuous ping will keep sending requests until I stop/exit the command.  

![image](https://github.com/user-attachments/assets/3d9583bd-aaf9-47ac-830b-cf665f11732d)

I then went into the Network Security Settings in my Linux virtual machine, to the Linux security group, and configured an inbound security rule to block all ICMP traffic. I then went back to my Windows virtual machine to observe the results of implementing the new rule. 

![image](https://github.com/user-attachments/assets/433aa65e-d0d2-4b69-91d7-c3b3766455e3)

I observed in Powershell that the traffic started to time out. This makes sense and showed the firewall configuration to block all ICMP traffic was working correctly. 

![image](https://github.com/user-attachments/assets/516e5b61-2557-4358-b4cb-ffad49a2fedc)

I also observed in Wireshark that the traffic stopped receiving acknowledgments and only received the ping request.  

![image](https://github.com/user-attachments/assets/ac5bf84d-a9df-46e5-a89e-a0fbf3efbce1)

I then deleted the security rule to block all incoming ICMP traffic and observed the traffic results begin again in both Wireshark and Powershell. The requests and replies started to show again, which shows that the firewall configuration was deleted successfully and allowed ICMP traffic again.  

![image](https://github.com/user-attachments/assets/7b0ffde3-8c84-4b27-9211-7108db3f20af)

I then "SSH into" the Linux virtual machine through Powershell and observed the traffic through Wireshark while typing random commands into Powershell. All of the traffic is showing as "encrypted". This shows that I correctly "SSH into" the system, because SSH encrypts all traffic, keystrokes, etc. 

![image](https://github.com/user-attachments/assets/a71c8221-de1c-40a6-8380-b0b8816c2f2f)

I then filtered for dns traffic only in Wireshark. I typed nslookup google.com in Powershell and observed the traffic in Wireshark. The traffic returned showed me the IP address for google.com

![image](https://github.com/user-attachments/assets/a5ddc277-3229-454a-8ebc-ebc3dbf0e62b)

The last thing that was done with Wireshark was I searched for RDP(tcp.port==3389) traffic only and observed the constant stream of traffic as the RDP was always transmitting between my Linux virtual machine and the Windows 10 Pro virtual machine.  
