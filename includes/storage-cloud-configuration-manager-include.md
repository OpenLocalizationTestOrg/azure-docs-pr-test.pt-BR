<span data-ttu-id="32c67-101">Olá [biblioteca de Gerenciador de configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fornece uma classe para analisar uma cadeia de caracteres de conexão de um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="32c67-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="32c67-102">Olá [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analisa as definições de configuração, independentemente se o aplicativo de cliente hello está em execução na área de trabalho hello, em um dispositivo móvel, em uma máquina virtual do Azure ou em um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="32c67-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="32c67-103">tooreference Olá CloudConfigurationManager pacote, adicione o seguinte Olá `using` diretiva:</span><span class="sxs-lookup"><span data-stu-id="32c67-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="32c67-104">Aqui está um exemplo que mostra como tooretrieve uma conexão de cadeia de caracteres de um arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="32c67-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="32c67-105">Usar hello Azure Configuration Manager é opcional.</span><span class="sxs-lookup"><span data-stu-id="32c67-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="32c67-106">Você também pode usar uma API como Olá do .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="32c67-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

