---
title: "LoadBalance a service using Netscaler"
date: 2022-03-10T07:26:31+11:00
draft: false
toc: false
images:
tags:
  - Netscaler
  - LoadBalancer
---

I am no expert in Netscaler. However, I have been in situations where I had to figure out and place few services behind Netscaler. Since it was Non-production environment, I thought I might as well try and learn. Here is my version of steps that needs to be performed.

Scenario: You have a external and internal service and you need to secure the external service using SSL and place both services behind Netscaler.

Just a simple diagram to show my use case 

{{<image src="../images/Services-Netscaler01.PNG">}}

At a high-level I typically follow these steps -

1. Create Servers in Netscaler. These are the VMs or backend pool resources

{{<image src="../images/Netscaler-Config01.PNG">}}


2. Create Service Group. So, in reference to the above diagram, there would be two service group.

i. External Service Group

ii. Internal Service Group

This is a typical service group

{{<image src="../images/Netscaler-ServiceGP-Config01.PNG">}}


Service Group --> Monitors

This can be a simple ping or can be a custom monitor to check a service health.

Example of Service Group simple monitor using ping -

{{<image src="../images/NetScaler-ServiceGP-Monitor.png">}}  

Example of Service Group Custom monitor -


{{<image src="../images/NetScaler-ServiceGP-CustomMonitor.PNG">}}  

3. Next, is the virtual server which is the loadbalancing virtual server (VIP). Here you assign loadbalancer IP, Port eg. 443 and secure it with Certificate. Also, the most important step is association with a service group.


Sample load balancing virtual server 

{{<image src="../images/NetScaler-VirtualServer-VIP.PNG">}}  


Certiciate is a different process (refer below for Cert steps)

Thanks to Netscaler User Interface, it shows a high-level of steps need to be performed for Certificates.

{{<image src="../images/NetScaler-Cert-Config01.PNG">}}


i. Following the above steps, first create a key and then a CSR.


{{<image src="../images/NetScaler-Cert-Config02.PNG">}}

ii. Submit this to your certificate management tool eg. Venafi and generate a new certificate.

iii. Extract the certificate and grab the .crt and upload to NetScaler

iv. Now, you can bind the cert under Virtual server Certificate options.


{{<image src="../images/NetScaler-Cert-Bind.png">}}




