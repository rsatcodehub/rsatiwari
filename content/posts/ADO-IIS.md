---
title: "Azure DevOps and Configure IIS"
date: 2023-03-01T07:00:21+11:00
draft: false
toc: false
images:
tags:
  - ADO
---
Scenario: You need to register a Windows Virtual machines as a deployment target in Azure DevOps Project. Also, the VMs are placed in a secure zone where files cannot be downloaded directly due to firewall restrictions. Hence, you cannot use the ADO default registration script to download the vsts agent and register it.

Steps to configure it -

1. Azure DevOps - Create a new Deployment Group eg. DG-External


``` 
{{<image src="../images/ADO-IIS-DeploymentGroup.PNG">}}



You need to configure IIS using Azure DevOps 

In this blog I will use Classic UI version, next one I will cover yaml version

Steps to configure it -

1. Azure DevOps - Create a new Deployment Group eg. DG-External


``` 
{{<image src="../images/ADO-IIS-DeploymentGroup.PNG">}}















