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
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="26295-104">Conceitos de gatilhos e de associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="26295-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="26295-105">As funções do Azure permite toowrite código na resposta tooevents no Azure e outros serviços, pela *gatilhos* e *associações*.</span><span class="sxs-lookup"><span data-stu-id="26295-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="26295-106">Este artigo é uma visão geral conceitual dos gatilhos e associações para todas as linguagens de programação com suporte.</span><span class="sxs-lookup"><span data-stu-id="26295-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="26295-107">Recursos que são associações de tooall comuns são descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="26295-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="26295-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="26295-108">Overview</span></span>

<span data-ttu-id="26295-109">Associações e gatilhos são uma forma declarativa toodefine como uma função é chamada e quais dados ele funciona com.</span><span class="sxs-lookup"><span data-stu-id="26295-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="26295-110">Um *gatilho* define como uma função é invocada.</span><span class="sxs-lookup"><span data-stu-id="26295-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="26295-111">Uma função deve ter exatamente um gatilho.</span><span class="sxs-lookup"><span data-stu-id="26295-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="26295-112">Gatilhos com dados, que geralmente é carga Olá que disparou a função hello associados.</span><span class="sxs-lookup"><span data-stu-id="26295-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="26295-113">Entrada e saída *associações* fornecem um toodata de tooconnect de forma declarativa de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="26295-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="26295-114">Tootriggers semelhante, você especificar cadeias de caracteres de conexão e outras propriedades na sua configuração de função.</span><span class="sxs-lookup"><span data-stu-id="26295-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="26295-115">Associações são opcionais e uma função pode ter várias associações de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="26295-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="26295-116">Usando gatilhos e associações, você pode escrever código que é mais genérico e não não codificar Olá detalhes dos serviços de saudação com a qual ele interage.</span><span class="sxs-lookup"><span data-stu-id="26295-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="26295-117">Dados provenientes de serviços simplesmente tornam-se valores de entrada para o código de função.</span><span class="sxs-lookup"><span data-stu-id="26295-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="26295-118">serviço toooutput de tooanother de dados (como criar uma nova linha no armazenamento de tabela do Azure), use o valor de retorno de saudação do método hello.</span><span class="sxs-lookup"><span data-stu-id="26295-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="26295-119">Ou, se você precisar toooutput vários valores, use um objeto auxiliar.</span><span class="sxs-lookup"><span data-stu-id="26295-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="26295-120">Gatilhos e associações possuem um **nome** propriedade, que é um identificador que você usa em sua associação de saudação do código tooaccess.</span><span class="sxs-lookup"><span data-stu-id="26295-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="26295-121">Você pode configurar associações e gatilhos Olá **integrar** no portal do Azure funções hello.</span><span class="sxs-lookup"><span data-stu-id="26295-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="26295-122">Sob Olá coberturas, a saudação da interface do usuário modifica um arquivo chamado *function.json* arquivo no diretório de função hello.</span><span class="sxs-lookup"><span data-stu-id="26295-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="26295-123">Você pode editar esse arquivo alterando toohello **editor avançado**.</span><span class="sxs-lookup"><span data-stu-id="26295-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="26295-124">Olá tabela a seguir mostra os gatilhos de saudação e associações que são compatíveis com funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="26295-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="26295-125">Exemplo: gatilho de fila e associação de saída de tabela</span><span class="sxs-lookup"><span data-stu-id="26295-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="26295-126">Suponha que você queira toowrite um tooAzure de linha novo armazenamento de tabela sempre que uma nova mensagem é exibida no armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="26295-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="26295-127">Esse cenário pode ser implementado usando um gatilho de Filas do Azure e uma associação de saída de Tabela.</span><span class="sxs-lookup"><span data-stu-id="26295-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="26295-128">Olá Olá informações a seguir exige que um gatilho de fila **integrar** guia:</span><span class="sxs-lookup"><span data-stu-id="26295-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="26295-129">nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão de conta de armazenamento Olá para fila Olá</span><span class="sxs-lookup"><span data-stu-id="26295-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="26295-130">nome da fila Olá</span><span class="sxs-lookup"><span data-stu-id="26295-130">hello queue name</span></span>
* <span data-ttu-id="26295-131">Olá identificador em seu conteúdo de Olá tooread código de mensagem da fila de saudação, como `order`.</span><span class="sxs-lookup"><span data-stu-id="26295-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="26295-132">toowrite tooAzure armazenamento de tabela, use uma associação de saída com hello detalhes a seguir:</span><span class="sxs-lookup"><span data-stu-id="26295-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="26295-133">nome de saudação da configuração de aplicativo hello que contém a cadeia de conexão de conta de armazenamento Olá para tabela Olá</span><span class="sxs-lookup"><span data-stu-id="26295-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="26295-134">nome da tabela Olá</span><span class="sxs-lookup"><span data-stu-id="26295-134">hello table name</span></span>
* <span data-ttu-id="26295-135">Identificador Olá toocreate seu código de saída itens ou valor de retorno de saudação do função hello.</span><span class="sxs-lookup"><span data-stu-id="26295-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="26295-136">Associações usam configurações do aplicativo para Olá tooenforce de cadeias de caracteres de conexão melhor práticas que *function.json* não contêm segredos de serviço.</span><span class="sxs-lookup"><span data-stu-id="26295-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="26295-137">Em seguida, use identificadores de saudação fornecido toointegrate com armazenamento do Azure no seu código.</span><span class="sxs-lookup"><span data-stu-id="26295-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

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

