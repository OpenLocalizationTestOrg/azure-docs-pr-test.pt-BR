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
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="4af4d-104">Associações de armazenamento de Blobs do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4af4d-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="4af4d-105">Este artigo explica como tooconfigure e trabalhar com associações de armazenamento de BLOBs do Azure em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="4af4d-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="4af4d-106">O Azure Functions dá suporte a associações de entrada, saída e gatilho para o Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4af4d-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="4af4d-107">Para os recursos que estão disponíveis em todas as associações, veja [Gatilhos e conceitos de associações do Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="4af4d-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="4af4d-108">Não há suporte para [conta de armazenamento somente de blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="4af4d-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="4af4d-109">Gatilhos de armazenamento de blobs e associações exigem uma conta de armazenamento de uso geral.</span><span class="sxs-lookup"><span data-stu-id="4af4d-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="4af4d-110">Gatilhos e associações de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="4af4d-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="4af4d-111">Usando um gatilho de armazenamento de BLOBs do Azure hello, seu código de função é chamado quando um blob novo ou atualizado é detectado.</span><span class="sxs-lookup"><span data-stu-id="4af4d-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="4af4d-112">conteúdo do blob Olá é fornecido como entrada toohello função.</span><span class="sxs-lookup"><span data-stu-id="4af4d-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="4af4d-113">Definir um gatilho de armazenamento de blob usando Olá **integrar** no portal de funções hello.</span><span class="sxs-lookup"><span data-stu-id="4af4d-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="4af4d-114">Olá, portal cria Olá após a definição no hello **associações** seção *function.json*:</span><span class="sxs-lookup"><span data-stu-id="4af4d-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="4af4d-115">Blob de entrada e saída associações são definidas usando `blob` como tipo de associação de saudação:</span><span class="sxs-lookup"><span data-stu-id="4af4d-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="4af4d-116">Olá `path` propriedade dá suporte à associação de expressões e parâmetros de filtro.</span><span class="sxs-lookup"><span data-stu-id="4af4d-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="4af4d-117">Veja [Padrões de nome](#pattern).</span><span class="sxs-lookup"><span data-stu-id="4af4d-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="4af4d-118">Olá `connection` propriedade deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4af4d-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="4af4d-119">No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você seleciona uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4af4d-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="4af4d-120">Quando você estiver usando um gatilho de blob em um plano de consumo, pode haver o atraso de 10 minutos tooa em processamento novos blobs depois que uma função de aplicativo estiver ocioso.</span><span class="sxs-lookup"><span data-stu-id="4af4d-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="4af4d-121">Olá função aplicativo em execução, os blobs são processados imediatamente.</span><span class="sxs-lookup"><span data-stu-id="4af4d-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="4af4d-122">tooavoid neste inicial atraso, considere uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="4af4d-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="4af4d-123">Use um plano do Serviço de Aplicativo com a opçao Sempre ativado habilitada.</span><span class="sxs-lookup"><span data-stu-id="4af4d-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="4af4d-124">Use outro blob de saudação do tootrigger mecanismo de processamento, como uma mensagem da fila que contém o nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="4af4d-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="4af4d-125">Para obter um exemplo, confira [Gatilho de fila com associação de entrada de blob](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="4af4d-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="4af4d-126">Padrões de nome</span><span class="sxs-lookup"><span data-stu-id="4af4d-126">Name patterns</span></span>
<span data-ttu-id="4af4d-127">Você pode especificar um padrão de nome de blob em Olá `path` propriedade, que pode ser uma expressão de filtro ou de associação.</span><span class="sxs-lookup"><span data-stu-id="4af4d-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="4af4d-128">Veja [Padrões e expressões de associação](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="4af4d-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="4af4d-129">Por exemplo, tooblobs toofilter que começam com a cadeia de caracteres hello "original", use Olá definição a seguir.</span><span class="sxs-lookup"><span data-stu-id="4af4d-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="4af4d-130">Esse caminho localiza um blob denominado *original Blob1.txt* em Olá *entrada* contêiner e valor Olá Olá `name` variável no código da função é `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="4af4d-131">extensão e nome de arquivo de blob toobind toohello separadamente, usam dois padrões.</span><span class="sxs-lookup"><span data-stu-id="4af4d-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="4af4d-132">Esse caminho também localiza um blob denominado *original Blob1.txt*e o valor de saudação do hello `blobname` e `blobextension` são variáveis no código de função *original Blob1* e *txt*.</span><span class="sxs-lookup"><span data-stu-id="4af4d-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="4af4d-133">Você pode restringir o tipo de arquivo hello de blobs usando um valor fixo para a extensão de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4af4d-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="4af4d-134">Por exemplo, tootrigger somente em arquivos. png, use saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="4af4d-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="4af4d-135">As chaves são caracteres especiais nos padrões de nome.</span><span class="sxs-lookup"><span data-stu-id="4af4d-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="4af4d-136">toospecify nomes de blob que têm chaves no nome hello, você pode sair chaves hello usando duas chaves.</span><span class="sxs-lookup"><span data-stu-id="4af4d-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="4af4d-137">Olá, exemplo a seguir localiza um blob denominado *{20140101}-soundfile.mp3* em Olá *imagens* contêiner e hello `name` valor da variável no código da função hello é * soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="4af4d-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="4af4d-138">Metadados de gatilho</span><span class="sxs-lookup"><span data-stu-id="4af4d-138">Trigger metadata</span></span>

<span data-ttu-id="4af4d-139">gatilho de blob Olá fornece várias propriedades de metadados.</span><span class="sxs-lookup"><span data-stu-id="4af4d-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="4af4d-140">Essas propriedades podem ser usadas como parte de expressões de associações em outras associações ou como parâmetros em seu código.</span><span class="sxs-lookup"><span data-stu-id="4af4d-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="4af4d-141">Esses valores têm Olá mesma semântica [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="4af4d-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="4af4d-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="4af4d-142">**BlobTrigger**.</span></span> <span data-ttu-id="4af4d-143">Digite `string`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-143">Type `string`.</span></span> <span data-ttu-id="4af4d-144">caminho de blob disparo Olá</span><span class="sxs-lookup"><span data-stu-id="4af4d-144">hello triggering blob path</span></span>
- <span data-ttu-id="4af4d-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="4af4d-145">**Uri**.</span></span> <span data-ttu-id="4af4d-146">Digite `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-146">Type `System.Uri`.</span></span> <span data-ttu-id="4af4d-147">URI do blob Olá local primário hello.</span><span class="sxs-lookup"><span data-stu-id="4af4d-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="4af4d-148">**Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="4af4d-148">**Properties**.</span></span> <span data-ttu-id="4af4d-149">Digite `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="4af4d-150">Olá propriedades do sistema do blob.</span><span class="sxs-lookup"><span data-stu-id="4af4d-150">hello blob's system properties.</span></span>
- <span data-ttu-id="4af4d-151">**Metadados**.</span><span class="sxs-lookup"><span data-stu-id="4af4d-151">**Metadata**.</span></span> <span data-ttu-id="4af4d-152">Digite `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="4af4d-153">Olá metadados definidos pelo usuário para blob hello.</span><span class="sxs-lookup"><span data-stu-id="4af4d-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="4af4d-154">Recebimentos de blob</span><span class="sxs-lookup"><span data-stu-id="4af4d-154">Blob receipts</span></span>
<span data-ttu-id="4af4d-155">Funções do Azure Olá runtime garante que nenhuma função de gatilho de blob é chamada mais de uma vez para Olá mesmo blob novo ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="4af4d-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="4af4d-156">toodetermine se uma versão de determinado blob tiver sido processada, ele mantém *recebimentos de blob*.</span><span class="sxs-lookup"><span data-stu-id="4af4d-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="4af4d-157">Repositórios de funções do Azure blob recebimentos em um contêiner chamado *hosts de trabalhos Web do azure* em Olá conta de armazenamento do Azure para seu aplicativo de função (definido pela configuração de aplicativo hello `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="4af4d-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="4af4d-158">Confirmação de blob tem Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4af4d-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="4af4d-159">Olá disparou função ("*&lt;nome de função do aplicativo >*. Funções. * &lt;nome da função >*", por exemplo:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="4af4d-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="4af4d-160">nome do contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="4af4d-160">hello container name</span></span>
* <span data-ttu-id="4af4d-161">tipo de blob Hello ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4af4d-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4af4d-162">nome do blob Olá</span><span class="sxs-lookup"><span data-stu-id="4af4d-162">hello blob name</span></span>
* <span data-ttu-id="4af4d-163">Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4af4d-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="4af4d-164">tooforce reprocessamento de um blob, excluir a confirmação de blob de saudação para esse blob da saudação *hosts de trabalhos Web do azure* contêiner manualmente.</span><span class="sxs-lookup"><span data-stu-id="4af4d-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="4af4d-165">Manipulação de blobs suspeitos</span><span class="sxs-lookup"><span data-stu-id="4af4d-165">Handling poison blobs</span></span>
<span data-ttu-id="4af4d-166">Quando uma função de gatilho de blob falhar para um determinado blob, o Azure Functions repete essa função até cinco vezes por padrão.</span><span class="sxs-lookup"><span data-stu-id="4af4d-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="4af4d-167">Se todas as 5 tentativas falharem, funções do Azure adiciona uma fila de armazenamento de tooa mensagem denominada *webjobs-blobtrigger-suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="4af4d-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="4af4d-168">mensagem da fila Olá para blobs suspeitas é um objeto JSON que contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="4af4d-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="4af4d-169">FunctionId (no formato de saudação * &lt;nome de função do aplicativo >*. Funções. * &lt;nome da função >*)</span><span class="sxs-lookup"><span data-stu-id="4af4d-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="4af4d-170">BlobType ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4af4d-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4af4d-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="4af4d-171">ContainerName</span></span>
* <span data-ttu-id="4af4d-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="4af4d-172">BlobName</span></span>
* <span data-ttu-id="4af4d-173">ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4af4d-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="4af4d-174">Sondagem de blobs para grandes contêineres</span><span class="sxs-lookup"><span data-stu-id="4af4d-174">Blob polling for large containers</span></span>
<span data-ttu-id="4af4d-175">Se o contêiner de blob hello está sendo monitorado contém mais de 10.000 blobs, verificações de tempo de execução de funções de saudação log toowatch de arquivos para blobs novos ou alterados.</span><span class="sxs-lookup"><span data-stu-id="4af4d-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="4af4d-176">Esse processo não ocorre em tempo real.</span><span class="sxs-lookup"><span data-stu-id="4af4d-176">This process is not real time.</span></span> <span data-ttu-id="4af4d-177">Uma função não poderá obter disparada até vários minutos ou mais depois Olá blob é criado.</span><span class="sxs-lookup"><span data-stu-id="4af4d-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="4af4d-178">Além disso, [logs de armazenamento são criados da "melhor forma dentro do possível"](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="4af4d-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="4af4d-179">Não há nenhuma garantia de que todos os eventos são capturados.</span><span class="sxs-lookup"><span data-stu-id="4af4d-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="4af4d-180">Sob algumas condições, logs poderão ser perdidos.</span><span class="sxs-lookup"><span data-stu-id="4af4d-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="4af4d-181">Se você precisar de processamento de blob mais rápida ou mais confiável, considere a criação de um [mensagem da fila](../storage/queues/storage-dotnet-how-to-use-queues.md) ao criar blob hello.</span><span class="sxs-lookup"><span data-stu-id="4af4d-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="4af4d-182">Em seguida, use uma [gatilho fila](functions-bindings-storage-queue.md) em vez de um blob de saudação do blob gatilho tooprocess.</span><span class="sxs-lookup"><span data-stu-id="4af4d-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="4af4d-183">Usando um gatilho de blob e uma associação de entrada</span><span class="sxs-lookup"><span data-stu-id="4af4d-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="4af4d-184">Em funções do .NET, acessar dados de blob hello usando um parâmetro de método como `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="4af4d-185">Aqui, `paramName` é Olá valor especificado em Olá [configuração do disparador](#trigger).</span><span class="sxs-lookup"><span data-stu-id="4af4d-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="4af4d-186">Em funções do Node. js, Olá acesso entrada dados blob usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="4af4d-187">No .NET, você pode associar tooany dos tipos de saudação na lista de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="4af4d-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="4af4d-188">Se for usado como uma associação de entrada, alguns desses tipos exigem uma direção de associação `inout` no *function.json*.</span><span class="sxs-lookup"><span data-stu-id="4af4d-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="4af4d-189">Não há suporte para nessa direção pelo editor padrão do hello, portanto, você deve usar Olá editor avançado.</span><span class="sxs-lookup"><span data-stu-id="4af4d-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="4af4d-190">`ICloudBlob` (exige a direção de associação "inout")</span><span class="sxs-lookup"><span data-stu-id="4af4d-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="4af4d-191">`CloudBlockBlob` (exige a direção de associação "inout")</span><span class="sxs-lookup"><span data-stu-id="4af4d-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="4af4d-192">`CloudPageBlob` (exige a direção de associação "inout")</span><span class="sxs-lookup"><span data-stu-id="4af4d-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="4af4d-193">`CloudAppendBlob` (exige a direção de associação "inout")</span><span class="sxs-lookup"><span data-stu-id="4af4d-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="4af4d-194">Se os blobs de texto são esperados, você também pode associar tooa .NET `string` tipo.</span><span class="sxs-lookup"><span data-stu-id="4af4d-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="4af4d-195">Isso é recomendado somente se o tamanho do blob Olá é pequeno, como conteúdo de blob inteiro Olá é carregado na memória.</span><span class="sxs-lookup"><span data-stu-id="4af4d-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="4af4d-196">Geralmente, é preferível toouse um `Stream` ou `CloudBlockBlob` tipo.</span><span class="sxs-lookup"><span data-stu-id="4af4d-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="4af4d-197">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="4af4d-197">Trigger sample</span></span>
<span data-ttu-id="4af4d-198">Suponha que você tenha Olá function.json que define um gatilho de armazenamento de blob a seguir:</span><span class="sxs-lookup"><span data-stu-id="4af4d-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="4af4d-199">Consulte Olá específico do idioma exemplo registra o conteúdo de saudação de cada blob que é adicionado contêiner monitorado toohello.</span><span class="sxs-lookup"><span data-stu-id="4af4d-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="4af4d-200">C#</span><span class="sxs-lookup"><span data-stu-id="4af4d-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="4af4d-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="4af4d-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="4af4d-202">Exemplos de gatilho de blob em C#</span><span class="sxs-lookup"><span data-stu-id="4af4d-202">Blob trigger examples in C#</span></span> #

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

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="4af4d-203">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="4af4d-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="4af4d-204">Usando uma associação de saída de blob</span><span class="sxs-lookup"><span data-stu-id="4af4d-204">Using a blob output binding</span></span>

<span data-ttu-id="4af4d-205">Em funções do .NET, você deve usar um `out string` parâmetro em sua assinatura de função ou usar um dos tipos de saudação em Olá lista a seguir.</span><span class="sxs-lookup"><span data-stu-id="4af4d-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="4af4d-206">Funções do Node. js, você acessa Olá saída blob usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="4af4d-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="4af4d-207">Em funções do .NET, você pode extrair tooany de saudação tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4af4d-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="4af4d-208">Gatilho de fila com amostra de entrada e saída de blob</span><span class="sxs-lookup"><span data-stu-id="4af4d-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="4af4d-209">Suponha que você tenha Olá function.json a seguir, que define uma [gatilho de armazenamento de fila](functions-bindings-storage-queue.md), um armazenamento de blob de entrada e saída de um armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="4af4d-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="4af4d-210">Aviso uso Olá Olá `queueTrigger` propriedade de metadados.</span><span class="sxs-lookup"><span data-stu-id="4af4d-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="4af4d-211">no blob de saudação de entrada e saída `path` propriedades:</span><span class="sxs-lookup"><span data-stu-id="4af4d-211">in hello blob input and output `path` properties:</span></span>

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

<span data-ttu-id="4af4d-212">Consulte Olá específico do idioma exemplo que copia o blob de saída de toohello Olá blob de entrada.</span><span class="sxs-lookup"><span data-stu-id="4af4d-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="4af4d-213">C#</span><span class="sxs-lookup"><span data-stu-id="4af4d-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="4af4d-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="4af4d-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="4af4d-215">Exemplo de associação de blob em C#</span><span class="sxs-lookup"><span data-stu-id="4af4d-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="4af4d-216">Exemplo de associação de blob em Node.js</span><span class="sxs-lookup"><span data-stu-id="4af4d-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="4af4d-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4af4d-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

