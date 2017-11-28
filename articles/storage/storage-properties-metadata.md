---
title: objeto de aaaSet e recuperar propriedades e metadados no armazenamento do Azure | Microsoft Docs
description: Armazene metadados personalizados em objetos no Armazenamento do Azure e defina e recupere propriedades do sistema.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="392e9-103">Definir e recuperar as propriedades e os metadados</span><span class="sxs-lookup"><span data-stu-id="392e9-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="392e9-104">Objetos nas propriedades de suporte do sistema de armazenamento do Azure e metadados definidos pelo usuário, além de toohello dados que eles contêm.</span><span class="sxs-lookup"><span data-stu-id="392e9-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="392e9-105">Este artigo aborda as propriedades do sistema de gerenciamento e os metadados definidos pelo usuário com hello [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="392e9-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="392e9-106">**Propriedades do sistema**: existem propriedades do sistema em cada recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="392e9-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="392e9-107">Algumas podem ser lidas ou definidas, enquanto outras são de somente leitura.</span><span class="sxs-lookup"><span data-stu-id="392e9-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="392e9-108">Em Olá oculta, algumas propriedades de sistema correspondem toocertain os cabeçalhos HTTP padrão.</span><span class="sxs-lookup"><span data-stu-id="392e9-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="392e9-109">biblioteca de cliente de armazenamento do Azure Olá mantém para você.</span><span class="sxs-lookup"><span data-stu-id="392e9-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="392e9-110">**Metadados definidos pelo usuário**: metadados definidos pelo usuário são metadados que você especificar um determinado recurso na forma de saudação de um par nome-valor.</span><span class="sxs-lookup"><span data-stu-id="392e9-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="392e9-111">Você pode usar os valores de metadados toostore adicionais com um recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="392e9-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="392e9-112">Esses valores de metadados adicionais são usados para seus próprios fins apenas e não afetam o comportamento do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="392e9-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="392e9-113">Recuperar os valores da propriedade e dos metadados para um recurso de armazenamento é um processo de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="392e9-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="392e9-114">Antes de ler esses valores, você deve buscá-los explicitamente por chamada hello **FetchAttributes** método.</span><span class="sxs-lookup"><span data-stu-id="392e9-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="392e9-115">Valores de propriedades e metadados para um recurso de armazenamento não são preenchidos, a menos que você chame um dos Olá **FetchAttributes** métodos.</span><span class="sxs-lookup"><span data-stu-id="392e9-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="392e9-116">Você receberá um `400 Bad Request` se quaisquer pares de nome/valor contiverem caracteres não ASCII.</span><span class="sxs-lookup"><span data-stu-id="392e9-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="392e9-117">Pares de nome/valor de metadados são cabeçalhos HTTP válidos e, portanto, deve aderir tooall restrições que regem cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="392e9-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="392e9-118">Portanto, recomendamos o uso da codificação de URL ou da codificação de Base64 para nomes e valores que contêm caracteres não ASCII.</span><span class="sxs-lookup"><span data-stu-id="392e9-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="392e9-119">Configurando e recuperando as propriedades</span><span class="sxs-lookup"><span data-stu-id="392e9-119">Setting and retrieving properties</span></span>
<span data-ttu-id="392e9-120">valores de propriedade tooretrieve, chamada hello **FetchAttributes** método em seu contêiner ou blob toopopulate Olá propriedades, em seguida, ler valores hello.</span><span class="sxs-lookup"><span data-stu-id="392e9-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="392e9-121">tooset propriedades em um objeto, especifique o valor da propriedade hello e chame Olá **SetProperties** método.</span><span class="sxs-lookup"><span data-stu-id="392e9-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="392e9-122">Olá exemplo de código a seguir cria um contêiner, em seguida, grava alguns sua janela de console de tooa de valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="392e9-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="392e9-123">Configurando e recuperando os metadados</span><span class="sxs-lookup"><span data-stu-id="392e9-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="392e9-124">Você pode especificar os metadados como um ou mais pares de nome-valor em um recurso de contêiner ou blob.</span><span class="sxs-lookup"><span data-stu-id="392e9-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="392e9-125">metadados tooset, adicionar pares nome-valor toohello **metadados** coleção no recurso hello, em seguida, chamar hello **SetMetadata** saudação do método toosave valores toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="392e9-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="392e9-126">nome de saudação dos metadados deve obedecer toohello convenções de nomenclatura dos identificadores c#.</span><span class="sxs-lookup"><span data-stu-id="392e9-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="392e9-127">Olá exemplo de código a seguir define metadados em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="392e9-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="392e9-128">Um valor é definido usando a coleção de saudação **adicionar** método.</span><span class="sxs-lookup"><span data-stu-id="392e9-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="392e9-129">Olá outro valor é definido usando a sintaxe de chave/valor implícito.</span><span class="sxs-lookup"><span data-stu-id="392e9-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="392e9-130">Ambos são válidos.</span><span class="sxs-lookup"><span data-stu-id="392e9-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="392e9-131">metadados de tooretrieve, chamada hello **FetchAttributes** método no seu Olá toopopulate blob ou contêiner **metadados** coleção, em seguida, ler valores hello, conforme mostrado no exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="392e9-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="392e9-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="392e9-132">Next steps</span></span>
* [<span data-ttu-id="392e9-133">Biblioteca do cliente de armazenamento do Azure para a referência do .NET</span><span class="sxs-lookup"><span data-stu-id="392e9-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="392e9-134">Biblioteca do cliente de armazenamento do Azure para o pacote NuGet do .NET</span><span class="sxs-lookup"><span data-stu-id="392e9-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
