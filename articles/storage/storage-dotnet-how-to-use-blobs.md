---
title: "aaaGet de Introdução ao armazenamento de BLOBs do Azure (armazenamento de objeto) usando .NET | Microsoft Docs"
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>Introdução ao Armazenamento de Blobs do Azure usando o .NET

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.

### <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial mostra como toowrite .NET código em alguns cenários comuns usando o armazenamento de BLOBs do Azure. Os cenários incluem upload, listagem, download e exclusão de blobs.

**Pré-requisitos:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Biblioteca do Cliente de Armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gerenciador de Configurações do Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Uma conta do Armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Mais exemplos
Para obter exemplos adicionais usando o Armazenamento de Blobs, confira [Introdução ao Armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/). Você pode baixar o aplicativo de exemplo hello e executá-lo ou procurar Olá código no GitHub.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adicionar diretivas using
Adicione o seguinte Olá **usando** superior de toohello de diretivas de saudação `Program.cs` arquivo:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Analisar a cadeia de conexão Olá
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Criar o cliente do serviço Blob Olá
Olá **CloudBlobClient** classe permite que você tooretrieve contêineres e blobs armazenados no armazenamento de Blob. Aqui está o cliente do serviço Olá toocreate unidirecional:

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Agora você está pronto toowrite código lê e grava o armazenamento de tooBlob de dados.

## <a name="create-a-container"></a>Criar um contêiner
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Este exemplo mostra como toocreate um contêiner se ele ainda não existir:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

Por padrão, o novo contêiner de saudação é privado, o que significa que você deve especificar seus blobs de toodownload chave de acesso de armazenamento desse contêiner. Se você quiser toomake arquivos Olá Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público. No entanto, você pode modificar ou excluí-los somente se você tiver a chave de acesso de conta apropriada de saudação ou uma assinatura de acesso compartilhado.

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.  Na maioria dos casos, o blob de blocos é hello recomendado toouse de tipo.

tooupload um blob de blocos de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob de bloco. Quando você tem uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **UploadFromStream** método. Essa operação cria blob Olá se ela não existia anteriormente ou substituí-lo se ele existir.

Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner. Você pode usar do contêiner Olá **ListBlobs** blobs de saudação do método tooretrieve e/ou diretórios dentro dele. tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **IListBlobItem**, você deve converter tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto. Se o tipo de saudação for desconhecido, você pode usar um toodetermine de verificação de tipo que toocast-o para. Olá código a seguir demonstra como tooretrieve e saída Olá URI de cada item em Olá _fotos_ contêiner:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

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
```

Ao incluir informações de caminho nos nomes de blob, você poderá criar uma estrutura de diretório virtual que pode organizar e percorrer como faria com um sistema de arquivos tradicional. estrutura de diretórios de saudação é virtual--Olá somente os recursos disponíveis no armazenamento de Blob são contêineres e blobs. No entanto, a biblioteca de cliente de armazenamento Olá oferece um **CloudBlobDirectory** objeto de diretório virtual do toorefer tooa e simplificar o processo de saudação do trabalho com blobs são organizados dessa maneira.

Por exemplo, considere Olá após o conjunto de blobs de bloco em um contêiner chamado *fotos*:

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

Quando você chama **ListBlobs** em Olá *fotos* contêiner (como Olá precede o trecho de código), uma lista hierárquica é retornada. Ele contém ambos **CloudBlobDirectory** e **CloudBlockBlob** objetos, que representam diretórios hello e blobs no contêiner hello, respectivamente. saída resultante Olá aparência:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Opcionalmente, você pode definir Olá **UseFlatBlobListing** parâmetro hello **ListBlobs** método **true**. Nesse caso, cada blob no contêiner de saudação é retornado como um **CloudBlockBlob** objeto. Olá chamada muito**ListBlobs** tooreturn uma lista simples tem esta aparência:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

e resultados de saudação ter esta aparência:

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Baixar blobs
blobs toodownload, recuperar uma referência de blob e, em seguida, chamar hello **os métodos DownloadToStream** método. Olá, exemplo a seguir usa Olá **os métodos DownloadToStream** método tootransfer Olá conteúdo tooa fluxo objeto blob que, em seguida, você pode persistir o arquivo local tooa.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

Você também pode usar o hello **os métodos DownloadToStream** conteúdo de saudação do método toodownload de um blob como uma cadeia de caracteres de texto.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a>Excluir blobs
toodelete um blob, primeiro obter uma referência de blob e, em seguida, chame o **excluir** método nele.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a>Listar blobs em páginas de maneira assíncrona
Se estiver listando um grande número de blobs ou desejar toocontrol Olá número de resultados de que retorno em uma operação de listagem, você pode listar blobs em páginas de resultados. Este exemplo mostra como tooreturn resulta em páginas de forma assíncrona, para que a execução não é bloqueada durante a espera tooreturn um grande conjunto de resultados.

Este exemplo mostra uma simples listagem do blob, mas você também pode executar uma lista hierárquica, definindo Olá _useFlatBlobListing_ parâmetro hello **ListBlobsSegmentedAsync** too_false_ de método.

Como o método de exemplo hello chama um método assíncrono, ela deve ser precedida por hello _async_ palavra-chave e ele devem retornar um **tarefa** objeto. Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo hello até Olá listagem tarefa ser concluída.

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
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
```

