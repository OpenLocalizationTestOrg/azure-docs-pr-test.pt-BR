---
title: "associações de armazenamento de Blob de funções aaaAzure | Microsoft Docs"
description: "Entenda como dispara toouse armazenamento do Azure e associações em funções do Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Associações de armazenamento de Blobs do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e trabalhar com associações de armazenamento de BLOBs do Azure em funções do Azure. O Azure Functions dá suporte a associações de entrada, saída e gatilho para o Azure Blob Storage. Para os recursos que estão disponíveis em todas as associações, veja [Gatilhos e conceitos de associações do Azure Functions](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> Não há suporte para [conta de armazenamento somente de blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts). Gatilhos de armazenamento de blobs e associações exigem uma conta de armazenamento de uso geral. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Gatilhos e associações de armazenamento de blobs

Usando um gatilho de armazenamento de BLOBs do Azure hello, seu código de função é chamado quando um blob novo ou atualizado é detectado. conteúdo do blob Olá é fornecido como entrada toohello função.

Definir um gatilho de armazenamento de blob usando Olá **integrar** no portal de funções hello. Olá, portal cria Olá após a definição no hello **associações** seção *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

Blob de entrada e saída associações são definidas usando `blob` como tipo de associação de saudação:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Olá `path` propriedade dá suporte à associação de expressões e parâmetros de filtro. Veja [Padrões de nome](#pattern).
* Olá `connection` propriedade deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento. No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você seleciona uma conta de armazenamento.

> [!NOTE]
> Quando você estiver usando um gatilho de blob em um plano de consumo, pode haver o atraso de 10 minutos tooa em processamento novos blobs depois que uma função de aplicativo estiver ocioso. Olá função aplicativo em execução, os blobs são processados imediatamente. tooavoid neste inicial atraso, considere uma saudação as opções a seguir:
> - Use um plano do Serviço de Aplicativo com a opçao Sempre ativado habilitada.
> - Use outro blob de saudação do tootrigger mecanismo de processamento, como uma mensagem da fila que contém o nome do blob hello. Para obter um exemplo, confira [Gatilho de fila com associação de entrada de blob](#input-sample).

<a name="pattern"></a>

### <a name="name-patterns"></a>Padrões de nome
Você pode especificar um padrão de nome de blob em Olá `path` propriedade, que pode ser uma expressão de filtro ou de associação. Veja [Padrões e expressões de associação](functions-triggers-bindings.md#binding-expressions-and-patterns).

Por exemplo, tooblobs toofilter que começam com a cadeia de caracteres hello "original", use Olá definição a seguir. Esse caminho localiza um blob denominado *original Blob1.txt* em Olá *entrada* contêiner e valor Olá Olá `name` variável no código da função é `Blob1`.

```json
"path": "input/original-{name}",
```

extensão e nome de arquivo de blob toobind toohello separadamente, usam dois padrões. Esse caminho também localiza um blob denominado *original Blob1.txt*e o valor de saudação do hello `blobname` e `blobextension` são variáveis no código de função *original Blob1* e *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

Você pode restringir o tipo de arquivo hello de blobs usando um valor fixo para a extensão de arquivo hello. Por exemplo, tootrigger somente em arquivos. png, use saudação padrão a seguir:

```json
"path": "samples/{name}.png",
```

As chaves são caracteres especiais nos padrões de nome. toospecify nomes de blob que têm chaves no nome hello, você pode sair chaves hello usando duas chaves. Olá, exemplo a seguir localiza um blob denominado *{20140101}-soundfile.mp3* em Olá *imagens* contêiner e hello `name` valor da variável no código da função hello é * soundfile.mp3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Metadados de gatilho

gatilho de blob Olá fornece várias propriedades de metadados. Essas propriedades podem ser usadas como parte de expressões de associações em outras associações ou como parâmetros em seu código. Esses valores têm Olá mesma semântica [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. Digite `string`. caminho de blob disparo Olá
- **Uri**. Digite `System.Uri`. URI do blob Olá local primário hello.
- **Propriedades**. Digite `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`. Olá propriedades do sistema do blob.
- **Metadados**. Digite `IDictionary<string,string>`. Olá metadados definidos pelo usuário para blob hello.

<a name="receipts"></a>

### <a name="blob-receipts"></a>Recebimentos de blob
Funções do Azure Olá runtime garante que nenhuma função de gatilho de blob é chamada mais de uma vez para Olá mesmo blob novo ou atualizado. toodetermine se uma versão de determinado blob tiver sido processada, ele mantém *recebimentos de blob*.

Repositórios de funções do Azure blob recebimentos em um contêiner chamado *hosts de trabalhos Web do azure* em Olá conta de armazenamento do Azure para seu aplicativo de função (definido pela configuração de aplicativo hello `AzureWebJobsStorage`). Confirmação de blob tem Olá informações a seguir:

* Olá disparou função ("*&lt;nome de função do aplicativo >*. Funções. * &lt;nome da função >*", por exemplo:"MyFunctionApp.Functions.CopyBlob")
* nome do contêiner Olá
* tipo de blob Hello ("BlockBlob" ou "PageBlob")
* nome do blob Olá
* Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

tooforce reprocessamento de um blob, excluir a confirmação de blob de saudação para esse blob da saudação *hosts de trabalhos Web do azure* contêiner manualmente.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Manipulação de blobs suspeitos
Quando uma função de gatilho de blob falhar para um determinado blob, o Azure Functions repete essa função até cinco vezes por padrão. 

Se todas as 5 tentativas falharem, funções do Azure adiciona uma fila de armazenamento de tooa mensagem denominada *webjobs-blobtrigger-suspeitas*. mensagem da fila Olá para blobs suspeitas é um objeto JSON que contém Olá propriedades a seguir:

* FunctionId (no formato de saudação * &lt;nome de função do aplicativo >*. Funções. * &lt;nome da função >*)
* BlobType ("BlockBlob" ou "PageBlob")
* ContainerName
* BlobName
* ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

### <a name="blob-polling-for-large-containers"></a>Sondagem de blobs para grandes contêineres
Se o contêiner de blob hello está sendo monitorado contém mais de 10.000 blobs, verificações de tempo de execução de funções de saudação log toowatch de arquivos para blobs novos ou alterados. Esse processo não ocorre em tempo real. Uma função não poderá obter disparada até vários minutos ou mais depois Olá blob é criado. Além disso, [logs de armazenamento são criados da "melhor forma dentro do possível"](/rest/api/storageservices/About-Storage-Analytics-Logging). Não há nenhuma garantia de que todos os eventos são capturados. Sob algumas condições, logs poderão ser perdidos. Se você precisar de processamento de blob mais rápida ou mais confiável, considere a criação de um [mensagem da fila](../storage/queues/storage-dotnet-how-to-use-queues.md) ao criar blob hello. Em seguida, use uma [gatilho fila](functions-bindings-storage-queue.md) em vez de um blob de saudação do blob gatilho tooprocess.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Usando um gatilho de blob e uma associação de entrada
Em funções do .NET, acessar dados de blob hello usando um parâmetro de método como `Stream paramName`. Aqui, `paramName` é Olá valor especificado em Olá [configuração do disparador](#trigger). Em funções do Node. js, Olá acesso entrada dados blob usando `context.bindings.<name>`.

No .NET, você pode associar tooany dos tipos de saudação na lista de saudação abaixo. Se for usado como uma associação de entrada, alguns desses tipos exigem uma direção de associação `inout` no *function.json*. Não há suporte para nessa direção pelo editor padrão do hello, portanto, você deve usar Olá editor avançado.

* `TextReader`
* `Stream`
* `ICloudBlob` (exige a direção de associação "inout")
* `CloudBlockBlob` (exige a direção de associação "inout")
* `CloudPageBlob` (exige a direção de associação "inout")
* `CloudAppendBlob` (exige a direção de associação "inout")

Se os blobs de texto são esperados, você também pode associar tooa .NET `string` tipo. Isso é recomendado somente se o tamanho do blob Olá é pequeno, como conteúdo de blob inteiro Olá é carregado na memória. Geralmente, é preferível toouse um `Stream` ou `CloudBlockBlob` tipo.

## <a name="trigger-sample"></a>Exemplo de gatilho
Suponha que você tenha Olá function.json que define um gatilho de armazenamento de blob a seguir:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

Consulte Olá específico do idioma exemplo registra o conteúdo de saudação de cada blob que é adicionado contêiner monitorado toohello.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>Exemplos de gatilho de blob em C# #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Exemplo de gatilho em Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Usando uma associação de saída de blob

Em funções do .NET, você deve usar um `out string` parâmetro em sua assinatura de função ou usar um dos tipos de saudação em Olá lista a seguir. Funções do Node. js, você acessa Olá saída blob usando `context.bindings.<name>`.

Em funções do .NET, você pode extrair tooany de saudação tipos a seguir:

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Gatilho de fila com amostra de entrada e saída de blob
Suponha que você tenha Olá function.json a seguir, que define uma [gatilho de armazenamento de fila](functions-bindings-storage-queue.md), um armazenamento de blob de entrada e saída de um armazenamento de blob. Aviso uso Olá Olá `queueTrigger` propriedade de metadados. no blob de saudação de entrada e saída `path` propriedades:

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

Consulte Olá específico do idioma exemplo que copia o blob de saída de toohello Olá blob de entrada.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>Exemplo de associação de blob em C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Exemplo de associação de blob em Node.js

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

