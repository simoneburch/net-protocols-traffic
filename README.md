<p align="center">
<img src="https://github.com/simoneburch/net-protocols-wireshark/assets/152559137/72121abf-ee1d-4370-92ae-3a840a7f7dd3" height="60%" width="60%" alt="Wireshark Logo"/>
</p>

<h1>Observe and Filter Network Traffic between Azure Virtual Machines</h1>
Wireshark analyzes and filters network protocols. We'll use it with command-line tools and network security groups to inspect traffic during networking activities between two virtual machines.<br />

<!--<h2>Video Demonstration</h2>

- ### [YouTube: How to Use Wireshark to Filter for Various Networking Protocols](https://www.youtube.com) -->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Wireshark
- Various Command-Line Tools
- Network Protocols (SSH, DHCP, DNS, RDP)

<h2>Operating Systems Used </h2>

- Ubuntu Server
- Windows 10 (21H2)

<h2>High-Level Steps</h2>

This demo uses Virtual Machines deployed on Azure. You need to already have an Azure subscription to make these resources and follow along using Wireshark.

- Step 1: Create your Azure Resources and Install Wireshark
- Step 2: Ping your Ubuntu VM from your Windows VM (ICMP traffic)
- Step 3: Observe SSH, DHCP, DNS, and RDP Traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>Create a Resource Group in the Azure portal. Within that resource group create a Windows 10 VM and then a Linux (Ubuntu) VM. When creating the Linux VM make sure it is in the same Resource Group as the Windows VM and that they also share the same vnet. The "Network Watcher" Resource Group will be automatically created and can observe your virtual network from there.   
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Connect to your Windows VM using Remote Desktop and install Wireshark from within it. Open Wireshark and filter for ICMP traffic only to capture that ping activity we'll generate next.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Retrieve the IP address of the Ubuntu VM and ping it from within the Windows VM. We can observe the ping requests and the replies in Wireshark.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open the Command Line from the Windows VM and ping a public website to demonstrate the ping replies and requests in Wireshark. Observe this successful network communication.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now initiate a perpetual ping from the Windows VM to the Ubuntu VM. Go to the Network Security Group for the Ubuntu VM and disable the inbound ICMP traffic. We'll observe the ICMP behavior in Wireshark as well as the Command Line ping activity in the Windows VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now enable the ICMP traffic in the Ubuntu VM's Network Security Group and we can observe how the activity begins again in Wireshark and the Command Line as well. You can stop the ping activity when you're finished.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Let's observe the activity of other network protocols. Filter for SSH traffic only back in Wireshark. From the Windows VM remote into, or "SSH into" the Ubuntu VM using its private IP address. You'll need to use the User and Password in the Linux SSH connection. Observe the SSH traffic back in Wireshark as SSH is being utilized. (You can type "exit" and then "Enter" to exit the SSH connection).
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Filter for DHCP traffic in Wireshark. From your Windows 10 VM, issue your VM a new IP address from the command line using "ipconfig /renew". You'll be able to observe the DHCP traffic that appears in Wireshark. The DHCP server is being accessed for that renewal IP address request.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Wireshark, filter for DNS traffic. Use "nslookup" in your Windows 10 command line to see what google.com and disney.com's IP addresses are. Also, observe the DNS traffic in Wireshark as the access to the DNS server is seen while it translates those domain names into IP addresses. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Wireshark, filter for RDP (tcp.port == 3389) traffic. Observe how there seems to be non-stop spam for RDP and realize it's a result of our current remote connection!
</p>
<br />
<p>Wireshark is a useful tool for network troubleshooting and analysis as this quick guide has demonstrated.</p>
