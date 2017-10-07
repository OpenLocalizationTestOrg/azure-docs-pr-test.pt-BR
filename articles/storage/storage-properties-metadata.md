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
# <a name="set-and-retrieve-properties-and-metadata"></a>Definir e recuperar as propriedades e os metadados

Objetos nas propriedades de suporte do sistema de armazenamento do Azure e metadados definidos pelo usuário, além de toohello dados que eles contêm. Este artigo aborda as propriedades do sistema de gerenciamento e os metadados definidos pelo usuário com hello [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Propriedades do sistema**: existem propriedades do sistema em cada recurso de armazenamento. Algumas podem ser lidas ou definidas, enquanto outras são de somente leitura. Em Olá oculta, algumas propriedades de sistema correspondem toocertain os cabeçalhos HTTP padrão. biblioteca de cliente de armazenamento do Azure Olá mantém para você.

* **Metadados definidos pelo usuário**: metadados definidos pelo usuário são metadados que você especificar um determinado recurso na forma de saudação de um par nome-valor. Você pode usar os valores de metadados toostore adicionais com um recurso de armazenamento. Esses valores de metadados adicionais são usados para seus próprios fins apenas e não afetam o comportamento do recurso de saudação.

Recuperar os valores da propriedade e dos metadados para um recurso de armazenamento é um processo de duas etapas. Antes de ler esses valores, você deve buscá-los explicitamente por chamada hello **FetchAttributes** método.

> [!IMPORTANT]
> Valores de propriedades e metadados para um recurso de armazenamento não são preenchidos, a menos que você chame um dos Olá **FetchAttributes** métodos.
>
> Você receberá um `400 Bad Request` se quaisquer pares de nome/valor contiverem caracteres não ASCII. Pares de nome/valor de metadados são cabeçalhos HTTP válidos e, portanto, deve aderir tooall restrições que regem cabeçalhos HTTP. Portanto, recomendamos o uso da codificação de URL ou da codificação de Base64 para nomes e valores que contêm caracteres não ASCII.
>

## <a name="setting-and-retrieving-properties"></a>Configurando e recuperando as propriedades
valores de propriedade tooretrieve, chamada hello **FetchAttributes** método em seu contêiner ou blob toopopulate Olá propriedades, em seguida, ler valores hello.

tooset propriedades em um objeto, especifique o valor da propriedade hello e chame Olá **SetProperties** método.

Olá exemplo de código a seguir cria um contêiner, em seguida, grava alguns sua janela de console de tooa de valores de propriedade.

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

## <a name="setting-and-retrieving-metadata"></a>Configurando e recuperando os metadados
Você pode especificar os metadados como um ou mais pares de nome-valor em um recurso de contêiner ou blob. metadados tooset, adicionar pares nome-valor toohello **metadados** coleção no recurso hello, em seguida, chamar hello **SetMetadata** saudação do método toosave valores toohello serviço.

> [!NOTE]
> nome de saudação dos metadados deve obedecer toohello convenções de nomenclatura dos identificadores c#.
>
>

Olá exemplo de código a seguir define metadados em um contêiner. Um valor é definido usando a coleção de saudação **adicionar** método. Olá outro valor é definido usando a sintaxe de chave/valor implícito. Ambos são válidos.

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

metadados de tooretrieve, chamada hello **FetchAttributes** método no seu Olá toopopulate blob ou contêiner **metadados** coleção, em seguida, ler valores hello, conforme mostrado no exemplo hello abaixo.

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

## <a name="next-steps"></a>Próximas etapas
* [Biblioteca do cliente de armazenamento do Azure para a referência do .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Biblioteca do cliente de armazenamento do Azure para o pacote NuGet do .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
