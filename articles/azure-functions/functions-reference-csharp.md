---
title: "aaaAzure Referência do desenvolvedor funções Script c# | Microsoft Docs"
description: "Entender como toodevelop funções do Azure usando o c#."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="a49cf-104">Referência do desenvolvedor de scripts C# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a49cf-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a49cf-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="a49cf-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="a49cf-106">Script em F#</span><span class="sxs-lookup"><span data-stu-id="a49cf-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="a49cf-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="a49cf-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="a49cf-108">Olá c# experiência de script para funções do Azure baseia-se em Olá SDK do Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="a49cf-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="a49cf-109">Fluxos de dados na sua função C# por meio de argumentos de método.</span><span class="sxs-lookup"><span data-stu-id="a49cf-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="a49cf-110">Os nomes de argumento são especificados em `function.json`, e existem nomes predefinidos para acessar as coisas como Olá tokens de agente e o cancelamento de função.</span><span class="sxs-lookup"><span data-stu-id="a49cf-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="a49cf-111">Este artigo pressupõe que você já leu Olá [referência do desenvolvedor do Azure funções](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a49cf-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="a49cf-112">Para obter informações sobre como usar as bibliotecas de classes C#, consulte [Usando bibliotecas de classes do .NET com o Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="a49cf-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="a49cf-113">Como o .csx funciona</span><span class="sxs-lookup"><span data-stu-id="a49cf-113">How .csx works</span></span>
<span data-ttu-id="a49cf-114">Olá `.csx` formato permite que você toowrite menos "boilerplate" e foco sobre a escrita de apenas uma função c#.</span><span class="sxs-lookup"><span data-stu-id="a49cf-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="a49cf-115">Inclua todos os namespaces no início de saudação do arquivo hello e referências de assembly como de costume.</span><span class="sxs-lookup"><span data-stu-id="a49cf-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="a49cf-116">Em vez de encapsular tudo em um namespace e uma classe, basta definir um método `Run`.</span><span class="sxs-lookup"><span data-stu-id="a49cf-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="a49cf-117">Se você precisar tooinclude todas as classes, para a instância toodefine simples objetos antigo objeto CLR (POCO), você pode incluir uma classe em Olá mesmo arquivo.</span><span class="sxs-lookup"><span data-stu-id="a49cf-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="a49cf-118">Associação tooarguments</span><span class="sxs-lookup"><span data-stu-id="a49cf-118">Binding tooarguments</span></span>
<span data-ttu-id="a49cf-119">Olá, várias associações são associados tooa c# função via Olá `name` propriedade Olá *function.json* configuração.</span><span class="sxs-lookup"><span data-stu-id="a49cf-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="a49cf-120">Cada associação tem seus próprios tipos com suporte; por exemplo, um gatilho de blob pode dar suporte a uma cadeia de caracteres, um POCO ou um CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="a49cf-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="a49cf-121">tipos de saudação com suporte são documentados na referência de Olá para cada associação.</span><span class="sxs-lookup"><span data-stu-id="a49cf-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="a49cf-122">Um objeto POCO deve ter um getter e setter definido para cada propriedade.</span><span class="sxs-lookup"><span data-stu-id="a49cf-122">A POCO object must have a getter and setter defined for each property.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="a49cf-123">Usando o valor retornado de um método em uma associação de saída</span><span class="sxs-lookup"><span data-stu-id="a49cf-123">Using method return value for output binding</span></span>

<span data-ttu-id="a49cf-124">Você pode usar um valor de retorno do método para uma associação de saída, usando o nome da saudação `$return` na *function.json*:</span><span class="sxs-lookup"><span data-stu-id="a49cf-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a><span data-ttu-id="a49cf-125">Gravando vários valores de saída</span><span class="sxs-lookup"><span data-stu-id="a49cf-125">Writing multiple output values</span></span>

