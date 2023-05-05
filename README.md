<h2>Deploy Azure VM and join to legacy Domain</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#deploy-azure-vm-and-join-to-legacy-domain-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of different Azure VMs and join these to AD (Only Windows).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fmain.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h2>ChatGPT Sentinel Integration</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#chatgpt-sentinel-integration-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of a Logic App in order to be triggered by Sentinel during the creation of an incident.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fchatgptsentinel.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h2>ChatGPT Advisor Cost Integration</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#chatgpt-advisor-cost-integration-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of a Logic App in order to be triggered by Azure Advisor during the creation of a new recommendation related cost saving.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fchatgptadvisorcost.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h2>ChatGPT Tenant Subscription Resources Assessment</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#chatgpt-tenant-subscription-resources-assessment-1" target="_blank">Configuration</a>

This template can be used for the deployment of a Logic App which can help during Subscription Assessment.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2FTenantSubAssessment.json" target="_blank">
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

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| Question  | Insert the Question for OpenAI  | The parameter is inside the first "Initialize Variable". Put your question in the "value" attribute |
| api-key | The API code for manage your OpenAI service | The parameter is inside the second "Initialize Variable". Put your question in the "value" attribute  |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

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

<h3>ChatGPT Advisor Cost Integration: Configuration</h3>

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| changesubid  | Insert the subscription id | You can found the Sub id in different ways, one of them is to get the Subscription ID inside "Subscription" services in the Azure Portal  |
| Question  | Insert the Question for OpenAI  | The parameter is inside "Question variable". Put your question in the "value" attribute |
| api-key | The API code for manage your OpenAI service | The parameter is inside "API-KEY variable". Put your question in the "value" attribute  |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |


<h3>Required Identity</h3>
<h4>Managed Identity</h4>

When the deployment is completed go in your Logic App and create a Managed Identity following the example below:

<img src="https://i.ibb.co/kSnwJ1G/managed-identity.jpg" alt="InitialTrigger" title="InitialTrigger">

When the Managed identity is created ensure to configure the first HTTP module (Get Recommendation) to use them:

<img src="https://i.ibb.co/jbTJqGZ/get-recommendation-list.jpg" alt="get-recommendation-list" title="get-recommendation-list">

<h4>Http Send recommendation to OpenAI Connector</h4>

Change the URI string inside the "Send recommendation to OpenAI" block. Insert the endpoint name and model name following the example below (In my example the endpoint name is OPENAISERVICE and the model name is SUPPORTENGINEER):

<img src="https://i.ibb.co/bF6J2MY/trigger-4-http.jpg" alt="Uri" title="Uri">

<h3>Send Email</h3>

When the data elaboration is completed you can send results using e-mail. In order to achieve that insert the Send an email (V2) module at the end inside the last For Cycle. Put the module under "True" condition and configure the module following the screen:

<img src="https://i.ibb.co/MCQPHwC/emailform.jpg" alt="emailform" title="emailform">

<img src="https://i.ibb.co/NCQ9W99/email.jpg" alt="email" title="email">

<h3>ChatGPT Tenant Subscription Resources Assessment</h3>

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| api-key | The API code for manage your OpenAI service | The parameter is inside the second "Initialize Variable". Put your question in the "value" attribute  |
| api-key-users | The API code for manage your OpenAI service | The parameter is inside the second "Initialize Variable". Put your question in the "value" attribute |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

<h3>Required Connector</h3>

When the deployment is completed go in your Logic App and create the Subscription connector "List Resources by subscription" based on the screen below, between modules "When HTTP request is received" and "Create Report Variable":

<img src="https://i.ibb.co/KV0WG4N/listresourcesbysubscription.jpg" alt="SubscriptionConnector" title="SubscriptionConnector">

For the cycle "For Each Resource" change the item with "value" following the example below:

<img src="https://i.ibb.co/s5XCKp7/foreachresource.jpg" alt="foreachresource" title="foreachresource">

Configure the Graph-API Connector using as example the screen below. Keep in mind that you must create a new Application under your Azure Tenant in order to start Graph-API request. The new application must have all the delegation permission for GraphAPI communication. For help follow this link: <a href="https://techcommunity.microsoft.com/t5/integrations-on-azure-blog/calling-graph-api-from-azure-logic-apps-using-delegated/ba-p/1997666" target="_blank"> 

<img src="https://i.ibb.co/9VDHgBB/getuserlistconfiguration.jpg" alt="GraphAPI" title="GraphAPI">

Regarding the HTTP Connector, these are used for send request to OpenAI Service. You have to configure the api-key and api-key-users that are the secret used for the OpenAI Connections. Also you have to manage the endpoint and model name of the Connector following the example below: 

<img src="https://i.ibb.co/bF6J2MY/trigger-4-http.jpg" alt="HTTP" title="HTTP">

Now is the time to configure the Send-Email(V2) module. This module will be used for send result to an e-mail address. Place this module in the end of Logic App. Follow the configuration below:

<img src="https://i.ibb.co/S7zdmD9/sendemail.jpg" alt="sendemail" title="sendemail">

Body part:

<img src="https://i.ibb.co/SxBvQ95/sendemailconfiguration.jpg" alt="SendEmail" title="SendEmail">

Run After Configuration:

<img src="https://i.ibb.co/2KBZ766/sendemailconfigurationrunafter.jpg" alt="sendemailconfigurationrunafter" title="sendemailconfigurationrunafter">

Ensure that the Workflow Setting related "High throughput" is enabled. Logic Apps are usually used for script that not require a long rung. With this option you can extend the execution up to 15 minutes. 

<img src="https://i.ibb.co/s2xmcHr/runtimeoptions.jpg" alt="runtimeoptions" title="runtimeoptions">

If you have too much resources in your environment another way to complete the assessment is to run the Logic App under the Resources Groupe you need to analyze. In order to do that replace the "list resources by subscription" module with "list resources by resource group" module:

<img src="https://i.ibb.co/BfB4KGq/listresourcesbyresourcegroup.jpg" alt="listresourcesbyresourcegroup" title="listresourcesbyresourcegroup">
