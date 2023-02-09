<h2>Deploy Azure VM and join to legacy Domain</h2>

This template can be used for the deployment of different Azure VMs and join these to AD (Only Windows).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FDevOpsStyle%2FARM_Templates%2Fmain%2Fmain.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<h3>Required Parameters</h3>

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

![alt text](https://ibb.co/rfrHYhY)

After the deploy the IT Administrator can found the Computer Object in the specified OU:

![alt text](https://ibb.co/v38fkMx)
