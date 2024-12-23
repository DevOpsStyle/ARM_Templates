<h2>ELZ OpenAI</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#ELZ-Configuration" target="_blank">Configuration</a>

This template can be used for the deployment of different Azure VMs and join these to AD (Only Windows).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Frefs%2Fheads%2Fmain%2FAIServicesForInfraELZ.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h2>Azure Hybrid Group Membership Notification</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#azure-hybrid-group-membership-notification-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of different Azure VMs and join these to AD (Only Windows).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2FHybridGroupNotification.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

-------------------------------------------------------------------------------------

<h2>Deploy Azure VM and join to legacy Domain</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#deploy-azure-vm-and-join-to-legacy-domain-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of different Azure VMs and join these to AD (Only Windows).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fmain.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

-------------------------------------------------------------------------------------

<h2>ChatGPT Sentinel Integration</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#chatgpt-sentinel-integration-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of a Logic App in order to be triggered by Sentinel during the creation of an incident.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fchatgptsentinel.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

-------------------------------------------------------------------------------------

<h2>ChatGPT Advisor Cost Integration</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#chatgpt-advisor-cost-integration-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of a Logic App in order to be triggered by Azure Advisor during the creation of a new recommendation related cost saving.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fchatgptadvisorcost.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

-------------------------------------------------------------------------------------

<h2>ChatGPT Tenant Subscription Resources Assessment</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#chatgpt-tenant-subscription-resources-assessment-1" target="_blank">Configuration</a>

This template can be used for the deployment of a Logic App which can help during Subscription Assessment.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2FTenantSubAssessment.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

-------------------------------------------------------------------------------------

<h2>CostManagement monitoring with Azure OpenAI Integration V2</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#costmanagement-monitoring-with-azure-openai-integration-v2-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of a Cost Management Logic App using Azure OpenAI.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fcostmanagementmonthlycheck.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

-------------------------------------------------------------------------------------

<h2>OpenAI Smart Update Analysis</h2>

<a href="https://github.com/DevOpsStyle/ARM_Templates#openai-smart-update-analysis-configuration" target="_blank">Configuration</a>

This template can be used for the deployment of different Azure VMs and join these to AD (Only Windows).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2FSmartUpdateAnalysis.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

-------------------------------------------------------------------------------------

<h3>Azure Hybrid Group Membership Notification: Configuration</h3>

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| replacewithsubid | Connection setting during deployment | Replace with your Subscription ID |
| replacewithRGname | Connection setting during deployment | Replace with the selected RG Name for the deployment |
| replace with tenant id | HTTP Module: Tenant ID | Replace with your Tenant ID |
| replace with clientid | HTTP Module: Service Principal Client ID | Replace with Service Principal Client ID |
| replace with secret | HTTP Module: Service Principal Secret ID | Replace with Service Principal Secret ID |

N.B. The solution require a Storage Account for store the logs about audit logs.

<h3> Deployment and Result </h3>

Durint the deployment please change the required value inside the connection string with the subscription id and the resource group name. After that, when the deployment is completed, please follow the documentation:

Change che API connection with a new one following your requirement. The solution must have permission to write and read the storage account.

<img src="https://i.ibb.co/SdP3K8p/connection1.png" alt="Connection" title="Connection">

The first "Get blob content (V2)" block must be configured with the final name of the blob (read file) that will store the Delta URL Link (in yellow). Please Use the same Blob Name for all the Blob Blocs:

<img src="https://i.ibb.co/PDG15vz/containerconfig.png" alt="containerconfig" title="containerconfig">

The Flow have different HTTP blocks required for get informations from Azure Graph. Please exand all the foreach blocks and customize the HTTP blocks as shown below. Keep in mind that the chosen solution must have permission to read Azure Graph. Ensure to have a Service Principal with all the required permission <a href=https://learn.microsoft.com/en-us/graph/api/user-get?>reported here</a>  and <a href=https://learn.microsoft.com/en-us/azure/purview/create-service-principal-azure>here</a>. For a tutorial please refer to <a href=https://techcommunity.microsoft.com/t5/azure-integration-services-blog/calling-graph-api-from-azure-logic-apps-using-delegated/ba-p/1997666>this link</a>:

<img src="https://i.ibb.co/ZTPXx8t/HTTPrequest.png" alt="HTTPrequest" title="HTTPrequest">

Remember to change the group name inside the foreach block in order to check only modification to the required group:

<img src="https://i.ibb.co/VgsHD4b/groupname.png" alt="groupname" title="groupname">

The last step is to add and customise the Send e-mail form (V2) to send an e-mail with the requested information. You can customise it as you wish. The block must be placed at the end of the logic app flow.