<span data-ttu-id="26295-138">Aqui está a saudação *function.json* que corresponde a toohello anterior do código.</span><span class="sxs-lookup"><span data-stu-id="26295-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="26295-139">Observe que Olá a mesma configuração pode ser usada, independentemente do idioma de saudação da implementação da função hello.</span><span class="sxs-lookup"><span data-stu-id="26295-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

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
<span data-ttu-id="26295-140">tooview e editar conteúdo de saudação do *function.json* no hello portal do Azure, clique em Olá **editor avançado** opção em Olá **integrar** guia de sua função.</span><span class="sxs-lookup"><span data-stu-id="26295-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="26295-141">Para ver exemplos de código e detalhes sobre a integração com o Armazenamento do Azure, consulte [Gatilhos e associações do Azure Functions para o Armazenamento do Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="26295-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="26295-142">Direção de associação</span><span class="sxs-lookup"><span data-stu-id="26295-142">Binding direction</span></span>

<span data-ttu-id="26295-143">Todos os disparadores e associações têm uma propriedade `direction`:</span><span class="sxs-lookup"><span data-stu-id="26295-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="26295-144">Para gatilhos, direção Olá é sempre`in`</span><span class="sxs-lookup"><span data-stu-id="26295-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="26295-145">Associações de entrada e saída usam `in` e `out`</span><span class="sxs-lookup"><span data-stu-id="26295-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="26295-146">Algumas associações dão suporte a uma direção especial `inout`.</span><span class="sxs-lookup"><span data-stu-id="26295-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="26295-147">Se você usar `inout`, somente Olá **editor avançado** está disponível no hello **integrar** guia.</span><span class="sxs-lookup"><span data-stu-id="26295-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="26295-148">Usando tooreturn tipo de retorno da função hello uma única saída</span><span class="sxs-lookup"><span data-stu-id="26295-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="26295-149">Olá exemplo anterior mostra como tooprovide de valor de retorno de função toouse Olá saída associação tooa, que é obtida usando o parâmetro de nome especial hello `$return`.</span><span class="sxs-lookup"><span data-stu-id="26295-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="26295-150">(Isso tem suporte em linguagens que têm um valor retornado, como C#, JavaScript e F#.) Se uma função tiver várias associações de saída, use `$return` apenas para uma saudação de associações de saída.</span><span class="sxs-lookup"><span data-stu-id="26295-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="26295-151">exemplos de saudação abaixo mostra como retornam tipos são usados com associações de saída em c#, JavaScript e F #.</span><span class="sxs-lookup"><span data-stu-id="26295-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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

## <a name="binding-datatype-property"></a><span data-ttu-id="26295-152">Associação da propriedade dataType</span><span class="sxs-lookup"><span data-stu-id="26295-152">Binding dataType property</span></span>

