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

<p align="center">
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/574576c7-3885-4d52-9fcf-a3dbf97b3bd0" alt="Resource examples"/>
</p>
<p>Create a Resource Group in the Azure portal. Within that resource group create a Windows 10 VM and then a Linux (Ubuntu) VM. When creating the Linux VM make sure it is in the same Resource Group as the Windows VM (The "Network Watcher" Resource Group will be automatically created) and that they also share the same virtual network. We'll use the Wireshark packet analyzer in the following examples. 
</p>
<br />

<p>
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/3d90028f-7f85-441e-91c7-e21961654115)" height="50%" width="50%" alt="VM wireshark traffic"/>
</p>
<p>
Connect to your Windows VM using Remote Desktop and install Wireshark from within it. Open Wireshark and filter for ICMP traffic only to capture that ping activity we'll generate next.
</p>
<br />

<p>
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/138cad94-14ba-436b-87fd-f717aa07f94b" height="70%" width="70%" alt="Ping requests/replies"/>
</p>
<p>
Retrieve the private IP address of the Ubuntu VM and ping it from within the Windows VM. We can observe the ping requests and the replies in Wireshark.
</p>
<br />

<p>
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/e9012525-ef17-48e9-968c-e22e5fa0671b" height="60%" width="60%" alt="Google ping"/>
</p>
<p>
Ping a public website, like google.com from the Windows VM to demonstrate those ping replies and requests in Wireshark. Observe this successful network communication.
</p>
<br />

<p align="center">
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/b39ed4f3-80d5-4990-b65d-e5dc23def96d" height="80%" width="80%" alt="ICMP traffic blocked"/>
</p>
<p>
Now initiate a perpetual ping (ping 10.0.0.5 -t) from the Windows VM to the Ubuntu VM. Go to the Network Security Group for the Ubuntu VM and create an inbound security rule to deny ICMP traffic. We'll observe the ICMP behavior in Wireshark as well as the Command Line ping activity: the ICMP traffic is now being blocked by the Ubuntu VM's firewall (NSG).
</p>
<br />

<p>
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/3e9a5849-cb00-4d75-b94c-5fdeb430c31f" height="80%" width="80%" alt="ICMP traffic returns"/>
</p>
<p>
Now enable the ICMP traffic in the Ubuntu VM's Network Security Group and we can observe how the activity begins again in Wireshark. (Deleting the rule from the Inbound Security Rules list will get the same result). You can stop the ping activity when you're finished.
</p>
<br />

<p>
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/ecf6b900-8669-4066-a24e-7a679e2bd349" height="80%" width="80%" alt="SSH traffic"/>
</p>
<p>
Let's observe the activity of other network protocols. Filter for SSH traffic back in Wireshark. From the Windows VM remote into, or "SSH into", the Ubuntu VM using its private IP address. You'll need to use the User and Password in the Linux SSH connection with the IP (ssh labuser@10.0.0.5). Observe the SSH traffic back in Wireshark as SSH is being utilized. (You can type "exit" and then "Enter" to close the SSH connection).
</p>
<br />

<p>
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/1dae7534-99d7-4f94-94db-87668f1f0863" height="80%" width="80%" alt="DHCP traffic"/>
</p>
<p>
Filter for DHCP traffic in Wireshark. From your Windows 10 VM, issue your VM a new IP address from the command line using "ipconfig /renew". But first, use the "ipconfig" command to check your current adapter settings to compare after the IP is reissued. You'll be able to observe the DHCP traffic that appears in Wireshark. The DHCP server is being accessed for that renewal IP address request.
</p>
<br />

<p align="center">
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/60428f90-2cdb-4f77-acbc-2ad26a5c0f1f" height="80%" width="80%" alt="DNS traffic"/>
</p>
<p>
In Wireshark, filter for DNS traffic. Use "nslookup" in your Windows 10 command line to see what Google.com and Disney.com's IP addresses are. Also, observe the DNS traffic in Wireshark while the DNS server translates those domain names into IP addresses. (DNS uses port 53 so you can also see that udp.port == 53 was used to filter for DNS as well. You can do this for the others and their corresponding ports if they use a port.)
</p>
<br />

<p align="center">
<img src="https://github.com/simoneburch/net-protocols-traffic/assets/152559137/469e5705-911a-4efe-8b41-243a13d6a6c0" height="80%" width="80%" alt="RDP traffic"/>
</p>
<p>
In Wireshark, filter for RDP (tcp.port == 3389) traffic. Observe how there seems to be a non-stop stream of RDP traffic coming through and realize it's a result of our current, live remote connection! 
</p>
<br />
<p>Be sure to close your remote connection and delete your Resource Groups when you're finished!</p>
<p>Thanks for stopping by :)</p>
