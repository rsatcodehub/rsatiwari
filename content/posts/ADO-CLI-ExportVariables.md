---
title: "ADO CLI and Variables List"
date: 2023-02-01T07:26:31+11:00
draft: false
toc: false
images:
tags:
  - azcli
  - ado
---

Scenario:

I wanted to export a long list of variables defined in release pipeline in Azure DevOps. This was on classic GUI based pipeline. I wanted to understand the values it was populated. If you have similar challenge, the below solution may help you.

One Possible Solution:

I am sure there may be another way to work through this solution. The way I got the results was using the below steps -


Classic UI Screenshot for a release pipeline with variables -

{{<image src="../images/ado-variables-gui.PNG">}}


 1. I used Azure Cloud Shell to install the devops extension ```az devops extension install```

 2. Login to azure ```az login``` and I dont think context matter in this scenario.

 3. Run the following command to see the output on console

 ```az pipelines release definition show --name "Name of the pipeline" --org https://dev.azure.com/typically-companyname/ --project "ADO Project Name"```


4. Validate the #3 command works correctly, to export it in a file format

```az pipelines release definition show --name "Name of the pipeline" --org https://dev.azure.com/typically-companyname/ --project "ADO Project Name" --output json > pipelinenamevars.json```

Change pipelinenamevars.json to your desired name .json
