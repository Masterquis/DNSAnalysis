<h1>DNS and Network Performance Analysis and Fix</h1>

<!-- ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo) -->

<h2>Project Overview</h2>
This case study demonstrates the troubleshooting process for resolving slow network performance caused by incorrect 
DNS configuration on Windows Server 2019 and Windows 10 machines. Both the Windows Server 2019 and Windows 10 machines are experiencing 
DNS resolution delays and network performance issues.
<br />


<h2>Tools and Utilities Used</h2>

- <b>Virtual Box</b>
- <b>Windows Server</b>
- <b>Windows 10</b>
- <b>DNS Manager</b>
- <b>Command Prompt (ipconfig, nslookup, ping)</b>

<h2>Setup & Configuration</h2>

- <b>Windows Server 2019</b></br>
  IP Address <b>10.0.2.15 /24</b> <i>(EXTERNAL NIC)</i></br>
  IP Address <b>172.16.0.1 /24</b> <i>(INTERNAL NIC)</i></br>
  DNS Server Address <b>8.8.8.8 /24</b>
  
- <b>Windows 10</b></br>
  IP Address <b>172.16.0.100 /24</b></br>
  DNS Server Address <b>8.8.8.8 /24</b>

<h2>Troubleshooting Steps</h2>

- <b>ACTION:</b> Used nslookup and ping to verify the Windows 10 Machine could not resolve the Server name through DNS <br/>
- <b>FINDING:</b> The Windows 10 Machine cannot find the Windows 2019 Server by its Hostname. Also shows a DNS server that is NOT pointing to the internal IP Address for the Server <br/>
<img src="https://i.imgur.com/IvR9mcN.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/OMmXO6f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>ACTION:</b> Used ipconfig /all to check the IP Address and DNS Settings of the Windows Server <br/>
- <b>FINDING:</b> The DNS Settings of the INTERNAL NIC are pointing to an EXTERNAL DNS Server (8.8.8.8) instead of the Server's own Address<br/>
<img src="https://i.imgur.com/biO9iAJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>ACTION:</b> Checked the DNS Settings of the INTERNAL NIC <br/>
- <b>VERIFICATION:</b> The DNS Settings of the INTERNAL NIC are indeed to an EXTERNAL DNS Server (8.8.8.8) instead of the Server's own Address<br/>
- <b>CORRECTION:</b> Changed the DNS for the Server's INTERNAL NIC to the Server's IP Address, allowing it to resolve INTERNAL queries </br>
<img src="https://i.imgur.com/Kpf9jvn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/s4HeNB5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Xl5yWwu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
- <b>ACTION:</b> Checked the Forwarders inside of the DNS Manager on the Server to see if queries outside of the network are using the Server's EXTERNAL NIC <br/>
- <b>FINDING:</b> The Forwarders are NOT using the Server's EXTERNAL NIC's IP Address (10.0.2.15). They are using a DNS that is not attached to the Network (8.8.8.8). This was causing delays when accessing external resources and web-browsing.<br/>
- <b>CORRECTION:</b> Updated the Forwarders to use the correct address. </br>
<img src="https://i.imgur.com/KDD2L0a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/LsBo2ej.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/KlVKWvJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
- <b>ACTION:</b> Checked the DNS Settings on the Windows 10 Machine to see what they were set to <br/>
- <b>FINDING:</b> Windows 10 Machine's DNS was also pointing to an External DNS Server <br/>
- <b>CORRECTION:</b> Updated the DNS Settings on the Windows 10 Machine to match the Server's Internal DNS Settings <br/>
<img src="https://i.imgur.com/f9vCS7a.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/LwyQQdM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>ACTION:</b> Used the Ipconfig /flushdns command on both the Windows Server and Windows 10 Machine to ensure no remnants of past configurations remain cached. <br/>
<img src="https://i.imgur.com/W7mc5FQ.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/wqS8ozp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>FINDING:</b> Windows 10 Machine is now able to successfully perform an nslookup and ping of the Server. Normal DNS Operation has been restored. <br/>
<img src="https://i.imgur.com/jmSw8jQ.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/M4fFlvX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>Challenges and Solutions</h2>
- <b>CHALLENGE:</b> Could not get the Windows 10 Machine to contact the Server via the Internal Network <br/>
- <b>SOLUTION:</b> Updated the Server's and Windows 10 Machine's DNS Settings to use the correct addresses <br/>
<br />
- <b>CHALLENGE:</b> Windows 10 Machine was experiencing delays loading websites and resources outside of the Internal Network <br/>
- <b>SOLUTION:</b> Updated the Server's Forwarders via DNS Manager to use the Server's EXTERNAL NIC. <br/>
<br />

<h2>Conclusion and Key Learnings</h2>
This lab demonstrates the importance of correct DNS configuration in maintaining optimal network performance. 
Through this challenge, I learned to diagnose DNS issues, configure DNS settings, and improve network connectivity, which are essential skills for a Tier 2 Help Desk role.

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
