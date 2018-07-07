# Azure Key Vault - Getting Started in .NET

This sample demonstrates how to get started with Key Vault in .NET
This project allows you to do 
- Create an application in Azure Active Directory
- Create a Service Principal associated with the application 
- Create a Key Vault
- Give permissions to the Service Principal created above to access Key Vault 
- Create a secret in Key Vault
- Read the secret from Key Vault

## Getting Started

### Prerequisites

If you don't have an Azure subscription, please create a **[free account](https://azure.microsoft.com/free/?ref=microsoft.com&amp;utm_source=microsoft.com&amp;utm_medium=docs)** before you begin.
In addition you would need

* [.NET Core](https://www.microsoft.com/net/learn/get-started/windows)
    * Please install .NET Core. This can be run on Windows, Mac and Linux.
* [Git](https://www.git-scm.com/)
    * Please download git from [here](https://git-scm.com/downloads).
* [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
    * For the purpose of this tutorial we would work with Azure CLI which is available on Windows, Mac and Linux

### Quickstart
#### On Windows
- Clone this repo by running this command
   ```
   git clone https://github.com/Azure-Samples/key-vault-dotnet-quickstart.git
   ```
- change directory into this folder by running 
   ```
   cd key-vault-dotnet-quickstart
   ```
- Find the powershell command in this repo (Named Setup.ps1) and run it in administrator mode by running the following command in a powershell window
   ```
   .\Setup.ps1
   ```
   ```
   Please remember the password you give when you run this powershell command
   ```
- Find the certificate named .pfx file in the current folder (The name of the certificate that the powershell command created)
  and install it on your machine (by right clicking on the .pfx file and selecting Install)
  
- Open the repo in any text editor and run the following command with respect to that folder. The commands are listed as below
   ```
    dotnet restore
    dotnet run
   ```
    :+1: You should see that you did all the steps listed [above](https://github.com/Azure-Samples/key-vault-dotnet-quickstart#azure-key-vault---getting-started-in-net)
    
#### On Mac\Linux
- This quickstart requires that you are running the Azure CLI version 2.0.4 or later. To find the version, run `az --version`. If you need to install or upgrade, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).
- First we want to download / clone this [repo](https://github.com/yvprashanth/key-vault-dotnet-quickstart)
- Then cd into dotnetconsole folder
- We then want to set these variables by running the following commands
    - On Windows (Use set)
    - On Mac/Linux (Use export instead of set)
    <br />
    ```
        export SERVICE_PRINCIPAL_NAME="service_principal_name" 
    ```
    <br />
    ```
        export RESOURCE_GROUP_NAME="resource_group_name"
    ```
    <br />
    ```
        export VAULT_NAME="vault_name"
    ```
- This command creates a self signed certificate. It also creates an Application (service principal) in AAD and assigns this self signed certificate as it's key

    ```
    az ad sp create-for-rbac -n $SERVICE_PRINCIPAL_NAME --create-cert > ServicePrincipal.json
    ```
    
    output of the `create-for-rbac` command is in the following format:
    
    ```json
    {
      "appId": "APP_ID",
      "displayName": "ServicePrincipalName",
      "fileWithCertAndPrivateKey" : "PathToYourPrivateKey",
      "name": "http://ServicePrincipalName",
      "password": ...,
      "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
    }
    ```

    > [!NOTE]
    > Please make a copy of the APP_ID from the ServicePrincipal.json file output

    We run the following command to find the thumbprint of the cert that's just created (you can find this from PathToYourPrivateKey shown in the previous result)

    ```
    openssl x509 -in <CERTNAME>.pem -noout -sha1 -fingerprint > CertThumbprint.txt
    ```
    
    The `appId`, `tenant` values are used for authentication. The `displayName` is used when searching for an existing service principal. Please make a copy of the `appId` as you will need it later.
    
    > [!NOTE]
    > If your account does not have sufficient permissions to create a service principal, you see an error message containing "Insufficient privileges to complete the operation." Contact your Azure Active Directory admin to create a service principal.

- Before deploying any resources to your subscription, you must create a resource group that will contain the resources. 

    ```
    az group create --name $RESOURCE_GROUP_NAME --location "East US"
    ```

- [This command creates a Key Vault in the specified Resource Group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/xplat-cli-azure-resource-manager#create-a-resource-group)
(Please replace the VaultName and ResourceGroupName with values you choose).
    ```
    az keyvault create --name $VAULT_NAME --resource-group $RESOURCE_GROUP_NAME --location eastus > KeyVault.json
    ```
    
    To authorize the above created application to read secrets in your vault, run the following:
    
    ```
    az keyvault set-policy --name $VAULT_NAME --spn APP_ID --secret-permissions get
    ```

- Once done, with above commands clone this [repo](https://github.com/yvprashanth/key-vault-dotnet-quickstart) by running the following command
    ```
    git clone https://github.com/yvprashanth/key-vault-dotnet-quickstart.git
    ```

    Then cd into that folder and run dotnet run

    ```
    dotnet run
    ```
:+1: You should see that you did all the steps listed [above](https://github.com/Azure-Samples/key-vault-dotnet-quickstart#azure-key-vault---getting-started-in-net)

## Resources

(Any additional resources or related projects)

- [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/)
- [Azure Key Vault Documentation](https://docs.microsoft.com/en-us/azure/key-vault/)
- [Azure SDK For .NET](https://github.com/Azure/azure-sdk-for-net)
- [Azure REST API Reference](https://docs.microsoft.com/en-us/rest/api/keyvault/?redirectedfrom=AzureSamples)