<span data-ttu-id="26295-153">No .NET, use o tipo de dados do hello tipos toodefine Olá para dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="26295-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="26295-154">Por exemplo, use `string` toobind toohello texto de um gatilho de fila e um tooread de matriz de bytes como binário.</span><span class="sxs-lookup"><span data-stu-id="26295-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="26295-155">Para idiomas dinamicamente são digitados como JavaScript, use Olá `dataType` propriedade na definição de associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="26295-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="26295-156">Por exemplo, tooread Olá conteúdo de uma solicitação HTTP em formato binário, use o tipo de saudação `binary`:</span><span class="sxs-lookup"><span data-stu-id="26295-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="26295-157">Outras opções para `dataType` são `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="26295-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="26295-158">Resolvendo configurações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="26295-158">Resolving app settings</span></span>
<span data-ttu-id="26295-159">Como prática recomendada, os segredos e cadeias de conexão devem ser gerenciados usando configurações do aplicativo, em vez de arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="26295-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="26295-160">Isso limita o acesso toothese segredos e torna seguro toostore *function.json* em um repositório de controle de origem pública.</span><span class="sxs-lookup"><span data-stu-id="26295-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="26295-161">Configurações do aplicativo também são úteis sempre que quiser toochange configuração com base no ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="26295-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="26295-162">Por exemplo, em um ambiente de teste, convém toomonitor um contêiner de armazenamento de blob ou fila diferente.</span><span class="sxs-lookup"><span data-stu-id="26295-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="26295-163">Configurações do aplicativo são resolvidas sempre que um valor está entre sinais de porcentagem, como `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="26295-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="26295-164">Observe que Olá `connection` é um caso especial de propriedade de gatilhos e associações e resolve automaticamente os valores de configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26295-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="26295-165">Olá, exemplo a seguir é um gatilho de fila que usa uma configuração de aplicativo `%input-queue-name%` toodefine Olá fila tootrigger em.</span><span class="sxs-lookup"><span data-stu-id="26295-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="26295-166">Propriedades de metadados de gatilho</span><span class="sxs-lookup"><span data-stu-id="26295-166">Trigger metadata properties</span></span>

<span data-ttu-id="26295-167">Em adição toohello dados carga fornecida por um gatilho (como fila mensagem de saudação que disparou uma função), vários disparadores fornecem valores de metadados adicionais.</span><span class="sxs-lookup"><span data-stu-id="26295-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="26295-168">Esses valores podem ser usados como parâmetros de entrada em c# e F # ou propriedades em Olá `context.bindings` objeto em JavaScript.</span><span class="sxs-lookup"><span data-stu-id="26295-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="26295-169">Por exemplo, um gatilho de fila dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="26295-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="26295-170">QueueTrigger – disparar o conteúdo da mensagem em caso de uma cadeia de caracteres válida</span><span class="sxs-lookup"><span data-stu-id="26295-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="26295-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="26295-171">DequeueCount</span></span>
* <span data-ttu-id="26295-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="26295-172">ExpirationTime</span></span>
* <span data-ttu-id="26295-173">ID</span><span class="sxs-lookup"><span data-stu-id="26295-173">Id</span></span>
* <span data-ttu-id="26295-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="26295-174">InsertionTime</span></span>
* <span data-ttu-id="26295-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="26295-175">NextVisibleTime</span></span>
* <span data-ttu-id="26295-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="26295-176">PopReceipt</span></span>

