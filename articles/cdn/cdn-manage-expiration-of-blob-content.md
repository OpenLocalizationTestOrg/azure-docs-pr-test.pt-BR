---
title: "expiração de aaaManage de blobs de armazenamento do Azure no Azure CDN | Microsoft Docs"
description: "Saiba mais sobre opções de saudação para controlar o tempo de vida para blobs no cache de CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Gerenciar a expiração dos blobs de Armazenamento do Azure na CDN do Azure
> [!div class="op_single_selector"]
> * [Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Serviço Blob do Armazenamento do Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

Olá [do serviço blob](../storage/common/storage-introduction.md#blob-storage) na [armazenamento do Azure](../storage/common/storage-introduction.md) uma das várias origens baseado no Azure é integrada com o Azure CDN.  Qualquer conteúdo de blob publicamente acessível pode ser armazenado em cache no Azure CDN até que o tempo de vida (TTL) seja decorrido.  Olá TTL é determinado pelo Olá [ *Cache-Control* cabeçalho](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) na resposta HTTP de saudação do armazenamento do Azure.

> [!TIP]
> Você não pode escolher tooset nenhum TTL em um blob.  Nesse caso, o Azure CDN aplica automaticamente um TTL padrão de sete dias.
> 
> Para obter mais informações sobre como funciona o Azure CDN toospeed tooblobs de acesso e outros arquivos, consulte Olá [visão geral do Azure CDN](cdn-overview.md).
> 
> Para obter mais detalhes sobre Olá serviço de blob de armazenamento do Azure, consulte [conceitos do serviço Blob](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

Este tutorial demonstra várias maneiras que você pode definir o TTL da saudação em um blob no armazenamento do Azure.  

## <a name="azure-powershell"></a>Azure PowerShell
[O Azure PowerShell](/powershell/azure/overview) é uma saudação maneiras mais rápida e mais eficiente tooadminister os serviços do Azure.  Saudação de uso `Get-AzureStorageBlob` tooget cmdlet um blob de toohello de referência, em seguida, defina Olá `.ICloudBlob.Properties.CacheControl` propriedade. 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> Você também pode usar o PowerShell muito[gerenciar os perfis CDN e os pontos de extremidade](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>Biblioteca do Cliente de Armazenamento do Azure para .NET
tooset um blob do TTL usando .NET, use Olá [biblioteca de cliente de armazenamento do Azure para .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset Olá [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) propriedade.

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> Há muitos exemplos de código .NET mais disponíveis no hello [exemplos de armazenamento de Blob do Azure para .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Outros métodos
* [Interface de linha de comando do Azure](../cli-install-nodejs.md)
  
    Ao carregar o blob hello, defina Olá *cacheControl* propriedade usando Olá `-p` alternar.  Este exemplo define a hora de tooone TTL de saudação (3.600 segundos).
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [API REST de serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    Explicitamente o conjunto Olá *x-ms---controle de cache blob* propriedade em uma [Blob Put](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [colocar lista de blocos](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), ou [definir propriedades de Blob](https://msdn.microsoft.com/library/azure/ee691966.aspx) solicitação.
* Ferramentas de gerenciamento de armazenamento de terceiros
  
    Algumas ferramentas de gerenciamento de armazenamento do Azure de terceiros permitem Olá tooset *CacheControl* propriedade em blobs. 

## <a name="testing-hello-cache-control-header"></a>Olá teste *Cache-Control* cabeçalho
Você pode facilmente verificar Olá TTL de seus blobs.  Usando o navegador [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), teste se o blob é incluindo Olá *Cache-Control* cabeçalho de resposta.  Você também pode usar uma ferramenta como **wget**, [carteiro](https://www.getpostman.com/), ou [Fiddler](http://www.telerik.com/fiddler) tooexamine cabeçalhos de resposta de saudação.

## <a name="next-steps"></a>Próximas etapas
* [Leia sobre Olá *Cache-Control* cabeçalho](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Saiba como toomanage expiração de conteúdo do serviço de nuvem no Azure CDN](cdn-manage-expiration-of-cloud-service-content.md)

