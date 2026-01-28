<p align="center">
<img src="https://i.imgur.com/q1LyYzN.png" alt="Wireshark logo"/>
</p>

<h1>Wireshark - Post-Install Configuration</h1>
This is a tutorial that outlines the use of the open-source network protocol analyzer Wireshark to monitor network traffic. For this tutorial, we will have 2 freshly prepared virtual machines on the same network, VM1 will be running on Windows 10, whilst VM2 will be running on Ubuntu.<br />

<h2>Technologies Used</h2>

- Microsoft Azure (2 Virtual Machines/Computers)
- Windows 10(VM1)
- Ubuntu(VM2)
- Remote Desktop Connection
- Wireshark
  
<h2>Objectives</h2>

- Connect to VM1 with Remote Desktop
- Install and Set Up Wireshark
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Project Steps</h2>

<h3>Connect to VM1 with Remote Desktop</h3>
<p>
<img src="https://imgur.com/ai3vW4J.png" height="50%" width="50%" alt="Remote Desktop Connection"/>
</p>
<p>
Firstly, we will need to connect to VM1 using Remote Desktop. If you are a Windows User, you will have the Remote Desktop Connection installed by default. Otherwise, you will have to download a remote desktop application. You can connect to VM1 by inputting the machine's public IP into the "computer" field. For my virtual machine, it was (20.81.160.69). You can then log in to the machine using the credentials you assigned to it.</p>
<p>
<img src="https://imgur.com/oapyYUZ.png" height="50%" width="50%" alt="VM1"/>
</p>
<br />

<h3>Install and Set Up Wireshark</h3>
<p>
<img src="https://imgur.com/zwyr25D.png" height="50%" width="50%" alt="Download Wireshark"/>
</p>
<p>
After logging in to VM1, visit the <a href="https://www.wireshark.org/download.html">Wireshark website</a> and download the latest stable version of the Wireshark installer for Windows. Once downloaded, activate the installer and go through the installation process. The default settings should be fine, but be sure that the "Install Npcap" option is checked, as it is required for capturing live network traffic.
</p>
<p>
<img src="https://imgur.com/Szm4UFH.png" height="50%" width="50%" alt="npcap checked"/>
</p>
<p>
Once you have installed Wireshark, open the application. You will notice a list of options for what stream Wireshark will operate on. Choose the stream that has activity showing, represented by the frequency lines. Usually, this will be Ethernet. In my case, I had Ethernet and Ethernet 2, both seemed to have the same activity, and I chose Ethernet 2.
</p>
<p>
<img src="https://imgur.com/LSEmZrP.png" height="50%" width="50%" alt="npcap checked"/>
</p>

<br />

<h3>Observe ICMP Traffic</h3>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
