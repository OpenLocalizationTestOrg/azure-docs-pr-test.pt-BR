---
title: "aaaGet de Introdução ao armazenamento de blob e o Visual Studio serviços conectados (serviços de nuvem) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de BLOBs do Azure em um projeto de serviço de nuvem no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introdução ao Armazenamento de Blob do Azure e aos serviços conectados do Visual Studio (projetos de serviços de nuvem)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Este artigo descreve como tooget iniciada com o armazenamento de Blob do Azure após a criação ou referenciado uma conta de armazenamento do Azure usando o Visual Studio de saudação **adicionar serviços conectados** projeto dos serviços de caixa de diálogo em uma nuvem do Visual Studio. Mostraremos como tooaccess e criar contêineres de blob e como tarefas comuns de tooperform deseja carregar, listar e baixar blobs. exemplos de saudação são escritos em C\# e usar Olá [biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS. Um único blob pode ter qualquer tamanho. Blobs podem ser coisas como imagens, arquivos de áudio e vídeo, dados brutos e arquivos de documentos.

Assim como arquivos residem em pastas, blobs de armazenamento residem em contêineres. Depois de criar um armazenamento, você cria um ou mais contêineres no armazenamento hello. Por exemplo, em um armazenamento chamado "Livro de recortes", você pode criar contêineres em armazenamento Olá chamado imagens de toostore "imagens" e outro chamado "áudio" toostore arquivos de áudio. Depois de criar contêineres de saudação, você pode carregar toothem de arquivos de blob individuais.

* Para obter mais informações sobre a manipulação de bobs com programação, consulte a [Introdução ao Armazenamento de Blobs do Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).
* Para obter informações gerais sobre o Armazenamento do Azure, consulte a [documentação do Armazenamento](https://azure.microsoft.com/documentation/services/storage/).
* Para obter informações gerais sobre os Serviços de Nuvem do Azure, consulte a [documentação dos Serviços de Nuvem](https://azure.microsoft.com/documentation/services/cloud-services/).
* Para saber mais sobre como programar aplicativos ASP.NET, consulte [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Acessar contêineres de blob em código
tooprogrammatically acessar blobs em projetos de serviço de nuvem, você precisa de saudação tooadd itens, a seguir se eles não ainda estiver presentes.

1. Adicione Olá código declarações de namespace toohello superior de qualquer arquivo c# no qual você deseja acesso tooprogrammatically armazenamento do Azure a seguir.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento. Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Obter um **CloudBlobClient** tooreference um contêiner existente na sua conta de armazenamento do objeto.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Obter um **CloudBlobContainer** tooreference um contêiner de blob específico do objeto.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Use todo código Olá mostrado no procedimento anterior de saudação na frente do código Olá mostrado Olá seções a seguir.
> 
> 

## <a name="create-a-container-in-code"></a>Criar um contêiner no código
> [!NOTE]
> Algumas APIs que executam chamadas tooAzure armazenamento no ASP.NET são assíncronas. Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais. código Olá Olá exemplo a seguir supõe que você esteja usando métodos de programação assíncrona.
> 
> 

toocreate um contêiner na conta de armazenamento, tudo o que você precisa toodo é adicionar uma chamada muito**CreateIfNotExistsAsync** como Olá código a seguir:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


arquivos de saudação toomake dentro Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público, mas você pode modificar ou excluí-los somente se você tiver a chave de acesso apropriadas de saudação.

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
O Armazenamento do Azure dá suporte a blobs de blocos e a blobs de páginas. Na maioria Olá dos casos, blob de blocos é hello recomendado toouse de tipo.

tooupload um blob de blocos de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob de bloco. Quando você tem uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **UploadFromStream** método. Essa operação cria blob Olá se ela não existia anteriormente ou substituí-lo se ele existir. Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner. Você pode usar do contêiner Olá **ListBlobs** blobs de saudação do método tooretrieve e/ou diretórios dentro dele. tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **IListBlobItem**, você deve converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto. Se o tipo de saudação for desconhecido, você pode usar um toodetermine de verificação de tipo que toocast-o para. Olá código a seguir demonstra como tooretrieve e saída Olá URI de cada item em Olá **fotos** contêiner:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
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

Conforme mostrado no exemplo de código anterior Olá, serviço de blob Olá tem conceito de saudação de diretórios em contêineres, também. Isso é para que você possa organizar seus blobs em uma estrutura mais semelhante a uma pasta. Por exemplo, considere Olá após o conjunto de blobs de bloco em um contêiner chamado **fotos**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Quando você chama **ListBlobs** no contêiner de saudação (como no exemplo anterior de saudação), coleção Olá retornada contém **CloudBlobDirectory** e **CloudBlockBlob** objetos que representam diretórios hello e blobs presentes no nível superior de saudação. Aqui está a saída resultante hello:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


Opcionalmente, você pode definir Olá **UseFlatBlobListing** parâmetro de saudação **ListBlobs** método **true**. Isso resulta no retorno de cada blob como um **CloudBlockBlob**, independentemente do diretório. Aqui está a chamada de saudação muito**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

e estes são os resultados de saudação:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Para obter mais informações, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Baixar blobs
blobs toodownload, recuperar uma referência de blob e, em seguida, chamar hello **os métodos DownloadToStream** método. Olá, exemplo a seguir usa Olá **os métodos DownloadToStream** método tootransfer Olá conteúdo tooa fluxo objeto blob que, em seguida, você pode persistir o arquivo local tooa.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

Você também pode usar o hello **os métodos DownloadToStream** conteúdo de saudação do método toodownload de um blob como uma cadeia de caracteres de texto.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Excluir blobs
toodelete um blob, primeiro obter uma referência de blob e, em seguida, chame o **excluir** método.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Listar blobs em páginas de maneira assíncrona
Se estiver listando um grande número de blobs ou desejar toocontrol Olá número de resultados de que retorno em uma operação de listagem, você pode listar blobs em páginas de resultados. Este exemplo mostra como tooreturn resulta em páginas de forma assíncrona, para que a execução não é bloqueada durante a espera tooreturn um grande conjunto de resultados.

Este exemplo mostra uma simples listagem do blob, mas você também pode executar uma lista hierárquica, definindo Olá **useFlatBlobListing** parâmetro hello **ListBlobsSegmentedAsync** método muito **False**.

Como o método de exemplo hello chama um método assíncrono, ela deve ser precedida por hello **async** palavra-chave e ele devem retornar um **tarefa** objeto. Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo hello até Olá listagem tarefa ser concluída.

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

