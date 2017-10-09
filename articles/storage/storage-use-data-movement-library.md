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
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Transferência de dados com hello biblioteca de movimentação de dados de armazenamento do Microsoft Azure

## <a name="overview"></a>Visão geral
Olá biblioteca de movimentação de dados de armazenamento do Microsoft Azure é uma biblioteca de software livre de plataforma cruzada que foi projetada para carregar, baixar e cópia de Blobs de armazenamento do Azure e arquivos de alto desempenho. Essa biblioteca é de estrutura movimentação de dados de núcleo de saudação que alimenta [AzCopy](storage-use-azcopy.md). Olá biblioteca de movimentação de dados fornece métodos convenientes que não estão disponíveis no nosso tradicional [biblioteca de cliente de armazenamento do Azure .NET](storage-dotnet-how-to-use-blobs.md). Isso inclui Olá capacidade tooset Olá número de operações paralelas, controlar o progresso de transferência, facilmente retomar uma transferência cancelada e muito mais.  

Essa biblioteca também usa o .NET Core, que significa que você pode usá-la ao criar aplicativos .NET para Windows, Linux e macOS. toolearn mais sobre o núcleo do .NET, consulte toohello [documentação .NET Core](https://dotnet.github.io/). Essa biblioteca também funciona para aplicativos tradicionais do .NET Framework para Windows. 

Este documento demonstra como aplicativo que que é executado no Windows, Linux e macOS e executa os seguintes cenários de saudação do console toocreate um núcleo do .NET:

- Carregar tooBlob armazenamento de arquivos e diretórios.
- Defina o número de saudação de operações paralelas durante a transferência de dados.
- Acompanhar o progresso de transferência de dados.
- Retomar a transferência de dados cancelada. 
- Copie o arquivo de armazenamento de tooBlob de URL. 
- Copiar do armazenamento de Blob tooBlob armazenamento.

**O que você precisa:**

* [Visual Studio Code](https://code.visualstudio.com/)
* [Uma conta do Armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Este guia pressupõe que você já esteja familiarizado com o [Armazenamento do Azure](https://azure.microsoft.com/services/storage/). Se não, lendo Olá [tooAzure Introdução armazenamento](storage-introduction.md) documentação é útil. Mais importante, é necessário muito[criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) toostart usando Olá biblioteca de movimentação de dados.
> 
> 

## <a name="setup"></a>Configuração  

1. Visite Olá [guia de instalação do .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. Ao selecionar o seu ambiente, escolha a opção de linha de comando hello. 
2. Na linha de comando hello, crie um diretório para seu projeto. Navegue nesse diretório, digite `dotnet new` toocreate c# projeto de console.
3. Abra esse diretório no Visual Studio Code. Esta etapa pode ser feita rapidamente por meio da linha de comando Olá digitando `code .`.  
4. Instalar Olá [c# extensão](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) de saudação Marketplace de código do Visual Studio. Reinicie o Visual Studio Code. 
5. Neste ponto, você deve ver dois prompts. Uma é adicionando "toobuild ativos necessária e debug". Clique em “sim”. Outro prompt é para restaurar dependências não resolvidas. Clique em “restaurar”.
6. Seu aplicativo agora deve conter um `launch.json` arquivo hello `.vscode` directory. Nesse arquivo, alterar Olá `externalConsole` valor muito`true`.
7. Código do Visual Studio permite que aplicativos de .NET Core toodebug. Acertos `F5` toorun seu aplicativo e verificar se a configuração está funcionando. Você deve ver o "Hello World!" console toohello impresso. 

## <a name="add-data-movement-library-tooyour-project"></a>Adicionar projeto de biblioteca de movimentação de dados de tooyour

1. Adicionar mais recente versão Olá Olá biblioteca de movimentação de dados toohello `dependencies` seção do seu `project.json` arquivo. No momento da saudação de gravação, esta versão seria`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Adicionar `"portable-net45+win8"` toohello `imports` seção. 
3. Um prompt deve exibir toorestore seu projeto. Botão hello "restauração". Você também pode restaurar seu projeto da linha de comando Olá digitando o comando Olá `dotnet restore` na raiz de saudação do diretório do projeto.

Modifique `project.json`:

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

## <a name="set-up-hello-skeleton-of-your-application"></a>Configurar o esqueleto de saudação do seu aplicativo
Olá primeira coisa que fazemos é configurar hello "esqueleto" código de nosso aplicativo. Esse código nos solicitará um nome e a conta chave de conta do armazenamento e usa essas credenciais toocreate um `CloudStorageAccount` objeto. Esse objeto é usado toointeract com nossa conta de armazenamento em todos os cenários de transferência. código de saudação também solicita nos toochoose tipo de saudação da operação de transferência, gostaríamos tooexecute. 

Modifique `Program.cs`:

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

## <a name="transfer-local-file-tooazure-blob"></a>Transferência de arquivo local tooAzure Blob
Adicionar métodos Olá `GetSourcePath` e `GetBlob` muito`Program.cs`:

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

Modificar Olá `TransferLocalFileToAzureBlob` método:

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

Esse código solicita nos Olá caminho tooa local arquivo, o nome de saudação de um contêiner de novo ou existente e o nome de saudação de um novo blob. Olá `TransferManager.UploadAsync` método executa o carregamento de saudação usando essas informações. 

Acertos `F5` toorun seu aplicativo. Você pode verificar esse carregamento Olá ocorreu exibindo sua conta de armazenamento com hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Definir o número de operações paralelas
Um ótimo recurso oferecido pelo Olá que biblioteca de movimentação de dados é o número de saudação de tooset de capacidade de saudação operações paralelas tooincrease Olá transferência de transferência de dados. Por padrão, a saudação biblioteca de movimentação de dados define o número de Olá de operações paralelas too8 * hello número de núcleos em sua máquina. 

Tenha em mente que muitas operações paralelas em um ambiente de baixa largura de banda podem sobrecarregar a conexão de rede hello e evita que as operações de ser totalmente concluída. Você precisará tooexperiment com esta configuração toodetermine o que funciona melhor com base em sua largura de banda de rede disponível. 

Vamos adicionar algum código que nos permite tooset número de saudação de operações paralelas. Vamos adicionar código que vezes quanto tempo demora para Olá transferência toocomplete também.

Adicionar um `SetNumberOfParallelOperations` método muito`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Modificar Olá `ExecuteChoice` método toouse `SetNumberOfParallelOperations`:

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

Modificar Olá `TransferLocalFileToAzureBlob` método toouse um timer:

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

## <a name="track-transfer-progress"></a>Acompanhar o progresso de transferência
É ótimo saber quanto tempo demorou para tootransfer nossos dados. No entanto, sendo toosee capaz de progresso de saudação da nossa transferência *durante* operação de transferência Olá seria ainda melhor. tooachieve nesse cenário, é preciso toocreate um `TransferContext` objeto. Olá `TransferContext` objeto vem em duas formas: `SingleTransferContext` e `DirectoryTransferContext`. Olá anterior é para transferir um único arquivo (que é o que estamos fazendo agora) e Olá segundo é para transferir um diretório de arquivos (que estamos adicionando mais tarde).

Adicionar métodos Olá `GetSingleTransferContext` e `GetDirectoryTransferContext` muito`Program.cs`: 

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

Modificar Olá `TransferLocalFileToAzureBlob` método toouse `GetSingleTransferContext`:

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

## <a name="resume-a-canceled-transfer"></a>Retomar uma transferência cancelada
Outro recurso conveniente oferecido pelo Olá biblioteca de movimentação de dados é Olá capacidade tooresume uma transferência cancelada. Vamos adicionar algum código que nos permite tootemporarily Cancelar Olá transferência digitando `c`e, em seguida, continuar a transferência Olá 3 segundos mais tarde.

Modifique `TransferLocalFileToAzureBlob`:

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

Até agora, nosso `checkpoint` valor sempre foi definido muito`null`. Agora, se podemos Cancelar transferência hello, podemos recuperar o último ponto de verificação de saudação do nosso transferência, use este novo ponto de verificação em nosso contexto de transferência. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Diretório de Blob do diretório local tooAzure de transferência
Seria decepcionantes se Olá biblioteca de movimentação de dados só pode transferir um arquivo por vez. Felizmente, isso não é o caso de saudação. Olá biblioteca de movimentação de dados fornece Olá capacidade tootransfer um diretório de arquivos e todas as suas subpastas. Vamos adicionar algum código que nos permite toodo exatamente isso.

Primeiro, adicione o método hello `GetBlobDirectory` muito`Program.cs`:

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

Em seguida, modifique `TransferLocalDirectoryToAzureBlobDirectory`:

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

Há algumas diferenças entre este método e o método hello para carregar um único arquivo. Agora que estamos usando `TransferManager.UploadDirectoryAsync` e hello `getDirectoryTransferContext` método criado anteriormente. Além disso, agora, nós fornecemos uma `options` valor operação de carregamento de tooour, que nos permite tooindicate que desejamos subdiretórios tooinclude em nosso carregamento. 

## <a name="copy-file-from-url-tooazure-blob"></a>Copie o arquivo de URL tooAzure Blob
Agora, vamos adicionar o código que nos permite toocopy um arquivo de uma URL de tooan BLOBs do Azure. 

Modifique `TransferUrlToAzureBlob`:

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

Um caso de uso importantes para esse recurso é quando você precisa toomove dados de outro tooAzure (por exemplo, AWS) do serviço de nuvem. Como você tem uma URL que fornece acesso toohello recursos, você pode mover facilmente esse recurso em Blobs do Azure usando Olá `TransferManager.CopyAsync` método. Esse método também introduz um novo parâmetro booliano. Definir esse parâmetro muito`true` indica que desejamos cópia toodo um assíncrona no lado do servidor. Definir esse parâmetro muito`false` indica uma cópia síncrona - que significa que recursos Olá é máquina local tooour baixados em primeiro lugar, em seguida, carregados tooAzure Blob. No entanto, cópia síncrona está apenas disponível para a cópia de um tooanother de recursos de armazenamento do Azure. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Transferência de BLOBs do Azure tooAzure Blob
Outro recurso exclusivamente fornecida pelo Olá biblioteca de movimentação de dados é Olá toocopy de capacidade de um tooanother de recursos de armazenamento do Azure. 

Modifique `TransferAzureBlobToAzureBlob`:

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

Neste exemplo, vamos definir parâmetro booliano Olá `TransferManager.CopyAsync` muito`false` tooindicate que desejamos toodo uma cópia síncrona. Isso significa que o recurso de saudação for máquina local tooour baixado primeiro, carregado tooAzure Blob. opção de cópia síncrona Olá é um tooensure excelente maneira que a operação de cópia tenha uma velocidade consistente. Por outro lado, a velocidade de saudação de uma cópia assíncrona do lado do servidor é dependente de Olá largura de banda disponível no servidor de saudação, que pode flutuar. No entanto, cópia síncrona pode gerar saída adicional em comparação de custo tooasynchronous cópia. Olá recomendado abordagem é a cópia síncrona toouse em uma VM do Azure que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.

## <a name="conclusion"></a>Conclusão
Agora nosso aplicativo de movimentação de dados está concluído. [exemplo de código completo Hello está disponível no GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Próximas etapas
Neste guia de introdução, criamos um aplicativo que interage com o Armazenamento do Azure e é executado no Windows, Linux e macOS. Este guia de introdução se concentrou no Armazenamento de Blobs. No entanto, esse mesmo conhecimento pode ser aplicado tooFile armazenamento. toolearn mais, confira [documentação de referência da biblioteca de movimentação de dados de armazenamento do Azure](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