<span data-ttu-id="a49cf-126">toowrite tooan de vários valores de saída de associação, use Olá [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) tipos.</span><span class="sxs-lookup"><span data-stu-id="a49cf-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="a49cf-127">Esses tipos são coleções de somente gravação que são a associação de saída toohello escrito quando o método hello for concluída.</span><span class="sxs-lookup"><span data-stu-id="a49cf-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="a49cf-128">Este exemplo grava várias mensagens de fila usando `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="a49cf-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="a49cf-129">Registro em log</span><span class="sxs-lookup"><span data-stu-id="a49cf-129">Logging</span></span>
<span data-ttu-id="a49cf-130">toolog saída tooyour os logs de streaming em c#, incluir um argumento do tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="a49cf-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="a49cf-131">Recomendamos nomeá-lo como `log`.</span><span class="sxs-lookup"><span data-stu-id="a49cf-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="a49cf-132">Evite usar `Console.Write` no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a49cf-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="a49cf-133">`TraceWriter`é definido em Olá [SDK do Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="a49cf-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="a49cf-134">Olá o nível de log para `TraceWriter` podem ser configurados em [host\.json].</span><span class="sxs-lookup"><span data-stu-id="a49cf-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="a49cf-135">Assíncrono</span><span class="sxs-lookup"><span data-stu-id="a49cf-135">Async</span></span>
<span data-ttu-id="a49cf-136">toomake uma função assíncrona, use Olá `async` palavra-chave e retornar um `Task` objeto.</span><span class="sxs-lookup"><span data-stu-id="a49cf-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="a49cf-137">Token de cancelamento</span><span class="sxs-lookup"><span data-stu-id="a49cf-137">Cancellation Token</span></span>
<span data-ttu-id="a49cf-138">Algumas operações exigem um desligamento normal.</span><span class="sxs-lookup"><span data-stu-id="a49cf-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="a49cf-139">Embora sempre seja melhor código toowrite que pode lidar com falha, em casos onde você deseja toohandle solicitações de desligamento normal, você define uma [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumento de tipo.</span><span class="sxs-lookup"><span data-stu-id="a49cf-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="a49cf-140">Um `CancellationToken` é fornecida toosignal que um desligamento de host é disparado.</span><span class="sxs-lookup"><span data-stu-id="a49cf-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="a49cf-141">Importando namespaces</span><span class="sxs-lookup"><span data-stu-id="a49cf-141">Importing namespaces</span></span>
<span data-ttu-id="a49cf-142">Se você precisar tooimport namespaces, você pode fazer isso como de costume, com hello `using` cláusula.</span><span class="sxs-lookup"><span data-stu-id="a49cf-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="a49cf-143">Olá namespaces a seguir são automaticamente importados e, portanto, são opcionais:</span><span class="sxs-lookup"><span data-stu-id="a49cf-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="a49cf-144">Referenciando Assemblies Externos</span><span class="sxs-lookup"><span data-stu-id="a49cf-144">Referencing External Assemblies</span></span>
<span data-ttu-id="a49cf-145">Para assemblies do framework, adicione referências usando Olá `#r "AssemblyName"` diretiva.</span><span class="sxs-lookup"><span data-stu-id="a49cf-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="a49cf-146">Hello assemblies a seguir são automaticamente adicionados pelas funções do Azure Olá ambiente de hospedagem:</span><span class="sxs-lookup"><span data-stu-id="a49cf-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="a49cf-147">Olá assemblies a seguir podem ser referenciados por nome simples (por exemplo, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="a49cf-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="a49cf-148">Referenciando assemblies personalizados</span><span class="sxs-lookup"><span data-stu-id="a49cf-148">Referencing custom assemblies</span></span>

