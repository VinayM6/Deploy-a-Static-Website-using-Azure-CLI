# Deploy-a-Static-Website-using-Azure-CLI
Deploy a Static Website using Azure CLI where all required services are to be created using ARM.
1.	Login into Azure CLI
2.	Use ARM to create:
•	Resource Group
•	storage account - (optional: with static website config in ARM)

3.	Configure storage account with static website config via CLI
4.	Upload a web page file(get something from the internet) to storage account via CLI
5.	Get the Site Public URL via CLI
6.	Access it in browser 
Note static website config:
Mandatory: Cros policy, public access


Solution:
-------------------------------------------
Step 1: Login into Azure CLI
Open terminal or command prompt in the project Folder.

az login

Step 2: Use ARM to create:
•	Resource Group

az group create --name myprojectrg --location eastus
•	storage account - (optional: with static website config in ARM)

az deployment group create --resource-group myprojectrg --
template-file template.json --parameters storageAccountName=myvswsa

Step 3: Configure storage account with static website config via CLI

az storage blob service-properties update --account-name myvswsa --static-website --index-document index.html

Step 4: Upload a web page file(get something from the internet) to storage account via CLI

az storage blob service-properties update --account-name myvswsa --static-website --index-document index.html

Step 5: Get the Site Public URL via CLI

az storage blob list --account-name myvswsa --container-name $web --output table

az deployment group show --resource-group myprojectrg --name template --query "properties.outputs.staticWebsiteUrl.value" --output tsv

Step 6: Access it in browser.

https://myvswsa.z13.web.core.windows.net
