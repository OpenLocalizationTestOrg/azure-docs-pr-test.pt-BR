---
title: "aaaWork com disparadores e associações em funções do Azure | Microsoft Docs"
description: "Saiba como toouse dispara e associações em funções do Azure tooconnect seus eventos de tooonline de execução de código e serviços baseados em nuvem."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Conceitos de gatilhos e de associações do Azure Functions
As funções do Azure permite toowrite código na resposta tooevents no Azure e outros serviços, pela *gatilhos* e *associações*. Este artigo é uma visão geral conceitual dos gatilhos e associações para todas as linguagens de programação com suporte. Recursos que são associações de tooall comuns são descritos aqui.

## <a name="overview"></a>Visão geral

Associações e gatilhos são uma forma declarativa toodefine como uma função é chamada e quais dados ele funciona com. Um *gatilho* define como uma função é invocada. Uma função deve ter exatamente um gatilho. Gatilhos com dados, que geralmente é carga Olá que disparou a função hello associados. 

Entrada e saída *associações* fornecem um toodata de tooconnect de forma declarativa de dentro de seu código. Tootriggers semelhante, você especificar cadeias de caracteres de conexão e outras propriedades na sua configuração de função. Associações são opcionais e uma função pode ter várias associações de entrada e saída. 

Usando gatilhos e associações, você pode escrever código que é mais genérico e não não codificar Olá detalhes dos serviços de saudação com a qual ele interage. Dados provenientes de serviços simplesmente tornam-se valores de entrada para o código de função. serviço toooutput de tooanother de dados (como criar uma nova linha no armazenamento de tabela do Azure), use o valor de retorno de saudação do método hello. Ou, se você precisar toooutput vários valores, use um objeto auxiliar. Gatilhos e associações possuem um **nome** propriedade, que é um identificador que você usa em sua associação de saudação do código tooaccess.

Você pode configurar associações e gatilhos Olá **integrar** no portal do Azure funções hello. Sob Olá coberturas, a saudação da interface do usuário modifica um arquivo chamado *function.json* arquivo no diretório de função hello. Você pode editar esse arquivo alterando toohello **editor avançado**.

Olá tabela a seguir mostra os gatilhos de saudação e associações que são compatíveis com funções do Azure. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Exemplo: gatilho de fila e associação de saída de tabela

Suponha que você queira toowrite um tooAzure de linha novo armazenamento de tabela sempre que uma nova mensagem é exibida no armazenamento de fila do Azure. Esse cenário pode ser implementado usando um gatilho de Filas do Azure e uma associação de saída de Tabela. 

Olá Olá informações a seguir exige que um gatilho de fila **integrar** guia:

* nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão de conta de armazenamento Olá para fila Olá
* nome da fila Olá
* Olá identificador em seu conteúdo de Olá tooread código de mensagem da fila de saudação, como `order`.

toowrite tooAzure armazenamento de tabela, use uma associação de saída com hello detalhes a seguir:

* nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão de conta de armazenamento Olá para tabela Olá
* nome da tabela Olá
* Identificador Olá toocreate seu código de saída itens ou valor de retorno de saudação do função hello.

Associações usam configurações do aplicativo para Olá tooenforce de cadeias de caracteres de conexão melhor práticas que *function.json* não contêm segredos de serviço.

Em seguida, use identificadores de saudação fornecido toointegrate com armazenamento do Azure no seu código.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Aqui está a saudação *function.json* que corresponde a toohello anterior do código. Observe que Olá a mesma configuração pode ser usada, independentemente do idioma de saudação da implementação da função hello.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
tooview e editar conteúdo de saudação do *function.json* no hello portal do Azure, clique em Olá **editor avançado** opção em Olá **integrar** guia de sua função.

Para ver exemplos de código e detalhes sobre a integração com o Armazenamento do Azure, consulte [Gatilhos e associações do Azure Functions para o Armazenamento do Azure](functions-bindings-storage.md).

### <a name="binding-direction"></a>Direção de associação

Todos os disparadores e associações têm uma propriedade `direction`:

- Para gatilhos, direção Olá é sempre`in`
- Associações de entrada e saída usam `in` e `out`
- Algumas associações dão suporte a uma direção especial `inout`. Se você usar `inout`, somente Olá **editor avançado** está disponível no hello **integrar** guia.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>Usando tooreturn tipo de retorno da função hello uma única saída

