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
ms.openlocfilehash: 79855f178111483edea13014b8eeecc3376dd4e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="ea55f-103">Desenvolver para o Armazenamento de Arquivos do Azure com o .NET</span><span class="sxs-lookup"><span data-stu-id="ea55f-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="ea55f-104">Este artigo mostra como toomanage armazenamento de arquivo do Azure com o código .NET.</span><span class="sxs-lookup"><span data-stu-id="ea55f-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="ea55f-105">toolearn mais sobre armazenamento de arquivo do Azure, consulte Olá [tooAzure Introdução armazenamento de arquivo](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea55f-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="ea55f-106">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="ea55f-106">About this tutorial</span></span>
<span data-ttu-id="ea55f-107">Este tutorial demonstra Noções básicas de saudação do uso de aplicativos do .NET toodevelop ou serviços que usam dados de arquivo de toostore de armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea55f-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="ea55f-108">Neste tutorial, vamos criar um aplicativo de console simples e mostram como ações básicas de tooperform com armazenamento .NET e o arquivo do Azure:</span><span class="sxs-lookup"><span data-stu-id="ea55f-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="ea55f-109">Obter o conteúdo de saudação de um arquivo</span><span class="sxs-lookup"><span data-stu-id="ea55f-109">Get hello contents of a file</span></span>
* <span data-ttu-id="ea55f-110">Definir uma cota de saudação (tamanho máximo) para compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="ea55f-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="ea55f-111">Crie uma assinatura de acesso compartilhado (chave SAS) para um arquivo que usa uma política de acesso compartilhado definida no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea55f-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="ea55f-112">Copiar um arquivo de tooanother Olá mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="ea55f-113">Copiar um blob de tooa arquivo hello mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="ea55f-114">Usar métricas de armazenamento do Azure para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ea55f-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="ea55f-115">Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando as classes System.IO padrão Olá para e/s de arquivo.</span><span class="sxs-lookup"><span data-stu-id="ea55f-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="ea55f-116">Este artigo descreve como aplicativos toowrite que usam hello Azure Storage SDK do .NET, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ea55f-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="ea55f-117">Criar aplicativo de console hello e obter assembly hello</span><span class="sxs-lookup"><span data-stu-id="ea55f-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="ea55f-118">No Visual Studio, crie um novo aplicativo de console do Windows.</span><span class="sxs-lookup"><span data-stu-id="ea55f-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="ea55f-119">Olá, as etapas a seguir mostra como toocreate um aplicativo de console no Visual Studio de 2017, no entanto, etapas de saudação são semelhantes em outras versões do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea55f-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="ea55f-120">Selecione **Arquivo** > **Novo** > **Projeto**</span><span class="sxs-lookup"><span data-stu-id="ea55f-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="ea55f-121">Selecione **Instalado** > **Modelos** > **Visual C#** > **Área de trabalho clássica do Windows**</span><span class="sxs-lookup"><span data-stu-id="ea55f-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="ea55f-122">Selecione **Aplicativo do Console (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="ea55f-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="ea55f-123">Insira um nome para seu aplicativo no hello **nome:** campo</span><span class="sxs-lookup"><span data-stu-id="ea55f-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="ea55f-124">Selecione **OK**</span><span class="sxs-lookup"><span data-stu-id="ea55f-124">Select **OK**</span></span>

<span data-ttu-id="ea55f-125">Todos os exemplos de código neste tutorial podem ser adicionados toohello `Main()` método do seu aplicativo de console `Program.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ea55f-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="ea55f-126">Você pode usar o hello biblioteca de cliente de armazenamento do Azure em qualquer tipo de aplicativo .NET, incluindo um aplicativo de web ou serviço de nuvem do Azure e aplicativos de desktop e mobile.</span><span class="sxs-lookup"><span data-stu-id="ea55f-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="ea55f-127">Neste guia, usamos um aplicativo de console para simplificar.</span><span class="sxs-lookup"><span data-stu-id="ea55f-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="ea55f-128">Usar os pacotes do NuGet tooinstall Olá necessária</span><span class="sxs-lookup"><span data-stu-id="ea55f-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="ea55f-129">Existem dois pacotes, você precisa tooreference em seu projeto toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="ea55f-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="ea55f-130">[Biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): Este pacote fornece acesso programático a recursos toodata na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="ea55f-131">[Biblioteca do Gerenciador de Configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este pacote fornece uma classe para analisar uma cadeia de conexão em um arquivo de configuração, independentemente de onde o aplicativo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="ea55f-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="ea55f-132">Você pode usar ambos os pacotes do NuGet tooobtain.</span><span class="sxs-lookup"><span data-stu-id="ea55f-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="ea55f-133">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ea55f-133">Follow these steps:</span></span>

1. <span data-ttu-id="ea55f-134">Clique com o botão direito do mouse no seu projeto no **Gerenciador de Soluções** e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ea55f-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ea55f-135">Pesquisar online "Windowsazure" e clique em **instalar** tooinstall Olá biblioteca de cliente de armazenamento e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="ea55f-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="ea55f-136">Pesquisar online "WindowsAzure.ConfigurationManager" e clique em **instalar** tooinstall hello Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="ea55f-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="ea55f-137">Salve o arquivo App. config do armazenamento conta credenciais toohello</span><span class="sxs-lookup"><span data-stu-id="ea55f-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="ea55f-138">Em seguida, salve suas credenciais no arquivo app.config do projeto.</span><span class="sxs-lookup"><span data-stu-id="ea55f-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="ea55f-139">Edite o arquivo App. config de saudação para que parece semelhante toohello do exemplo a seguir, substituindo `myaccount` com seu nome de conta de armazenamento, e `mykey` com sua chave de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> versão mais recente de saudação do emulador de armazenamento do Azure Olá não oferece suporte para armazenamento de arquivo do Azure. <span data-ttu-id="ea55f-141">A cadeia de conexão deve usar uma conta de armazenamento do Azure no hello nuvem toowork com armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea55f-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="ea55f-142">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="ea55f-142">Add using directives</span></span>
<span data-ttu-id="ea55f-143">Olá abrir `Program.cs` arquivo no Gerenciador de soluções e adicione o seguinte hello usando diretivas toohello superior do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="ea55f-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="ea55f-144">Compartilhamento de arquivo de saudação de acesso programaticamente</span><span class="sxs-lookup"><span data-stu-id="ea55f-144">Access hello file share programmatically</span></span>
<span data-ttu-id="ea55f-145">Em seguida, adicione Olá toohello de código a seguir `Main()` cadeia de caracteres de conexão do método (após o código de saudação mostrado acima) tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="ea55f-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="ea55f-146">Esse código é um arquivo de toohello de referência que criamos anteriormente e gera sua janela de console toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ea55f-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

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

<span data-ttu-id="ea55f-147">Execute a saída de hello toosee do aplicativo de console hello.</span><span class="sxs-lookup"><span data-stu-id="ea55f-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="ea55f-148">Definir tamanho máximo de saudação para um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="ea55f-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="ea55f-149">Começando com a versão 5. x da saudação biblioteca de cliente de armazenamento do Azure, você pode definir conjunto Olá cota (ou o tamanho máximo) para um compartilhamento de arquivo, em gigabytes.</span><span class="sxs-lookup"><span data-stu-id="ea55f-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="ea55f-150">Você também pode verificar toosee a quantidade de dados é atualmente armazenado no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea55f-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="ea55f-151">Pela configuração cota Olá para um compartilhamento, você pode limitar o tamanho total de Olá Olá arquivos armazenados no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea55f-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="ea55f-152">Se excede o tamanho total de saudação de arquivos no compartilhamento de saudação cota Olá definidos no compartilhamento de saudação, os clientes serão tooincrease não é possível Olá tamanho dos arquivos existentes ou criar novos arquivos, a menos que esses arquivos estão vazios.</span><span class="sxs-lookup"><span data-stu-id="ea55f-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="ea55f-153">exemplo Hello abaixo mostra como toocheck Olá uso atual para um compartilhamento e como tooset Olá cota para compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea55f-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="ea55f-154">Gerar uma assinatura de acesso compartilhado para um arquivo ou compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="ea55f-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="ea55f-155">Começando com a versão 5. x da Olá biblioteca de cliente de armazenamento do Azure, você pode gerar uma assinatura de acesso compartilhado (SAS) para um compartilhamento de arquivos ou para um arquivo individual.</span><span class="sxs-lookup"><span data-stu-id="ea55f-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="ea55f-156">Você pode também criar uma política de acesso compartilhado um acesso de toomanage compartilhado de compartilhamento de arquivo assinaturas.</span><span class="sxs-lookup"><span data-stu-id="ea55f-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="ea55f-157">Criar uma política de acesso compartilhado é recomendada, pois ele fornece um meio de revogar Olá SAS se ela deve ser comprometida.</span><span class="sxs-lookup"><span data-stu-id="ea55f-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="ea55f-158">saudação de exemplo a seguir cria uma política de acesso compartilhado em um compartilhamento e usa que compartilham tooprovide Olá restrições para uma SAS em um arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="ea55f-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

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

<span data-ttu-id="ea55f-159">Para saber mais sobre como criar e usar as assinaturas de acesso compartilhado, confira [Como usar SAS (Assinaturas de Acesso Compartilhado)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) e [Criar e usar uma SAS com os Blobs do Azure](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="ea55f-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="ea55f-160">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="ea55f-160">Copy files</span></span>
<span data-ttu-id="ea55f-161">Começando com a versão 5. x da Olá biblioteca de cliente de armazenamento do Azure, você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="ea55f-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="ea55f-162">Nas seções de Avançar hello, demonstraremos como tooperform esses copiam operações programaticamente.</span><span class="sxs-lookup"><span data-stu-id="ea55f-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="ea55f-163">Você também pode usar AzCopy toocopy um arquivo tooanother ou toocopy um arquivo ou vice-versa de tooa do blob.</span><span class="sxs-lookup"><span data-stu-id="ea55f-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="ea55f-164">Consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea55f-164">See [Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="ea55f-165">Se você estiver copiando um arquivo de blob tooa ou um blob de tooa de arquivo, você deve usar um objeto de origem do acesso compartilhado (SAS) de assinatura tooauthenticate hello, mesmo se estiver copiando em Olá mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="ea55f-166">**Copiar um arquivo tooanother** hello exemplo a seguir copia um arquivo tooanother arquivo hello mesmo compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="ea55f-167">Como essa operação de cópia copia entre Olá de arquivos na mesma conta de armazenamento, você pode usar a cópia de saudação de tooperform de autenticação de chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="ea55f-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

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

<span data-ttu-id="ea55f-168">**Copiar um blob de tooa arquivo** hello exemplo a seguir cria um arquivo e copiá-lo tooa blob dentro Olá mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="ea55f-169">exemplo Hello cria um SAS para o arquivo de origem hello, qual serviço Olá usa o arquivo de origem tooauthenticate acesso toohello durante a operação de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea55f-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

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

<span data-ttu-id="ea55f-170">Você pode copiar um arquivo de blob tooa em Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="ea55f-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="ea55f-171">Se o objeto de origem de saudação é um blob, em seguida, crie um blob de toothat SAS tooauthenticate acesso durante a operação de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ea55f-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="ea55f-172">Solução de problemas de Armazenamento de Arquivos do Azure usando métricas</span><span class="sxs-lookup"><span data-stu-id="ea55f-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="ea55f-173">A Análise de Armazenamento do Azure agora dá suporte a métricas para o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea55f-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="ea55f-174">Com dados de métricas, você pode rastrear solicitações e diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="ea55f-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="ea55f-175">Você pode habilitar as métricas do Azure para armazenamento de arquivo de saudação [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea55f-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="ea55f-176">Você também pode habilitar métricas programaticamente por chamada hello operação definir propriedades de serviço de arquivo por meio de saudação API REST, ou uma das suas semelhanças em Olá biblioteca de cliente de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ea55f-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="ea55f-177">saudação de exemplo de código a seguir mostra como toouse Olá biblioteca de cliente de armazenamento para métricas de tooenable .NET para armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea55f-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="ea55f-178">Primeiro, adicione o seguinte Olá `using` diretivas tooyour `Program.cs` arquivo, além de toothose adicionadas acima:</span><span class="sxs-lookup"><span data-stu-id="ea55f-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="ea55f-179">Observe que, enquanto Blobs do Azure, tabela do Azure e filas do Azure, use Olá compartilhado `ServiceProperties` tipo no hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, o armazenamento de arquivos do Azure usa seu próprio tipo hello `FileServiceProperties` tipo no hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span><span class="sxs-lookup"><span data-stu-id="ea55f-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="ea55f-180">Ambos os namespaces devem ser referenciadas no seu código, no entanto, para Olá toocompile de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ea55f-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

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

<span data-ttu-id="ea55f-181">Além disso, você pode consultar muito[artigo de solução de problemas de armazenamento de arquivo do Azure](storage-troubleshoot-windows-file-connection-problems.md) para obter diretrizes sobre solução de problemas de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="ea55f-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea55f-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea55f-182">Next steps</span></span>
<span data-ttu-id="ea55f-183">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea55f-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="ea55f-184">Artigos e vídeos conceituais</span><span class="sxs-lookup"><span data-stu-id="ea55f-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="ea55f-185">Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="ea55f-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="ea55f-186">Como toouse armazenamento de arquivo do Azure com Linux</span><span class="sxs-lookup"><span data-stu-id="ea55f-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="ea55f-187">Suporte de ferramentas para o armazenamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="ea55f-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="ea55f-188">Como toouse AzCopy com o armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ea55f-188">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="ea55f-189">Usando Olá CLI do Azure com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ea55f-189">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="ea55f-190">Solução de problemas do armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea55f-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="ea55f-191">Referência</span><span class="sxs-lookup"><span data-stu-id="ea55f-191">Reference</span></span>
* [<span data-ttu-id="ea55f-192">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="ea55f-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="ea55f-193">Referência à API REST do serviço de arquivos</span><span class="sxs-lookup"><span data-stu-id="ea55f-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="ea55f-194">Postagens no blog</span><span class="sxs-lookup"><span data-stu-id="ea55f-194">Blog posts</span></span>
* [<span data-ttu-id="ea55f-195">O Armazenamento de arquivos do Azure agora está disponível ao público geral</span><span class="sxs-lookup"><span data-stu-id="ea55f-195">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="ea55f-196">Por dentro do Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea55f-196">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="ea55f-197">Apresentando o serviço de arquivo do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ea55f-197">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="ea55f-198">TooMicrosoft de conexões persistentes armazenamento de arquivo do Azure</span><span class="sxs-lookup"><span data-stu-id="ea55f-198">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