## <a name="writing-tooan-append-blob"></a>Blob de acréscimo tooan de gravação
Um blob de acréscimo é otimizado para operações de acréscimo, como o registro em log. Como um blob de bloco, um blob de acréscimo é composto por blocos, mas quando você adiciona um novo blob de acréscimo de tooan de bloco, é sempre anexado toohello final de blob de saudação. Não é possível atualizar ou excluir um bloco existente em um blob de acréscimo. IDs de bloco Olá para um blob de acréscimo não são expostos como eles são para um blob de bloco.

Cada bloco em um blob de acréscimo pode ter um tamanho diferente, o máximo de tooa de 4 MB, e um blob de acréscimo pode incluir até 50.000 blocos. tamanho máximo de saudação de um blob de acréscimo, portanto, é um pouco mais de 195 GB (4 MB X 50.000 blocos).

exemplo Hello abaixo cria um novo blob de acréscimo e acrescenta alguns tooit de dados, com uma simulação de uma operação de log simples.

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

Consulte [Compreendendo Blobs de bloco, Blobs de página e Blobs de acréscimo](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) para obter mais informações sobre as diferenças de saudação entre tipos de saudação três de blobs.

## <a name="managing-security-for-blobs"></a>Gerenciamento da segurança de blobs
Por padrão, o armazenamento do Azure mantém seus dados seguros, limitando o acesso toohello proprietário da conta, que está em posse das chaves de acesso de conta hello. Quando você precisar de dados de blob tooshare na sua conta de armazenamento, é importante toodo caso sem comprometer a segurança de saudação de suas chaves de acesso da conta. Além disso, você pode criptografar tooensure de dados de blob que é seguro vai conexão hello e no armazenamento do Azure.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Controlando acesso tooblob dados
Por padrão, os dados de blob de saudação em sua conta de armazenamento são acessível somente toostorage conta o proprietário. Autenticar solicitações em relação ao armazenamento de Blob exige a chave de acesso de conta Olá por padrão. No entanto, você poderá toomake determinados usuários tooother disponíveis de dados de blob. Você tem duas opções:

* **Acesso anônimo:** você pode tornar um contêiner ou seus blobs publicamente disponíveis para acesso anônimo. Consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](storage-manage-access-to-resources.md) para obter mais informações.
* **Assinaturas de acesso compartilhado:** podem fornecer aos clientes com uma assinatura de acesso compartilhado (SAS), que fornece acesso delegado tooa recursos em sua conta de armazenamento, com as permissões que você especificar e em um intervalo que você especificar. Confira [Usando Assinaturas de Acesso Compartilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para saber mais.

### <a name="encrypting-blob-data"></a>Criptografia de dados de blobs
Armazenamento do Azure oferece suporte à criptografia de dados de blob no cliente hello e no servidor de saudação:

* **Criptografia do lado do cliente:** Olá biblioteca de cliente de armazenamento para .NET oferece suporte a criptografia de dados em aplicativos cliente antes de carregar tooAzure armazenamento e a descriptografia de dados durante o download toohello cliente. biblioteca de saudação também oferece suporte à integração com o Cofre de chaves do Azure para gerenciamento de chaves de conta de armazenamento. Confira [Criptografia no cliente com o .NET para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md) para saber mais. Confira também [Tutorial: Criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Cofre de Chaves do Azure](storage-encrypt-decrypt-blobs-key-vault.md).
* **Criptografia no servidor**: o Armazenamento do Azure agora dá suporte à criptografia no servidor. Confira [Criptografia do Serviço de Armazenamento do Azure para dados em repouso (Visualização)](storage-service-encryption.md).

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de Blob, siga essas toolearn links mais.

### <a name="microsoft-azure-storage-explorer"></a>Gerenciador do Armazenamento do Microsoft Azure
* [Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.

### <a name="blob-storage-samples"></a>Exemplos de Armazenamento de Blobs
* [Introdução ao Armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Referência do Armazenamento de Blobs
* [Referência à Biblioteca de Cliente de Armazenamento para .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Referência da API REST](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Guias conceituais
* [Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)
* [Introdução ao Armazenamento de arquivos para .NET](storage-dotnet-how-to-use-files.md)
* [Como toouse Azure blob storage com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
