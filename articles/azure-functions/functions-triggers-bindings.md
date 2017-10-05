---
title: "Trabalhar com gatilhos e associações no Azure Functions | Microsoft Docs"
description: "Saiba como usar gatilhos e associações no Azure Functions para conectar a execução de seu código a eventos online e a serviços baseados em nuvem."
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
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="ef7a2-104">Conceitos de gatilhos e de associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ef7a2-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="ef7a2-105">O Azure Functions permite escrever código em resposta a eventos no Azure e outros serviços, por meio de *gatilhos* e *associações*.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="ef7a2-106">Este artigo é uma visão geral conceitual dos gatilhos e associações para todas as linguagens de programação com suporte.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="ef7a2-107">Recursos que são comuns a todas as associações são descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="ef7a2-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ef7a2-108">Overview</span></span>

<span data-ttu-id="ef7a2-109">Gatilhos e associações são uma forma declarativa de definir como uma função é invocada e com que dados ela trabalha.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="ef7a2-110">Um *gatilho* define como uma função é invocada.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="ef7a2-111">Uma função deve ter exatamente um gatilho.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="ef7a2-112">Gatilhos têm dados associados, que geralmente é o conteúdo que disparou a função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="ef7a2-113">*Associações* de entrada e saída fornecem uma maneira declarativa de se conectar aos dados de dentro do seu código.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="ef7a2-114">Semelhante aos gatilhos, as cadeias de conexão e outras propriedades são especificadas na configuração da função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="ef7a2-115">Associações são opcionais e uma função pode ter várias associações de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="ef7a2-116">Usando gatilhos e associações, você pode escrever código que é mais genérico e não codificar os detalhes dos serviços com os quais ele interage.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="ef7a2-117">Dados provenientes de serviços simplesmente tornam-se valores de entrada para o código de função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="ef7a2-118">Para exibir os dados de saída para outro serviço (tal como criar uma nova linha no Armazenamento de Tabelas do Azure), use o valor retornado do método.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="ef7a2-119">Ou então, se você precisar gerar vários valores de saída, use um objeto auxiliar.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="ef7a2-120">Gatilhos e associações têm uma propriedade **name**, que é um identificador usado no código para acessar a associação.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="ef7a2-121">Você pode configurar os gatilhos e associações na guia **Integrar** no Portal do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="ef7a2-122">Nos bastidores, a interface do usuário modifica um arquivo chamado *function.json* arquivo no diretório da função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="ef7a2-123">Você pode editar esse arquivo mudando para o **Editor avançado**.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="ef7a2-124">A tabela a seguir mostra os gatilhos e as associações com suporte no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="ef7a2-125">Exemplo: gatilho de fila e associação de saída de tabela</span><span class="sxs-lookup"><span data-stu-id="ef7a2-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="ef7a2-126">Suponha que você deseja gravar uma nova linha no Armazenamento de Tabelas do Azure sempre que uma nova mensagem aparece no Armazenamento de Filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="ef7a2-127">Esse cenário pode ser implementado usando um gatilho de Filas do Azure e uma associação de saída de Tabela.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="ef7a2-128">Um gatilho de fila requer as seguintes informações na guia **Integrar**:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="ef7a2-129">O nome da configuração do aplicativo que contém a cadeia de conexão da conta de armazenamento para a fila</span><span class="sxs-lookup"><span data-stu-id="ef7a2-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="ef7a2-130">O nome da fila</span><span class="sxs-lookup"><span data-stu-id="ef7a2-130">The queue name</span></span>
* <span data-ttu-id="ef7a2-131">O identificador em seu código para ler o conteúdo da mensagem da fila, como `order`.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="ef7a2-132">Para gravar no Armazenamento de Tabelas do Azure, use uma associação de saída com os seguintes detalhes:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="ef7a2-133">O nome da configuração do aplicativo que contém a cadeia de conexão de conta de armazenamento para a tabela</span><span class="sxs-lookup"><span data-stu-id="ef7a2-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="ef7a2-134">O nome da tabela</span><span class="sxs-lookup"><span data-stu-id="ef7a2-134">The table name</span></span>
* <span data-ttu-id="ef7a2-135">O identificador em seu código para criar itens de saída, ou o valor retornado da função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="ef7a2-136">Associações usam as configurações de aplicativo para cadeias de conexão para impor a melhor prática que dita que *function.json* não contêm segredos do serviço.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="ef7a2-137">Em seguida, use os identificadores que você forneceu para integrar o Armazenamento do Azure em seu código.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
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

