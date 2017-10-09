Olá [biblioteca de Gerenciador de configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fornece uma classe para analisar uma cadeia de caracteres de conexão de um arquivo de configuração. Olá [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analisa as definições de configuração, independentemente se o aplicativo de cliente hello está em execução na área de trabalho hello, em um dispositivo móvel, em uma máquina virtual do Azure ou em um serviço de nuvem do Azure.

tooreference Olá CloudConfigurationManager pacote, adicione o seguinte Olá `using` diretiva:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Aqui está um exemplo que mostra como tooretrieve uma conexão de cadeia de caracteres de um arquivo de configuração:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

Usar hello Azure Configuration Manager é opcional. Você também pode usar uma API como Olá do .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.

