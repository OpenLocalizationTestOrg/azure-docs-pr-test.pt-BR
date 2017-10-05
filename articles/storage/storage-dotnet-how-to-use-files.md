---
title: Desenvolver para o Armazenamento de Arquivos do Azure com o .NET | Microsoft Docs
description: "Saiba como desenvolver aplicativos e serviços .NET que usem o Armazenamento de Arquivos do Azure para armazenar dados de arquivo."
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
ms.openlocfilehash: e26da88ef1803d47d7286c5ae836ac9c041dadd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="b345b-103">Desenvolver para o Armazenamento de Arquivos do Azure com o .NET</span><span class="sxs-lookup"><span data-stu-id="b345b-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="b345b-104">Este artigo mostra como gerenciar o Armazenamento de Arquivos do Azure com o código .NET.</span><span class="sxs-lookup"><span data-stu-id="b345b-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="b345b-105">Para saber mais sobre o Armazenamento de Arquivos do Azure, veja a [Introdução ao Armazenamento de Arquivos do Azure](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b345b-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="b345b-106">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="b345b-106">About this tutorial</span></span>
<span data-ttu-id="b345b-107">Este tutorial demonstrará as noções básicas de uso do .NET para desenvolver aplicativos ou serviços que usam o Armazenamento de Arquivos do Azure para armazenar dados de arquivo.</span><span class="sxs-lookup"><span data-stu-id="b345b-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="b345b-108">Neste tutorial, criaremos um aplicativo de console simples e mostraremos como executar ações básicas com .NET e o Armazenamento de Arquivos do Azure:</span><span class="sxs-lookup"><span data-stu-id="b345b-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="b345b-109">Obter o conteúdo de um arquivo</span><span class="sxs-lookup"><span data-stu-id="b345b-109">Get the contents of a file</span></span>
* <span data-ttu-id="b345b-110">Defina a cota (tamanho máximo) para o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b345b-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="b345b-111">Crie uma assinatura de acesso compartilhado (chave SAS) para um arquivo que usa uma política de acesso compartilhado definida no compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="b345b-112">Copie um arquivo em outro arquivo na mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="b345b-113">Copie um arquivo em um blob na mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="b345b-114">Usar métricas de armazenamento do Azure para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b345b-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="b345b-115">Como o Armazenamento de Arquivos do Azure pode ser acessado via SMB, é possível escrever aplicativos simples que acessem o compartilhamento de arquivo do Azure usando as classes System.IO padrão para E/S de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="b345b-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="b345b-116">Este artigo descreverá como escrever aplicativos que usam o SDK do .NET do Armazenamento do Azure, que usa a [API REST do Armazenamento de Arquivos do Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) para conversar com o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b345b-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="b345b-117">Criar o aplicativo do console e obter o assembly</span><span class="sxs-lookup"><span data-stu-id="b345b-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="b345b-118">No Visual Studio, crie um novo aplicativo de console do Windows.</span><span class="sxs-lookup"><span data-stu-id="b345b-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="b345b-119">As etapas a seguir mostram como criar um aplicativo de console no Visual Studio 2017. No entanto, as etapas são semelhantes em outras versões do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b345b-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="b345b-120">Selecione **Arquivo** > **Novo** > **Projeto**</span><span class="sxs-lookup"><span data-stu-id="b345b-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="b345b-121">Selecione **Instalado** > **Modelos** > **Visual C#** > **Área de trabalho clássica do Windows**</span><span class="sxs-lookup"><span data-stu-id="b345b-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="b345b-122">Selecione **Aplicativo do Console (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="b345b-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="b345b-123">Insira um nome para seu aplicativo no campo **Nome:**</span><span class="sxs-lookup"><span data-stu-id="b345b-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="b345b-124">Selecione **OK**</span><span class="sxs-lookup"><span data-stu-id="b345b-124">Select **OK**</span></span>

<span data-ttu-id="b345b-125">Todos os exemplos de código neste tutorial podem ser adicionados ao método `Main()` no arquivo`Program.cs` do aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="b345b-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="b345b-126">Você pode usar a Biblioteca de Cliente da Armazenamento do Azure em qualquer tipo de aplicativo .NET, incluindo um serviço de nuvem do Azure, um aplicativo Web do Azure e aplicativos da área de trabalho ou móvel.</span><span class="sxs-lookup"><span data-stu-id="b345b-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="b345b-127">Neste guia, usamos um aplicativo de console para simplificar.</span><span class="sxs-lookup"><span data-stu-id="b345b-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="b345b-128">Use o NuGet para instalar os pacotes necessários</span><span class="sxs-lookup"><span data-stu-id="b345b-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="b345b-129">Há dois pacotes que você precisará referenciar em seu projeto para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="b345b-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="b345b-130">[Biblioteca de Cliente de Armazenamento do Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): este pacote fornece acesso programático aos recursos de dados em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="b345b-131">[Biblioteca do Gerenciador de Configuração do Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este pacote fornece uma classe para analisar uma cadeia de conexão em um arquivo de configuração, independentemente de onde o aplicativo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="b345b-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="b345b-132">Você pode usar NuGet para obter os dois pacotes.</span><span class="sxs-lookup"><span data-stu-id="b345b-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="b345b-133">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="b345b-133">Follow these steps:</span></span>

1. <span data-ttu-id="b345b-134">Clique com o botão direito do mouse no seu projeto no **Gerenciador de Soluções** e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b345b-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b345b-135">Pesquise online por "Windowsazure.Storage" e clique em **Instalar** para instalar a Biblioteca de Cliente de Armazenamento e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="b345b-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="b345b-136">Pesquise online por "WindowsAzure.ConfigurationManager" e clique em **Instalar** para instalar o Gerenciador de Configuração do Azure.</span><span class="sxs-lookup"><span data-stu-id="b345b-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="b345b-137">Salvar suas credenciais da conta de armazenamento no arquivo app.config</span><span class="sxs-lookup"><span data-stu-id="b345b-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="b345b-138">Em seguida, salve suas credenciais no arquivo app.config do projeto.</span><span class="sxs-lookup"><span data-stu-id="b345b-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="b345b-139">Edite o arquivo app.config para que ele se pareça com o exemplo a seguir, substituindo `myaccount` pelo nome da conta de armazenamento e `mykey` pela chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> A versão mais recente do emulador de armazenamento do Azure não dá suporte ao Armazenamento de Arquivos do Azure. <span data-ttu-id="b345b-141">Sua cadeia de conexão deve ter como destino uma Conta de Armazenamento do Azure na nuvem para funcionar com o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b345b-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="b345b-142">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="b345b-142">Add using directives</span></span>
<span data-ttu-id="b345b-143">Abra o arquivo `Program.cs` no Gerenciador de Soluções e adicione as diretivas using a seguir à parte superior do arquivo.</span><span class="sxs-lookup"><span data-stu-id="b345b-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="b345b-144">Acessar o compartilhamento de arquivos programaticamente</span><span class="sxs-lookup"><span data-stu-id="b345b-144">Access the file share programmatically</span></span>
<span data-ttu-id="b345b-145">Em seguida, adicione o código a seguir ao método `Main()` (após o código mostrado acima) para recuperar a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="b345b-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="b345b-146">Esse código obtém uma referência para o arquivo que criamos anteriormente e exporta seu conteúdo para a janela do console.</span><span class="sxs-lookup"><span data-stu-id="b345b-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="b345b-147">Execute o aplicativo de console para ver a saída.</span><span class="sxs-lookup"><span data-stu-id="b345b-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="b345b-148">Definir o tamanho máximo de um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="b345b-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="b345b-149">A partir da versão 5.x da Biblioteca de Cliente do Armazenamento do Azure, você pode definir a cota (ou tamanho máximo) de um compartilhamento de arquivos, em gigabytes.</span><span class="sxs-lookup"><span data-stu-id="b345b-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="b345b-150">Você também pode verificar a quantidade de dados atualmente armazenada no compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="b345b-151">Ao definir a cota para um compartilhamento, você pode limitar o tamanho total dos arquivos armazenados no compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="b345b-152">Se o tamanho total dos arquivos no compartilhamento ultrapassar a cota definida no compartilhamento, os clientes não poderão aumentar o tamanho dos arquivos existentes ou criar novos arquivos, a menos que eles estejam vazios.</span><span class="sxs-lookup"><span data-stu-id="b345b-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="b345b-153">O exemplo a seguir mostra como verificar o uso atual de um compartilhamento e como definir a cota para o compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="b345b-154">Gerar uma assinatura de acesso compartilhado para um arquivo ou compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="b345b-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="b345b-155">A partir da versão 5.x da Biblioteca de Cliente do Armazenamento do Azure, você pode gerar uma SAS (assinatura de acesso compartilhado) para um compartilhamento de arquivos ou para um arquivo individual.</span><span class="sxs-lookup"><span data-stu-id="b345b-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="b345b-156">Você também pode criar uma política de acesso compartilhado em um compartilhamento de arquivos para gerenciar assinaturas de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="b345b-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="b345b-157">Recomendamos a criação de uma política de acesso compartilhado, pois ela fornece um meio de revogar o SAS se ele for comprometido.</span><span class="sxs-lookup"><span data-stu-id="b345b-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="b345b-158">O exemplo a seguir cria uma política de acesso compartilhado em um compartilhamento e, em seguida, usa essa política para fornecer as restrições a um SAS em um arquivo no compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="b345b-159">Para saber mais sobre como criar e usar as assinaturas de acesso compartilhado, confira [Como usar SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md) e [Criar e usar uma SAS com os Blobs do Azure](storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="b345b-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="b345b-160">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="b345b-160">Copy files</span></span>
<span data-ttu-id="b345b-161">A partir da versão 5.x da Biblioteca de Cliente do Armazenamento do Azure, você pode copiar um arquivo em outro arquivo, um arquivo em um blob ou um blob em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="b345b-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="b345b-162">Nas próximas seções, demonstramos como executar essas operações de cópia de modo programático.</span><span class="sxs-lookup"><span data-stu-id="b345b-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="b345b-163">Você também pode usar o AzCopy para copiar um arquivo para outro, ou para copiar um blob em um arquivo ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="b345b-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="b345b-164">Veja [Transferir dados com o Utilitário da Linha de Comando AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b345b-164">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b345b-165">Se você estiver copiando um blob em um arquivo, ou um arquivo em um blob, use uma assinatura de acesso compartilhado (SAS) para autenticar o objeto de origem, mesmo se você estiver copiando dentro da mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="b345b-166">**Copiar um arquivo para outro arquivo** O exemplo a seguir copia um arquivo em outro arquivo no mesmo compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="b345b-167">Como essa operação de cópia realiza a cópia entre arquivos na mesma conta de armazenamento, você pode usar a autenticação de Chave compartilhada para executar a cópia.</span><span class="sxs-lookup"><span data-stu-id="b345b-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="b345b-168">**Copiar um arquivo para um blob** O exemplo a seguir cria um arquivo e o copia em um blob dentro da mesma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="b345b-169">O exemplo cria uma SAS para o arquivo de origem, que o serviço usa para autenticar o acesso ao arquivo de origem durante a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="b345b-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="b345b-170">Você pode copiar um blob em um arquivo da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="b345b-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="b345b-171">Se o objeto de origem for um blob, crie uma SAS para autenticar o acesso ao blob durante a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="b345b-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="b345b-172">Solução de problemas de Armazenamento de Arquivos do Azure usando métricas</span><span class="sxs-lookup"><span data-stu-id="b345b-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="b345b-173">A Análise de Armazenamento do Azure agora dá suporte a métricas para o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b345b-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="b345b-174">Com dados de métricas, você pode rastrear solicitações e diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="b345b-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="b345b-175">É possível habilitar métricas para o Armazenamento de Arquivos do Azure por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b345b-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="b345b-176">Você também pode habilitar métricas programaticamente ao chamar a operação Definir Propriedades de Serviço do Arquivo pela API REST ou uma operação semelhante na biblioteca de cliente de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b345b-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="b345b-177">O exemplo de código a seguir mostra como usar a Biblioteca de Cliente de Armazenamento para .NET para habilitar as métricas para o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b345b-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="b345b-178">Primeiro, adicione as seguintes diretivas `using` ao arquivo `Program.cs` além daquelas adicionadas acima:</span><span class="sxs-lookup"><span data-stu-id="b345b-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="b345b-179">Observe que, enquanto os Blobs do Azure, a Tabela do Azure e as Filas do Azure usam o tipo `ServiceProperties` compartilhado no namespace `Microsoft.WindowsAzure.Storage.Shared.Protocol`, o Armazenamento de Arquivos do Azure usa seu próprio tipo, o `FileServiceProperties`, no namespace `Microsoft.WindowsAzure.Storage.File.Protocol`.</span><span class="sxs-lookup"><span data-stu-id="b345b-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="b345b-180">Os namespaces devem ser referenciados no seu código, no entanto, para que o código a seguir seja compilado.</span><span class="sxs-lookup"><span data-stu-id="b345b-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read the metrics properties we just set.
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

<span data-ttu-id="b345b-181">Além disso, você pode consultar o [artigo Solução de problemas do Armazenamento de Arquivos do Azure](storage-troubleshoot-file-connection-problems.md) para obter diretrizes completas de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="b345b-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b345b-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b345b-182">Next steps</span></span>
<span data-ttu-id="b345b-183">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="b345b-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="b345b-184">Artigos e vídeos conceituais</span><span class="sxs-lookup"><span data-stu-id="b345b-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="b345b-185">Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="b345b-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="b345b-186">Como utilizar o Armazenamento de Arquivos do Azure com Linux</span><span class="sxs-lookup"><span data-stu-id="b345b-186">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="b345b-187">Suporte de ferramentas para o armazenamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="b345b-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="b345b-188">Usando o PowerShell do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b345b-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="b345b-189">Como usar o AzCopy com o Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b345b-189">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="b345b-190">Usando a CLI do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b345b-190">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="b345b-191">Solução de problemas do armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="b345b-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="b345b-192">Referência</span><span class="sxs-lookup"><span data-stu-id="b345b-192">Reference</span></span>
* [<span data-ttu-id="b345b-193">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="b345b-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="b345b-194">Referência à API REST do serviço de arquivos</span><span class="sxs-lookup"><span data-stu-id="b345b-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="b345b-195">Postagens no blog</span><span class="sxs-lookup"><span data-stu-id="b345b-195">Blog posts</span></span>
* [<span data-ttu-id="b345b-196">O Armazenamento de arquivos do Azure agora está disponível ao público geral</span><span class="sxs-lookup"><span data-stu-id="b345b-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="b345b-197">Por dentro do Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="b345b-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="b345b-198">Apresentando o serviço de arquivo do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b345b-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="b345b-199">Conexões persistentes para o Armazenamento de Arquivos do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b345b-199">Persisting connections to Microsoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)