<span data-ttu-id="ef7a2-138">Este é o *function.json* que corresponde ao código anterior.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="ef7a2-139">Observe que a mesma configuração pode ser usada, independentemente da linguagem de implementação da função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

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
<span data-ttu-id="ef7a2-140">Para exibir e editar o conteúdo de *function.json* no Portal do Azure, clique na opção **Editor avançado** na guia **Integrar** da sua função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="ef7a2-141">Para ver exemplos de código e detalhes sobre a integração com o Armazenamento do Azure, consulte [Gatilhos e associações do Azure Functions para o Armazenamento do Azure](functions-bindings-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ef7a2-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="ef7a2-142">Direção de associação</span><span class="sxs-lookup"><span data-stu-id="ef7a2-142">Binding direction</span></span>

<span data-ttu-id="ef7a2-143">Todos os disparadores e associações têm uma propriedade `direction`:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="ef7a2-144">Para gatilhos, a direção sempre é `in`</span><span class="sxs-lookup"><span data-stu-id="ef7a2-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="ef7a2-145">Associações de entrada e saída usam `in` e `out`</span><span class="sxs-lookup"><span data-stu-id="ef7a2-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="ef7a2-146">Algumas associações dão suporte a uma direção especial `inout`.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="ef7a2-147">Se você usar `inout`, somente o **Editor avançado** estará disponível na guia **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="ef7a2-148">Usando o tipo de retorno da função para retornar um único resultado</span><span class="sxs-lookup"><span data-stu-id="ef7a2-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="ef7a2-149">O exemplo anterior mostra como usar o valor retornado da função para fornecer saída para uma associação, que é obtida usando o parâmetro de nome especial `$return`.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="ef7a2-150">(Isso tem suporte em linguagens que têm um valor retornado, como C#, JavaScript e F#.) Se uma função tiver várias associações de saída, use `$return` apenas para uma delas.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="ef7a2-151">Os exemplos a seguir mostram como tipos de retorno são usados com associações de saída em C#, JavaScript e F#.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in the second parameter to context.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="ef7a2-152">Associação da propriedade dataType</span><span class="sxs-lookup"><span data-stu-id="ef7a2-152">Binding dataType property</span></span>

<span data-ttu-id="ef7a2-153">No .NET, use os tipos para definir o tipo de dados para os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="ef7a2-154">Por exemplo, use `string` para associar ao texto de um gatilho de fila e uma matriz de bytes para ler como binário.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="ef7a2-155">Para idiomas que são digitados dinamicamente como JavaScript, use a propriedade `dataType` na definição da associação.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="ef7a2-156">Por exemplo, para ler o conteúdo de uma solicitação HTTP em formato binário, use o tipo `binary`:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="ef7a2-157">Outras opções para `dataType` são `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="ef7a2-158">Resolvendo configurações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ef7a2-158">Resolving app settings</span></span>
<span data-ttu-id="ef7a2-159">Como prática recomendada, os segredos e cadeias de conexão devem ser gerenciados usando configurações do aplicativo, em vez de arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="ef7a2-160">Isso limita o acesso a esses segredos e torna seguro armazenar *function.json* em um repositório de controle do código-fonte público.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="ef7a2-161">Configurações do aplicativo também são úteis sempre que você desejar alterar a configuração com base no ambiente.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="ef7a2-162">Por exemplo, em um ambiente de teste, pode ser útil monitorar um contêiner de armazenamento de filas ou de blobs diferente.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="ef7a2-163">Configurações do aplicativo são resolvidas sempre que um valor está entre sinais de porcentagem, como `%MyAppSetting%`.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="ef7a2-164">Observe que a propriedade `connection` dos gatilhos e associações é um caso especial e resolve automaticamente os valores de configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="ef7a2-165">O exemplo a seguir é um gatilho de fila que usa uma configuração de aplicativo `%input-queue-name%` para definir a fila de gatilho.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="ef7a2-166">Propriedades de metadados de gatilho</span><span class="sxs-lookup"><span data-stu-id="ef7a2-166">Trigger metadata properties</span></span>

<span data-ttu-id="ef7a2-167">Além do conteúdo dos dados fornecido por um gatilho (como a mensagem da fila que disparou uma função), vários gatilhos fornecem valores de metadados adicionais.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="ef7a2-168">Esses valores podem ser usados como parâmetros de entrada em C# e F# ou propriedades no objeto `context.bindings` em JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="ef7a2-169">Por exemplo, um gatilho de fila dá suporte às seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="ef7a2-170">QueueTrigger – disparar o conteúdo da mensagem em caso de uma cadeia de caracteres válida</span><span class="sxs-lookup"><span data-stu-id="ef7a2-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="ef7a2-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="ef7a2-171">DequeueCount</span></span>
* <span data-ttu-id="ef7a2-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="ef7a2-172">ExpirationTime</span></span>
* <span data-ttu-id="ef7a2-173">ID</span><span class="sxs-lookup"><span data-stu-id="ef7a2-173">Id</span></span>
* <span data-ttu-id="ef7a2-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="ef7a2-174">InsertionTime</span></span>
* <span data-ttu-id="ef7a2-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="ef7a2-175">NextVisibleTime</span></span>
* <span data-ttu-id="ef7a2-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="ef7a2-176">PopReceipt</span></span>

<span data-ttu-id="ef7a2-177">Detalhes de propriedades de metadados para cada gatilho são descritos no tópico de referência correspondente.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="ef7a2-178">A documentação também está disponível na guia **Integrar** do portal, na seção **Documentação** abaixo da área de configuração de associação.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="ef7a2-179">Por exemplo, como gatilhos de blobs apresentam alguns atrasos, você pode usar um gatilho de fila para executar sua função (consulte [Gatilho de Armazenamento de Blobs](functions-bindings-storage-blob.md#storage-blob-trigger).</span><span class="sxs-lookup"><span data-stu-id="ef7a2-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="ef7a2-180">A mensagem da fila conteria o nome do arquivo a ser disparado no blob.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="ef7a2-181">Usando a propriedade de metadados `queueTrigger`, é possível especificar esse comportamento completo na sua configuração, em vez do código.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="ef7a2-182">Propriedades de metadados de um gatilho também podem ser usadas em uma *expressão de associação* para outra associação, conforme descrito na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="ef7a2-183">Padrões e expressões de associação</span><span class="sxs-lookup"><span data-stu-id="ef7a2-183">Binding expressions and patterns</span></span>

<span data-ttu-id="ef7a2-184">Um dos recursos mais poderosos de gatilhos e associações são as *expressões de associação*.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="ef7a2-185">Dentro da associação, é possível definir expressões padrão que podem ser usadas em outras associações ou no seu código.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="ef7a2-186">Metadados de gatilho também podem ser usado em expressões de associação, como mostrado no exemplo na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="ef7a2-187">Por exemplo, suponha que você deseja redimensionar imagens no contêiner de armazenamento de blobs específico, semelhante ao modelo **Redimensionador de Imagem** na página **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="ef7a2-188">Acesse **Nova Função** -> Linguagem **C#** -> Cenário **Exemplos** -> **ImageResizer-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="ef7a2-189">Essa é a definição *function.json*:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-189">Here is the *function.json* definition:</span></span>

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

<span data-ttu-id="ef7a2-190">Observe que o parâmetro `filename` é usado na definição do gatilho de blobs e na associação de saída de blobs.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="ef7a2-191">Esse parâmetro também pode ser usado no código de função.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="ef7a2-192">GUIDs aleatórios</span><span class="sxs-lookup"><span data-stu-id="ef7a2-192">Random GUIDs</span></span>
<span data-ttu-id="ef7a2-193">O Azure Functions fornece uma sintaxe conveniente para gerar GUIDs em suas associações por meio da expressão de associação `{rand-guid}`.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="ef7a2-194">O exemplo a seguir usa isso para gerar um nome exclusivo de blob:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="ef7a2-195">Hora atual</span><span class="sxs-lookup"><span data-stu-id="ef7a2-195">Current time</span></span>

<span data-ttu-id="ef7a2-196">Você pode usar a expressão de associação `DateTime`, que resolve para `DateTime.UtcNow`.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="ef7a2-197">Associe as propriedades personalizadas de entrada em uma expressão de associação</span><span class="sxs-lookup"><span data-stu-id="ef7a2-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="ef7a2-198">Expressões de associação também podem fazer referência a propriedades que são definidas no próprio conteúdo de gatilho.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="ef7a2-199">Por exemplo, pode ser útil associar dinamicamente um arquivos de armazenamento de blobs de um nome de arquivo fornecido em um webhook.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="ef7a2-200">Por exemplo, o *function.json* a seguir usa uma propriedade chamada `BlobName` do conteúdo do gatilho:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

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

<span data-ttu-id="ef7a2-201">Para fazer isso em C# e F#, você deve definir um POCO que define os campos que serão desserializados no conteúdo do gatilho.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

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

<span data-ttu-id="ef7a2-202">No JavaScript, a desserialização JSON é executada automaticamente e você pode usar as propriedades diretamente.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="ef7a2-203">Configuração de associação de dados em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="ef7a2-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="ef7a2-204">No C# e em outras linguagens .NET, você pode usar um padrão de associação obrigatório, em vez de associações declarativas em *function.json*.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="ef7a2-205">A associação obrigatória é útil quando os parâmetros de associação precisam ser calculado no tempo de execução, em vez do tempo de design.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="ef7a2-206">Para obter mais informações, consulte [Associação em tempo de execução por meio de associações obrigatórias](functions-reference-csharp.md#imperative-bindings) na referência do desenvolvedor do C#.</span><span class="sxs-lookup"><span data-stu-id="ef7a2-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef7a2-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef7a2-207">Next steps</span></span>
<span data-ttu-id="ef7a2-208">Para saber mais sobre uma associação específica, consulte os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ef7a2-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="ef7a2-209">HTTP e webhooks</span><span class="sxs-lookup"><span data-stu-id="ef7a2-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="ef7a2-210">Timer</span><span class="sxs-lookup"><span data-stu-id="ef7a2-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="ef7a2-211">Armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="ef7a2-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="ef7a2-212">Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="ef7a2-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="ef7a2-213">Armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="ef7a2-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="ef7a2-214">Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="ef7a2-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="ef7a2-215">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ef7a2-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="ef7a2-216">BD Cosmos</span><span class="sxs-lookup"><span data-stu-id="ef7a2-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="ef7a2-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="ef7a2-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="ef7a2-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="ef7a2-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="ef7a2-219">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="ef7a2-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="ef7a2-220">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="ef7a2-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="ef7a2-221">Arquivo externo</span><span class="sxs-lookup"><span data-stu-id="ef7a2-221">External file</span></span>](functions-bindings-external-file.md)
