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
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="6847c-103">Associações de arquivo externo do Azure Functions (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="6847c-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="6847c-104">Este artigo mostra como toomanipulate arquivos de SaaS diferentes provedores (por exemplo, OneDrive, Dropbox) em sua função utilizando ligações internas.</span><span class="sxs-lookup"><span data-stu-id="6847c-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="6847c-105">O Azure Functions dá suporte a associações de gatilho, entrada e saída de arquivos externos.</span><span class="sxs-lookup"><span data-stu-id="6847c-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="6847c-106">Esta associação cria conexões API tooSaaS provedores ou usa conexões existentes de API do grupo de recursos do seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="6847c-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="6847c-107">Conexões de arquivo com suporte</span><span class="sxs-lookup"><span data-stu-id="6847c-107">Supported File connections</span></span>

|<span data-ttu-id="6847c-108">Conector</span><span class="sxs-lookup"><span data-stu-id="6847c-108">Connector</span></span>|<span data-ttu-id="6847c-109">Gatilho</span><span class="sxs-lookup"><span data-stu-id="6847c-109">Trigger</span></span>|<span data-ttu-id="6847c-110">Entrada</span><span class="sxs-lookup"><span data-stu-id="6847c-110">Input</span></span>|<span data-ttu-id="6847c-111">Saída</span><span class="sxs-lookup"><span data-stu-id="6847c-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="6847c-112">Box</span><span class="sxs-lookup"><span data-stu-id="6847c-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="6847c-113">x</span><span class="sxs-lookup"><span data-stu-id="6847c-113">x</span></span>|<span data-ttu-id="6847c-114">x</span><span class="sxs-lookup"><span data-stu-id="6847c-114">x</span></span>|<span data-ttu-id="6847c-115">x</span><span class="sxs-lookup"><span data-stu-id="6847c-115">x</span></span>
|[<span data-ttu-id="6847c-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="6847c-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="6847c-117">x</span><span class="sxs-lookup"><span data-stu-id="6847c-117">x</span></span>|<span data-ttu-id="6847c-118">x</span><span class="sxs-lookup"><span data-stu-id="6847c-118">x</span></span>|<span data-ttu-id="6847c-119">x</span><span class="sxs-lookup"><span data-stu-id="6847c-119">x</span></span>
|[<span data-ttu-id="6847c-120">FTP</span><span class="sxs-lookup"><span data-stu-id="6847c-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="6847c-121">x</span><span class="sxs-lookup"><span data-stu-id="6847c-121">x</span></span>|<span data-ttu-id="6847c-122">x</span><span class="sxs-lookup"><span data-stu-id="6847c-122">x</span></span>|<span data-ttu-id="6847c-123">x</span><span class="sxs-lookup"><span data-stu-id="6847c-123">x</span></span>
|[<span data-ttu-id="6847c-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="6847c-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="6847c-125">x</span><span class="sxs-lookup"><span data-stu-id="6847c-125">x</span></span>|<span data-ttu-id="6847c-126">x</span><span class="sxs-lookup"><span data-stu-id="6847c-126">x</span></span>|<span data-ttu-id="6847c-127">x</span><span class="sxs-lookup"><span data-stu-id="6847c-127">x</span></span>
|[<span data-ttu-id="6847c-128">OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="6847c-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="6847c-129">x</span><span class="sxs-lookup"><span data-stu-id="6847c-129">x</span></span>|<span data-ttu-id="6847c-130">x</span><span class="sxs-lookup"><span data-stu-id="6847c-130">x</span></span>|<span data-ttu-id="6847c-131">x</span><span class="sxs-lookup"><span data-stu-id="6847c-131">x</span></span>
|[<span data-ttu-id="6847c-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="6847c-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="6847c-133">x</span><span class="sxs-lookup"><span data-stu-id="6847c-133">x</span></span>|<span data-ttu-id="6847c-134">x</span><span class="sxs-lookup"><span data-stu-id="6847c-134">x</span></span>|<span data-ttu-id="6847c-135">x</span><span class="sxs-lookup"><span data-stu-id="6847c-135">x</span></span>
|[<span data-ttu-id="6847c-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="6847c-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="6847c-137">x</span><span class="sxs-lookup"><span data-stu-id="6847c-137">x</span></span>|<span data-ttu-id="6847c-138">x</span><span class="sxs-lookup"><span data-stu-id="6847c-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="6847c-139">Conexões de arquivo externo também podem ser usadas no [Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="6847c-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="6847c-140">Associação de gatilho de arquivo externo</span><span class="sxs-lookup"><span data-stu-id="6847c-140">External File trigger binding</span></span>

<span data-ttu-id="6847c-141">gatilho de arquivo externo do Azure Olá permite monitorar uma pasta remota e executar seu código de função quando forem detectadas alterações.</span><span class="sxs-lookup"><span data-stu-id="6847c-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="6847c-142">gatilho de arquivo externo Olá usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json</span><span class="sxs-lookup"><span data-stu-id="6847c-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

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

### <a name="name-patterns"></a><span data-ttu-id="6847c-143">Padrões de nome</span><span class="sxs-lookup"><span data-stu-id="6847c-143">Name patterns</span></span>
<span data-ttu-id="6847c-144">Você pode especificar um padrão de nome de arquivo em Olá `path` propriedade.</span><span class="sxs-lookup"><span data-stu-id="6847c-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="6847c-145">pasta Olá referenciada deve existir no provedor de SaaS hello.</span><span class="sxs-lookup"><span data-stu-id="6847c-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="6847c-146">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="6847c-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="6847c-147">Esse caminho deve localizar um arquivo chamado *original File1.txt* em Olá *entrada* pasta e valor Olá Olá `name` variável no código de função seria `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="6847c-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="6847c-148">Outro exemplo:</span><span class="sxs-lookup"><span data-stu-id="6847c-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="6847c-149">Esse caminho também deve localizar um arquivo chamado *original File1.txt*e o valor de saudação do hello `filename` e `fileextension` variáveis no código de função seria *File1 original* e  *txt*.</span><span class="sxs-lookup"><span data-stu-id="6847c-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="6847c-150">Você pode restringir o tipo de arquivo hello de arquivos usando um valor fixo para a extensão de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="6847c-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="6847c-151">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6847c-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="6847c-152">Nesse caso, somente *. PNG* arquivos Olá *exemplos* função de saudação do gatilho de pasta.</span><span class="sxs-lookup"><span data-stu-id="6847c-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="6847c-153">As chaves são caracteres especiais nos padrões de nome.</span><span class="sxs-lookup"><span data-stu-id="6847c-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="6847c-154">nomes de arquivo toospecify que têm chaves no nome hello, double Olá entre chaves.</span><span class="sxs-lookup"><span data-stu-id="6847c-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="6847c-155">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6847c-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="6847c-156">Esse caminho deve localizar um arquivo chamado *{20140101}-soundfile.mp3* em Olá *imagens* pasta e hello `name` seria o valor da variável no código da função hello *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="6847c-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

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

### <a name="handling-poison-files"></a><span data-ttu-id="6847c-157">Tratando arquivos suspeitos</span><span class="sxs-lookup"><span data-stu-id="6847c-157">Handling poison files</span></span>
<span data-ttu-id="6847c-158">Quando uma função de gatilho de arquivo externo falhar, funções do Azure repete essa função too5 horas por padrão (incluindo a primeira tentativa de saudação) para um determinado arquivo.</span><span class="sxs-lookup"><span data-stu-id="6847c-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="6847c-159">Se todas as 5 tentativas falharem, funções adiciona uma fila de armazenamento de tooa mensagem denominada *webjobs-apihubtrigger-suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="6847c-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="6847c-160">mensagem da fila Olá para arquivos suspeitas é um objeto JSON que contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="6847c-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="6847c-161">FunctionId (no formato de saudação  *&lt;nome de função do aplicativo >*. Funções.  *&lt;nome da função >*)</span><span class="sxs-lookup"><span data-stu-id="6847c-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="6847c-162">FileType</span><span class="sxs-lookup"><span data-stu-id="6847c-162">FileType</span></span>
* <span data-ttu-id="6847c-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="6847c-163">FolderName</span></span>
* <span data-ttu-id="6847c-164">FileName</span><span class="sxs-lookup"><span data-stu-id="6847c-164">FileName</span></span>
* <span data-ttu-id="6847c-165">ETag (um identificador de versão de arquivo, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6847c-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="6847c-166">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="6847c-166">Trigger usage</span></span>
<span data-ttu-id="6847c-167">Em c# funções, você deve associar dados do arquivo de entrada toohello usando um parâmetro nomeado na sua assinatura de função, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="6847c-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6847c-168">Onde `T` é o tipo de dados de saudação que você deseja toodeserialize Olá dados, e `paramName` é o nome hello especificado no [disparar JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="6847c-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="6847c-169">Em funções do Node. js, acessar dados de arquivo de entrada hello usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6847c-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6847c-170">arquivo Hello pode ser desserializado em qualquer um dos seguintes tipos de saudação:</span><span class="sxs-lookup"><span data-stu-id="6847c-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="6847c-171">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) – útil para dados de arquivo serializado para JSON.</span><span class="sxs-lookup"><span data-stu-id="6847c-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6847c-172">Se você declarar um tipo personalizado de entrada (por exemplo, `FooType`), funções do Azure tentativas de dados do toodeserialize Olá JSON para o tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="6847c-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="6847c-173">Cadeia de caracteres – útil para dados de arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="6847c-173">String - useful for text file data.</span></span>

<span data-ttu-id="6847c-174">No c# funções, você também pode associar tooany dos seguintes tipos de saudação e tempo de execução de funções hello tenta desserializar usando esse tipo de dados de arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="6847c-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="6847c-175">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="6847c-175">Trigger sample</span></span>
<span data-ttu-id="6847c-176">Suponha que você tenha Olá function.json a seguir, que define um gatilho de arquivo externo:</span><span class="sxs-lookup"><span data-stu-id="6847c-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="6847c-177">Consulte exemplo específico do idioma hello que registra o conteúdo de saudação de cada arquivo que é adicionado a pasta monitorada toohello.</span><span class="sxs-lookup"><span data-stu-id="6847c-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="6847c-178">C#</span><span class="sxs-lookup"><span data-stu-id="6847c-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="6847c-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="6847c-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="6847c-180">Uso de gatilhos em C#</span><span class="sxs-lookup"><span data-stu-id="6847c-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="6847c-181">Uso de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="6847c-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="6847c-182">Associação de entrada de arquivo externo</span><span class="sxs-lookup"><span data-stu-id="6847c-182">External File input binding</span></span>
<span data-ttu-id="6847c-183">associação de entrada Hello arquivos externos do Azure permite que você toouse um arquivo de uma pasta externo em sua função.</span><span class="sxs-lookup"><span data-stu-id="6847c-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="6847c-184">função de tooa de entrada de arquivo externo Hello usa Olá seguintes objetos JSON em hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="6847c-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="6847c-185">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6847c-185">Note hello following:</span></span>

* <span data-ttu-id="6847c-186">`path`deve conter o nome da pasta de saudação e nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="6847c-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="6847c-187">Por exemplo, se você tiver um [gatilho fila](functions-bindings-storage-queue.md) na sua função, você pode usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa arquivo hello `samples-workitems` pasta com um nome que corresponda o nome do arquivo hello especificado na mensagem de saudação do gatilho.</span><span class="sxs-lookup"><span data-stu-id="6847c-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="6847c-188">Uso de entrada</span><span class="sxs-lookup"><span data-stu-id="6847c-188">Input usage</span></span>
<span data-ttu-id="6847c-189">Em c# funções, você deve associar dados do arquivo de entrada toohello usando um parâmetro nomeado na sua assinatura de função, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="6847c-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6847c-190">Onde `T` é o tipo de dados de saudação que você deseja toodeserialize Olá dados, e `paramName` é o nome hello especificado no [associação de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="6847c-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="6847c-191">Em funções do Node. js, acessar dados de arquivo de entrada hello usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6847c-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6847c-192">arquivo Hello pode ser desserializado em qualquer um dos seguintes tipos de saudação:</span><span class="sxs-lookup"><span data-stu-id="6847c-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="6847c-193">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) – útil para dados de arquivo serializado para JSON.</span><span class="sxs-lookup"><span data-stu-id="6847c-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6847c-194">Se você declarar um tipo personalizado de entrada (por exemplo, `InputType`), funções do Azure tentativas de dados do toodeserialize Olá JSON para o tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="6847c-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="6847c-195">Cadeia de caracteres – útil para dados de arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="6847c-195">String - useful for text file data.</span></span>

<span data-ttu-id="6847c-196">No c# funções, você também pode associar tooany dos seguintes tipos de saudação e tempo de execução de funções hello tenta desserializar usando esse tipo de dados de arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="6847c-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="6847c-197">Associação de saída de arquivo externo</span><span class="sxs-lookup"><span data-stu-id="6847c-197">External File output binding</span></span>
<span data-ttu-id="6847c-198">Olá arquivos externos do Azure saída vinculação permite pasta externa de toowrite arquivos tooan em sua função.</span><span class="sxs-lookup"><span data-stu-id="6847c-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="6847c-199">arquivo externo de saudação de saída para uma função usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="6847c-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="6847c-200">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6847c-200">Note hello following:</span></span>

* <span data-ttu-id="6847c-201">`path`deve conter o nome da pasta hello e Olá toowrite de nome de arquivo para.</span><span class="sxs-lookup"><span data-stu-id="6847c-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="6847c-202">Por exemplo, se você tiver um [gatilho fila](functions-bindings-storage-queue.md) na sua função, você pode usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa arquivo hello `samples-workitems` pasta com um nome que corresponda o nome do arquivo hello especificado na mensagem de saudação do gatilho.</span><span class="sxs-lookup"><span data-stu-id="6847c-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="6847c-203">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="6847c-203">Output usage</span></span>
<span data-ttu-id="6847c-204">Em c# funções, você vincular o arquivo de saída toohello usando Olá denominado `out` parâmetro em sua assinatura de função, como `out <T> <name>`, onde `T` é o tipo de dados de saudação que você deseja tooserialize Olá dados, e `paramName` é Olá nome especificado no [associação de saída](#output).</span><span class="sxs-lookup"><span data-stu-id="6847c-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="6847c-205">Em funções do Node. js, acessar arquivo de saída de hello usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6847c-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6847c-206">Você pode gravar o arquivo de saída toohello usando qualquer um dos seguintes tipos de saudação:</span><span class="sxs-lookup"><span data-stu-id="6847c-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="6847c-207">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - útil para serialização JSON.</span><span class="sxs-lookup"><span data-stu-id="6847c-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="6847c-208">Se você declarar um tipo de saída personalizado (por exemplo, `out OutputType paramName`), funções do Azure tenta tooserialize objeto em JSON.</span><span class="sxs-lookup"><span data-stu-id="6847c-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="6847c-209">Se o parâmetro de saída de hello é nulo quando Olá função for encerrada, o tempo de execução de funções hello cria um arquivo como um objeto nulo.</span><span class="sxs-lookup"><span data-stu-id="6847c-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="6847c-210">Cadeia de caracteres – (`out string paramName`) útil para dados de arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="6847c-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="6847c-211">tempo de execução de funções Hello cria um arquivo somente se o parâmetro de cadeia de caracteres for não nulo quando a função hello será encerrado.</span><span class="sxs-lookup"><span data-stu-id="6847c-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="6847c-212">No c# funções você também pode gerar tooany de saudação tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6847c-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="6847c-213">Amostra de entrada + saída</span><span class="sxs-lookup"><span data-stu-id="6847c-213">Input + Output sample</span></span>
<span data-ttu-id="6847c-214">Suponha que você tenha Olá function.json a seguir, que define uma [gatilho de fila de armazenamento](functions-bindings-storage-queue.md), um arquivo externo de entrada e saída de um arquivo externo:</span><span class="sxs-lookup"><span data-stu-id="6847c-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="6847c-215">Consulte Olá específico do idioma exemplo que copia o arquivo de saída de toohello de arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="6847c-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="6847c-216">C#</span><span class="sxs-lookup"><span data-stu-id="6847c-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="6847c-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="6847c-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="6847c-218">Uso em C#</span><span class="sxs-lookup"><span data-stu-id="6847c-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="6847c-219">Uso em Node.js</span><span class="sxs-lookup"><span data-stu-id="6847c-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="6847c-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6847c-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
