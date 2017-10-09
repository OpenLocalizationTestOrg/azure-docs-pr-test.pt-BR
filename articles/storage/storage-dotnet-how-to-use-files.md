---
title: aaaDevelop para o armazenamento de arquivos do Azure com o .NET | Microsoft Docs
description: "Saiba como toodevelop aplicativos e serviços .NET que usam toostore de armazenamento do Azure arquivo dados de arquivos."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>Desenvolver para o Armazenamento de Arquivos do Azure com o .NET 
> [!NOTE]
> Este artigo mostra como toomanage armazenamento de arquivo do Azure com o código .NET. toolearn mais sobre armazenamento de arquivo do Azure, consulte Olá [tooAzure Introdução armazenamento de arquivo](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial demonstra Noções básicas de saudação do uso de aplicativos do .NET toodevelop ou serviços que usam dados de arquivo de toostore de armazenamento de arquivo do Azure. Neste tutorial, vamos criar um aplicativo de console simples e mostram como ações básicas de tooperform com armazenamento .NET e o arquivo do Azure:

* Obter o conteúdo de saudação de um arquivo
* Definir uma cota de saudação (tamanho máximo) para compartilhamento de arquivo hello.
* Crie uma assinatura de acesso compartilhado (chave SAS) para um arquivo que usa uma política de acesso compartilhado definida no compartilhamento de saudação.
* Copiar um arquivo de tooanother Olá mesma conta de armazenamento.
* Copiar um blob de tooa arquivo hello mesma conta de armazenamento.
* Usar métricas de armazenamento do Azure para solucionar problemas

> [!Note]  
> Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando as classes System.IO padrão Olá para e/s de arquivo. Este artigo descreve como aplicativos toowrite que usam hello Azure Storage SDK do .NET, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Criar aplicativo de console hello e obter assembly hello
No Visual Studio, crie um novo aplicativo de console do Windows. Olá, as etapas a seguir mostra como toocreate um aplicativo de console no Visual Studio de 2017, no entanto, etapas de saudação são semelhantes em outras versões do Visual Studio.

1. Selecione **Arquivo** > **Novo** > **Projeto**
2. Selecione **Instalado** > **Modelos** > **Visual C#** > **Área de trabalho clássica do Windows**
3. Selecione **Aplicativo do Console (.NET Framework)**
4. Insira um nome para seu aplicativo no hello **nome:** campo
5. Selecione **OK**

Todos os exemplos de código neste tutorial podem ser adicionados toohello `Main()` método do seu aplicativo de console `Program.cs` arquivo.

Você pode usar o hello biblioteca de cliente de armazenamento do Azure em qualquer tipo de aplicativo .NET, incluindo um aplicativo de web ou serviço de nuvem do Azure e aplicativos de desktop e mobile. Neste guia, usamos um aplicativo de console para simplificar.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>Usar os pacotes do NuGet tooinstall Olá necessária
Existem dois pacotes, você precisa tooreference em seu projeto toocomplete este tutorial:

* [Biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): Este pacote fornece acesso programático a recursos toodata na sua conta de armazenamento.
* [Biblioteca do Gerenciador de Configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este pacote fornece uma classe para analisar uma cadeia de conexão em um arquivo de configuração, independentemente de onde o aplicativo está sendo executado.

Você pode usar ambos os pacotes do NuGet tooobtain. Siga estas etapas:

1. Clique com o botão direito do mouse no seu projeto no **Gerenciador de Soluções** e escolha **Gerenciar Pacotes NuGet**.
2. Pesquisar online "Windowsazure" e clique em **instalar** tooinstall Olá biblioteca de cliente de armazenamento e suas dependências.
3. Pesquisar online "WindowsAzure.ConfigurationManager" e clique em **instalar** tooinstall hello Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Salve o arquivo App. config do armazenamento conta credenciais toohello
Em seguida, salve suas credenciais no arquivo app.config do projeto. Edite o arquivo App. config de saudação para que parece semelhante toohello do exemplo a seguir, substituindo `myaccount` com seu nome de conta de armazenamento, e `mykey` com sua chave de conta de armazenamento.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> versão mais recente de saudação do emulador de armazenamento do Azure Olá não oferece suporte para armazenamento de arquivo do Azure. A cadeia de conexão deve usar uma conta de armazenamento do Azure no hello nuvem toowork com armazenamento de arquivo do Azure.

## <a name="add-using-directives"></a>Adicionar diretivas using
Olá abrir `Program.cs` arquivo no Gerenciador de soluções e adicione o seguinte hello usando diretivas toohello superior do arquivo hello.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Compartilhamento de arquivo de saudação de acesso programaticamente
Em seguida, adicione Olá toohello de código a seguir `Main()` cadeia de caracteres de conexão do método (após o código de saudação mostrado acima) tooretrieve hello. Esse código é um arquivo de toohello de referência que criamos anteriormente e gera sua janela de console toohello conteúdo.

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

Execute a saída de hello toosee do aplicativo de console hello.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Definir tamanho máximo de saudação para um compartilhamento de arquivos
Começando com a versão 5. x da saudação biblioteca de cliente de armazenamento do Azure, você pode definir conjunto Olá cota (ou o tamanho máximo) para um compartilhamento de arquivo, em gigabytes. Você também pode verificar toosee a quantidade de dados é atualmente armazenado no compartilhamento de saudação.

Pela configuração cota Olá para um compartilhamento, você pode limitar o tamanho total de Olá Olá arquivos armazenados no compartilhamento de saudação. Se excede o tamanho total de saudação de arquivos no compartilhamento de saudação cota Olá definidos no compartilhamento de saudação, os clientes serão tooincrease não é possível Olá tamanho dos arquivos existentes ou criar novos arquivos, a menos que esses arquivos estão vazios.

exemplo Hello abaixo mostra como toocheck Olá uso atual para um compartilhamento e como tooset Olá cota para compartilhamento de saudação.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Gerar uma assinatura de acesso compartilhado para um arquivo ou compartilhamento de arquivos
Começando com a versão 5. x da Olá biblioteca de cliente de armazenamento do Azure, você pode gerar uma assinatura de acesso compartilhado (SAS) para um compartilhamento de arquivos ou para um arquivo individual. Você pode também criar uma política de acesso compartilhado um acesso de toomanage compartilhado de compartilhamento de arquivo assinaturas. Criar uma política de acesso compartilhado é recomendada, pois ele fornece um meio de revogar Olá SAS se ela deve ser comprometida.

saudação de exemplo a seguir cria uma política de acesso compartilhado em um compartilhamento e usa que compartilham tooprovide Olá restrições para uma SAS em um arquivo hello.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

Para saber mais sobre como criar e usar as assinaturas de acesso compartilhado, confira [Como usar SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md) e [Criar e usar uma SAS com os Blobs do Azure](storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Copiar arquivos
Começando com a versão 5. x da Olá biblioteca de cliente de armazenamento do Azure, você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob. Nas seções de Avançar hello, demonstraremos como tooperform esses copiam operações programaticamente.

Você também pode usar AzCopy toocopy um arquivo tooanother ou toocopy um arquivo ou vice-versa de tooa do blob. Consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).

> [!NOTE]
> Se você estiver copiando um arquivo de blob tooa ou um blob de tooa de arquivo, você deve usar um objeto de origem do acesso compartilhado (SAS) de assinatura tooauthenticate hello, mesmo se estiver copiando em Olá mesma conta de armazenamento.
> 
> 

**Copiar um arquivo tooanother** hello exemplo a seguir copia um arquivo tooanother arquivo hello mesmo compartilhamento. Como essa operação de cópia copia entre Olá de arquivos na mesma conta de armazenamento, você pode usar a cópia de saudação de tooperform de autenticação de chave compartilhada.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

**Copiar um blob de tooa arquivo** hello exemplo a seguir cria um arquivo e copiá-lo tooa blob dentro Olá mesma conta de armazenamento. exemplo Hello cria um SAS para o arquivo de origem hello, qual serviço Olá usa o arquivo de origem tooauthenticate acesso toohello durante a operação de cópia de saudação.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

Você pode copiar um arquivo de blob tooa em Olá mesma maneira. Se o objeto de origem de saudação é um blob, em seguida, crie um blob de toothat SAS tooauthenticate acesso durante a operação de cópia de saudação.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Solução de problemas de Armazenamento de Arquivos do Azure usando métricas
A Análise de Armazenamento do Azure agora dá suporte a métricas para o Armazenamento de Arquivos do Azure. Com dados de métricas, você pode rastrear solicitações e diagnosticar problemas.


Você pode habilitar as métricas do Azure para armazenamento de arquivo de saudação [Portal do Azure](https://portal.azure.com). Você também pode habilitar métricas programaticamente por chamada hello operação definir propriedades de serviço de arquivo por meio de saudação API REST, ou uma das suas semelhanças em Olá biblioteca de cliente de armazenamento.


saudação de exemplo de código a seguir mostra como toouse Olá biblioteca de cliente de armazenamento para métricas de tooenable .NET para armazenamento de arquivo do Azure.

Primeiro, adicione o seguinte Olá `using` diretivas tooyour `Program.cs` arquivo, além de toothose adicionadas acima:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Observe que, enquanto Blobs do Azure, tabela do Azure e filas do Azure, use Olá compartilhado `ServiceProperties` tipo no hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, o armazenamento de arquivos do Azure usa seu próprio tipo hello `FileServiceProperties` tipo no hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace. Ambos os namespaces devem ser referenciadas no seu código, no entanto, para Olá toocompile de código a seguir.

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

Além disso, você pode consultar muito[artigo de solução de problemas de armazenamento de arquivo do Azure](storage-troubleshoot-file-connection-problems.md) para obter diretrizes sobre solução de problemas de ponta a ponta.

## <a name="next-steps"></a>Próximas etapas
Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.

### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos conceituais
* [Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Como toouse armazenamento de arquivo do Azure com Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Suporte de ferramentas para o armazenamento de arquivos
* [Usando o PowerShell do Azure com o Armazenamento do Azure](storage-powershell-guide-full.md)
* [Como toouse AzCopy com o armazenamento do Microsoft Azure](storage-use-azcopy.md)
* [Usando Olá CLI do Azure com o armazenamento do Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Solução de problemas do armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Referência
* [Referência à Biblioteca de Cliente de Armazenamento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referência à API REST do serviço de arquivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Postagens no blog
* [O Armazenamento de arquivos do Azure agora está disponível ao público geral](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Por dentro do Armazenamento de Arquivos do Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Apresentando o serviço de arquivo do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [TooMicrosoft de conexões persistentes armazenamento de arquivo do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
