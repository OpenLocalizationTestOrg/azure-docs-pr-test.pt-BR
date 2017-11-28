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
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="ef4a6-103">Gerenciar a expiração dos blobs de Armazenamento do Azure na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ef4a6-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef4a6-104">Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="ef4a6-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="ef4a6-105">Serviço Blob do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ef4a6-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="ef4a6-106">Olá [do serviço blob](../storage/common/storage-introduction.md#blob-storage) na [armazenamento do Azure](../storage/common/storage-introduction.md) uma das várias origens baseado no Azure é integrada com o Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="ef4a6-107">Qualquer conteúdo de blob publicamente acessível pode ser armazenado em cache no Azure CDN até que o tempo de vida (TTL) seja decorrido.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="ef4a6-108">Olá TTL é determinado pelo Olá [ *Cache-Control* cabeçalho](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) na resposta HTTP de saudação do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="ef4a6-109">Você não pode escolher tooset nenhum TTL em um blob.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="ef4a6-110">Nesse caso, o Azure CDN aplica automaticamente um TTL padrão de sete dias.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="ef4a6-111">Para obter mais informações sobre como funciona o Azure CDN toospeed tooblobs de acesso e outros arquivos, consulte Olá [visão geral do Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef4a6-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="ef4a6-112">Para obter mais detalhes sobre Olá serviço de blob de armazenamento do Azure, consulte [conceitos do serviço Blob](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef4a6-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="ef4a6-113">Este tutorial demonstra várias maneiras que você pode definir o TTL da saudação em um blob no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="ef4a6-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef4a6-114">Azure PowerShell</span></span>
<span data-ttu-id="ef4a6-115">[O Azure PowerShell](/powershell/azure/overview) é uma saudação maneiras mais rápida e mais eficiente tooadminister os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="ef4a6-116">Saudação de uso `Get-AzureStorageBlob` tooget cmdlet um blob de toohello de referência, em seguida, defina Olá `.ICloudBlob.Properties.CacheControl` propriedade.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

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
> <span data-ttu-id="ef4a6-117">Você também pode usar o PowerShell muito[gerenciar os perfis CDN e os pontos de extremidade](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ef4a6-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="ef4a6-118">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="ef4a6-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="ef4a6-119">tooset um blob do TTL usando .NET, use Olá [biblioteca de cliente de armazenamento do Azure para .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset Olá [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) propriedade.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

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
> <span data-ttu-id="ef4a6-120">Há muitos exemplos de código .NET mais disponíveis no hello [exemplos de armazenamento de Blob do Azure para .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="ef4a6-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="ef4a6-121">Outros métodos</span><span class="sxs-lookup"><span data-stu-id="ef4a6-121">Other methods</span></span>
* [<span data-ttu-id="ef4a6-122">Interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="ef4a6-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="ef4a6-123">Ao carregar o blob hello, defina Olá *cacheControl* propriedade usando Olá `-p` alternar.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="ef4a6-124">Este exemplo define a hora de tooone TTL de saudação (3.600 segundos).</span><span class="sxs-lookup"><span data-stu-id="ef4a6-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="ef4a6-125">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ef4a6-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="ef4a6-126">Explicitamente o conjunto Olá *x-ms---controle de cache blob* propriedade em uma [Blob Put](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [colocar lista de blocos](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), ou [definir propriedades de Blob](https://msdn.microsoft.com/library/azure/ee691966.aspx) solicitação.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="ef4a6-127">Ferramentas de gerenciamento de armazenamento de terceiros</span><span class="sxs-lookup"><span data-stu-id="ef4a6-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="ef4a6-128">Algumas ferramentas de gerenciamento de armazenamento do Azure de terceiros permitem Olá tooset *CacheControl* propriedade em blobs.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="ef4a6-129">Olá teste *Cache-Control* cabeçalho</span><span class="sxs-lookup"><span data-stu-id="ef4a6-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="ef4a6-130">Você pode facilmente verificar Olá TTL de seus blobs.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="ef4a6-131">Usando o navegador [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), teste se o blob é incluindo Olá *Cache-Control* cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="ef4a6-132">Você também pode usar uma ferramenta como **wget**, [carteiro](https://www.getpostman.com/), ou [Fiddler](http://www.telerik.com/fiddler) tooexamine cabeçalhos de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef4a6-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef4a6-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef4a6-133">Next Steps</span></span>
* [<span data-ttu-id="ef4a6-134">Leia sobre Olá *Cache-Control* cabeçalho</span><span class="sxs-lookup"><span data-stu-id="ef4a6-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="ef4a6-135">Saiba como toomanage expiração de conteúdo do serviço de nuvem no Azure CDN</span><span class="sxs-lookup"><span data-stu-id="ef4a6-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

