---
title: "aaaGet de Introdução ao armazenamento de blob e o Visual Studio serviços conectados (ASP.NET Core) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de BLOBs do Azure em um projeto do Visual Studio ASP.NET Core depois de ter criado uma conta de armazenamento usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: a4c31c08c38d99eb9c66fe2af72ca42fa3804688
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Este artigo descreve como tooget iniciado usando o armazenamento de BLOBs do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto do ASP.NET Core usando Olá Visual Studio conectado de diálogo Adicionar serviços.

Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS. Um único blob pode ter qualquer tamanho. Blobs podem ser coisas como imagens, arquivos de áudio e vídeo, dados brutos e arquivos de documentos. Este artigo descreve como tooget iniciada com o armazenamento de blob depois de criar uma conta de armazenamento do Azure usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo em um projeto do ASP.NET Core.

Assim como arquivos residem em pastas, blobs de armazenamento residem em contêineres. Depois de criar um armazenamento, você cria um ou mais contêineres no armazenamento hello. Por exemplo, em um armazenamento chamado "Livro de recortes", você pode criar contêineres em armazenamento Olá chamado imagens de toostore "imagens" e outro chamado "áudio" toostore arquivos de áudio. Depois de criar contêineres de saudação, você pode carregar toothem de arquivos de blob individuais. Consulte [Introdução ao Armazenamento de Blobs do Azure usando .NET](storage-dotnet-how-to-use-blobs.md) para obter mais informações sobre como manipular blobs com programação.

## <a name="access-blob-containers-in-code"></a>Acessar contêineres de blob em código
tooprogrammatically acessar blobs em projetos do ASP.NET Core, é necessário tooadd Olá itens, a seguir se eles não ainda estiver presentes.

1. Adicione Olá código declarações de namespace toohello superior de qualquer arquivo c# no qual você deseja acesso tooprogrammatically armazenamento do Azure a seguir.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento. Use Olá tooget de código a seguir, sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Observação:** Use todos Olá acima código código Olá Olá seções a seguir.
3. Use um **CloudBlobClient** objeto tooget um **CloudBlobContainer** contêiner existente do tooan de referência em sua conta de armazenamento.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Criar um contêiner no código
Você também pode usar o hello **CloudBlobClient** toocreate um contêiner na conta de armazenamento. Você só precisa toodo é tooadd uma chamada muito**CreateIfNotExistsAsync** como Olá código a seguir:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Observação:** Olá APIs que executam chamadas tooAzure armazenamento no núcleo do ASP.NET são assíncronas. Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais. código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.

arquivos de saudação toomake dentro Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
tooupload um arquivo de blob em um contêiner, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob. Depois de ter uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **UploadFromStreamAsync** método. Essa operação cria blob Olá se ele não ainda estiver lá, ou substituí-lo se ele existir. Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner. Em seguida, você pode chamar do contêiner Olá **ListBlobsSegmentedAsync** blobs de saudação do método tooretrieve e/ou diretórios dentro dele. tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **IListBlobItem**, você deve converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto. Se você não souber o blob de saudação tipo, você pode usar um toodetermine de verificação de tipo que toocast-o para. saudação de código a seguir demonstra como tooretrieve e saída Olá URI de cada item em um contêiner.

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
        {
            if (item.GetType() == typeof(CloudBlockBlob))
            {
                CloudBlockBlob blob = (CloudBlockBlob)item;
                Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);
            }

            else if (item.GetType() == typeof(CloudPageBlob))
            {
                CloudPageBlob pageBlob = (CloudPageBlob)item;

                Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);
            }

            else if (item.GetType() == typeof(CloudBlobDirectory))
            {
                CloudBlobDirectory directory = (CloudBlobDirectory)item;

                Console.WriteLine("Directory: {0}", directory.Uri);
            }
        }
    } while (token != null);

Há-outros conteúdos de saudação toolist maneiras de um contêiner de blob. Consulte [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para obter mais informações.

## <a name="download-a-blob"></a>Baixar um blob
toodownload um blob, primeiro obter um blob de toohello de referência e, em seguida, chamar hello **DownloadToStreamAsync** método. Olá, exemplo a seguir usa Olá **DownloadToStreamAsync** método tootransfer Olá conteúdo tooa fluxo objeto blob que você pode salvar como um arquivo local.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Existem outras maneiras toosave blobs como arquivos. Consulte [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) para obter mais informações.

## <a name="delete-a-blob"></a>Excluir um blob
toodelete um blob, primeiro obter um blob de toohello de referência e, em seguida, chamar hello **DeleteAsync** método nele.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

