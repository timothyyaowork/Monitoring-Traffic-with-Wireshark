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
Once you have installed Wireshark, open the application. You will notice a list of options for what stream Wireshark will operate on. Choose the stream that has activity showing, represented by the frequency lines. Usually, this will be "Ethernet". In my case, I had Ethernet and Ethernet 2. Both seemed to have the same activity, and I chose Ethernet 2. After selecting the stream, click the blue sharkfin icon to start capturing packets. When you do, you will notice a rapidly updating feed appear on the top half of the window, along with 2 tables on the bottom half. The feed is the stream of packets being captured by the application, whilst the two tables contain information about the currently selected packet.
</p>
<p>
<img src="https://imgur.com/LSEmZrP.png" height="50%" width="50%" alt="starting wireshark"/>
</p>
<p>
<img src="https://imgur.com/jzEvACz.png" height="50%" width="50%" alt="raw stream"/>
</p>

<br />

<h3>Observe ICMP Traffic</h3>
<p>
To observe any specific type of traffic, we first have to filter out any miscellaneous traffic from the feed. We can do this by typing in the kind of traffic we are looking for in the display filter above the feed. In this case, we are trying to observe ICMP traffic, so we will input 'icmp' into the filter.
</p>
<p>
<img src="https://imgur.com/7Tnv4E0.png" height="50%" width="50%" alt="icmp filter"/>
</p>
<p>
After applying the filter, we will then open PowerShell and use the ping command to contact a network entity with a reachable IP address, this can be something such as a web domain or another computer. In this case, we will be contacting VM2, this can be done by pinging VM2's private IP, which in this case is (172.16.1.4). In this case, the full command was "ping 172.16.1.4".</p>
<p>
<img src="https://imgur.com/uaLNFo8.png" height="50%" width="50%" alt="ping VM2"/>
</p>
<p>
After pinging VM2, we will find new entries in the feed that are labelled "request" and "reply". In this case, the "request" packets are sent from VM1 to VM2, whilst the "reply" packets are sent from VM2 to VM1 in response to receiving a request packet. In the data tables, we can see various pieces of information such as the frame the packet was contained in, the Ethernet information of the machines involved(such as their MAC addresses), the IP information of the machines involved, and the data contained in the packet. In the case of ICMP, the data contained in the ICMP packet is "abcdefghijklmnopqrstuvwabcdefghi."</p>
<p>
<img src="https://imgur.com/wM8GsyS.png" height="50%" width="50%" alt="icmp packet"/>
</p>

<h3>Observe SSH Traffic</h3>
<p>
  To observe SSH traffic, we will first have to apply a new filter to hide the miscellaneous traffic from the feed. For SSH traffic, we can either input "ssh" or "tcp.port==22" since SSH uses tcp port 22.
  </p>
<p>
<img src="https://imgur.com/29Gh8rl.png" height="50%" width="50%" alt="SSH"/>
</p>
<p>  
After applying the filter, we will then use PowerShell to connect to VM2 using SSH. This can be done by using the command ssh followed by the username@machineIP. In this case, the full command was "ssh labuser@172.16.1.4". After inputting the command, you will have to input the contacted machine's password to complete the connection. 
</p>
<p>
<img src="https://imgur.com/TDlRa68.png" height="50%" width="50%" alt="SSH"/>
</p>
<p>
Once you have successfully connected to the VM2, you will notice a new series of entries in the Wireshark feed. Like before with the ICMP packets, the tables will show information related to the packet frame, Ethernet, IP, and the packet data, with the addition of a "Transmission Control Protocol" field since SSH uses TCP. Note how, unlike the data of the ICMP packet, the data of the SSH packet is unintelligible. This is because SSH sends packets with encryption.
</p>
<p>
<img src="https://imgur.com/LKheJQH.png" height="50%" width="50%" alt="SSH"/>
</p>
<p>
  Also note how every new command you input in PowerShell whilst the SSH connection is active will create new entries in the feed, this will allow you to keep track of any SSH activity.
</p>

<h3>Observe DHCP Traffic</h3>
<p>
  Like before, to observe DHCP traffic, we must apply a DHCP filter to the Wireshark feed, we can do this by inputting "dhcp". Alternatively, "udp.port==67" or "udp.port==68" can also be used since DHCP runs on UDP ports 67 and 68. 
</p>

<p>
<img src="https://imgur.com/MIrRfeH.png" height="50%" width="50%" alt="SSH"/>
</p>
<p>
  After applying the filter, we will use PowerShell to initiate DHCP traffic. This can be done with the command "ipconfig /renew", which will refresh the network configuration, requesting a new IP lease from the DHCP server. 
</p>
<p>
<img src="https://imgur.com/NY3M7XV.png" height="50%" width="50%" alt="icmp filter"/>
</p>
<p>
Like the ICMP packets, the tables will show information related to the packet frame, Ethernet, IP, and the packet data. But the DHCP packet has the additional "User Datagram Protocol" field since DHCP uses UDP. 
</p>

<h3>Observe DNS Traffic</h3>
<p>
  Like previously, to observe DNS traffic, we have to apply a new filter for DNS traffic to the Wireshark feed. We can do this by inputting "dns" or "udp.port==53" since DNS runs on UDP port 53. 
</p>
<p>
<img src="https://imgur.com/rqmFXxU.png" height="50%" width="50%" alt="icmp filter"/>
</p>
<p>
To create DNS traffic, we will use PowerShell and the nslookup command on disney.com. This will send a request to the DNS server to find the IP address of the web domain.
</p>
<p>
<img src="https://imgur.com/jUje7Y8.png" height="50%" width="50%" alt="icmp filter"/>
</p>
<p>
After a series of queries, the command returns the information that disney.com has the IP of 130.211.198.204.
Just like the DHCP packet, the tables show information related to the packet frame, Ethernet, IP, the packet data, and UDP, since DNS uses UDP.
</p>

<h3>Observe RDP Traffic</h3>
<p>
  Finally, to observe RDP traffic, we need to apply a filter for RDP traffic to the Wireshark feed. This can be done by inputting "tcp.port==3389" since RDP runs on TCP port 3389. 
</p>
<img src="https://imgur.com/T3usweJ.png" height="50%" width="50%" alt="icmp filter"/>
<p>
  After applying the RDP filter, we will notice a large stream of entries in the Wireshark feed. This is because we are using RDP to connect to VM1, which is sending a constant stream of data between VM1 and the computer connecting to it.
  The RDP packets' tables will have information on the packet frame, Ethernet, IP, the packet data, TCP(since RDP runs on a TCP port), and TLS.
</p>

<br />
