---
title: "ADO Agent Installation for Windows VM in a secure environment"
date: 2023-02-23T02:26:31+11:00
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
```

This is where the VMs will be registered.


2. Once the #1 is completed, you should see registration script something like below

``` 
{{<image src="../images/ADO-Registration-Script.PNG">}}
```

Use the copy option and since we are going to download manually ADO agent file (refer to step3), we need to modify this script.

Grab the last bit of the registration script, so it would be something like this 

```.\config.cmd --deploymentgroup --deploymentgroupname "DG-External" --agent $env:COMPUTERNAME --runasservice --work '_work' --url 'https://companyname.visualstudio.com/' --projectname 'ADO Project Name' --auth PAT --token xxxxxxxxxxxxxxxxxx```

url --> replace companyname with your relevent ADO 

The rest are self explanatory, when you generate the registration script, PAT token is automatically generated, which is typically valid less than a day.

3. Now, download the ADO/vsts agent for windows from the below location

https://github.com/microsoft/azure-pipelines-agent/releases


4. You may not need it, but for my scenario these VMs were clone and had previous ADO agent installed.

To remove/unregister ADO agent ```.\config.cmd remove --unattended``` remember to run this from the location where previous install of ADO agent is, eg. C:\adoagent\A1


5. Once you have populated all the fields in code in step 2, start powershell and run it



``` 
{{<image src="../images/registeradoclient01.PNG">}}
```

You can either use the default account or if you have a service account use it here

``` 
{{<image src="../images/registeradoclient02.PNG">}}
```

This should complete your registration steps. 

Validate it in Azure DevOps Project deployment group and add any tags against this, it could be useful in pipeline






