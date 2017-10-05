---
title: "Associações do Banco de Dados Cosmos do Azure Functions | Microsoft Docs"
description: "Entenda como usar associações do Banco de Dados Cosmo do Azure no Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="0c888-104">Associações do Banco de Dados Cosmos do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0c888-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0c888-105">Este artigo explica como configurar e codificar associações do Banco de Dados Cosmos do Azure no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0c888-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="0c888-106">O Azure Functions dá suporte a associações de entrada e saída para o Banco de Dados Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0c888-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="0c888-107">Para saber mais sobre o Banco de Dados Cosmos, veja [Introdução ao Banco de Dados Cosmos](../documentdb/documentdb-introduction.md) e [Criar um aplicativo de console do Banco de Dados Cosmos](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c888-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="0c888-108">Associação de entrada da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c888-108">DocumentDB API input binding</span></span>
<span data-ttu-id="0c888-109">A associação de entrada da API do DocumentDB recupera um documento do Banco de Dados Cosmos e o passa ao parâmetro de entrada nomeada da função.</span><span class="sxs-lookup"><span data-stu-id="0c888-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="0c888-110">A ID do documento pode ser determinada com base no gatilho que invoca a função.</span><span class="sxs-lookup"><span data-stu-id="0c888-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="0c888-111">A associação de entrada da API do DocumentDB tem as seguintes propriedades em *function.json*:</span><span class="sxs-lookup"><span data-stu-id="0c888-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="0c888-112">`name` : nome do Identificador usado no código de função para o documento</span><span class="sxs-lookup"><span data-stu-id="0c888-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="0c888-113">`type` : deve ser definido como "documentdb"</span><span class="sxs-lookup"><span data-stu-id="0c888-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="0c888-114">`databaseName` : O banco de dados que contém o documento</span><span class="sxs-lookup"><span data-stu-id="0c888-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="0c888-115">`collectionName` : A coleção que contém o documento</span><span class="sxs-lookup"><span data-stu-id="0c888-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="0c888-116">`id` : a ID do documento a ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="0c888-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="0c888-117">Essa propriedade oferece suporte a parâmetros de associações; consulte [Associar a propriedades personalizadas de entrada em uma expressão de associação](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) no artigo [Conceitos de associações e gatilhos de funções do Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="0c888-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="0c888-118">`sqlQuery`: uma consulta SQL do Banco de Dados Cosmos usada para recuperar vários documentos.</span><span class="sxs-lookup"><span data-stu-id="0c888-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="0c888-119">A consulta oferece suporte a associações de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0c888-119">The query supports runtime bindings.</span></span> <span data-ttu-id="0c888-120">Por exemplo: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="0c888-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="0c888-121">`connection`: o nome da configuração do aplicativo que contém a cadeia de conexão do Banco de Dados Cosmos</span><span class="sxs-lookup"><span data-stu-id="0c888-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="0c888-122">`direction` : deve ser definido como `"in"`.</span><span class="sxs-lookup"><span data-stu-id="0c888-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="0c888-123">As propriedades `id` e `sqlQuery` não podem ser especificadas.</span><span class="sxs-lookup"><span data-stu-id="0c888-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="0c888-124">Se `id` nem `sqlQuery` estiver definido, toda a coleção é recuperada.</span><span class="sxs-lookup"><span data-stu-id="0c888-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="0c888-125">Utilizar uma associação de entrada de API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c888-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="0c888-126">Em funções C# e F#, todas as alterações feitas no documento de entrada por parâmetros de entrada nomeados são persistidas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0c888-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="0c888-127">Funções de JavaScript, as atualizações não são feitas automaticamente após a saída da função.</span><span class="sxs-lookup"><span data-stu-id="0c888-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="0c888-128">Em vez disso, use `context.bindings.<documentName>In` e `context.bindings.<documentName>Out` para fazer atualizações.</span><span class="sxs-lookup"><span data-stu-id="0c888-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="0c888-129">Consulte o [exemplo JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="0c888-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="0c888-130">Exemplo de entrada para um único documento</span><span class="sxs-lookup"><span data-stu-id="0c888-130">Input sample for single document</span></span>
<span data-ttu-id="0c888-131">Suponha que você tenha a seguinte associação de entrada da API do DocumentDB na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="0c888-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

<span data-ttu-id="0c888-132">Veja o exemplo de idioma específico que usa essa associação de entrada para atualizar o valor de texto do documento.</span><span class="sxs-lookup"><span data-stu-id="0c888-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="0c888-133">C#</span><span class="sxs-lookup"><span data-stu-id="0c888-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="0c888-134">F#</span><span class="sxs-lookup"><span data-stu-id="0c888-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="0c888-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c888-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="0c888-136">Exemplo de entrada em C#</span><span class="sxs-lookup"><span data-stu-id="0c888-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="0c888-137">Exemplo de entrada em F#</span><span class="sxs-lookup"><span data-stu-id="0c888-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="0c888-138">Esse exemplo requer um arquivo `project.json` que especifique as dependências `FSharp.Interop.Dynamic` e `Dynamitey` do NuGet:</span><span class="sxs-lookup"><span data-stu-id="0c888-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="0c888-139">Para adicionar um arquivo do `project.json`, veja [Gerenciamento de pacotes do F#](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="0c888-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="0c888-140">Amostra de entrada no JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c888-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="0c888-141">Exemplo de entrada com vários documentos</span><span class="sxs-lookup"><span data-stu-id="0c888-141">Input sample with multiple documents</span></span>

<span data-ttu-id="0c888-142">Suponha que você deseja recuperar vários documentos especificados por uma consulta SQL, usando um gatilho de fila para personalizar os parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="0c888-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="0c888-143">Neste exemplo, o gatilho de fila fornece um parâmetro `departmentId`. Uma mensagem da fila de `{ "departmentId" : "Finance" }` retornará todos os registros para o departamento financeiro.</span><span class="sxs-lookup"><span data-stu-id="0c888-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="0c888-144">Usar o seguinte em *function.json*:</span><span class="sxs-lookup"><span data-stu-id="0c888-144">Use the following in *function.json*:</span></span>

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="0c888-145">Exemplo de entrada com vários documentos em C#</span><span class="sxs-lookup"><span data-stu-id="0c888-145">Input sample with multiple documents in C#</span></span>

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="0c888-146">Exemplo de entrada com vários documentos em JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c888-146">Input sample with multiple documents in JavaScript</span></span>

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <span data-ttu-id="0c888-147"><a id="docdboutput"></a>Associação de saída da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c888-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="0c888-148">A associação de saída da API do DocumentDB permite que você escreva um novo documento em um banco de dados do Banco de Dados Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c888-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="0c888-149">O *function.json* especifica as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c888-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="0c888-150">`name` : nome do Identificador usado no código de função para o novo documento</span><span class="sxs-lookup"><span data-stu-id="0c888-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="0c888-151">`type` : deve ser definido como `"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="0c888-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="0c888-152">`databaseName` : o banco de dados que contém a coleção na qual o novo documento será criado.</span><span class="sxs-lookup"><span data-stu-id="0c888-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="0c888-153">`collectionName` : a coleção na qual o novo documento será criado.</span><span class="sxs-lookup"><span data-stu-id="0c888-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="0c888-154">`createIfNotExists` : é um valor booliano para indicar se a coleção será criada se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="0c888-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="0c888-155">O padrão é *false*.</span><span class="sxs-lookup"><span data-stu-id="0c888-155">The default is *false*.</span></span> <span data-ttu-id="0c888-156">O motivo para isso é que as novas coleções são criadas com a taxa de transferência reservada, o que tem implicações de preço.</span><span class="sxs-lookup"><span data-stu-id="0c888-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="0c888-157">Para obter mais detalhes, visite a [página de preços](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0c888-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="0c888-158">`connection`: o nome da configuração do aplicativo que contém a cadeia de conexão do Banco de Dados Cosmos</span><span class="sxs-lookup"><span data-stu-id="0c888-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="0c888-159">`direction` : deve ser definido como `"out"`</span><span class="sxs-lookup"><span data-stu-id="0c888-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="0c888-160">Usar uma associação de saída de API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c888-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="0c888-161">Esta seção mostra como usar a associação de saída da API do DocumentDB em seu código da função.</span><span class="sxs-lookup"><span data-stu-id="0c888-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="0c888-162">Quando você grava para o parâmetro de saída em sua função, por padrão um novo documento é gerado no banco de dados, com um GUID gerado automaticamente como a ID do documento.</span><span class="sxs-lookup"><span data-stu-id="0c888-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="0c888-163">Você pode especificar a ID do documento de saída, especificando a propriedade `id` JSON no parâmetro de saída.</span><span class="sxs-lookup"><span data-stu-id="0c888-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="0c888-164">Ao especificar a ID de um documento existente, ela é substituída pelo novo documento de saída.</span><span class="sxs-lookup"><span data-stu-id="0c888-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="0c888-165">Para obter vários documentos de saída, você também pode associar a `ICollector<T>` ou `IAsyncCollector<T>`, sendo `T` um dos tipos com suporte.</span><span class="sxs-lookup"><span data-stu-id="0c888-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="0c888-166">Exemplo de associação de saída da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c888-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="0c888-167">Suponha que você tenha a seguinte associação de saída da API do DocumentDB na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="0c888-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

<span data-ttu-id="0c888-168">E que você tenha uma associação de entrada de fila para uma fila que recebe o JSON no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="0c888-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="0c888-169">E você deseja criar documentos do Banco de Dados Cosmos no formato a seguir para cada registro:</span><span class="sxs-lookup"><span data-stu-id="0c888-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="0c888-170">Veja o exemplo de idioma específico que usa essa associação de saída para adicionar documentos ao seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0c888-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="0c888-171">C#</span><span class="sxs-lookup"><span data-stu-id="0c888-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="0c888-172">F#</span><span class="sxs-lookup"><span data-stu-id="0c888-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="0c888-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c888-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="0c888-174">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="0c888-174">Output sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="0c888-175">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="0c888-175">Output sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

<span data-ttu-id="0c888-176">Esse exemplo requer um arquivo `project.json` que especifique as dependências `FSharp.Interop.Dynamic` e `Dynamitey` do NuGet:</span><span class="sxs-lookup"><span data-stu-id="0c888-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="0c888-177">Para adicionar um arquivo do `project.json`, veja [Gerenciamento de pacotes do F#](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="0c888-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="0c888-178">Amostra de saída no JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c888-178">Output sample in JavaScript</span></span>

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
