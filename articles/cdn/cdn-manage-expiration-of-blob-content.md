---
title: "Gerenciar a expiração dos blobs de Armazenamento do Azure na CDN do Azure | Microsoft Docs"
description: "Aprenda sobre as opções para controlar a vida útil de blobs no cache do Azure CDN."
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
ms.openlocfilehash: d4741921806e443d92c385a04b781cec296c2ae8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="df3a8-103">Gerenciar a expiração dos blobs de Armazenamento do Azure na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="df3a8-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="df3a8-104">Serviços de Nuvem/Aplicativos Web do Azure, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="df3a8-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="df3a8-105">Serviço Blob do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="df3a8-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="df3a8-106">O [serviço blob](../storage/common/storage-introduction.md#blob-storage) no [Armazenamento do Azure](../storage/common/storage-introduction.md) é uma das várias origens baseadas no Azure integrada à CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="df3a8-106">The [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="df3a8-107">Qualquer conteúdo de blob publicamente acessível pode ser armazenado em cache no Azure CDN até que o tempo de vida (TTL) seja decorrido.</span><span class="sxs-lookup"><span data-stu-id="df3a8-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="df3a8-108">O TTL é determinado pelo [*Controle de Cache* ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) na resposta HTTP do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="df3a8-108">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="df3a8-109">Você pode optar por não definir nenhum TTL em um blob.</span><span class="sxs-lookup"><span data-stu-id="df3a8-109">You may choose to set no TTL on a blob.</span></span>  <span data-ttu-id="df3a8-110">Nesse caso, o Azure CDN aplica automaticamente um TTL padrão de sete dias.</span><span class="sxs-lookup"><span data-stu-id="df3a8-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="df3a8-111">Para obter mais informações sobre como a CDN do Azure trabalha para acelerar o acesso aos blobs e a outros arquivos, consulte a [Visão geral da CDN do Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df3a8-111">For more information about how Azure CDN works to speed up access to blobs and other files, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="df3a8-112">Para obter mais detalhes sobre o serviço Azure Storage Blob, consulte [Conceitos do serviço Blob](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="df3a8-112">For more details on the Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="df3a8-113">Este tutorial demonstra várias maneiras que você pode definir o TTL em um blob no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="df3a8-113">This tutorial demonstrates several ways that you can set the TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="df3a8-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df3a8-114">Azure PowerShell</span></span>
<span data-ttu-id="df3a8-115">[Azure PowerShell](/powershell/azure/overview) é uma das maneiras mais rápidas e eficientes de administrar os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="df3a8-115">[Azure PowerShell](/powershell/azure/overview) is one of the quickest, most powerful ways to administer your Azure services.</span></span>  <span data-ttu-id="df3a8-116">Use o cmdlet `Get-AzureStorageBlob` para obter uma referência para o blob, em seguida, defina a propriedade `.ICloudBlob.Properties.CacheControl`.</span><span class="sxs-lookup"><span data-stu-id="df3a8-116">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="df3a8-117">Você também pode usar o PowerShell para [gerenciar os perfis e os pontos de extremidade da CDN](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="df3a8-117">You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="df3a8-118">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="df3a8-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="df3a8-119">Para definir o TTL de um blob usando o .NET, use a [Biblioteca do Cliente de Armazenamento do Azure para .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) para definir a propriedade [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx).</span><span class="sxs-lookup"><span data-stu-id="df3a8-119">To set a blob's TTL using .NET, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="df3a8-120">Existem muitos exemplos de código .NET disponíveis nos [Exemplos de Armazenamento de Blobs do Azure para .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="df3a8-120">There are many more .NET code samples available in the [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="df3a8-121">Outros métodos</span><span class="sxs-lookup"><span data-stu-id="df3a8-121">Other methods</span></span>
* [<span data-ttu-id="df3a8-122">Interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="df3a8-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="df3a8-123">Ao carregar o blob, defina a propriedade *cacheControl* usando o argumento `-p`.</span><span class="sxs-lookup"><span data-stu-id="df3a8-123">When uploading the blob, set the *cacheControl* property using the `-p` switch.</span></span>  <span data-ttu-id="df3a8-124">Este exemplo define o TTL para uma hora (3.600 segundos).</span><span class="sxs-lookup"><span data-stu-id="df3a8-124">This example sets the TTL to one hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="df3a8-125">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="df3a8-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="df3a8-126">Defina explicitamente a propriedade *x-ms-blob-cache-control* em uma solicitação [Put Block](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), ou [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx).</span><span class="sxs-lookup"><span data-stu-id="df3a8-126">Explicitly set the *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="df3a8-127">Ferramentas de gerenciamento de armazenamento de terceiros</span><span class="sxs-lookup"><span data-stu-id="df3a8-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="df3a8-128">Algumas ferramentas de gerenciamento de Armazenamento do Azure de terceiros permitem que você defina a propriedade *CacheControl* em blobs.</span><span class="sxs-lookup"><span data-stu-id="df3a8-128">Some third-party Azure Storage management tools allow you to set the *CacheControl* property on blobs.</span></span> 

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="df3a8-129">Testando o cabeçalho de *Controle de Cache*</span><span class="sxs-lookup"><span data-stu-id="df3a8-129">Testing the *Cache-Control* header</span></span>
<span data-ttu-id="df3a8-130">Você pode verificar facilmente a TTL de seus blobs.</span><span class="sxs-lookup"><span data-stu-id="df3a8-130">You can easily verify the TTL of your blobs.</span></span>  <span data-ttu-id="df3a8-131">Usando as [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)do seu navegador, teste se o blob está incluso no cabeçalho de resposta de *Controle de Cache* .</span><span class="sxs-lookup"><span data-stu-id="df3a8-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including the *Cache-Control* response header.</span></span>  <span data-ttu-id="df3a8-132">Você também pode usar uma ferramenta como **wget**, [Postman](https://www.getpostman.com/) ou [Fiddler](http://www.telerik.com/fiddler) para examinar os cabeçalhos de resposta.</span><span class="sxs-lookup"><span data-stu-id="df3a8-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df3a8-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df3a8-133">Next Steps</span></span>
* [<span data-ttu-id="df3a8-134">Leia sobre o cabeçalho *Cache-Control*</span><span class="sxs-lookup"><span data-stu-id="df3a8-134">Read about the *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="df3a8-135">Saiba como gerenciar a expiração do conteúdo do Serviço de Nuvem na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="df3a8-135">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

