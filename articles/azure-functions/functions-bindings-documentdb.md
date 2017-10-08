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
# <a name="azure-functions-cosmos-db-bindings"></a>Associações do Banco de Dados Cosmos do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como as associações de banco de dados do Azure Cosmos tooconfigure e código em funções do Azure. O Azure Functions dá suporte a associações de entrada e saída para o Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Para obter mais informações sobre o banco de dados do Cosmos, consulte [tooCosmos Introdução DB](../documentdb/documentdb-introduction.md) e [criar um aplicativo de console de banco de dados do Cosmos](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>Associação de entrada da API do DocumentDB
Olá associação de entrada da API DocumentDB recupera um documento de banco de dados do Cosmos e passa toohello nomeado o parâmetro de entrada da função hello. documento Hello que ID pode ser determinado com base no disparador Olá que invoca a função hello. 

Olá associação de entrada da API do DocumentDB tem Olá seguintes propriedades em *function.json*:

- `name`: Nome de identificador usado no código de função para documento Olá
- `type`: deve ser definido muito "documentos"
- `databaseName`: banco de dados de saudação que contém o documento de saudação
- `collectionName`: coleta Olá que contém o documento de saudação
- `id`: Olá Id da saudação tooretrieve de documento. Essa propriedade oferece suporte a parâmetros de associações; consulte [ligar as propriedades de entrada toocustom em uma expressão de associação](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) artigo Olá [gatilhos de funções do Azure e conceitos de associações](functions-triggers-bindings.md).
- `sqlQuery`: uma consulta SQL do Banco de Dados Cosmos usada para recuperar vários documentos. consulta de saudação dá suporte a associações de tempo de execução. Por exemplo: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão do banco de dados do Cosmos
- `direction`: deve ser definido muito`"in"`.

Olá propriedades `id` e `sqlQuery` não podem ser especificados. Se nem `id` nem `sqlQuery` for definida, hello toda coleção é recuperada.

## <a name="using-a-documentdb-api-input-binding"></a>Utilizar uma associação de entrada de API do DocumentDB

* Em c# e F # funções, quando a função hello encerrada com êxito, qualquer alteração feita toohello o documento de entrada por meio de parâmetros de entrada nomeados é automaticamente persistidas. 
* Funções de JavaScript, as atualizações não são feitas automaticamente após a saída da função. Em vez disso, use `context.bindings.<documentName>In` e `context.bindings.<documentName>Out` toomake atualizações. Consulte Olá [JavaScript exemplo](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Exemplo de entrada para um único documento
Suponha que você tenha a seguinte Olá API DocumentDB entrada associação em Olá `bindings` matriz de function.json:

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

Consulte Olá específico do idioma exemplo que usa o valor de texto do documento associação de entrada tooupdate hello.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Exemplo de entrada em C# #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Exemplo de entrada em F# #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

Este exemplo requer uma `project.json` arquivo Especifica Olá `FSharp.Interop.Dynamic` e `Dynamitey` dependências do NuGet:

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

tooadd um `project.json` de arquivos, consulte [gerenciamento de pacotes do F #](functions-reference-fsharp.md#package).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>Amostra de entrada no JavaScript

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Exemplo de entrada com vários documentos

Suponha que você deseja tooretrieve vários documentos especificados por uma consulta SQL, usando parâmetros de consulta uma fila gatilho toocustomize hello. 

Neste exemplo, o gatilho de fila Olá fornece um parâmetro `departmentId`. Uma mensagem da fila de `{ "departmentId" : "Finance" }` retornará todos os registros para o departamento de finanças hello. Use a seguinte Olá no *function.json*:

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

### <a name="input-sample-with-multiple-documents-in-c"></a>Exemplo de entrada com vários documentos em C#

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a>Exemplo de entrada com vários documentos em JavaScript

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

## <a id="docdboutput"></a>Associação de saída da API do DocumentDB
Olá API DocumentDB associação permite que você escreva um novo documento tooan banco de dados do Azure Cosmos banco de dados de saída. Ele tem Olá seguintes propriedades em *function.json*:

- `name`: O identificador usado no código de função para Olá novo documento
- `type`: deve ser definido muito`"documentdb"`
- `databaseName`: banco de dados de saudação que contém a coleção Olá onde Olá novo documento será criado.
- `collectionName`: Olá coleção onde Olá novo documento será criado.
- `createIfNotExists`: Um valor booleano tooindicate se Olá coleção será criada se não existir. saudação padrão é *false*. Olá motivo para isso é uma novidade as coleções são criadas com a taxa de transferência reservada que tem implicações de preços. Para obter mais detalhes, visite Olá [página de preços](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão do banco de dados do Cosmos
- `direction`: deve ser definido muito`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Usar uma associação de saída de API do DocumentDB
Esta seção mostra como toouse sua API de documentos de saída no seu código de função de associação.

Quando você escreve um parâmetro de saída toohello na sua função, por padrão, que um novo documento é gerado no banco de dados, com um GUID gerado automaticamente como Olá documento ID. Você pode especificar a ID do documento de saudação do documento de saída especificando Olá `id` propriedade JSON em Olá parâmetro de saída. 

>[!Note]  
>Quando você especificar Olá ID de um documento existente, ele obtém substituído por novo documento de saída hello. 

toooutput vários documentos, você também pode associar muito`ICollector<T>` ou `IAsyncCollector<T>` onde `T` é um dos tipos de saudação com suporte.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>Exemplo de associação de saída da API do DocumentDB
Suponha que você tenha a seguinte Olá API DocumentDB saída associação em Olá `bindings` matriz de function.json:

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

E você tem uma associação de entrada de fila para uma fila que recebe o JSON no hello formato a seguir:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

E toocreate Cosmos DB documentos em Olá formato para cada registro a seguir:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Consulte Olá específico do idioma exemplo que usa essa saída associação tooadd documentos tooyour banco de dados.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Amostra de saída em C# #

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

### <a name="output-sample-in-f"></a>Amostra de saída em F# #

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

Este exemplo requer uma `project.json` arquivo Especifica Olá `FSharp.Interop.Dynamic` e `Dynamitey` dependências do NuGet:

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

tooadd um `project.json` de arquivos, consulte [gerenciamento de pacotes do F #](functions-reference-fsharp.md#package).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>Amostra de saída no JavaScript

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