<span data-ttu-id="26295-177">Detalhes de propriedades de metadados para cada gatilho são descritos no tópico de referência correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="26295-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="26295-178">Documentação também está disponível em Olá **integrar** guia do portal hello, em Olá **documentação** seção abaixo da área de configuração de associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="26295-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="26295-179">Por exemplo, como gatilhos de blob tem alguns atrasos, você pode usar um toorun de gatilho de fila sua função (consulte [gatilho de armazenamento de Blob](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="26295-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="26295-180">mensagem de saudação do fila conteria Olá blob filename tootrigger em.</span><span class="sxs-lookup"><span data-stu-id="26295-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="26295-181">Usando Olá `queueTrigger` propriedade de metadados, você pode especificar esse comportamento em sua configuração, em vez de seu código.</span><span class="sxs-lookup"><span data-stu-id="26295-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="26295-182">Propriedades de metadados de um gatilho também podem ser usadas em uma *associação expressão* para outra associação, como Olá descrito na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="26295-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="26295-183">Padrões e expressões de associação</span><span class="sxs-lookup"><span data-stu-id="26295-183">Binding expressions and patterns</span></span>

<span data-ttu-id="26295-184">Um dos recursos mais avançados de saudação de gatilhos e associações é *expressões de associação*.</span><span class="sxs-lookup"><span data-stu-id="26295-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="26295-185">Dentro da associação, é possível definir expressões padrão que podem ser usadas em outras associações ou no seu código.</span><span class="sxs-lookup"><span data-stu-id="26295-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="26295-186">Metadados de gatilho também podem ser usado em associação de expressões, como é mostrado no exemplo de Olá Olá anterior da seção.</span><span class="sxs-lookup"><span data-stu-id="26295-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="26295-187">Por exemplo, suponha que você deseja tooresize imagens no contêiner de armazenamento de blob específico, toohello semelhante **redimensionamento da imagem** modelo Olá **nova função** página.</span><span class="sxs-lookup"><span data-stu-id="26295-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="26295-188">Vá muito**nova função** -> idioma **c#** -> cenário **exemplos** -> **ImageResizer CSharp**.</span><span class="sxs-lookup"><span data-stu-id="26295-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="26295-189">Aqui está a saudação *function.json* definição:</span><span class="sxs-lookup"><span data-stu-id="26295-189">Here is hello *function.json* definition:</span></span>

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

<span data-ttu-id="26295-190">Observe que Olá `filename` parâmetro é usado na definição de gatilho de blob hello, bem como blob Olá associação de saída.</span><span class="sxs-lookup"><span data-stu-id="26295-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="26295-191">Esse parâmetro também pode ser usado no código de função.</span><span class="sxs-lookup"><span data-stu-id="26295-191">This parameter can also be used in function code.</span></span>

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


### <a name="random-guids"></a><span data-ttu-id="26295-192">GUIDs aleatórios</span><span class="sxs-lookup"><span data-stu-id="26295-192">Random GUIDs</span></span>
<span data-ttu-id="26295-193">As funções do Azure fornece uma sintaxe de conveniência para gerar GUIDs em suas associações, a saudação `{rand-guid}` expressão de associação.</span><span class="sxs-lookup"><span data-stu-id="26295-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="26295-194">Olá, exemplo a seguir usa este toogenerate um nome exclusivo de blob:</span><span class="sxs-lookup"><span data-stu-id="26295-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="26295-195">Hora atual</span><span class="sxs-lookup"><span data-stu-id="26295-195">Current time</span></span>

<span data-ttu-id="26295-196">Você pode usar uma expressão de associação Olá `DateTime`, que resolve muito`DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="26295-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="26295-197">Associar propriedades de entrada toocustom em uma expressão de associação</span><span class="sxs-lookup"><span data-stu-id="26295-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="26295-198">Expressões de associação também podem referenciar as propriedades que são definidas na carga de gatilho Olá em si.</span><span class="sxs-lookup"><span data-stu-id="26295-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="26295-199">Por exemplo, talvez você queira arquivo de armazenamento de blob toodynamically bind tooa de um nome de arquivo fornecido em um webhook.</span><span class="sxs-lookup"><span data-stu-id="26295-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="26295-200">Por exemplo, Olá a seguir *function.json* usa uma propriedade chamada `BlobName` da carga de gatilho Olá:</span><span class="sxs-lookup"><span data-stu-id="26295-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

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

<span data-ttu-id="26295-201">tooaccomplish esse em c# e F #, você deve definir um POCO que define os campos de saudação que serão desserializados na carga de gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="26295-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

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

<span data-ttu-id="26295-202">Em JavaScript, desserialização JSON é executada automaticamente e você pode usar propriedades de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="26295-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="26295-203">Configuração de associação de dados em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="26295-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="26295-204">Em c# e outras linguagens .NET, você pode usar um padrão de associação fundamental, como associações de toohello contrário declarativa em *function.json*.</span><span class="sxs-lookup"><span data-stu-id="26295-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="26295-205">Associação fundamental é útil quando precisam de parâmetros de ligação toobe computado em tempo de execução, em vez de design.</span><span class="sxs-lookup"><span data-stu-id="26295-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="26295-206">mais, consulte toolearn [associação em tempo de execução por meio de ligações fundamental](functions-reference-csharp.md#imperative-bindings) na referência do desenvolvedor Olá c#.</span><span class="sxs-lookup"><span data-stu-id="26295-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26295-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26295-207">Next steps</span></span>
<span data-ttu-id="26295-208">Para obter mais informações sobre uma associação específica, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="26295-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="26295-209">HTTP e webhooks</span><span class="sxs-lookup"><span data-stu-id="26295-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="26295-210">Timer</span><span class="sxs-lookup"><span data-stu-id="26295-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="26295-211">Armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="26295-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="26295-212">Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="26295-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="26295-213">Armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="26295-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="26295-214">Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="26295-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="26295-215">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="26295-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="26295-216">BD Cosmos</span><span class="sxs-lookup"><span data-stu-id="26295-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="26295-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="26295-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="26295-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="26295-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="26295-219">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="26295-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="26295-220">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="26295-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="26295-221">Arquivo externo</span><span class="sxs-lookup"><span data-stu-id="26295-221">External file</span></span>](functions-bindings-external-file.md)
