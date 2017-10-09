---
title: "aaaTransfer dados com hello biblioteca de movimentação de dados de armazenamento do Microsoft Azure | Microsoft Docs"
description: "Use Olá biblioteca de movimentação de dados toomove ou copiar dados tooor do blob e o arquivo de conteúdo. Copiar dados tooAzure armazenamento de arquivos locais, ou copie dados dentro ou entre contas de armazenamento. Migre facilmente o armazenamento de tooAzure de dados."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 5de902d132565a8eafdc672f7a1a18e1a2db3a06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="8b25a-105">Transferência de dados com hello biblioteca de movimentação de dados de armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8b25a-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="8b25a-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8b25a-106">Overview</span></span>
<span data-ttu-id="8b25a-107">Olá biblioteca de movimentação de dados de armazenamento do Microsoft Azure é uma biblioteca de software livre de plataforma cruzada que foi projetada para carregar, baixar e cópia de Blobs de armazenamento do Azure e arquivos de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="8b25a-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="8b25a-108">Essa biblioteca é de estrutura movimentação de dados de núcleo de saudação que alimenta [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="8b25a-108">This library is hello core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="8b25a-109">Olá biblioteca de movimentação de dados fornece métodos convenientes que não estão disponíveis no nosso tradicional [biblioteca de cliente de armazenamento do Azure .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8b25a-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8b25a-110">Isso inclui Olá capacidade tooset Olá número de operações paralelas, controlar o progresso de transferência, facilmente retomar uma transferência cancelada e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8b25a-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="8b25a-111">Essa biblioteca também usa o .NET Core, que significa que você pode usá-la ao criar aplicativos .NET para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="8b25a-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="8b25a-112">toolearn mais sobre o núcleo do .NET, consulte toohello [documentação .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="8b25a-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="8b25a-113">Essa biblioteca também funciona para aplicativos tradicionais do .NET Framework para Windows.</span><span class="sxs-lookup"><span data-stu-id="8b25a-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="8b25a-114">Este documento demonstra como aplicativo que que é executado no Windows, Linux e macOS e executa os seguintes cenários de saudação do console toocreate um núcleo do .NET:</span><span class="sxs-lookup"><span data-stu-id="8b25a-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="8b25a-115">Carregar tooBlob armazenamento de arquivos e diretórios.</span><span class="sxs-lookup"><span data-stu-id="8b25a-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="8b25a-116">Defina o número de saudação de operações paralelas durante a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="8b25a-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="8b25a-117">Acompanhar o progresso de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="8b25a-117">Track data transfer progress.</span></span>
- <span data-ttu-id="8b25a-118">Retomar a transferência de dados cancelada.</span><span class="sxs-lookup"><span data-stu-id="8b25a-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="8b25a-119">Copie o arquivo de armazenamento de tooBlob de URL.</span><span class="sxs-lookup"><span data-stu-id="8b25a-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="8b25a-120">Copiar do armazenamento de Blob tooBlob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b25a-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="8b25a-121">**O que você precisa:**</span><span class="sxs-lookup"><span data-stu-id="8b25a-121">**What you need:**</span></span>

