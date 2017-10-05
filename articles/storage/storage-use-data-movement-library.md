---
title: "Transferir dados com a Biblioteca de Movimentação de Dados do Armazenamento do Microsoft Azure | Microsoft Docs"
description: "Use a Biblioteca de Movimentação de Dados para mover ou copiar dados de ou para o conteúdo de blob e arquivo. Copie dados para o Armazenamento do Azure de arquivos locais ou copie dados dentro na mesma conta ou entre contas de armazenamento. Migre facilmente seus dados para o Armazenamento do Azure."
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
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="d5b29-105">Transferir dados com a Biblioteca de Movimentação de Dados do Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d5b29-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="d5b29-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d5b29-106">Overview</span></span>
<span data-ttu-id="d5b29-107">A Biblioteca de Movimentação de Dados do Armazenamento do Microsoft Azure é uma biblioteca de software livre entre plataformas que foi projetada para o upload, download e cópia de alto desempenho de arquivos e blobs do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b29-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="d5b29-108">Essa biblioteca é a estrutura de movimentação de dados principal que capacita o [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="d5b29-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="d5b29-109">A Biblioteca de Movimentação de Dados fornece métodos convenientes que não estão disponíveis em nossa [Biblioteca do Cliente do Armazenamento do Azure para .NET](storage-dotnet-how-to-use-blobs.md) tradicional.</span><span class="sxs-lookup"><span data-stu-id="d5b29-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d5b29-110">Isso inclui a capacidade de definir o número de operações paralelas, acompanhar o progresso de transferência, facilmente retomar uma transferência cancelada e muito mais.</span><span class="sxs-lookup"><span data-stu-id="d5b29-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="d5b29-111">Essa biblioteca também usa o .NET Core, que significa que você pode usá-la ao criar aplicativos .NET para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="d5b29-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="d5b29-112">Para saber mais sobre o .NET Core, consulte a [documentação do .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="d5b29-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="d5b29-113">Essa biblioteca também funciona para aplicativos tradicionais do .NET Framework para Windows.</span><span class="sxs-lookup"><span data-stu-id="d5b29-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="d5b29-114">Este documento demonstra como criar um aplicativo de console .NET Core que é executado no Windows, Linux e macOS e executa os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="d5b29-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="d5b29-115">Carregar arquivos e diretórios no Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="d5b29-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="d5b29-116">Definir o número de operações paralelas durante a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="d5b29-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="d5b29-117">Acompanhar o progresso de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="d5b29-117">Track data transfer progress.</span></span>
- <span data-ttu-id="d5b29-118">Retomar a transferência de dados cancelada.</span><span class="sxs-lookup"><span data-stu-id="d5b29-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="d5b29-119">Copiar o arquivo da URL para o Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="d5b29-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="d5b29-120">Copiar do Armazenamento de Blobs para o Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="d5b29-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="d5b29-121">**O que você precisa:**</span><span class="sxs-lookup"><span data-stu-id="d5b29-121">**What you need:**</span></span>

* [<span data-ttu-id="d5b29-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d5b29-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="d5b29-123">[Uma conta do Armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="d5b29-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="d5b29-124">Este guia pressupõe que você já esteja familiarizado com o [Armazenamento do Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="d5b29-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="d5b29-125">Se não estiver, é útil ler a documentação [Introdução ao Armazenamento do Azure](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5b29-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="d5b29-126">Acima de tudo, você precisa [criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) para começar a usar a Biblioteca de Movimentação de Dados.</span><span class="sxs-lookup"><span data-stu-id="d5b29-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="d5b29-127">Configuração</span><span class="sxs-lookup"><span data-stu-id="d5b29-127">Setup</span></span>  

1. <span data-ttu-id="d5b29-128">Visite o [.NET Core Installation Guide](https://www.microsoft.com/net/core) (Guia de Instalação do .NET Core) para instalar o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d5b29-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="d5b29-129">Ao selecionar o seu ambiente, escolha a opção de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="d5b29-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="d5b29-130">Na linha de comando, crie um diretório para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d5b29-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="d5b29-131">Navegue nesse diretório, digite `dotnet new` para criar um projeto de console C#.</span><span class="sxs-lookup"><span data-stu-id="d5b29-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="d5b29-132">Abra esse diretório no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d5b29-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="d5b29-133">Esta etapa pode ser feita rapidamente por meio da linha de comando digitando `code .`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="d5b29-134">Instale a [extensão do C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) do Marketplace do Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d5b29-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="d5b29-135">Reinicie o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d5b29-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="d5b29-136">Neste ponto, você deve ver dois prompts.</span><span class="sxs-lookup"><span data-stu-id="d5b29-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="d5b29-137">Uma é para adicionar os "ativos necessários para criar e depurar".</span><span class="sxs-lookup"><span data-stu-id="d5b29-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="d5b29-138">Clique em “sim”.</span><span class="sxs-lookup"><span data-stu-id="d5b29-138">Click "yes."</span></span> <span data-ttu-id="d5b29-139">Outro prompt é para restaurar dependências não resolvidas.</span><span class="sxs-lookup"><span data-stu-id="d5b29-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="d5b29-140">Clique em “restaurar”.</span><span class="sxs-lookup"><span data-stu-id="d5b29-140">Click "restore."</span></span>
6. <span data-ttu-id="d5b29-141">Seu aplicativo agora deve conter um arquivo `launch.json` sob o diretório `.vscode`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="d5b29-142">Nesse arquivo, altere o valor de `externalConsole` para `true`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="d5b29-143">O Visual Studio Code permite que você depure aplicativos do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d5b29-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="d5b29-144">Pressione `F5` para executar o aplicativo e verificar se a configuração está funcionando.</span><span class="sxs-lookup"><span data-stu-id="d5b29-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="d5b29-145">Você deve ver o "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="d5b29-145">You should see "Hello World!"</span></span> <span data-ttu-id="d5b29-146">impresso no console.</span><span class="sxs-lookup"><span data-stu-id="d5b29-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="d5b29-147">Adicionar a Biblioteca de Movimentação de Dados ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="d5b29-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="d5b29-148">Adicione a versão mais recente da Biblioteca de Movimentação de Dados à seção `dependencies` do seu arquivo `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="d5b29-149">No momento da escrita, esta versão seria `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="d5b29-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="d5b29-150">Adicione `"portable-net45+win8"` à seção `imports`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="d5b29-151">Deve ser exibido um prompt para restaurar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d5b29-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="d5b29-152">Clique no botão "restaurar".</span><span class="sxs-lookup"><span data-stu-id="d5b29-152">Click the "restore" button.</span></span> <span data-ttu-id="d5b29-153">Você também pode restaurar seu projeto na linha de comando digitando o comando `dotnet restore` na raiz do diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="d5b29-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="d5b29-154">Modifique `project.json`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="d5b29-155">Configurar o esqueleto do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d5b29-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="d5b29-156">A primeira coisa que fazemos é configurar o código de "esqueleto" do nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5b29-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="d5b29-157">Esse código nos solicita um nome de conta de armazenamento e uma chave de conta e usa essas credenciais para criar um objeto `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="d5b29-158">Esse objeto é usado para interagir com nossa conta de armazenamento em todos os cenários de transferência.</span><span class="sxs-lookup"><span data-stu-id="d5b29-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="d5b29-159">O código também solicita a escolha do tipo de operação de transferência que gostaríamos de executar.</span><span class="sxs-lookup"><span data-stu-id="d5b29-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="d5b29-160">Modifique `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="d5b29-161">Transferir o arquivo local para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="d5b29-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="d5b29-162">Adicione os métodos `GetSourcePath` e `GetBlob` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="d5b29-163">Modifique o método `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="d5b29-164">Esse código nos solicita o caminho para um arquivo local, o nome de um contêiner de novo ou existente e o nome de um novo blob.</span><span class="sxs-lookup"><span data-stu-id="d5b29-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="d5b29-165">O método `TransferManager.UploadAsync` realiza o upload usando essas informações.</span><span class="sxs-lookup"><span data-stu-id="d5b29-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="d5b29-166">Pressione `F5` para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5b29-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="d5b29-167">Você pode verificar se o upload ocorreu exibindo sua conta de armazenamento com o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d5b29-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="d5b29-168">Definir o número de operações paralelas</span><span class="sxs-lookup"><span data-stu-id="d5b29-168">Set number of parallel operations</span></span>
<span data-ttu-id="d5b29-169">Um ótimo recurso oferecido pela Biblioteca de Movimentação de Dados é a capacidade de definir o número de operações paralelas para aumentar a taxa de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="d5b29-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="d5b29-170">Por padrão, a Biblioteca de Movimentação de Dados define o número de operações paralelas como 8 * o número de núcleos em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d5b29-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="d5b29-171">Tenha em mente que muitas operações paralelas em um ambiente de baixa largura de banda podem sobrecarregar a conexão de rede e na verdade impedir que as operações sejam totalmente concluídas.</span><span class="sxs-lookup"><span data-stu-id="d5b29-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="d5b29-172">Você precisará experimentar com essa configuração para determinar o que funciona melhor com base na largura de banda de rede disponível.</span><span class="sxs-lookup"><span data-stu-id="d5b29-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="d5b29-173">Vamos adicionar um código que nos permite definir o número de operações paralelas.</span><span class="sxs-lookup"><span data-stu-id="d5b29-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="d5b29-174">Também vamos adicionar código cronometra quanto tempo demora para a transferência ser concluída.</span><span class="sxs-lookup"><span data-stu-id="d5b29-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="d5b29-175">Adicione o método `SetNumberOfParallelOperations` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="d5b29-176">Modifique o método `ExecuteChoice` para usar `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="d5b29-177">Modifique o método `TransferLocalFileToAzureBlob` para usar um temporizador:</span><span class="sxs-lookup"><span data-stu-id="d5b29-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="d5b29-178">Acompanhar o progresso de transferência</span><span class="sxs-lookup"><span data-stu-id="d5b29-178">Track transfer progress</span></span>
<span data-ttu-id="d5b29-179">É ótimo saber quanto tempo demorou para nossos dados serem transferidos.</span><span class="sxs-lookup"><span data-stu-id="d5b29-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="d5b29-180">No entanto, ser capaz de ver o progresso da transferência *durante* a operação de transferência seria ainda melhor.</span><span class="sxs-lookup"><span data-stu-id="d5b29-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="d5b29-181">Para obter esse cenário, precisamos criar um objeto `TransferContext`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="d5b29-182">O objeto `TransferContext` vem em duas formas: `SingleTransferContext` e `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="d5b29-183">A primeira é para a transferência de um único arquivo (que é o que estamos fazendo agora) e a segunda é para transferir um diretório de arquivos (que adicionaremos posteriormente).</span><span class="sxs-lookup"><span data-stu-id="d5b29-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="d5b29-184">Adicione os métodos `GetSingleTransferContext` e `GetDirectoryTransferContext` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="d5b29-185">Modifique o método `TransferLocalFileToAzureBlob` para usar `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="d5b29-186">Retomar uma transferência cancelada</span><span class="sxs-lookup"><span data-stu-id="d5b29-186">Resume a canceled transfer</span></span>
<span data-ttu-id="d5b29-187">Outro recurso conveniente oferecido pela Biblioteca de Movimentação de Dados é a capacidade de retomar uma transferência cancelada.</span><span class="sxs-lookup"><span data-stu-id="d5b29-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="d5b29-188">Vamos adicionar um pouco de código que permite cancelar temporariamente a transferência digitando `c` e, em seguida, retomar a transferência de 3 segundos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d5b29-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="d5b29-189">Modifique `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d5b29-190">Até agora, nosso valor `checkpoint` sempre foi definido como `null`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="d5b29-191">Agora, se cancelarmos a transferência, recuperamos o último ponto de verificação da nossa transferência e usamos esse novo ponto de verificação em nosso contexto de transferência.</span><span class="sxs-lookup"><span data-stu-id="d5b29-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="d5b29-192">Transferir o diretório local para o diretório do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="d5b29-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="d5b29-193">Seria decepcionante se a Biblioteca de Movimentação de Dados pudesse transferir apenas um arquivo por vez.</span><span class="sxs-lookup"><span data-stu-id="d5b29-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="d5b29-194">Felizmente, esse não é o caso.</span><span class="sxs-lookup"><span data-stu-id="d5b29-194">Luckily, this is not the case.</span></span> <span data-ttu-id="d5b29-195">A Biblioteca de Movimentação de Dados fornece a capacidade de transferir um diretório de arquivos e todos os seus subdiretórios.</span><span class="sxs-lookup"><span data-stu-id="d5b29-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="d5b29-196">Vamos adicionar um pouco de código que nos permite fazer exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="d5b29-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="d5b29-197">Primeiro, adicione o método `GetBlobDirectory` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="d5b29-198">Em seguida, modifique `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d5b29-199">Há algumas diferenças entre este método e o método de carregamento de um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="d5b29-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="d5b29-200">Agora estamos usando `TransferManager.UploadDirectoryAsync` e o método `getDirectoryTransferContext` criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d5b29-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="d5b29-201">Além disso, agora fornecemos um valor `options` para nossa operação de upload, o que permite indicar que queremos incluir subdiretórios em nosso upload.</span><span class="sxs-lookup"><span data-stu-id="d5b29-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="d5b29-202">Copiar o arquivo da URL para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="d5b29-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="d5b29-203">Agora, vamos adicionar o código que permite copiar um arquivo de uma URL para um Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b29-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="d5b29-204">Modifique `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d5b29-205">Um caso de uso importante para esse recurso é quando você precisa mover dados de outro serviço de nuvem (por exemplo, AWS) para o Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b29-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="d5b29-206">Contanto que você tenha uma URL que fornece acesso ao recurso, pode mover facilmente esse recurso para Blobs do Azure usando o método `TransferManager.CopyAsync`.</span><span class="sxs-lookup"><span data-stu-id="d5b29-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="d5b29-207">Esse método também introduz um novo parâmetro booliano.</span><span class="sxs-lookup"><span data-stu-id="d5b29-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="d5b29-208">Configurar esse parâmetro como `true` indica que queremos fazer uma cópia assíncrona do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="d5b29-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="d5b29-209">Configurar esse parâmetro para `false` indica uma cópia síncrona – o que significa que o recurso é baixado primeiramente para nosso computador local e então carregado para o Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b29-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="d5b29-210">No entanto, a cópia síncrona está disponível apenas para a cópia de um recurso do Armazenamento do Azure para outro.</span><span class="sxs-lookup"><span data-stu-id="d5b29-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="d5b29-211">Transferir do Blob do Azure para Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="d5b29-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="d5b29-212">Outro recurso que é fornecido exclusivamente pela Biblioteca de Movimentação de Dados é a capacidade de copiar de um recurso de Armazenamento do Azure para outro.</span><span class="sxs-lookup"><span data-stu-id="d5b29-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="d5b29-213">Modifique `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d5b29-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d5b29-214">Neste exemplo, definimos o parâmetro booliano em `TransferManager.CopyAsync` como `false` para indicar que queremos fazer uma cópia síncrona.</span><span class="sxs-lookup"><span data-stu-id="d5b29-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="d5b29-215">Isso significa que o recurso é baixado para o computador local primeiro e, em seguida, carregado no Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b29-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="d5b29-216">A opção de cópia síncrona é uma ótima maneira de garantir que a operação de cópia tenha uma velocidade consistente.</span><span class="sxs-lookup"><span data-stu-id="d5b29-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="d5b29-217">Por outro lado, a velocidade de uma cópia assíncrona do lado do servidor é dependente da largura de banda de rede disponível no servidor, que pode flutuar.</span><span class="sxs-lookup"><span data-stu-id="d5b29-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="d5b29-218">No entanto, a cópia síncrona pode gerar custo de saída adicional em comparação com a cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="d5b29-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="d5b29-219">A abordagem recomendada é usar essa a cópia síncrona na VM do Azure que está na mesma região que a sua conta de armazenamento de origem, a fim de evitar o custo de saída.</span><span class="sxs-lookup"><span data-stu-id="d5b29-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d5b29-220">Conclusão</span><span class="sxs-lookup"><span data-stu-id="d5b29-220">Conclusion</span></span>
<span data-ttu-id="d5b29-221">Agora nosso aplicativo de movimentação de dados está concluído.</span><span class="sxs-lookup"><span data-stu-id="d5b29-221">Our data movement application is now complete.</span></span> <span data-ttu-id="d5b29-222">[O exemplo de código completo está disponível no GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="d5b29-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d5b29-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5b29-223">Next steps</span></span>
<span data-ttu-id="d5b29-224">Neste guia de introdução, criamos um aplicativo que interage com o Armazenamento do Azure e é executado no Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="d5b29-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="d5b29-225">Este guia de introdução se concentrou no Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="d5b29-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="d5b29-226">No entanto, esse mesmo conhecimento pode ser aplicado ao Armazenamento de Arquivos.</span><span class="sxs-lookup"><span data-stu-id="d5b29-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="d5b29-227">Para obter mais informações, confira a [Documentação de referência da Biblioteca de Movimentação de Dados do Armazenamento do Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="d5b29-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