Olá exemplo anterior mostra como tooprovide de valor de retorno de função toouse Olá saída associação tooa, que é obtida usando o parâmetro de nome especial hello `$return`. (Isso tem suporte em linguagens que têm um valor retornado, como C#, JavaScript e F#.) Se uma função tiver várias associações de saída, use `$return` apenas para uma saudação de associações de saída. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

exemplos de saudação abaixo mostra como retornam tipos são usados com associações de saída em c#, JavaScript e F #.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>Associação da propriedade dataType

No .NET, use o tipo de dados do hello tipos toodefine Olá para dados de entrada. Por exemplo, use `string` toobind toohello texto de um gatilho de fila e um tooread de matriz de bytes como binário.

Para idiomas dinamicamente são digitados como JavaScript, use Olá `dataType` propriedade na definição de associação de saudação. Por exemplo, tooread Olá conteúdo de uma solicitação HTTP em formato binário, use o tipo de saudação `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Outras opções para `dataType` são `stream` e `string`.

## <a name="resolving-app-settings"></a>Resolvendo configurações de aplicativo
Como prática recomendada, os segredos e cadeias de conexão devem ser gerenciados usando configurações do aplicativo, em vez de arquivos de configuração. Isso limita o acesso toothese segredos e torna seguro toostore *function.json* em um repositório de controle de origem pública.

Configurações do aplicativo também são úteis sempre que quiser toochange configuração com base no ambiente de saudação. Por exemplo, em um ambiente de teste, convém toomonitor um contêiner de armazenamento de blob ou fila diferente.

Configurações do aplicativo são resolvidas sempre que um valor está entre sinais de porcentagem, como `%MyAppSetting%`. Observe que Olá `connection` é um caso especial de propriedade de gatilhos e associações e resolve automaticamente os valores de configurações do aplicativo. 

Olá, exemplo a seguir é um gatilho de fila que usa uma configuração de aplicativo `%input-queue-name%` toodefine Olá fila tootrigger em.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Propriedades de metadados de gatilho

Em adição toohello dados carga fornecida por um gatilho (como fila mensagem de saudação que disparou uma função), vários disparadores fornecem valores de metadados adicionais. Esses valores podem ser usados como parâmetros de entrada em c# e F # ou propriedades em Olá `context.bindings` objeto em JavaScript. 

Por exemplo, um gatilho de fila dá suporte a saudação propriedades a seguir:

* QueueTrigger – disparar o conteúdo da mensagem em caso de uma cadeia de caracteres válida
* DequeueCount
* ExpirationTime
* ID
* InsertionTime
* NextVisibleTime
* PopReceipt

Detalhes de propriedades de metadados para cada gatilho são descritos no tópico de referência correspondente hello. Documentação também está disponível em Olá **integrar** guia do portal hello, em Olá **documentação** seção abaixo da área de configuração de associação de saudação.  

Por exemplo, como gatilhos de blob tem alguns atrasos, você pode usar um toorun de gatilho de fila sua função (consulte [gatilho de armazenamento de Blob](functions-bindings-storage-blob.md#storage-blob-trigger). mensagem de saudação do fila conteria Olá blob filename tootrigger em. Usando Olá `queueTrigger` propriedade de metadados, você pode especificar esse comportamento em sua configuração, em vez de seu código.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Propriedades de metadados de um gatilho também podem ser usadas em uma *associação expressão* para outra associação, como Olá descrito na seção a seguir.

## <a name="binding-expressions-and-patterns"></a>Padrões e expressões de associação

Um dos recursos mais avançados de saudação de gatilhos e associações é *expressões de associação*. Dentro da associação, é possível definir expressões padrão que podem ser usadas em outras associações ou no seu código. Metadados de gatilho também podem ser usado em associação de expressões, como é mostrado no exemplo de Olá Olá anterior da seção.

Por exemplo, suponha que você deseja tooresize imagens no contêiner de armazenamento de blob específico, toohello semelhante **redimensionamento da imagem** modelo Olá **nova função** página. Vá muito**nova função** -> idioma **c#** -> cenário **exemplos** -> **ImageResizer CSharp**. 

Aqui está a saudação *function.json* definição:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Observe que Olá `filename` parâmetro é usado na definição de gatilho de blob hello, bem como blob Olá associação de saída. Esse parâmetro também pode ser usado no código de função.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>GUIDs aleatórios
As funções do Azure fornece uma sintaxe de conveniência para gerar GUIDs em suas associações, a saudação `{rand-guid}` expressão de associação. Olá, exemplo a seguir usa este toogenerate um nome exclusivo de blob: 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Hora atual

Você pode usar uma expressão de associação Olá `DateTime`, que resolve muito`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Associar propriedades de entrada toocustom em uma expressão de associação

Expressões de associação também podem referenciar as propriedades que são definidas na carga de gatilho Olá em si. Por exemplo, talvez você queira arquivo de armazenamento de blob toodynamically bind tooa de um nome de arquivo fornecido em um webhook.

Por exemplo, Olá a seguir *function.json* usa uma propriedade chamada `BlobName` da carga de gatilho Olá:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish esse em c# e F #, você deve definir um POCO que define os campos de saudação que serão desserializados na carga de gatilho hello.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

Em JavaScript, desserialização JSON é executada automaticamente e você pode usar propriedades de saudação diretamente.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Configuração de associação de dados em tempo de execução

Em c# e outras linguagens .NET, você pode usar um padrão de associação fundamental, como associações de toohello contrário declarativa em *function.json*. Associação fundamental é útil quando precisam de parâmetros de ligação toobe computado em tempo de execução, em vez de design. mais, consulte toolearn [associação em tempo de execução por meio de ligações fundamental](functions-reference-csharp.md#imperative-bindings) na referência do desenvolvedor Olá c#.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre uma associação específica, consulte Olá artigos a seguir:

- [HTTP e webhooks](functions-bindings-http-webhook.md)
- [Timer](functions-bindings-timer.md)
- [Armazenamento de filas](functions-bindings-storage-queue.md)
- [Armazenamento de Blobs](functions-bindings-storage-blob.md)
- [Armazenamento de tabelas](functions-bindings-storage-table.md)
- [Hub de Evento](functions-bindings-event-hubs.md)
- [Barramento de Serviço](functions-bindings-service-bus.md)
- [BD Cosmos](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Hubs de Notificação](functions-bindings-notification-hubs.md)
- [Aplicativos Móveis](functions-bindings-mobile-apps.md)
- [Arquivo externo](functions-bindings-external-file.md)
