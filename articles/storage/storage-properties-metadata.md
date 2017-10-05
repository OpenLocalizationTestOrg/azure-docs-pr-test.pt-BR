---
title: Definir e recuperar as propriedades e os metadados para objetos no Armazenamento do Azure | Microsoft Docs
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
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="cda83-103">Definir e recuperar as propriedades e os metadados</span><span class="sxs-lookup"><span data-stu-id="cda83-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="cda83-104">Os objetos no armazenamento do Azure oferecem suporte às propriedades do sistema e metadados definidos pelo usuário, além dos dados que eles contêm.</span><span class="sxs-lookup"><span data-stu-id="cda83-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="cda83-105">Este artigo discute o gerenciamento das propriedades do sistema e dos metadados definidos pelo usuário com a [Biblioteca de clientes de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="cda83-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="cda83-106">**Propriedades do sistema**: existem propriedades do sistema em cada recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cda83-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="cda83-107">Algumas podem ser lidas ou definidas, enquanto outras são de somente leitura.</span><span class="sxs-lookup"><span data-stu-id="cda83-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="cda83-108">Internamente, algumas propriedades do sistema correspondem a certos cabeçalhos HTTP padrão.</span><span class="sxs-lookup"><span data-stu-id="cda83-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="cda83-109">A biblioteca de cliente do armazenamento do Azure os mantém para você.</span><span class="sxs-lookup"><span data-stu-id="cda83-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="cda83-110">**Metadados definidos pelo usuário**: Os metadados definidos pelo usuário são metadados que você especifica em um determinado recurso, na forma de um par de nome-valor.</span><span class="sxs-lookup"><span data-stu-id="cda83-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="cda83-111">Você pode usar metadados para armazenar valores adicionais com um recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cda83-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="cda83-112">Esses valores de metadados adicionais são apenas para suas próprias finalidades e não afetam o comportamento do recurso.</span><span class="sxs-lookup"><span data-stu-id="cda83-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="cda83-113">Recuperar os valores da propriedade e dos metadados para um recurso de armazenamento é um processo de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="cda83-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="cda83-114">Antes de ler esses valores, é preciso buscá-los explicitamente chamando o método **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="cda83-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cda83-115">Os valores de propriedade e metadados para um recurso de armazenamento não são preenchidos, a menos que você chame um dos métodos **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="cda83-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="cda83-116">Você receberá um `400 Bad Request` se quaisquer pares de nome/valor contiverem caracteres não ASCII.</span><span class="sxs-lookup"><span data-stu-id="cda83-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="cda83-117">Pares de nome/valor de metadados são cabeçalhos HTTP válidos e, portanto, devem cumprir todas as restrições que regem cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="cda83-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="cda83-118">Portanto, recomendamos o uso da codificação de URL ou da codificação de Base64 para nomes e valores que contêm caracteres não ASCII.</span><span class="sxs-lookup"><span data-stu-id="cda83-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="cda83-119">Configurando e recuperando as propriedades</span><span class="sxs-lookup"><span data-stu-id="cda83-119">Setting and retrieving properties</span></span>
<span data-ttu-id="cda83-120">Para recuperar os valores da propriedade, chame o método **FetchAttributes** no blob ou no contêiner para preencher as propriedades e leia os valores.</span><span class="sxs-lookup"><span data-stu-id="cda83-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="cda83-121">Para definir as propriedades em um objeto, especifique o valor da propriedade, em seguida, chame o método **SetProperties** .</span><span class="sxs-lookup"><span data-stu-id="cda83-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="cda83-122">O exemplo de código a seguir cria um contêiner e escreve alguns dos valores da propriedade em uma janela do console.</span><span class="sxs-lookup"><span data-stu-id="cda83-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="cda83-123">Configurando e recuperando os metadados</span><span class="sxs-lookup"><span data-stu-id="cda83-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="cda83-124">Você pode especificar os metadados como um ou mais pares de nome-valor em um recurso de contêiner ou blob.</span><span class="sxs-lookup"><span data-stu-id="cda83-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="cda83-125">Para definir os metadados, adicione pares de nome-valor à coleção **Metadados** no recurso, em seguida, chame o método **SetMetadata** para salvar os valores no serviço.</span><span class="sxs-lookup"><span data-stu-id="cda83-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="cda83-126">O nome dos metadados deve estar em conformidade com as convenções de nomenclatura para os identificadores de C#.</span><span class="sxs-lookup"><span data-stu-id="cda83-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="cda83-127">O exemplo de código a seguir define os metadados em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="cda83-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="cda83-128">Um valor é definido usando o método **Add** da coleção.</span><span class="sxs-lookup"><span data-stu-id="cda83-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="cda83-129">O outro valor é definido usando a sintaxe implícita de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="cda83-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="cda83-130">Ambos são válidos.</span><span class="sxs-lookup"><span data-stu-id="cda83-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="cda83-131">Para recuperar os metadados, chame o método **FetchAttributes** no blob ou no contêiner para preencher a coleção **Metadados**, em seguida, leia os valores, conforme mostrado no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="cda83-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="cda83-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cda83-132">Next steps</span></span>
* [<span data-ttu-id="cda83-133">Biblioteca do cliente de armazenamento do Azure para a referência do .NET</span><span class="sxs-lookup"><span data-stu-id="cda83-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="cda83-134">Biblioteca do cliente de armazenamento do Azure para o pacote NuGet do .NET</span><span class="sxs-lookup"><span data-stu-id="cda83-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
