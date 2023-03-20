---
title: "ssh-pat-issues-ADO Repos"
date: 2023-03-10T07:26:31+11:00
draft: false
toc: false
images:
tags:
  - ADO Repos
  - Authentication
---
I recently was working on a new machine (Windows) and had to setup all the software and configuration on it.

It has been while and kept getting this issue when I installed or tried to follow ssh auth method for ADO repos.

I went through some troubleshooting and one of the errors was as below. 

Issue:

{{<image src="../images/ssh-pat-ado-issues-01.PNG">}}


Solution:

1. Open PowerShell as an administrator by right-clicking the start menu and selecting "Windows PowerShell (Admin)".

2. Generate SSH Key using the below command       
       ```ssh-keygen -t rsa -b 4096 -C "your_email@domain.com"```

3.  Copy the public key file ```Get-Content ~/.ssh/id_rsa.pub | clip```

4. On Azure DevOps account settings add SSH public keys under security

5. Test SSH connection 

   ```ssh -T git@ssh.dev.azure.com```
      
6. If it is successful, browse to Azure Repos and use SSH option to clone

7. However, if this unsuccessful, you may see some shell access error. It is possible your coprorate/VPN network does not allow SSH (port 22)

    Use the https option to clone and use PAT.

    i. On ADO under your account, generate new PAT with desired permissions.

    ii. In my case, as mentioned in issue, I was having issues with ssh agent service. Turns out it was disabled.

          
    Service Status check --> 
    ```powershell 
    Get-service ssh-agent
    ```

    Service start type check -->
          
    ```powershell
    Get-Service ssh-agent | Select-Object StartType
    ```

    In my case, it was Disabled

    Change Service Start to Automatic --> 
    
    ```powershell
    Set-Service ssh-agent -StartupType Automatic
    ```

    iii. Now, add the ssh key and PAT 

    list agent identities--> cd .\.ssh and ```ssh-add -l```

    add ssh key --> ssh-add ```.\id.rsa``` THis should display as identity and your name/email address
        
    iv. Git Config -

    *```git config --global credential.helper "store --file ~/.git-credentials"```*

    *```git config --global user.name "Name"```*

    *```git config --global user.email "youremail@domain.com"```*

    *```git config --global credential.https://dev.azure.com.username PAT```* Only update PAT the URL is correct

    Now, clone ADO Repo using https method, it would prompt or pop-up browser and next time it should work seamlessly.
 

 