<span data-ttu-id="a49cf-149">tooreference um assembly personalizado, você pode usar um *compartilhado* assembly ou um *privada* assembly:</span><span class="sxs-lookup"><span data-stu-id="a49cf-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="a49cf-150">Assemblies compartilhados são compartilhados entre todas as funções em um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="a49cf-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="a49cf-151">tooreference um assembly personalizado, carregar o aplicativo de função tooyour do assembly hello, como em um `bin` pasta na raiz do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="a49cf-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="a49cf-152">Assemblies particulares fazem parte do contexto de determinada função e dão suporte ao sideload de versões diferentes.</span><span class="sxs-lookup"><span data-stu-id="a49cf-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="a49cf-153">Assemblies privados devem ser carregados em um `bin` pasta no diretório de função hello.</span><span class="sxs-lookup"><span data-stu-id="a49cf-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="a49cf-154">Referência usando o nome do arquivo hello, como `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="a49cf-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="a49cf-155">Para obter informações sobre como tooupload arquivos de pasta de função tooyour, consulte Olá seção Gerenciamento de pacotes a seguir.</span><span class="sxs-lookup"><span data-stu-id="a49cf-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="a49cf-156">Diretórios inspecionados</span><span class="sxs-lookup"><span data-stu-id="a49cf-156">Watched directories</span></span>

<span data-ttu-id="a49cf-157">diretório Olá que contém o arquivo de script de função hello automaticamente é inspecionado tooassemblies de alterações.</span><span class="sxs-lookup"><span data-stu-id="a49cf-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="a49cf-158">toowatch alterações de assembly em outros diretórios, adicioná-las toohello `watchDirectories` lista [host\.json].</span><span class="sxs-lookup"><span data-stu-id="a49cf-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="a49cf-159">Usando pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="a49cf-159">Using NuGet packages</span></span>
<span data-ttu-id="a49cf-160">pacotes do NuGet toouse em uma função c#, carregar uma *Project* pasta toohello da função de arquivo no sistema de arquivos do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="a49cf-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="a49cf-161">Aqui está um exemplo *Project* arquivo que adiciona uma referência tooMicrosoft.ProjectOxford.Face versão 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="a49cf-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

