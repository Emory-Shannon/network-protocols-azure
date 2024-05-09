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

- Creating Resources
- Observing ICMP Traffic
- Observing SSH Traffic
- Observing DHCP Traffic
- Observing DNS Traffic
- Observing RDP Traffic

<h2>Creating Resources</h2>

<p>
<img src="ACN - Creating Resource Group.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - Creating VM 1.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN- Creating VM 2 (1).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - Creating VM 2 (2).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Step 1 of this lab is to create the needed resources. First create a Resource Group Called "RG-LAB-01". After creating the resource group, create your first virtual machine named "VM-1". When creating your second virtual machine, make sure the virtual network and subnet are the same as the first vitrual machine you created. Also wireshark is needed for the rest of this tutorial. To download it, search "Wireshark Download".
</p>
<br />

<h2> Observing ICMP Part 1 Traffic</h2>

<p>
<img src="ACN - ICMP Traffic (1).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - ICMP Traffic (2).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - ICMP Traffic (3).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - ICMP Traffic (4).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>



<p>
After downloading wireshark, open the application and click the ethernet option then click the blue fin in the top left. Once your observing traffic, filter the traffic by "icmp". To do that simply search for it on the bar above the traffic. Once filtered, go to your azure portal and find the private ip address for "VM-2". Head back to your "VM-1" and ping "VM-2" from your command line (ping "private IP Address"). Observe the traffic on Wireshark. You can also ping a web address like "www.google.com" to see the traffic.  
</p>
<br />

<h2> Observing ICMP Traffic Part 2</h2>

<p>
<img src="ACN - ICMP Traffic (5).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - ICMP Firewall (1).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - ICMP Firewall (2).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - ICMP Firewall (3).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - ICMP Firewall (4).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  This second part involves editing "VM-2" network security group and seeing the effects. The First step is to crete a perpetual ping to "VM-2". To do that, go to your command line and type, ping -t (private IP Address). A perpetual ping should start. Next, go to your "VM-2" network security group. You can do that by looking up "network security group" in the azure portal. Once your there, access the "inbound security rules" under the settings tab. Add a rule as shown above to deny ICMP traffic. You can now go back to your "VM-1" and observe the changes. The request should time out. Now go back to your "VM-2" network security group and edit the rule you made to allow ICMP traffic. Go back to "VM-1" and observe the changes. Reply's should be coming back. 
</p>

<h2>Observing SSH Traffic</h2>

<p>
<img src="ACN - SSH Traffic (1).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - SSH Traffic (2).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - SSH Traffic (3).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  First step to observing SSH traffic is to filter by SSH on wireshark. You can do that by typing ssh into the filter bar. Once your filtered, you are going to access your "VM-2" from "VM-1". You will need the username, password and private IP address from "VM-2". Once you have everything, you are going to type the command "ssh (username)@(Private IP Address). A prompt will show up, type yes, then type the password you used to create the virtual machine. You are now in the command line of your "VM-2". You can type commands such as "id" and "uname -a" to observe the SSH traffic in wireshark. 
</p>


<h2> Observing DHCP Traffic</h2>

<p>
<img src="ACN - DHCP Traffic (1).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="ACN - DHCP Traffic (2).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  The first step to observing DHCP traffic is filtering by "dhcp" traffic in wireshark. After your filtered, open up powershell and type the command "ipconfig /renew". This command gives your machine a new IP address. You can observe the traffic in wireshark. 
</p>


<h2> Observing DNS Traffic</h2>

<p>
<img src="ACN - DNS Traffic (1).PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  Since you already have powershell and wireshark open you can filter by DNS traffic. Once you've set the filter type the command "nslookup www.google.com". You should see some traffic come in on wireshark.
</p>

<h2> Oberving RDP Traffic</h2>

<p>
<img src="ACN - RDP Traffic.PNG" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  For RDP traffic, you just have to filter by RDP and you will see a spam of traffic, that is because you are using RDP to use your virtual machine. 
</p>