* [<span data-ttu-id="8b25a-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8b25a-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="8b25a-123">[Uma conta do Armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8b25a-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="8b25a-124">Este guia pressupõe que você já esteja familiarizado com o [Armazenamento do Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="8b25a-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="8b25a-125">Se não, lendo Olá [tooAzure Introdução armazenamento](storage-introduction.md) documentação é útil.</span><span class="sxs-lookup"><span data-stu-id="8b25a-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="8b25a-126">Mais importante, é necessário muito[criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) toostart usando Olá biblioteca de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="8b25a-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="8b25a-127">Configuração</span><span class="sxs-lookup"><span data-stu-id="8b25a-127">Setup</span></span>  

1. <span data-ttu-id="8b25a-128">Visite Olá [guia de instalação do .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8b25a-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="8b25a-129">Ao selecionar o seu ambiente, escolha a opção de linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="8b25a-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="8b25a-130">Na linha de comando hello, crie um diretório para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="8b25a-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="8b25a-131">Navegue nesse diretório, digite `dotnet new` toocreate c# projeto de console.</span><span class="sxs-lookup"><span data-stu-id="8b25a-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="8b25a-132">Abra esse diretório no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8b25a-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="8b25a-133">Esta etapa pode ser feita rapidamente por meio da linha de comando Olá digitando `code .`.</span><span class="sxs-lookup"><span data-stu-id="8b25a-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="8b25a-134">Instalar Olá [c# extensão](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) de saudação Marketplace de código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b25a-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="8b25a-135">Reinicie o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8b25a-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="8b25a-136">Neste ponto, você deve ver dois prompts.</span><span class="sxs-lookup"><span data-stu-id="8b25a-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="8b25a-137">Uma é adicionando "toobuild ativos necessária e debug".</span><span class="sxs-lookup"><span data-stu-id="8b25a-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="8b25a-138">Clique em “sim”.</span><span class="sxs-lookup"><span data-stu-id="8b25a-138">Click "yes."</span></span> <span data-ttu-id="8b25a-139">Outro prompt é para restaurar dependências não resolvidas.</span><span class="sxs-lookup"><span data-stu-id="8b25a-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="8b25a-140">Clique em “restaurar”.</span><span class="sxs-lookup"><span data-stu-id="8b25a-140">Click "restore."</span></span>
6. <span data-ttu-id="8b25a-141">Seu aplicativo agora deve conter um `launch.json` arquivo hello `.vscode` directory.</span><span class="sxs-lookup"><span data-stu-id="8b25a-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="8b25a-142">Nesse arquivo, alterar Olá `externalConsole` valor muito`true`.</span><span class="sxs-lookup"><span data-stu-id="8b25a-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="8b25a-143">Código do Visual Studio permite que aplicativos de .NET Core toodebug.</span><span class="sxs-lookup"><span data-stu-id="8b25a-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="8b25a-144">Acertos `F5` toorun seu aplicativo e verificar se a configuração está funcionando.</span><span class="sxs-lookup"><span data-stu-id="8b25a-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="8b25a-145">Você deve ver o "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="8b25a-145">You should see "Hello World!"</span></span> <span data-ttu-id="8b25a-146">console toohello impresso.</span><span class="sxs-lookup"><span data-stu-id="8b25a-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="8b25a-147">Adicionar projeto de biblioteca de movimentação de dados de tooyour</span><span class="sxs-lookup"><span data-stu-id="8b25a-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="8b25a-148">Adicionar mais recente versão Olá Olá biblioteca de movimentação de dados toohello `dependencies` seção do seu `project.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b25a-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="8b25a-149">No momento da saudação de gravação, esta versão seria`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="8b25a-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="8b25a-150">Adicionar `"portable-net45+win8"` toohello `imports` seção.</span><span class="sxs-lookup"><span data-stu-id="8b25a-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="8b25a-151">Um prompt deve exibir toorestore seu projeto.</span><span class="sxs-lookup"><span data-stu-id="8b25a-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="8b25a-152">Botão hello "restauração".</span><span class="sxs-lookup"><span data-stu-id="8b25a-152">Click hello "restore" button.</span></span> <span data-ttu-id="8b25a-153">Você também pode restaurar seu projeto da linha de comando Olá digitando o comando Olá `dotnet restore` na raiz de saudação do diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="8b25a-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="8b25a-154">Modifique `project.json`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-154">Modify `project.json`:</span></span>

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="8b25a-155">Configurar o esqueleto de saudação do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="8b25a-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="8b25a-156">Olá primeira coisa que fazemos é configurar hello "esqueleto" código de nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b25a-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="8b25a-157">Esse código nos solicitará um nome e a conta chave de conta do armazenamento e usa essas credenciais toocreate um `CloudStorageAccount` objeto.</span><span class="sxs-lookup"><span data-stu-id="8b25a-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="8b25a-158">Esse objeto é usado toointeract com nossa conta de armazenamento em todos os cenários de transferência.</span><span class="sxs-lookup"><span data-stu-id="8b25a-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="8b25a-159">código de saudação também solicita nos toochoose tipo de saudação da operação de transferência, gostaríamos tooexecute.</span><span class="sxs-lookup"><span data-stu-id="8b25a-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="8b25a-160">Modifique `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-160">Modify `Program.cs`:</span></span>

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="8b25a-161">Transferência de arquivo local tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="8b25a-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="8b25a-162">Adicionar métodos Olá `GetSourcePath` e `GetBlob` muito`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

<span data-ttu-id="8b25a-163">Modificar Olá `TransferLocalFileToAzureBlob` método:</span><span class="sxs-lookup"><span data-stu-id="8b25a-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="8b25a-164">Esse código solicita nos Olá caminho tooa local arquivo, o nome de saudação de um contêiner de novo ou existente e o nome de saudação de um novo blob.</span><span class="sxs-lookup"><span data-stu-id="8b25a-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="8b25a-165">Olá `TransferManager.UploadAsync` método executa o carregamento de saudação usando essas informações.</span><span class="sxs-lookup"><span data-stu-id="8b25a-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="8b25a-166">Acertos `F5` toorun seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b25a-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="8b25a-167">Você pode verificar esse carregamento Olá ocorreu exibindo sua conta de armazenamento com hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8b25a-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="8b25a-168">Definir o número de operações paralelas</span><span class="sxs-lookup"><span data-stu-id="8b25a-168">Set number of parallel operations</span></span>
<span data-ttu-id="8b25a-169">Um ótimo recurso oferecido pelo Olá que biblioteca de movimentação de dados é o número de saudação de tooset de capacidade de saudação operações paralelas tooincrease Olá transferência de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="8b25a-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="8b25a-170">Por padrão, a saudação biblioteca de movimentação de dados define o número de Olá de operações paralelas too8 * hello número de núcleos em sua máquina.</span><span class="sxs-lookup"><span data-stu-id="8b25a-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="8b25a-171">Tenha em mente que muitas operações paralelas em um ambiente de baixa largura de banda podem sobrecarregar a conexão de rede hello e evita que as operações de ser totalmente concluída.</span><span class="sxs-lookup"><span data-stu-id="8b25a-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="8b25a-172">Você precisará tooexperiment com esta configuração toodetermine o que funciona melhor com base em sua largura de banda de rede disponível.</span><span class="sxs-lookup"><span data-stu-id="8b25a-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="8b25a-173">Vamos adicionar algum código que nos permite tooset número de saudação de operações paralelas.</span><span class="sxs-lookup"><span data-stu-id="8b25a-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="8b25a-174">Vamos adicionar código que vezes quanto tempo demora para Olá transferência toocomplete também.</span><span class="sxs-lookup"><span data-stu-id="8b25a-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="8b25a-175">Adicionar um `SetNumberOfParallelOperations` método muito`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="8b25a-176">Modificar Olá `ExecuteChoice` método toouse `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

<span data-ttu-id="8b25a-177">Modificar Olá `TransferLocalFileToAzureBlob` método toouse um timer:</span><span class="sxs-lookup"><span data-stu-id="8b25a-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a><span data-ttu-id="8b25a-178">Acompanhar o progresso de transferência</span><span class="sxs-lookup"><span data-stu-id="8b25a-178">Track transfer progress</span></span>
<span data-ttu-id="8b25a-179">É ótimo saber quanto tempo demorou para tootransfer nossos dados.</span><span class="sxs-lookup"><span data-stu-id="8b25a-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="8b25a-180">No entanto, sendo toosee capaz de progresso de saudação da nossa transferência *durante* operação de transferência Olá seria ainda melhor.</span><span class="sxs-lookup"><span data-stu-id="8b25a-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="8b25a-181">tooachieve nesse cenário, é preciso toocreate um `TransferContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="8b25a-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="8b25a-182">Olá `TransferContext` objeto vem em duas formas: `SingleTransferContext` e `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="8b25a-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="8b25a-183">Olá anterior é para transferir um único arquivo (que é o que estamos fazendo agora) e Olá segundo é para transferir um diretório de arquivos (que estamos adicionando mais tarde).</span><span class="sxs-lookup"><span data-stu-id="8b25a-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="8b25a-184">Adicionar métodos Olá `GetSingleTransferContext` e `GetDirectoryTransferContext` muito`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

<span data-ttu-id="8b25a-185">Modificar Olá `TransferLocalFileToAzureBlob` método toouse `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="8b25a-186">Retomar uma transferência cancelada</span><span class="sxs-lookup"><span data-stu-id="8b25a-186">Resume a canceled transfer</span></span>
<span data-ttu-id="8b25a-187">Outro recurso conveniente oferecido pelo Olá biblioteca de movimentação de dados é Olá capacidade tooresume uma transferência cancelada.</span><span class="sxs-lookup"><span data-stu-id="8b25a-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="8b25a-188">Vamos adicionar algum código que nos permite tootemporarily Cancelar Olá transferência digitando `c`e, em seguida, continuar a transferência Olá 3 segundos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="8b25a-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="8b25a-189">Modifique `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="8b25a-190">Até agora, nosso `checkpoint` valor sempre foi definido muito`null`.</span><span class="sxs-lookup"><span data-stu-id="8b25a-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="8b25a-191">Agora, se podemos Cancelar transferência hello, podemos recuperar o último ponto de verificação de saudação do nosso transferência, use este novo ponto de verificação em nosso contexto de transferência.</span><span class="sxs-lookup"><span data-stu-id="8b25a-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="8b25a-192">Diretório de Blob do diretório local tooAzure de transferência</span><span class="sxs-lookup"><span data-stu-id="8b25a-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="8b25a-193">Seria decepcionantes se Olá biblioteca de movimentação de dados só pode transferir um arquivo por vez.</span><span class="sxs-lookup"><span data-stu-id="8b25a-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="8b25a-194">Felizmente, isso não é o caso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b25a-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="8b25a-195">Olá biblioteca de movimentação de dados fornece Olá capacidade tootransfer um diretório de arquivos e todas as suas subpastas.</span><span class="sxs-lookup"><span data-stu-id="8b25a-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="8b25a-196">Vamos adicionar algum código que nos permite toodo exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="8b25a-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="8b25a-197">Primeiro, adicione o método hello `GetBlobDirectory` muito`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

<span data-ttu-id="8b25a-198">Em seguida, modifique `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="8b25a-199">Há algumas diferenças entre este método e o método hello para carregar um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b25a-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="8b25a-200">Agora que estamos usando `TransferManager.UploadDirectoryAsync` e hello `getDirectoryTransferContext` método criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b25a-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="8b25a-201">Além disso, agora, nós fornecemos uma `options` valor operação de carregamento de tooour, que nos permite tooindicate que desejamos subdiretórios tooinclude em nosso carregamento.</span><span class="sxs-lookup"><span data-stu-id="8b25a-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="8b25a-202">Copie o arquivo de URL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="8b25a-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="8b25a-203">Agora, vamos adicionar o código que nos permite toocopy um arquivo de uma URL de tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b25a-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="8b25a-204">Modifique `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="8b25a-205">Um caso de uso importantes para esse recurso é quando você precisa toomove dados de outro tooAzure (por exemplo, AWS) do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8b25a-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="8b25a-206">Como você tem uma URL que fornece acesso toohello recursos, você pode mover facilmente esse recurso em Blobs do Azure usando Olá `TransferManager.CopyAsync` método.</span><span class="sxs-lookup"><span data-stu-id="8b25a-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="8b25a-207">Esse método também introduz um novo parâmetro booliano.</span><span class="sxs-lookup"><span data-stu-id="8b25a-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="8b25a-208">Definir esse parâmetro muito`true` indica que desejamos cópia toodo um assíncrona no lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="8b25a-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="8b25a-209">Definir esse parâmetro muito`false` indica uma cópia síncrona - que significa que recursos Olá é máquina local tooour baixados em primeiro lugar, em seguida, carregados tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="8b25a-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="8b25a-210">No entanto, cópia síncrona está apenas disponível para a cópia de um tooanother de recursos de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b25a-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="8b25a-211">Transferência de BLOBs do Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="8b25a-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="8b25a-212">Outro recurso exclusivamente fornecida pelo Olá biblioteca de movimentação de dados é Olá toocopy de capacidade de um tooanother de recursos de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b25a-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="8b25a-213">Modifique `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="8b25a-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="8b25a-214">Neste exemplo, vamos definir parâmetro booliano Olá `TransferManager.CopyAsync` muito`false` tooindicate que desejamos toodo uma cópia síncrona.</span><span class="sxs-lookup"><span data-stu-id="8b25a-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="8b25a-215">Isso significa que o recurso de saudação for máquina local tooour baixado primeiro, carregado tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="8b25a-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="8b25a-216">opção de cópia síncrona Olá é um tooensure excelente maneira que a operação de cópia tenha uma velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="8b25a-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="8b25a-217">Por outro lado, a velocidade de saudação de uma cópia assíncrona do lado do servidor é dependente de Olá largura de banda disponível no servidor de saudação, que pode flutuar.</span><span class="sxs-lookup"><span data-stu-id="8b25a-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="8b25a-218">No entanto, cópia síncrona pode gerar saída adicional em comparação de custo tooasynchronous cópia.</span><span class="sxs-lookup"><span data-stu-id="8b25a-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="8b25a-219">Olá recomendado abordagem é a cópia síncrona toouse em uma VM do Azure que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.</span><span class="sxs-lookup"><span data-stu-id="8b25a-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8b25a-220">Conclusão</span><span class="sxs-lookup"><span data-stu-id="8b25a-220">Conclusion</span></span>
<span data-ttu-id="8b25a-221">Agora nosso aplicativo de movimentação de dados está concluído.</span><span class="sxs-lookup"><span data-stu-id="8b25a-221">Our data movement application is now complete.</span></span> <span data-ttu-id="8b25a-222">[exemplo de código completo Hello está disponível no GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="8b25a-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8b25a-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b25a-223">Next steps</span></span>
<span data-ttu-id="8b25a-224">Neste guia de introdução, criamos um aplicativo que interage com o Armazenamento do Azure e é executado no Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="8b25a-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="8b25a-225">Este guia de introdução se concentrou no Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="8b25a-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="8b25a-226">No entanto, esse mesmo conhecimento pode ser aplicado tooFile armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b25a-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="8b25a-227">toolearn mais, confira [documentação de referência da biblioteca de movimentação de dados de armazenamento do Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="8b25a-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




