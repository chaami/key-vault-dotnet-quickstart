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
- Find the powershell command in this repo (Named Setup.ps1) and run it in administrator mode
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

## Resources

(Any additional resources or related projects)

- [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/)
- [Azure Key Vault Documentation](https://docs.microsoft.com/en-us/azure/key-vault/)
- [Azure SDK For .NET](https://github.com/Azure/azure-sdk-for-net)
- [Azure REST API Reference](https://docs.microsoft.com/en-us/rest/api/keyvault/?redirectedfrom=AzureSamples)
