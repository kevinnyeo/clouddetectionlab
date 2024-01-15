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
<br/>
 
<p align="center">
<b>[Step 2] Getting Data Into Sentinel</b> <br/>
<br/>
 1. Connect Windows Security Event Data to Microsoft Sentinel and define scope to resource group <br/>
 <img src="https://i.imgur.com/FGUJplQ.png" height="80%" width="80%" /><br/>
 <img src="https://i.imgur.com/3p0mHr5.png" height="80%" width="80%" /><br/>
 <img src="https://i.imgur.com/vWCpUxe.png" height="80%" width="80%" /><br/>
 <img src="https://i.imgur.com/zextD8p.png" height="80%" width="80%" /><br/>
 
<p align="center">
<b>[Step 3] Generating Security Events</b> <br/>
<br/>
 Now that our VM is connected to Sentinel and our Log Analytics Workspace we need to transport data from our Logs. <br/>
 To do this we need to simply need to perform some action on the Windows 10 events that will generate security alerts. <br/>
<br/>
 1. Login to connected VM via RDP. Open event viewer from start menu, under security tab, we can view all security event logs on the VM. <br/>
 An example event id in this case would be '4624' for successful logons onto our machine. <br/>
 <img src="https://i.imgur.com/IEcLoah.png" height="80%" width="80%" /><br/>
 <img src="https://i.imgur.com/9FP9IVu.png" height="80%" width="80%" /><br/>
<br/>

<p align="center">
<b>[Step 4] Sentinel KQL Queries</b> <br/>
<br/>
 1. Once we know properties of Windows Events logs such as the event IDs, we can query it in Sentinel using KQL.
 <img src="https://i.imgur.com/PDCCEON.png" height="80%" width="80%" /><br/>
<br/>

<p align="center">
<b>[Step 5] Writing Analytic Rules And Generating Scheduled Tasks</b> <br/>
<br/>
 Next, we can generate alerts for certain events by setting up custom analytic rules. <br/>
 We will be writing a rule for Scheduled Tasks and Persistence Techniques. <br/>
 <br/>
 According to the MITRE Attack Framework, “Adversaries may abuse task scheduling functionality to facilitate initial or recurring <br/>
 execution of malicious code. Utilities exist within all major operating systems to schedule programs or scripts to be executed at <br/>
 a specified date and time”. <br/>
 <br/>
 1. Create a scheduled task in the VM that executes a .exe program. <br/>
 <img src="https://i.imgur.com/KaTx6kl.png" height="80%" width="80%" /><br/>
 <img src="https://i.imgur.com/GonV5dt.png" height="80%" width="80%" /><br/>
 <br/>
 2. Obtain log properties of this type of event. In this case the Event ID for scheduled tasks creation is 4698. <br/>
 <img src="https://i.imgur.com/G8RG9wR.png" height="80%" width="80%" /><br/>
 <br/>
 3. Create an analytics rule to generate an alert. Select appropriate Severity level and TTP (technique, tactics, procedures) <br/>
 <img src="https://i.imgur.com/ozocACd.png" height="80%" width="80%" /><br/>
<br/>
 Basic rule query: <br/>
 <img src="https://i.imgur.com/p0wRsi5.png" height="80%" width="80%" /><br/>
<br/>
 The above rule will return logs corresponding to the rule. However, we can add in additional lines to parse out important information only.<br/>
 Example of updated query: <br/>
 <img src="https://i.imgur.com/Da2UdEg.png" height="80%" width="80%" /><br/>
 In this updated query, only important log information is displayed which would help if an analyst want to investigate the alert. <br/>
<br/> 
 4. Next, add in entities in the rule so that it would be easier for an analyst to investigate. <br/>
 In this example, User,  ProcessID, Computer host and name of tasks is added. <br/>
 <img src="https://i.imgur.com/SitNqNl.png" height="80%" width="80%" /><br/>
<br/>
 5. Lastly, we will test our rule by creating a scheduled task in our VM. <br/>
 We can see that a new incident/alert is generated on our dashboard. <br/>
 By clicking on the alert generated, we are able to access to information regarding to the log as per our rule configuration. <br/>
 <img src="https://i.imgur.com/R4szBfz.png" height="80%" width="80%" /><br/>
 <img src="https://i.imgur.com/JQAK9pB.png" height="80%" width="80%" /><br/>
<br/>
 






 
