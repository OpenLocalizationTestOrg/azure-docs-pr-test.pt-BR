---
title: "associações de funções Cosmos DB aaaAzure | Microsoft Docs"
description: "Entender como associações de banco de dados do Azure Cosmos toouse em funções do Azure."
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
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="853e5-104">Associações do Banco de Dados Cosmos do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="853e5-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="853e5-105">Este artigo explica como as associações de banco de dados do Azure Cosmos tooconfigure e código em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="853e5-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="853e5-106">O Azure Functions dá suporte a associações de entrada e saída para o Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="853e5-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="853e5-107">Para obter mais informações sobre o banco de dados do Cosmos, consulte [tooCosmos Introdução DB](../documentdb/documentdb-introduction.md) e [criar um aplicativo de console de banco de dados do Cosmos](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="853e5-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="853e5-108">Associação de entrada da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="853e5-108">DocumentDB API input binding</span></span>
<span data-ttu-id="853e5-109">Olá associação de entrada da API DocumentDB recupera um documento de banco de dados do Cosmos e passa toohello nomeado o parâmetro de entrada da função hello.</span><span class="sxs-lookup"><span data-stu-id="853e5-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="853e5-110">documento Hello que ID pode ser determinado com base no disparador Olá que invoca a função hello.</span><span class="sxs-lookup"><span data-stu-id="853e5-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="853e5-111">Olá associação de entrada da API do DocumentDB tem Olá seguintes propriedades em *function.json*:</span><span class="sxs-lookup"><span data-stu-id="853e5-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="853e5-112">`name`: Nome de identificador usado no código de função para documento Olá</span><span class="sxs-lookup"><span data-stu-id="853e5-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="853e5-113">`type`: deve ser definido muito "documentos"</span><span class="sxs-lookup"><span data-stu-id="853e5-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="853e5-114">`databaseName`: banco de dados de saudação que contém o documento de saudação</span><span class="sxs-lookup"><span data-stu-id="853e5-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="853e5-115">`collectionName`: coleta Olá que contém o documento de saudação</span><span class="sxs-lookup"><span data-stu-id="853e5-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="853e5-116">`id`: Olá Id da saudação tooretrieve de documento.</span><span class="sxs-lookup"><span data-stu-id="853e5-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="853e5-117">Essa propriedade oferece suporte a parâmetros de associações; consulte [ligar as propriedades de entrada toocustom em uma expressão de associação](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) artigo Olá [gatilhos de funções do Azure e conceitos de associações](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="853e5-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="853e5-118">`sqlQuery`: uma consulta SQL do Banco de Dados Cosmos usada para recuperar vários documentos.</span><span class="sxs-lookup"><span data-stu-id="853e5-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="853e5-119">consulta de saudação dá suporte a associações de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="853e5-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="853e5-120">Por exemplo: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="853e5-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="853e5-121">`connection`: nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão do banco de dados do Cosmos</span><span class="sxs-lookup"><span data-stu-id="853e5-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="853e5-122">`direction`: deve ser definido muito`"in"`.</span><span class="sxs-lookup"><span data-stu-id="853e5-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="853e5-123">Olá propriedades `id` e `sqlQuery` não podem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="853e5-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="853e5-124">Se nem `id` nem `sqlQuery` for definida, hello toda coleção é recuperada.</span><span class="sxs-lookup"><span data-stu-id="853e5-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="853e5-125">Utilizar uma associação de entrada de API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="853e5-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="853e5-126">Em c# e F # funções, quando a função hello encerrada com êxito, qualquer alteração feita toohello o documento de entrada por meio de parâmetros de entrada nomeados é automaticamente persistidas.</span><span class="sxs-lookup"><span data-stu-id="853e5-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="853e5-127">Funções de JavaScript, as atualizações não são feitas automaticamente após a saída da função.</span><span class="sxs-lookup"><span data-stu-id="853e5-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="853e5-128">Em vez disso, use `context.bindings.<documentName>In` e `context.bindings.<documentName>Out` toomake atualizações.</span><span class="sxs-lookup"><span data-stu-id="853e5-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="853e5-129">Consulte Olá [JavaScript exemplo](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="853e5-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="853e5-130">Exemplo de entrada para um único documento</span><span class="sxs-lookup"><span data-stu-id="853e5-130">Input sample for single document</span></span>
<span data-ttu-id="853e5-131">Suponha que você tenha a seguinte Olá API DocumentDB entrada associação em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="853e5-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="853e5-132">Consulte Olá específico do idioma exemplo que usa o valor de texto do documento associação de entrada tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="853e5-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="853e5-133">C#</span><span class="sxs-lookup"><span data-stu-id="853e5-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="853e5-134">F#</span><span class="sxs-lookup"><span data-stu-id="853e5-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="853e5-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="853e5-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="853e5-136">Exemplo de entrada em C#</span><span class="sxs-lookup"><span data-stu-id="853e5-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="853e5-137">Exemplo de entrada em F#</span><span class="sxs-lookup"><span data-stu-id="853e5-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="853e5-138">Este exemplo requer uma `project.json` arquivo Especifica Olá `FSharp.Interop.Dynamic` e `Dynamitey` dependências do NuGet:</span><span class="sxs-lookup"><span data-stu-id="853e5-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="853e5-139">tooadd um `project.json` de arquivos, consulte [gerenciamento de pacotes do F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="853e5-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="853e5-140">Amostra de entrada no JavaScript</span><span class="sxs-lookup"><span data-stu-id="853e5-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="853e5-141">Exemplo de entrada com vários documentos</span><span class="sxs-lookup"><span data-stu-id="853e5-141">Input sample with multiple documents</span></span>

<span data-ttu-id="853e5-142">Suponha que você deseja tooretrieve vários documentos especificados por uma consulta SQL, usando parâmetros de consulta uma fila gatilho toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="853e5-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="853e5-143">Neste exemplo, o gatilho de fila Olá fornece um parâmetro `departmentId`. Uma mensagem da fila de `{ "departmentId" : "Finance" }` retornará todos os registros para o departamento de finanças hello.</span><span class="sxs-lookup"><span data-stu-id="853e5-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="853e5-144">Use a seguinte Olá no *function.json*:</span><span class="sxs-lookup"><span data-stu-id="853e5-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="853e5-145">Exemplo de entrada com vários documentos em C#</span><span class="sxs-lookup"><span data-stu-id="853e5-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="853e5-146">Exemplo de entrada com vários documentos em JavaScript</span><span class="sxs-lookup"><span data-stu-id="853e5-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="853e5-147"><a id="docdboutput"></a>Associação de saída da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="853e5-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="853e5-148">Olá API DocumentDB associação permite que você escreva um novo documento tooan banco de dados do Azure Cosmos banco de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="853e5-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="853e5-149">Ele tem Olá seguintes propriedades em *function.json*:</span><span class="sxs-lookup"><span data-stu-id="853e5-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="853e5-150">`name`: O identificador usado no código de função para Olá novo documento</span><span class="sxs-lookup"><span data-stu-id="853e5-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="853e5-151">`type`: deve ser definido muito`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="853e5-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="853e5-152">`databaseName`: banco de dados de saudação que contém a coleção Olá onde Olá novo documento será criado.</span><span class="sxs-lookup"><span data-stu-id="853e5-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="853e5-153">`collectionName`: Olá coleção onde Olá novo documento será criado.</span><span class="sxs-lookup"><span data-stu-id="853e5-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="853e5-154">`createIfNotExists`: Um valor booleano tooindicate se Olá coleção será criada se não existir.</span><span class="sxs-lookup"><span data-stu-id="853e5-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="853e5-155">saudação padrão é *false*.</span><span class="sxs-lookup"><span data-stu-id="853e5-155">hello default is *false*.</span></span> <span data-ttu-id="853e5-156">Olá motivo para isso é uma novidade as coleções são criadas com a taxa de transferência reservada que tem implicações de preços.</span><span class="sxs-lookup"><span data-stu-id="853e5-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="853e5-157">Para obter mais detalhes, visite Olá [página de preços](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="853e5-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="853e5-158">`connection`: nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão do banco de dados do Cosmos</span><span class="sxs-lookup"><span data-stu-id="853e5-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="853e5-159">`direction`: deve ser definido muito`"out"`</span><span class="sxs-lookup"><span data-stu-id="853e5-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="853e5-160">Usar uma associação de saída de API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="853e5-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="853e5-161">Esta seção mostra como toouse sua API de documentos de saída no seu código de função de associação.</span><span class="sxs-lookup"><span data-stu-id="853e5-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="853e5-162">Quando você escreve um parâmetro de saída toohello na sua função, por padrão, que um novo documento é gerado no banco de dados, com um GUID gerado automaticamente como Olá documento ID.</span><span class="sxs-lookup"><span data-stu-id="853e5-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="853e5-163">Você pode especificar a ID do documento de saudação do documento de saída especificando Olá `id` propriedade JSON em Olá parâmetro de saída.</span><span class="sxs-lookup"><span data-stu-id="853e5-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="853e5-164">Quando você especificar Olá ID de um documento existente, ele obtém substituído por novo documento de saída hello.</span><span class="sxs-lookup"><span data-stu-id="853e5-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="853e5-165">toooutput vários documentos, você também pode associar muito`ICollector<T>` ou `IAsyncCollector<T>` onde `T` é um dos tipos de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="853e5-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="853e5-166">Exemplo de associação de saída da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="853e5-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="853e5-167">Suponha que você tenha a seguinte Olá API DocumentDB saída associação em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="853e5-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="853e5-168">E você tem uma associação de entrada de fila para uma fila que recebe o JSON no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="853e5-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="853e5-169">E toocreate Cosmos DB documentos em Olá formato para cada registro a seguir:</span><span class="sxs-lookup"><span data-stu-id="853e5-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="853e5-170">Consulte Olá específico do idioma exemplo que usa essa saída associação tooadd documentos tooyour banco de dados.</span><span class="sxs-lookup"><span data-stu-id="853e5-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="853e5-171">C#</span><span class="sxs-lookup"><span data-stu-id="853e5-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="853e5-172">F#</span><span class="sxs-lookup"><span data-stu-id="853e5-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="853e5-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="853e5-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="853e5-174">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="853e5-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="853e5-175">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="853e5-175">Output sample in F#</span></span> #

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

<span data-ttu-id="853e5-176">Este exemplo requer uma `project.json` arquivo Especifica Olá `FSharp.Interop.Dynamic` e `Dynamitey` dependências do NuGet:</span><span class="sxs-lookup"><span data-stu-id="853e5-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="853e5-177">tooadd um `project.json` de arquivos, consulte [gerenciamento de pacotes do F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="853e5-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="853e5-178">Amostra de saída no JavaScript</span><span class="sxs-lookup"><span data-stu-id="853e5-178">Output sample in JavaScript</span></span>

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
