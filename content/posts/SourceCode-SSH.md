---
title: "Github, Azure Repos and SSH Authentication"
date: 2023-01-10T07:00:21+11:00
draft: false
toc: false
images:
tags:
  - azure repos
  - github
  - ssh keys
---

I often need to setup ssh authentication to access repos (github/azure repos). This is a quick post to keep all that information handy.

1. On your local machine (using bash prompt), run the below command to generate key. You can add a passphrase which improves or adds another layer of security.

```ssh-keygen -C "youremail@email.com"```

This should generate two files id_rsa and id_rsa.pub. Remember to keep id_rsa safe and dont accidentially copy this in source code or any publicly accessible endpoint.

2. On Github or Azure DevOps Repo add the contents of id_rsa.pub


Adding new SSH key in Azure DevOps -

{{<image src="../images/ado-ssh01.PNG">}}

Adding new SSH key in Github -

``` 
{{<image src="../images/github-ssh01.PNG">}}
```

Select New Key and add the contents of id_rsa.pub here.

When you clone your repo, the first time it will ask for authentication and it is added to known_hosts file.

3. Before you run git clone (Azure repos in my case), change the default https to ssh.

``` 
{{<image src="../images/azurerepos-ssh-clone.PNG">}}
```