<span data-ttu-id="a49cf-162">Apenas hello do .NET Framework 4.6 tem suporte, portanto certifique-se que seu *Project* arquivo especifica `net46` conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="a49cf-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="a49cf-163">Quando você carrega um *Project* de arquivos, hello em tempo de execução obtém os pacotes de saudação e adiciona automaticamente os assemblies do pacote toohello referências.</span><span class="sxs-lookup"><span data-stu-id="a49cf-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="a49cf-164">Você não precisa tooadd `#r "AssemblyName"` diretivas.</span><span class="sxs-lookup"><span data-stu-id="a49cf-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="a49cf-165">tipos de saudação toouse definidos em pacotes do NuGet hello, adicionar Olá necessário `using` instruções tooyour *run.csx* arquivo</span><span class="sxs-lookup"><span data-stu-id="a49cf-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="a49cf-166">Em tempo de execução de funções hello, a restauração do NuGet funciona comparando `project.json` e `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="a49cf-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="a49cf-167">Se Olá carimbos de data e hora dos arquivos de saudação **não** correspondência, uma restauração do NuGet executa e pacotes de atualização de downloads do NuGet.</span><span class="sxs-lookup"><span data-stu-id="a49cf-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="a49cf-168">No entanto, se hello carimbos de data e hora dos arquivos de saudação **fazer** correspondência, o NuGet não realizar uma restauração.</span><span class="sxs-lookup"><span data-stu-id="a49cf-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="a49cf-169">Portanto, `project.lock.json` não deve ser implantado porque ele faz com que a restauração do pacote do NuGet tooskip.</span><span class="sxs-lookup"><span data-stu-id="a49cf-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="a49cf-170">tooavoid Implantando o bloqueio de saudação do arquivo, adicione Olá `project.lock.json` toohello `.gitignore` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a49cf-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="a49cf-171">toouse um feed personalizado do NuGet, especifique Olá feed em uma *config* arquivo na raiz do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="a49cf-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="a49cf-172">Para obter mais informações, consulte [Configurando o comportamento do NuGet](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="a49cf-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="a49cf-173">Usando um arquivo project.json</span><span class="sxs-lookup"><span data-stu-id="a49cf-173">Using a project.json file</span></span>
1. <span data-ttu-id="a49cf-174">Abra a função hello no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a49cf-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="a49cf-175">Olá registra a saída de instalação do pacote do guia exibe hello.</span><span class="sxs-lookup"><span data-stu-id="a49cf-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="a49cf-176">tooupload um arquivo Project. JSON, use um dos métodos de saudação descritos em Olá [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate) no tópico de referência de desenvolvedor Olá funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="a49cf-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="a49cf-177">Depois de saudação *Project* arquivo é carregado, você verá a saída como Olá exemplo em sua função a seguir do fluxo de log:</span><span class="sxs-lookup"><span data-stu-id="a49cf-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a><span data-ttu-id="a49cf-178">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="a49cf-178">Environment variables</span></span>
<span data-ttu-id="a49cf-179">tooget uma variável de ambiente ou um valor de configuração do aplicativo, use `System.Environment.GetEnvironmentVariable`, conforme mostrado no hello exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a49cf-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a><span data-ttu-id="a49cf-180">Reutilização de código .csx</span><span class="sxs-lookup"><span data-stu-id="a49cf-180">Reusing .csx code</span></span>
<span data-ttu-id="a49cf-181">Você pode usar classes e métodos definidos em outros arquivos *.csx* no seu arquivo *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="a49cf-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="a49cf-182">toodo que usam `#load` diretivas em seu *run.csx* arquivo.</span><span class="sxs-lookup"><span data-stu-id="a49cf-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="a49cf-183">Saudação de exemplo a seguir, uma rotina de log denominado `MyLogger` é compartilhado em *myLogger.csx* e carregados na *run.csx* usando Olá `#load` diretiva:</span><span class="sxs-lookup"><span data-stu-id="a49cf-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="a49cf-184">Exemplo de *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="a49cf-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="a49cf-185">Exemplo de *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="a49cf-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="a49cf-186">Usando um compartilhado *. CSx* é um padrão comum quando desejar toostrongly seus argumentos entre funções usando um objeto POCO de tipo.</span><span class="sxs-lookup"><span data-stu-id="a49cf-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="a49cf-187">Em Olá simplificada de exemplo a seguir, um gatilho HTTP e o gatilho de fila compartilham um objeto POCO chamado `Order` toostrongly dados de pedidos de saudação de tipo:</span><span class="sxs-lookup"><span data-stu-id="a49cf-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="a49cf-188">Exemplo *run.csx* para o gatilho HTTP:</span><span class="sxs-lookup"><span data-stu-id="a49cf-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="a49cf-189">Exemplo *run.csx* para o gatilho da fila:</span><span class="sxs-lookup"><span data-stu-id="a49cf-189">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="a49cf-190">Exemplo *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="a49cf-190">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="a49cf-191">Você pode usar um caminho relativo com hello `#load` diretiva:</span><span class="sxs-lookup"><span data-stu-id="a49cf-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="a49cf-192">`#load "mylogger.csx"`carrega um arquivo localizado na pasta de função hello.</span><span class="sxs-lookup"><span data-stu-id="a49cf-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="a49cf-193">`#load "loadedfiles\mylogger.csx"`carrega um arquivo localizado em uma pasta na pasta de função hello.</span><span class="sxs-lookup"><span data-stu-id="a49cf-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="a49cf-194">`#load "..\shared\mylogger.csx"`carrega um arquivo localizado em uma pasta no mesmo nível como pasta de função hello, ou seja, de saudação diretamente sob *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="a49cf-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="a49cf-195">Olá `#load` diretiva só funciona com *. CSx* arquivos (c# script), não com *. CS* arquivos.</span><span class="sxs-lookup"><span data-stu-id="a49cf-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="a49cf-196">Associação em tempo de execução por meio de associações obrigatórias</span><span class="sxs-lookup"><span data-stu-id="a49cf-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="a49cf-197">Em c# e outras linguagens .NET, você pode usar um [fundamental](https://en.wikipedia.org/wiki/Imperative_programming) padrão de associação, como contrário toohello [ *declarativa* ](https://en.wikipedia.org/wiki/Declarative_programming) associações em *function.json*.</span><span class="sxs-lookup"><span data-stu-id="a49cf-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="a49cf-198">Associação fundamental é útil quando precisam de parâmetros de ligação toobe computado em tempo de execução, em vez de design.</span><span class="sxs-lookup"><span data-stu-id="a49cf-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="a49cf-199">Com esse padrão, você pode associar toosupported entrada e saída associação em interrupções no seu código de função.</span><span class="sxs-lookup"><span data-stu-id="a49cf-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="a49cf-200">Defina uma associação obrigatória da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a49cf-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="a49cf-201">**Não** inclua uma entrada em *function.json* para as associações obrigatórias desejadas.</span><span class="sxs-lookup"><span data-stu-id="a49cf-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="a49cf-202">Passe um parâmetro de entrada [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) ou [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="a49cf-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="a49cf-203">Use Olá c# padrão tooperform Olá associação de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="a49cf-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="a49cf-204">onde `BindingTypeAttribute` é Olá .NET atributo que define a associação e `T` é Olá o tipo de entrada ou saído que é suportado por este tipo de associação.</span><span class="sxs-lookup"><span data-stu-id="a49cf-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="a49cf-205">`T` também não pode ser um tipo de parâmetro `out` (como `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="a49cf-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="a49cf-206">Por exemplo, a associação de saída de tabela dos Aplicativos Móveis dá suporte a [seis tipos de saída](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), mas você só pode usar [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) para `T`.</span><span class="sxs-lookup"><span data-stu-id="a49cf-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="a49cf-207">Olá, código de exemplo a seguir cria um [associação de saída blob de armazenamento](functions-bindings-storage-blob.md#using-a-blob-output-binding) com blob caminho que é definido em tempo de execução, em seguida, grava um blob de toohello de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a49cf-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="a49cf-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) define Olá [blob de armazenamento](functions-bindings-storage-blob.md) de entrada ou saída de associação, e [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) é um tipo de associação de saída com suporte.</span><span class="sxs-lookup"><span data-stu-id="a49cf-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="a49cf-209">Como é, o código de saudação obtém configuração de aplicativo padrão Olá para Olá cadeia de conexão da conta de armazenamento (que é `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="a49cf-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="a49cf-210">Você pode especificar um toouse de configuração de aplicativo personalizado adicionando o [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) e passar a matriz de atributos de saudação em `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="a49cf-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="a49cf-211">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="a49cf-211">For example,</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="a49cf-212">Olá tabela a seguir lista atributos de .NET Olá para cada pacotes de tipo e hello de associação no qual eles são definidos.</span><span class="sxs-lookup"><span data-stu-id="a49cf-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="a49cf-213">Associação</span><span class="sxs-lookup"><span data-stu-id="a49cf-213">Binding</span></span> | <span data-ttu-id="a49cf-214">Atributo</span><span class="sxs-lookup"><span data-stu-id="a49cf-214">Attribute</span></span> | <span data-ttu-id="a49cf-215">Adicionar referência</span><span class="sxs-lookup"><span data-stu-id="a49cf-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="a49cf-216">Banco de Dados Cosmos</span><span class="sxs-lookup"><span data-stu-id="a49cf-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="a49cf-217">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="a49cf-217">Event Hubs</span></span> | <span data-ttu-id="a49cf-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a49cf-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="a49cf-219">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="a49cf-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="a49cf-220">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="a49cf-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="a49cf-221">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="a49cf-221">Service Bus</span></span> | <span data-ttu-id="a49cf-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a49cf-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="a49cf-223">Fila de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a49cf-223">Storage queue</span></span> | <span data-ttu-id="a49cf-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a49cf-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="a49cf-225">Armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="a49cf-225">Storage blob</span></span> | <span data-ttu-id="a49cf-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a49cf-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="a49cf-227">Tabela de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a49cf-227">Storage table</span></span> | <span data-ttu-id="a49cf-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="a49cf-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="a49cf-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="a49cf-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="a49cf-230">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a49cf-230">Next steps</span></span>
<span data-ttu-id="a49cf-231">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a49cf-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="a49cf-232">Práticas recomendadas para o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a49cf-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="a49cf-233">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a49cf-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="a49cf-234">Referência do desenvolvedor em F# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a49cf-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="a49cf-235">Referência do desenvolvedor de NodeJS do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a49cf-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="a49cf-236">Gatilhos e associações de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a49cf-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
