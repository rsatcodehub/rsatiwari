---
title: "Terraform-quick-notes"
date: 2023-01-10T07:26:31+11:00
draft: false
toc: false
images:
tags:
  - Terraform
  
---

It has been a while since I used Terraform, recently I wanted to refresh my memory and skills.

So, I started creating some basic infra in Azure and ADO pipelines.

This is for a quick reference -

1. One way to structure TF files, you can also add providers etc in a separate file.

{{<image src="../images/Terraform-quick-notes-01.PNG">}}

2. Remember to add .gitignore for TF files

3. Commands to create Infra using TF

```terraform init```

```terraform plan --var-file=filename.tfvars``` --var-file is optional and depends on your folder structure

```terraform apply --var-file=filename.tfvars```

If you are just starting out and see lot of errors in previous runs, my troubleshooting is to get rid of terraform files and do init and try again. Ofcourse, this is lab so take caution for Production environment.


### My usecase: 

To create AKS cluster. To create AKS you would first need to create the following -
    - Virtual Network
    - Log Analytics (Optional)
    - AKS Cluster

Also, to use Azure Storage for TF state file.

#### My learnings -

1. Structure folder something like

   TF
    - AKS
    - LogAnalyticsWorkSpace
    - VirtualNetwork
  
  Also, a pre-requisite would be creating a resource group, storage account and container to hold state file.

2. Run in the following sequence 
     - VirtualNetwork
     - LogAnalyticsWorkSpace
     - AKS

An important thing to note - Create a separate folders for the above with .gitignore (terraform) for all and ensure state filename are all unique eg. virtualnetwork - vnettfstate, aks - akstfstate, otherwise the previous step will teardown your environment.

Also, this might be handy to check currently supported AKS cluster version ```az aks get-versions --location australiaeast -o table```



