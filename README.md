<h1>DNS and Network Performance Fix</h1>

<!-- ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo) -->

<h2>Project Overview</h2>
This case study demonstrates the troubleshooting process for resolving slow network performance caused by incorrect 
DNS configuration on a Windows Server 2019 machine. Both the Windows Server 2019 and Windows 10 machines are experiencing 
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

- <b>Action:</b> Used nslookup and ping to verify the Windows 10 Machine could not resolve the Server name through DNS <br/>
- <b>Finding:</b> The Windows 10 Machine cannot find the Windows 2019 Server by its Hostname. Also shows a DNS server that is NOT pointing to the internal IP Address for the Server <br/>
<img src="https://i.imgur.com/IvR9mcN.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/OMmXO6f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>Action:</b> Used ipconfig /all to check the IP Address and DNS Settings of the Windows Server <br/>
- <b>Finding:</b> The DNS Settings of the INTERNAL NIC are pointing to an EXTERNAL DNS Server (8.8.8.8) instead of the Server's own Address<br/>
<img src="https://i.imgur.com/biO9iAJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>Action:</b> Checked the DNS Settings of the INTERNAL NIC <br/>
- <b>Verification:</b> The DNS Settings of the INTERNAL NIC are indeed to an EXTERNAL DNS Server (8.8.8.8) instead of the Server's own Address<br/>
- <b>Correction:</b> Changed the DNS for the Server's INTERNAL NIC to the Server's IP Address, allowing it to resolve INTERNAL queries </br>
<img src="https://i.imgur.com/Kpf9jvn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/s4HeNB5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Xl5yWwu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
- <b>Action:</b> Checked the Forwarders inside of the DNS Manager on the Server to see if queries outside of the network are using the Server's EXTERNAL NIC <br/>
- <b>Finding:</b> The Forwarders are NOT using the Server's EXTERNAL NIC's IP Address (10.0.2.15). They are using a DNS that is not attached to the Network (8.8.8.8). This was causing delays when accessing external resources and web-browsing.<br/>
- <b>Correction:</b> Updated the Forwarders to use the correct address. </br>
<img src="https://i.imgur.com/KDD2L0a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/LsBo2ej.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/KlVKWvJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
- <b>Action:</b> Checked the DNS Settings on the Windows 10 Machine to see what they were set to <br/>
- <b>Finding:</b> Windows 10 Machine's DNS was also pointing to an External DNS Server <br/>
- <b>Correction:</b> Updated the DNS Settings on the Windows 10 Machine to match the Server's Internal DNS Settings <br/>
<img src="https://i.imgur.com/f9vCS7a.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/LwyQQdM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>Action:</b> Used the Ipconfig /flushdns command on both the Windows Server and Windows 10 Machine to ensure no remnants of past configurations remain cached. <br/>
<img src="https://i.imgur.com/W7mc5FQ.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/wqS8ozp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
- <b>FINDING:</b> Windows 10 Machine is now able to successfully perform an nslookup and ping of the Server. Normal DNS Operation has been restored. <br/>
<img src="https://i.imgur.com/jmSw8jQ.png" height="80%" width="80%" alt="VM and Server 2016 Steps"/>
<img src="https://i.imgur.com/M4fFlvX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We're going to enable Hyper-V to help with the smoothness of operation:  <br/>
<img src="https://i.imgur.com/fg4AGZE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Let's start the Windows 10 Installation:  <br/>
<img src="https://i.imgur.com/Iop3wZU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Choose Windows 10 Pro for the installation since we'll be operating in a Professional Environment it gives us options and featurese that Windows 10 Home doesn't have.  <br/>
<img src="https://i.imgur.com/4bsgzqO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Windows 10 has been installed and we're logged in.:  <br/>
<img src="https://i.imgur.com/dwU28JJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We need to change our DNS settings to point to our Domain Controller's IP so we can use it for DNS:  <br/>
<img src="https://i.imgur.com/hsiVq8C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Let's join this to our Active Directory Domain. First we navigate to Advanced System Settings:  <br/>
<img src="https://i.imgur.com/jmlt9HO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now we'll click change to get to Change our Computer name, but more importantly we'll be presented with the option to Join a Domain:  <br/>
<img src="https://i.imgur.com/wpB3RtB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We have to Authorize the Domain Addition by logging in with an account that is ALREADY a part of the DOMAIN (not the local machine). We're using the "Adminstrator" account here:  <br/>
<img src="https://i.imgur.com/tL9jXVo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We've successfully joined the domain, Lets check our Domain Controller and see what shows up...:  <br/>
<img src="https://i.imgur.com/hbTfEIq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In our Domain Controller, we can see we have an IP Address Lease from COMP-001 (our newly joined Computer):  <br/>
<img src="https://i.imgur.com/XtPcY32.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We can also see we have a new addition in Active Directory Users and Computers with our newly joined Computer:  <br/>
<img src="https://i.imgur.com/SRtdW08.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
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