<img src="https://i.ibb.co/MG4GQJd/email.png" alt="email" title="email">

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
| replacewithsubid | Connection setting during deployment | Replace with your Subscription ID |
| replacewithRGname | Connection setting during deployment | Replace with the selected RG Name for the deployment |
| Question  | Insert the Question for OpenAI  | The parameter is inside the first "Initialize Variable". Put your question in the "value" attribute |
| api-key | The API code for manage your OpenAI service | The parameter is inside the second "Initialize Variable". Put your question in the "value" attribute  |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

<h3>Required Connector</h3>

Durint the deployment please change the required value inside the connection string with the subscription id and the resource group name. After that, when the deployment is completed, please follow the documentation:

<img src="https://i.ibb.co/WfFw1zR/sentinel-connection.png" alt="Connection" title="Connection">

Configure the Question as you like. You can found a standard configuration by default:

<img src="https://i.ibb.co/g6h4gQ7/question.png" alt="question" title="question">

Configure the Api Key with the value inside your OpenAI Service:

<img src="https://i.ibb.co/yRjjnVW/api-key.png" alt="api-key" title="api-key">

Now configure the HTTP Connector for OpenAI Connection following this configuration:

<img src="https://i.ibb.co/mHtbp6J/HTTP.png" alt="HTTP" title="HTTP">

The last configuration is about the "Add Content to Incident (V3)". Follow the exaple below:

<img src="https://i.ibb.co/2yrrfV4/comments.png" alt="comments" title="comments">

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
| api-key | The API code for manage your OpenAI service | Get this value from your OpenAI Service  |
| api-key-users | The API code for manage your OpenAI service | Get this value from your OpenAI Service |
| apy-key-connections | The API code for manage your OpenAI service | Get this value from your OpenAI Service |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the OpenAI model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

<h3>Required Connector</h3>

When the deployment is completed go in your Logic App and create the Subscription connector "List Resources by subscription" and "List Resource Groups" based on the screen below. Keep attention to pur "List Resources by subscription" above "Create Report Variable" and "List Resource Groups" above "Api-Key Connections":

<img src="https://i.ibb.co/5BhrQ9B/list-resource-for-sub-and-rg-1.jpg" alt="ListResources" title="ListResources">

For the List Resource Group pipeline branch, ensure that the "For Each RG" Cycle have inside the "value" of the output "List Resource Groups":

<img src="https://i.ibb.co/R9wPDH4/For-Each-RG-value-list-rg-2.jpg" alt="ForEachRG" title="ForEachRG">

Regarding the Cycle "For Any Responses" ensure to cycle inside "value" of "Parse Connections Response":

<img src="https://i.ibb.co/LN35Z3g/for-any-response-3.jpg" alt="Foranyresponse" title="Foranyresponse">

The Cycle "For Each Connection Status" loop inside the "Choices" of Connections Response:

<img src="https://i.ibb.co/hKL9tkL/for-each-connection-status-4.jpg" alt="Foreachconnections" title="Foreachconnections">

For the List Resources by subscription pipeline branch, ensure that the "For Each Resource" Cycle have inside the "value" of the output "List Resources by subscription":

<img src="https://i.ibb.co/0ByCZ0L/for-each-resource-5.jpg" alt="ForEachRG" title="ForEachRG">

Inside this Cycle we have a Delay resource. The resource scope is to slow down the OpenAI request in order to not face with Quota Limit issues. If you have enough quota you can delete this.

<img src="https://i.ibb.co/zhqCywq/delay-6.jpg" alt="Delay" title="Delay">

For the Cicle "For Each Response" cycle inside the "Choices" of Parse Json:

<img src="https://i.ibb.co/d4GT9bx/for-each-response-7.jpg" alt="ForEachResponse" title="ForEachResponse">

For the Get User List pipeline branch, ensure to populate the module with all the required filed. Ensure to have a Service Principal with all the required permission <a href=https://learn.microsoft.com/en-us/graph/api/user-get?>reported here</a>  and <a href=https://learn.microsoft.com/en-us/azure/purview/create-service-principal-azure>here</a>. For a tutorial please refer to <a href=https://techcommunity.microsoft.com/t5/azure-integration-services-blog/calling-graph-api-from-azure-logic-apps-using-delegated/ba-p/1997666>this link</a>:

<img src="https://i.ibb.co/Rb9VBf7/get-user-list-8.jpg" alt="GetUserList" title="GetUserList">

Check the Cycle "For Each User" ensure to cycle inside Values of "Format_Json_Values":

<img src="https://i.ibb.co/h2PZz9p/for-each-user-9.jpg" alt="Foreachuser" title="Foreachuser">

Regarding "For Each Ouptut" Cycle ensure to cycle inside choices of "Parse Json 2":

<img src="https://i.ibb.co/Ch2k36H/for-each-output-9.jpg" alt="Foreachoutput" title="Foreachoutput">

Last step, the E-mail. For this template we chose to send assessment via E-Mail. This is a configuration Enxample. Place the module "Send Email(V2)" at the end point with the following configuration regarding "Run After":

