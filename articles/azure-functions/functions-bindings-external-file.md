---
title: "Associações de arquivo externo do Azure Functions (versão prévia) | Microsoft Docs"
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
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="309b7-103">Associações de arquivo externo do Azure Functions (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="309b7-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="309b7-104">Este artigo mostra como manipular arquivos de provedores SaaS diferentes (por exemplo, OneDrive, Dropbox) em sua função utilizando associações internas.</span><span class="sxs-lookup"><span data-stu-id="309b7-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="309b7-105">O Azure Functions dá suporte a associações de gatilho, entrada e saída de arquivos externos.</span><span class="sxs-lookup"><span data-stu-id="309b7-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="309b7-106">Essa associação cria conexões de API com provedores SaaS, ou usa conexões de API existentes do grupo de recursos do aplicativo da função.</span><span class="sxs-lookup"><span data-stu-id="309b7-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="309b7-107">Conexões de arquivo com suporte</span><span class="sxs-lookup"><span data-stu-id="309b7-107">Supported File connections</span></span>

|<span data-ttu-id="309b7-108">Conector</span><span class="sxs-lookup"><span data-stu-id="309b7-108">Connector</span></span>|<span data-ttu-id="309b7-109">Gatilho</span><span class="sxs-lookup"><span data-stu-id="309b7-109">Trigger</span></span>|<span data-ttu-id="309b7-110">Entrada</span><span class="sxs-lookup"><span data-stu-id="309b7-110">Input</span></span>|<span data-ttu-id="309b7-111">Saída</span><span class="sxs-lookup"><span data-stu-id="309b7-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="309b7-112">Box</span><span class="sxs-lookup"><span data-stu-id="309b7-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="309b7-113">x</span><span class="sxs-lookup"><span data-stu-id="309b7-113">x</span></span>|<span data-ttu-id="309b7-114">x</span><span class="sxs-lookup"><span data-stu-id="309b7-114">x</span></span>|<span data-ttu-id="309b7-115">x</span><span class="sxs-lookup"><span data-stu-id="309b7-115">x</span></span>
|[<span data-ttu-id="309b7-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="309b7-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="309b7-117">x</span><span class="sxs-lookup"><span data-stu-id="309b7-117">x</span></span>|<span data-ttu-id="309b7-118">x</span><span class="sxs-lookup"><span data-stu-id="309b7-118">x</span></span>|<span data-ttu-id="309b7-119">x</span><span class="sxs-lookup"><span data-stu-id="309b7-119">x</span></span>
|[<span data-ttu-id="309b7-120">FTP</span><span class="sxs-lookup"><span data-stu-id="309b7-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="309b7-121">x</span><span class="sxs-lookup"><span data-stu-id="309b7-121">x</span></span>|<span data-ttu-id="309b7-122">x</span><span class="sxs-lookup"><span data-stu-id="309b7-122">x</span></span>|<span data-ttu-id="309b7-123">x</span><span class="sxs-lookup"><span data-stu-id="309b7-123">x</span></span>
|[<span data-ttu-id="309b7-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="309b7-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="309b7-125">x</span><span class="sxs-lookup"><span data-stu-id="309b7-125">x</span></span>|<span data-ttu-id="309b7-126">x</span><span class="sxs-lookup"><span data-stu-id="309b7-126">x</span></span>|<span data-ttu-id="309b7-127">x</span><span class="sxs-lookup"><span data-stu-id="309b7-127">x</span></span>
|[<span data-ttu-id="309b7-128">OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="309b7-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="309b7-129">x</span><span class="sxs-lookup"><span data-stu-id="309b7-129">x</span></span>|<span data-ttu-id="309b7-130">x</span><span class="sxs-lookup"><span data-stu-id="309b7-130">x</span></span>|<span data-ttu-id="309b7-131">x</span><span class="sxs-lookup"><span data-stu-id="309b7-131">x</span></span>
|[<span data-ttu-id="309b7-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="309b7-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="309b7-133">x</span><span class="sxs-lookup"><span data-stu-id="309b7-133">x</span></span>|<span data-ttu-id="309b7-134">x</span><span class="sxs-lookup"><span data-stu-id="309b7-134">x</span></span>|<span data-ttu-id="309b7-135">x</span><span class="sxs-lookup"><span data-stu-id="309b7-135">x</span></span>
|[<span data-ttu-id="309b7-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="309b7-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="309b7-137">x</span><span class="sxs-lookup"><span data-stu-id="309b7-137">x</span></span>|<span data-ttu-id="309b7-138">x</span><span class="sxs-lookup"><span data-stu-id="309b7-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="309b7-139">Conexões de arquivo externo também podem ser usadas no [Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="309b7-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="309b7-140">Associação de gatilho de arquivo externo</span><span class="sxs-lookup"><span data-stu-id="309b7-140">External File trigger binding</span></span>

<span data-ttu-id="309b7-141">O gatilho de arquivo externo do Azure permite monitorar uma pasta remota e executar o código da função quando são detectadas alterações.</span><span class="sxs-lookup"><span data-stu-id="309b7-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="309b7-142">O gatilho de arquivo externo usa os seguintes objetos JSON na matriz `bindings` de function.json</span><span class="sxs-lookup"><span data-stu-id="309b7-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="309b7-143">Padrões de nome</span><span class="sxs-lookup"><span data-stu-id="309b7-143">Name patterns</span></span>
<span data-ttu-id="309b7-144">É possível especificar um padrão de nome de arquivo na propriedade `path`.</span><span class="sxs-lookup"><span data-stu-id="309b7-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="309b7-145">A pasta referenciada deve existir no provedor de SaaS.</span><span class="sxs-lookup"><span data-stu-id="309b7-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="309b7-146">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="309b7-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="309b7-147">Esse caminho deve encontrar um arquivo chamado *original-File1.txt* na *entrada* pasta e o valor da variável `name` no código de função seria `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="309b7-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="309b7-148">Outro exemplo:</span><span class="sxs-lookup"><span data-stu-id="309b7-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="309b7-149">Esse caminho também poderia ser um blob chamado *original-File1.txt* e o valor das variáveis `filename` e `fileextension` no código de função seria *original-File1* e *txt*.</span><span class="sxs-lookup"><span data-stu-id="309b7-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="309b7-150">Você pode restringir o tipo de arquivo dos arquivos usando um valor fixo para a extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="309b7-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="309b7-151">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="309b7-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="309b7-152">Nesse caso, apenas arquivos *.png* na pasta *amostras* disparam a função.</span><span class="sxs-lookup"><span data-stu-id="309b7-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="309b7-153">As chaves são caracteres especiais nos padrões de nome.</span><span class="sxs-lookup"><span data-stu-id="309b7-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="309b7-154">Para especificar nomes de arquivo com chaves, duplique as chaves.</span><span class="sxs-lookup"><span data-stu-id="309b7-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="309b7-155">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="309b7-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="309b7-156">Esse caminho encontraria um arquivo denominado *{20140101}-soundfile.mp3* na pasta *imagens* e o valor da variável `name` no código da função seria *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="309b7-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="309b7-157">Tratando arquivos suspeitos</span><span class="sxs-lookup"><span data-stu-id="309b7-157">Handling poison files</span></span>
<span data-ttu-id="309b7-158">Quando a função de gatilho de um arquivo externo falha, o Azure Functions repete essa função até 5 vezes por padrão (incluindo a primeira tentativa) para determinado arquivo.</span><span class="sxs-lookup"><span data-stu-id="309b7-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="309b7-159">Se todas as 5 tentativas falharem, o Functions adicionará uma mensagem para uma fila de armazenamento denominada *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="309b7-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="309b7-160">A mensagem da fila para arquivos suspeitos é um objeto JSON que contém as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="309b7-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="309b7-161">FunctionId (no formato *&lt;nome do aplicativo de funções>*.Functions.*&lt;nome da função>*)</span><span class="sxs-lookup"><span data-stu-id="309b7-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="309b7-162">FileType</span><span class="sxs-lookup"><span data-stu-id="309b7-162">FileType</span></span>
* <span data-ttu-id="309b7-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="309b7-163">FolderName</span></span>
* <span data-ttu-id="309b7-164">FileName</span><span class="sxs-lookup"><span data-stu-id="309b7-164">FileName</span></span>
* <span data-ttu-id="309b7-165">ETag (um identificador de versão de arquivo, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="309b7-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="309b7-166">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="309b7-166">Trigger usage</span></span>
<span data-ttu-id="309b7-167">Em funções do C#, você associa aos dados do arquivo de entrada usando um parâmetro nomeado na assinatura da função, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="309b7-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="309b7-168">Em que `T` é o tipo de dados no qual você deseja desserializar os dados e `paramName` é o nome especificado no [gatilho JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="309b7-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="309b7-169">Em funções do Node.js, você acessa os dados do arquivo de entrada usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="309b7-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="309b7-170">O arquivo pode ser desserializado em qualquer um destes tipos:</span><span class="sxs-lookup"><span data-stu-id="309b7-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="309b7-171">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) – útil para dados de arquivo serializado para JSON.</span><span class="sxs-lookup"><span data-stu-id="309b7-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="309b7-172">Se você declarar um tipo de entrada personalizado (por exemplo, `FooType`), o Azure Functions tenta desserializar os dados JSON para o tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="309b7-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="309b7-173">Cadeia de caracteres – útil para dados de arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="309b7-173">String - useful for text file data.</span></span>

<span data-ttu-id="309b7-174">Em funções do C#, você também pode associar a qualquer um dos seguintes tipos e o tempo de execução do Functions tentará desserializar os dados da tabela usando esse tipo:</span><span class="sxs-lookup"><span data-stu-id="309b7-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="309b7-175">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="309b7-175">Trigger sample</span></span>
<span data-ttu-id="309b7-176">Suponha que você tem o seguinte function.json, que define um gatilho de arquivo externo:</span><span class="sxs-lookup"><span data-stu-id="309b7-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="309b7-177">Veja a amostra específica a um idioma que registra o conteúdo de cada arquivo adicionado à pasta monitorada.</span><span class="sxs-lookup"><span data-stu-id="309b7-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="309b7-178">C#</span><span class="sxs-lookup"><span data-stu-id="309b7-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="309b7-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="309b7-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="309b7-180">Uso de gatilhos em C#</span><span class="sxs-lookup"><span data-stu-id="309b7-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="309b7-181">Uso de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="309b7-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="309b7-182">Associação de entrada de arquivo externo</span><span class="sxs-lookup"><span data-stu-id="309b7-182">External File input binding</span></span>
<span data-ttu-id="309b7-183">A associação de entrada de arquivo externo do Azure permite que você use um arquivo de uma pasta externa em sua função.</span><span class="sxs-lookup"><span data-stu-id="309b7-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="309b7-184">A entrada do arquivo externo em uma função usa os seguintes objetos JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="309b7-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="309b7-185">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="309b7-185">Note the following:</span></span>

* <span data-ttu-id="309b7-186">`path` deve conter o nome da pasta e o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="309b7-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="309b7-187">Por exemplo, se você tiver um [gatilho de fila](functions-bindings-storage-queue.md) em sua função, poderá usar `"path": "samples-workitems/{queueTrigger}"` para apontar para um arquivo na pasta `samples-workitems` com um nome que corresponda ao nome do arquivo especificado na mensagem de gatilho.</span><span class="sxs-lookup"><span data-stu-id="309b7-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="309b7-188">Uso de entrada</span><span class="sxs-lookup"><span data-stu-id="309b7-188">Input usage</span></span>
<span data-ttu-id="309b7-189">Em funções do C#, você associa aos dados do arquivo de entrada usando um parâmetro nomeado na assinatura da função, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="309b7-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="309b7-190">Em que `T` é o tipo de dados no qual você deseja desserializar os dados e `paramName` é o nome especificado na [associação de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="309b7-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="309b7-191">Em funções do Node.js, você acessa os dados do arquivo de entrada usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="309b7-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="309b7-192">O arquivo pode ser desserializado em qualquer um destes tipos:</span><span class="sxs-lookup"><span data-stu-id="309b7-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="309b7-193">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) – útil para dados de arquivo serializado para JSON.</span><span class="sxs-lookup"><span data-stu-id="309b7-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="309b7-194">Se você declarar um tipo de entrada personalizado (por exemplo, `InputType`), o Azure Functions tenta desserializar os dados JSON para o tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="309b7-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="309b7-195">Cadeia de caracteres – útil para dados de arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="309b7-195">String - useful for text file data.</span></span>

<span data-ttu-id="309b7-196">Em funções do C#, você também pode associar a qualquer um dos seguintes tipos e o tempo de execução do Functions tentará desserializar os dados da tabela usando esse tipo:</span><span class="sxs-lookup"><span data-stu-id="309b7-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="309b7-197">Associação de saída de arquivo externo</span><span class="sxs-lookup"><span data-stu-id="309b7-197">External File output binding</span></span>
<span data-ttu-id="309b7-198">A associação de saída de arquivo externo do Azure permite que você grave arquivos em uma pasta externa de sua função.</span><span class="sxs-lookup"><span data-stu-id="309b7-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="309b7-199">A saída do arquivo externo para uma função usa os seguintes objetos JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="309b7-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="309b7-200">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="309b7-200">Note the following:</span></span>

* <span data-ttu-id="309b7-201">`path` deve conter o nome da pasta e o nome do arquivo no qual gravar.</span><span class="sxs-lookup"><span data-stu-id="309b7-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="309b7-202">Por exemplo, se você tiver um [gatilho de fila](functions-bindings-storage-queue.md) em sua função, poderá usar `"path": "samples-workitems/{queueTrigger}"` para apontar para um arquivo na pasta `samples-workitems` com um nome que corresponda ao nome do arquivo especificado na mensagem de gatilho.</span><span class="sxs-lookup"><span data-stu-id="309b7-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="309b7-203">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="309b7-203">Output usage</span></span>
<span data-ttu-id="309b7-204">Em funções C#, você associa ao arquivo de saída usando o parâmetro `out` nomeado na assinatura da função, como `out <T> <name>`, em que `T` é o tipo de dados no qual você quer serializar os dados e `paramName` é o nome especificado na [associação de saída](#output).</span><span class="sxs-lookup"><span data-stu-id="309b7-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="309b7-205">Nas funções do Node.js, você acessa o arquivo de saída usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="309b7-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="309b7-206">Você pode gravar no arquivo de saída usando qualquer um dos seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="309b7-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="309b7-207">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - útil para serialização JSON.</span><span class="sxs-lookup"><span data-stu-id="309b7-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="309b7-208">Se você declarar um tipo de saída personalizada (por exemplo, `out OutputType paramName`), o Azure Functions tenta serializar o objeto em JSON.</span><span class="sxs-lookup"><span data-stu-id="309b7-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="309b7-209">Se o parâmetro de saída for nulo quando a função for encerrada, o tempo de execução do Functions criará um arquivo como um objeto nulo.</span><span class="sxs-lookup"><span data-stu-id="309b7-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="309b7-210">Cadeia de caracteres – (`out string paramName`) útil para dados de arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="309b7-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="309b7-211">O tempo de execução do Functions só criará um arquivo se o parâmetro de cadeia de caracteres não for nulo quando a função for encerrada.</span><span class="sxs-lookup"><span data-stu-id="309b7-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="309b7-212">Em funções do C#, também é possível executar a saída para qualquer um dos seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="309b7-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="309b7-213">Amostra de entrada + saída</span><span class="sxs-lookup"><span data-stu-id="309b7-213">Input + Output sample</span></span>
<span data-ttu-id="309b7-214">Suponha que você tem o function.json a seguir, que define um [gatilho de fila de armazenamento](functions-bindings-storage-queue.md), uma entrada de arquivo externo e uma saída de arquivo externo:</span><span class="sxs-lookup"><span data-stu-id="309b7-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="309b7-215">Consulte a amostra específica a um idioma que copia o arquivo de entrada no arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="309b7-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="309b7-216">C#</span><span class="sxs-lookup"><span data-stu-id="309b7-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="309b7-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="309b7-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="309b7-218">Uso em C#</span><span class="sxs-lookup"><span data-stu-id="309b7-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="309b7-219">Uso em Node.js</span><span class="sxs-lookup"><span data-stu-id="309b7-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="309b7-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="309b7-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
