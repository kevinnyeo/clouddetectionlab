<h1>Cloud Detection Lab On Azure</h1>

<h2>Description:</h2>

- <b>Configure and Deploy Azure Resources such as Log Analytics Workspace, Virtual Machines, and Microsoft Sentinel<b/>
- <b>Implement Network and Virtual Machine Security Best Practices<b/>
- <b>Utilize Data Connectors to bring data into Sentinel for Analysis<b/>
- <b>Understand Windows Security Event logs<b/>
- <b>Configure Windows Security Policies<b/>
- <b>Utilize KQL to query Logs<b/>
- <b>Write Custom Analytic Rules to detect Microsoft Security Events<b/>
- <b>Utilize MITRE ATT&CK to map adversary tactics, techniques, detection and mitigation procedures<b/>

<h2>Project Architecture</h2>

<p align="center">
 <img src="https://i.imgur.com/K7Bz2o7.png" height="80%" width="80%" />

<h2>Objectives:</h2>

- <b>Gain hands-on experience securing cloud resources and detecting anomalies<b/>

<h2>Languages and Utilities Used:</h2>

- <b>Azure Free Tier </b>

<h2>Program Overview:</h2>

Based on the infrastructure layout, the lab will be broken down into the following sections:<br/>

[Step 1] Creating Lab Resources <br/> 

[Step 2] Getting Data Into Sentinel<br/> 

[Step 3] Generating Security Events<br/> 

[Step 4] Sentinel KQL Queries<br/> 

[Step 5] Writing Analytic Rules And Generating Scheduled Tasks<br/> 


<h2>Program walk-through:</h2>

<p align="center">
<b>[Step 1] Creating Lab Resources</b> <br/>
  1. Create a new resource group and launch a virtual machine <br/>
 <img src="https://i.imgur.com/jmdk773.png" height="80%" width="80%" /><br/>
 <img src="https://i.imgur.com/RoJqnrL.png" height="80%" width="80%" /><br/>
<br/>
  Current NSG Rules:<br/>
  <img src="https://i.imgur.com/iFXu49u.png" height="80%" width="80%" /><br/>
<br/>
  2. Configure Network Security Group to secure Virtual Machine <br/>
  RDP port 3389 is open to public which is prone to brute force or password spray attacks. <br/>
  To reduce our attack surface, we need to enable Just-In-Time access which implements the principle of least privilege. <br/> 
  Enable JIT Access in Microsoft Cloud Defender And Select the VM.<br/>
  <img src="https://i.imgur.com/PVOun4W.png" height="80%" width="80%" /><br/>
  <img src="https://i.imgur.com/CEgou2t.png" height="80%" width="80%" /><br/>
  <img src="https://i.imgur.com/1lUZN9V.png" height="80%" width="80%" /><br/>
<br/>
  Current NSG Rules:<br/>
  <img src="https://i.imgur.com/nlTXEx9.png" height="80%" width="80%" /><br/>
  A new rule has been added by Cloud Defender to restrict all traffic to our RDP port. <br/>
  However, this means we cannot access the VM. So we need to create a rule to allow access to the RDP port only from our local IP address.<br/>
<br/>
  3. Request JIT access with our local IP address as the Source <br/>
  <img src="https://i.imgur.com/lPECrGA.png" height="80%" width="80%" /><br/>
<br/>
  A new NSG rule has been created with highest priority to allow access to the VM with our local IP address.<br/>
  <img src="https://i.imgur.com/90Imtip.png" height="80%" width="80%" /><br/>
<br/>
  4. Create Log Analytic Workspace and connect Microsoft Sentinel<br/>
  <img src="https://i.imgur.com/It20kIw.png" height="80%" width="80%" /><br/>
  <img src="https://i.imgur.com/NvCL22K.png" height="80%" width="80%" /><br/>
 
<p align="center">
<b>[Step 2] Getting Data Into Sentinel</b> <br/>
<br/>

<p align="center">
<b>[Step 3] Generating Security Events</b> <br/>
<br/>

<p align="center">
<b>[Step 4] Sentinel KQL Queries</b> <br/>
<br/>

<p align="center">
<b>[Step 5] Writing Analytic Rules And Generating Scheduled Tasks</b> <br/>
<br/>

