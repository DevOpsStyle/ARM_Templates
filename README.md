<h2>Deploy Azure VM and join to legacy Domain</h2>

This template can be used for the deployment of different Azure VMs and join these to AD (Only Windows).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fmain.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h2>ChatGPT Sentinel Integration</h2>

This template can be used for the deployment of a Logic App in order to be triggered by Sentinel during the creation of an incident.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fchatgptsentinel.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h2>ChatGPT Advisor Cost Integration</h2>

This template can be used for the deployment of a Logic App in order to be triggered by Azure Advisor during the creation of a new recommendation related cost saving.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fchatgptadvisorcost.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h3>Deploy Azure VM and join to legacy Domain: Configuration</h3>

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| Region  | Based on RG  | If the RG was already created will be shown the location of the RG |
| Network Interface Name | The name to assign to the new NIC | The name need to be available |
| Enable Accelerated Networking | Feature that increase the performance of the Network Interface | Available only for certains SKU |
| Subnet Name | The name of the subnet to use for the deployment | Ensure to have slots on the network site for the deployment |
| Virtual Network Id | The full Vnet ID of the network resoruce | Example: /subscriptions/5558a56e-5192-4c61-9c72-9acd05a5045e/resourceGroups/management-rg/providers/Microsoft.Network/virtualNetworks/Prd-network |
| Virtual Machine Name | The VM Name | The Name need to be unique in your environment |
| Virtual Machine RG | RG used for the deployment | \\ |
| System Type | Choose your system type | Example: MicrosoftWindowsServer |
| Offer | Choose the offer for the image | Example: WindowsServer |
| OS Version | Choose the OS level image | Example: 2019-datacenter-gensecond |
| OS Disk Type | Select the appropriate disk type for the VM | Example: StandardSSD_LRS |
| Os Disk Delete Option | If set to "Delete" the disk will be deleted with the resource | \\ |
| Virtual Machine Size | Choose the VM Size | Example: Standard_D2ads_v5 |
| Nic Delete Option | If set to "Delete" the NIC will be deleted with the resource | \\ |
| Admin Username | Admin Username for the VM | \\ |
| Admin Password | Admin Password for the VM | \\ |
| Patch Mode | Default is Manual. | If you choose the default option ensure to disable automatic updates |
| Enable Automatic Updates | True of False | If Patch Mode is Manual need to be disabled |
| Enable HotPatching | Only available for a few VM | Set the parameter to Disable for now |
| Domain Join User Name | Username used for join in to Domain | \\ |
| Domain Join User Password | Password of the Account used for the Domain Join | \\ |
| Domain FQDN | full FQDN of the domain | Example: Contoso.com |
| OU Path | Specific the OU were the VM will be placed | Example: OU=newvm,DC=contoso,DC=com |

<h3> Deployment and Result </h3>

The Deployment consist in 2 slot:
- Create VM
- Join VM to the AD Domain

<img src="https://i.ibb.co/935W606/deployment.jpg" alt="Deployment" title="Deployment">

After the deploy the IT Administrator can found the Computer Object in the specified OU:

<img src="https://i.ibb.co/GWjGRrv/computer.jpg" alt="Post Deployment" title="Post Deployment">

P.S. In case you have some open point... yes I called the VM "OldVM".

<h3>ChatGPT Sentinel Integration: Configuration</h3>

<h3>Required Connector</h3>
<h4>Sentinel Connector</h4>

When the deployment is completed go in your Logic App and create the Sentinel connector based on Sentinel Incident following the screen below:

<img src="https://i.ibb.co/8gLdy3Q/trigger-1.jpg" alt="InitialTrigger" title="InitialTrigger">

The last configuration is in the "for each" cycle. Click on "Add an Action" and select "Add a comment to incident (V3)" following the screen below:

<img src="https://i.ibb.co/B3pwXBr/trigger-2.jpg" alt="ForCicle" title="ForCicle">

Now configure the connector following the screen:

<img src="https://i.ibb.co/3FJ42TP/trigger-3.jpg" alt="AddComment" title="AddComment">

<h4>Http Connector</h4>

Change the URI string inside the HTTP block. Insert the endpoint name and model name following the example below (In my example the endpoint name is OPENAISERVICE and the model name is SUPPORTENGINEER):

<img src="https://i.ibb.co/bF6J2MY/trigger-4-http.jpg" alt="Uri" title="Uri">

<h3>Question</h3>

As already shared, the variable Question is the string that will be sent to OpenAI's private endpoint service. This represents the 'human question' to be addressed to the artificial intelligence. Write the Question following what you need to ask. Below an example:

<img src="https://i.ibb.co/3FJ42TP/trigger-5.jpg" alt="Uri" title="Uri">

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| Question  | Insert the Question for OpenAI  | The parameter is inside the first "Initialize Variable". Put your question in the "value" attribute |
| api-key | The name to assign to the new NIC | The parameter is inside the second "Initialize Variable". Put your question in the "value" attribute  |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

<h3>ChatGPT Advisor Cost Integration: Configuration</h3>

<h3>Required Identity</h3>
<h4>Managed Identity</h4>

When the deployment is completed go in your Logic App and create a Managed Identity following the example below:

<img src="https://i.ibb.co/kSnwJ1G/managed-identity.jpg" alt="InitialTrigger" title="InitialTrigger">

When the Managed identity is created ensure to configure the first HTTP module to use them:

<img src="https://i.ibb.co/pw86mGz/Use-the-managed-identity.jpg" alt="managedidentity" title="managedidentity">

<h4>Http Connector</h4>

Change the URI string inside the HTTP block. Insert the endpoint name and model name following the example below (In my example the endpoint name is OPENAISERVICE and the model name is SUPPORTENGINEER):

<img src="https://i.ibb.co/bF6J2MY/trigger-4-http.jpg" alt="Uri" title="Uri">

<h3>Question</h3>

As already shared, the variable Question is the string that will be sent to OpenAI's private endpoint service. This represents the 'human question' to be addressed to the artificial intelligence. Write the Question following what you need to ask. Below an example:

<img src="https://i.ibb.co/3FJ42TP/trigger-5.jpg" alt="Uri" title="Uri">

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| Question  | Insert the Question for OpenAI  | The parameter is inside the first "Initialize Variable". Put your question in the "value" attribute |
| api-key | The name to assign to the new NIC | The parameter is inside the second "Initialize Variable". Put your question in the "value" attribute  |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

<h3>Send Email</h3>

When the data elaboration is completed you can send results using e-mail. In order to achieve that insert the Send an email (V2) module at the end and configure the module following the screen:

<img src="https://i.ibb.co/6rtQsGD/email.jpg" alt="email" title="email">
