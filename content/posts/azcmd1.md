---
title: "Office365-Powershell"
date: 2023-02-10T07:26:31+11:00
draft: false
toc: false
images:
tags:
  - powershell
  - office365
---

Although, I dont work much on AAD or IDAM side, there are times when I quickly need to refer to some details in Office365. Mainly due to someone is after this info, side effects of having GOD mode access....

1. End result I would like to run Get-MsolAccountSku

i. Install MSOnline module on Windows Powershell, ```Install-Module MSOnline```

ii. Connecto MSolService ```Connect-MsolService``` this would prompt for username and password. So if you work in Azure PIM environment, elevate your access first before running this cmdlet.

iii. Now, ```Get-MsolAccountSku``` and similar cmdlets to get desired information