<img src="https://i.ibb.co/71pYWRg/send-email-10.jpg" alt="RunAfter" title="RunAfter">

For the body of the E-Mail you can follow this example:

<img src="https://i.ibb.co/D1hhFkc/email-11.jpg" alt="Email" title="Email">

<h3>OpenAI Smart Update Analysis: Configuration</h3>

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| api-key | The API code for manage your OpenAI service | Get this value from your OpenAI Service |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the OpenAI model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

<h3>Required Connector</h3>

In order to configure in the right way the solution follow the steps below. As first step please configure the required recurrence:

<img src="https://i.ibb.co/FKd2qDV/recurrence.jpg" alt="recurrence" title="recurrence">

Now configure the HTTP request to the Graph Explorer enabling the authentication via System Assigned Managed Identity. Please remind that the Managed Identity need to have the righ permission on the subscription for read the resources:

<img src="https://i.ibb.co/dDhzNwZ/managed-identity.jpg" alt="managed-identity" title="managed-identity">

Now is the time to set the Api Key for the connection with Azure Open AI Service:

<img src="https://i.ibb.co/NWLntGz/api-key.jpg" alt="api-key" title="api-key">

At this point we need to configure the Ask to OpenAI module replacing the required parameters:

<img src="https://i.ibb.co/nz0Qq24/OpenAI.jpg" alt="OpenAI" title="OpenAI">

In the example below we have a "Send Email V2" connector for send the final report to the required people for Cost Management revision. If you want to follow the same approach configure the module following the same example adding them at the end of the Logic App. Make sure to use the correct variable in the body of the email in order to have them correctly formatted:

<img src="https://i.ibb.co/DKJwTsW/email.jpg" alt="email" title="email">
<img src="https://i.ibb.co/d7nV1SQ/finalemail.png" alt="finalemail" title="finalemail">

Please ensure to have enabled Managed Identity for the Logic App with the required permission in order to access to the subscription:

<img src="https://i.ibb.co/ZWP22tq/8.jpg" alt="identity" title="identity">

<h3>CostManagement monitoring with Azure OpenAI Integration V2: Configuration</h3>

| **Parameters** | **Information** | **Note** |
| ------------- | ------------- | ------------- |
| replace-with-sub-id | The Subscription ID where we want to monitor the costs | Get this value from your Azure Services  |
| api-key | The API code for manage your OpenAI service | Get this value from your OpenAI Service |
| apy-key-connections | The API code for manage your OpenAI service | Get this value from your OpenAI Service |
| changeendpointname | Insert the OpenAI endpoint name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |
| changemodelname | Insert the OpenAI model name | You can found the value inside the OpenAI resource inside Azure Cognitive Service |

<h3>Required Connector</h3>

After the deployment we can proceed with the configuration. The first step is to set all the required parameters following the examples below. Configure the Subscription ID inside the "Query ultimi 30 giorni" connectors:

<img src="https://i.ibb.co/7zWxzCk/1.jpg" alt="SubID" title="SubID">

Now configure the URI inside the "Download report actual month" connector:

<img src="https://i.ibb.co/7NgFKMs/2.jpg" alt="downloadreport" title="downloadreport">

Do the same for the "Query -60 -30 giorni precedenti" and "Download report last month" connectors:

<img src="https://i.ibb.co/WF7NmFx/3.jpg" alt="query1" title="query1">
<img src="https://i.ibb.co/M5bCDBR/4.jpg" alt="query2" title="query2">

Please ensure that every query have the authentication configured with the system assigned managed identity:

<img src="https://i.ibb.co/T4Kc6mh/costmanagedidentity.png" alt="costmanagedidentity" title="costmanagedidentity">

Put your api key for OpenAI connection inside the variable "Api-Key":

<img src="https://i.ibb.co/6HfLgZT/5.jpg" alt="api" title="api">

In the example below we have a "Compose" module used for the email preparation. You can edit the contents following your requirement. The URL string in yellow represent the URL of your logo yo use inside the email:

<img src="https://i.ibb.co/N9xdL7v/compose.png" alt="Compose2" title="Compose2">
<img src="https://i.ibb.co/qsWj7Qs/compose-2.png" alt="Compose" title="Compose">

Finished to edit the Compose module the next step is to attach the "Send Email V2" Module after the compose with the Compose output inside:

<img src="https://i.ibb.co/MG4GQJd/email.png" alt="email" title="email">

Please ensure to have enabled Managed Identity for the Logic App with the required permission in order to access to the subscription:

<img src="https://i.ibb.co/ZWP22tq/8.jpg" alt="identity" title="identity">

<h2>DISCLAIMER</h2>

All models listed should be understood as a basic configuration in which the customer can create its own logical application. Please keep in mind that Microsoft can change the function of OpenAI Models, and in this case you need to configure again the interaction with the OpenAI model. Actually models used for this solution are GPT 3 (davinci) and GPT 3.5. Any Customization is responsability of customers.