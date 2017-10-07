---
title: "associações de arquivo externo funções aaaAzure (visualização) | Microsoft Docs"
description: "Usando associações de arquivo externo no Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a>Associações de arquivo externo do Azure Functions (versão prévia)
Este artigo mostra como toomanipulate arquivos de SaaS diferentes provedores (por exemplo, OneDrive, Dropbox) em sua função utilizando ligações internas. O Azure Functions dá suporte a associações de gatilho, entrada e saída de arquivos externos.

Esta associação cria conexões API tooSaaS provedores ou usa conexões existentes de API do grupo de recursos do seu aplicativo de função.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Conexões de arquivo com suporte

|Conector|Gatilho|Entrada|Saída|
|:-----|:---:|:---:|:---:|
|[Box](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive for Business](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google Drive](https://www.google.com/drive/)||x|x|

> [!NOTE]
> Conexões de arquivo externo também podem ser usadas no [Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list)

## <a name="external-file-trigger-binding"></a>Associação de gatilho de arquivo externo

gatilho de arquivo externo do Azure Olá permite monitorar uma pasta remota e executar seu código de função quando forem detectadas alterações.

gatilho de arquivo externo Olá usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a>Padrões de nome
Você pode especificar um padrão de nome de arquivo em Olá `path` propriedade. pasta Olá referenciada deve existir no provedor de SaaS hello.
Exemplos:

```json
"path": "input/original-{name}",
```

Esse caminho deve localizar um arquivo chamado *original File1.txt* em Olá *entrada* pasta e valor Olá Olá `name` variável no código de função seria `File1.txt`.

Outro exemplo:

```json
"path": "input/{filename}.{fileextension}",
```

Esse caminho também deve localizar um arquivo chamado *original File1.txt*e o valor de saudação do hello `filename` e `fileextension` variáveis no código de função seria *File1 original* e  *txt*.

Você pode restringir o tipo de arquivo hello de arquivos usando um valor fixo para a extensão de arquivo hello. Por exemplo:

```json
"path": "samples/{name}.png",
```

Nesse caso, somente *. PNG* arquivos Olá *exemplos* função de saudação do gatilho de pasta.

As chaves são caracteres especiais nos padrões de nome. nomes de arquivo toospecify que têm chaves no nome hello, double Olá entre chaves.
Por exemplo:

```json
"path": "images/{{20140101}}-{name}",
```

Esse caminho deve localizar um arquivo chamado *{20140101}-soundfile.mp3* em Olá *imagens* pasta e hello `name` seria o valor da variável no código da função hello *soundfile.mp3*.

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a>Tratando arquivos suspeitos
Quando uma função de gatilho de arquivo externo falhar, funções do Azure repete essa função too5 horas por padrão (incluindo a primeira tentativa de saudação) para um determinado arquivo.
Se todas as 5 tentativas falharem, funções adiciona uma fila de armazenamento de tooa mensagem denominada *webjobs-apihubtrigger-suspeitas*. mensagem da fila Olá para arquivos suspeitas é um objeto JSON que contém Olá propriedades a seguir:

* FunctionId (no formato de saudação  *&lt;nome de função do aplicativo >*. Funções.  *&lt;nome da função >*)
* FileType
* FolderName
* FileName
* ETag (um identificador de versão de arquivo, por exemplo: "0x8D1DC6E70A277EF")


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso de gatilho
Em c# funções, você deve associar dados do arquivo de entrada toohello usando um parâmetro nomeado na sua assinatura de função, como `<T> <name>`.
Onde `T` é o tipo de dados de saudação que você deseja toodeserialize Olá dados, e `paramName` é o nome hello especificado no [disparar JSON](#trigger). Em funções do Node. js, acessar dados de arquivo de entrada hello usando `context.bindings.<name>`.

arquivo Hello pode ser desserializado em qualquer um dos seguintes tipos de saudação:

* Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) – útil para dados de arquivo serializado para JSON.
  Se você declarar um tipo personalizado de entrada (por exemplo, `FooType`), funções do Azure tentativas de dados do toodeserialize Olá JSON para o tipo especificado.
* Cadeia de caracteres – útil para dados de arquivo de texto.

No c# funções, você também pode associar tooany dos seguintes tipos de saudação e tempo de execução de funções hello tenta desserializar usando esse tipo de dados de arquivo hello:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Exemplo de gatilho
Suponha que você tenha Olá function.json a seguir, que define um gatilho de arquivo externo:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

Consulte exemplo específico do idioma hello que registra o conteúdo de saudação de cada arquivo que é adicionado a pasta monitorada toohello.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>Uso de gatilhos em C# #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a>Uso de gatilho em Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Associação de entrada de arquivo externo
associação de entrada Hello arquivos externos do Azure permite que você toouse um arquivo de uma pasta externo em sua função.

função de tooa de entrada de arquivo externo Hello usa Olá seguintes objetos JSON em hello `bindings` matriz de function.json:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Observe o seguinte hello:

* `path`deve conter o nome da pasta de saudação e nome de arquivo hello. Por exemplo, se você tiver um [gatilho fila](functions-bindings-storage-queue.md) na sua função, você pode usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa arquivo hello `samples-workitems` pasta com um nome que corresponda o nome do arquivo hello especificado na mensagem de saudação do gatilho.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso de entrada
Em c# funções, você deve associar dados do arquivo de entrada toohello usando um parâmetro nomeado na sua assinatura de função, como `<T> <name>`.
Onde `T` é o tipo de dados de saudação que você deseja toodeserialize Olá dados, e `paramName` é o nome hello especificado no [associação de entrada](#input). Em funções do Node. js, acessar dados de arquivo de entrada hello usando `context.bindings.<name>`.

arquivo Hello pode ser desserializado em qualquer um dos seguintes tipos de saudação:

* Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) – útil para dados de arquivo serializado para JSON.
  Se você declarar um tipo personalizado de entrada (por exemplo, `InputType`), funções do Azure tentativas de dados do toodeserialize Olá JSON para o tipo especificado.
* Cadeia de caracteres – útil para dados de arquivo de texto.

No c# funções, você também pode associar tooany dos seguintes tipos de saudação e tempo de execução de funções hello tenta desserializar usando esse tipo de dados de arquivo hello:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Associação de saída de arquivo externo
Olá arquivos externos do Azure saída vinculação permite pasta externa de toowrite arquivos tooan em sua função.

arquivo externo de saudação de saída para uma função usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Observe o seguinte hello:

* `path`deve conter o nome da pasta hello e Olá toowrite de nome de arquivo para. Por exemplo, se você tiver um [gatilho fila](functions-bindings-storage-queue.md) na sua função, você pode usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa arquivo hello `samples-workitems` pasta com um nome que corresponda o nome do arquivo hello especificado na mensagem de saudação do gatilho.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de saída
Em c# funções, você vincular o arquivo de saída toohello usando Olá denominado `out` parâmetro em sua assinatura de função, como `out <T> <name>`, onde `T` é o tipo de dados de saudação que você deseja tooserialize Olá dados, e `paramName` é Olá nome especificado no [associação de saída](#output). Em funções do Node. js, acessar arquivo de saída de hello usando `context.bindings.<name>`.

Você pode gravar o arquivo de saída toohello usando qualquer um dos seguintes tipos de saudação:

* Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - útil para serialização JSON.
  Se você declarar um tipo de saída personalizado (por exemplo, `out OutputType paramName`), funções do Azure tenta tooserialize objeto em JSON. Se o parâmetro de saída de hello é nulo quando Olá função for encerrada, o tempo de execução de funções hello cria um arquivo como um objeto nulo.
* Cadeia de caracteres – (`out string paramName`) útil para dados de arquivo de texto. tempo de execução de funções Hello cria um arquivo somente se o parâmetro de cadeia de caracteres for não nulo quando a função hello será encerrado.

No c# funções você também pode gerar tooany de saudação tipos a seguir:

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Amostra de entrada + saída
Suponha que você tenha Olá function.json a seguir, que define uma [gatilho de fila de armazenamento](functions-bindings-storage-queue.md), um arquivo externo de entrada e saída de um arquivo externo:

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Consulte Olá específico do idioma exemplo que copia o arquivo de saída de toohello de arquivo de entrada hello.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>Uso em C# #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a>Uso em Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
