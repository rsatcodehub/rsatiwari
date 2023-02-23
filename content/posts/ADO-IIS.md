---
title: "Azure DevOps and IIS"
date: 2023-02-23T02:26:31+11:00
draft: false
toc: false
images:
tags:
  - ADO
---

Scenario: You need to setup IIS on Windows Virtual machines using Azure DevOps. Also, the VMs are placed in a secure zone where files cannot be downloaded directly due to firewall restrictions. Hence, you cannot use the ADO default registration script to download the vsts agent and register it.

Steps to configure it -

1. Azure DevOps - Create a new Deployment Group eg. DG-External


``` 
{{<image src="../images/ADO-IIS-DeploymentGroup.PNG">}}
```

This is where the VMs will be registered.


2. Once the #1 is completed, you should see registration script something like below

``` 
{{<image src="../images/ADO-Registration-Script.PNG">}}
```


3. Download the ADO/vsts agent for windows from the below location

https://github.com/microsoft/azure-pipelines-agent/releases


