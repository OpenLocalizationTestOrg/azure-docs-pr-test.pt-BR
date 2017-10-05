---
title: "Referência do desenvolvedor de scripts C# do Azure Functions | Microsoft Docs"
description: Entenda como desenvolver no Azure Functions usando NodeJS.
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="5ddb7-104">Referência do desenvolvedor de scripts C# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5ddb7-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ddb7-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="5ddb7-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="5ddb7-106">Script em F#</span><span class="sxs-lookup"><span data-stu-id="5ddb7-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="5ddb7-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="5ddb7-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="5ddb7-108">A experiência de scripts C# do Azure Functions baseia-se no SDK do Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="5ddb7-109">Fluxos de dados na sua função C# por meio de argumentos de método.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="5ddb7-110">Os nomes de argumentos são especificados em `function.json`e há nomes predefinidos para acessar itens como a função logger e os tokens de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="5ddb7-111">Este artigo pressupõe que você já tenha lido a [referência do desenvolvedor do Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="5ddb7-112">Para obter informações sobre como usar as bibliotecas de classes C#, consulte [Usando bibliotecas de classes do .NET com o Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="5ddb7-113">Como o .csx funciona</span><span class="sxs-lookup"><span data-stu-id="5ddb7-113">How .csx works</span></span>
<span data-ttu-id="5ddb7-114">O formato `.csx` permite escrever menos “texto clichê” e ter como foco apenas uma função do C#.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="5ddb7-115">Inclua todas as referências de assembly e todos os namespaces no início do arquivo, como de costume.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="5ddb7-116">Em vez de encapsular tudo em um namespace e uma classe, basta definir um método `Run`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="5ddb7-117">Se precisar incluir alguma classe, por exemplo, para definir objetos POCO (objeto CRL básico), você poderá incluir uma classe no mesmo arquivo.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="5ddb7-118">Binding para argumentos</span><span class="sxs-lookup"><span data-stu-id="5ddb7-118">Binding to arguments</span></span>
<span data-ttu-id="5ddb7-119">Vários bindings estão vinculados a uma função C# por meio da propriedade `name` na configuração *function.json* .</span><span class="sxs-lookup"><span data-stu-id="5ddb7-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="5ddb7-120">Cada associação tem seus próprios tipos com suporte; por exemplo, um gatilho de blob pode dar suporte a uma cadeia de caracteres, um POCO ou um CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="5ddb7-121">Os tipos com suporte são documentados na referência de cada associação.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="5ddb7-122">Um objeto POCO deve ter um getter e setter definido para cada propriedade.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="5ddb7-123">Usando o valor retornado de um método em uma associação de saída</span><span class="sxs-lookup"><span data-stu-id="5ddb7-123">Using method return value for output binding</span></span>

<span data-ttu-id="5ddb7-124">Use um valor retornado de um método em uma associação de saída, usando o nome `$return` em *function.json*:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="5ddb7-125">Gravando vários valores de saída</span><span class="sxs-lookup"><span data-stu-id="5ddb7-125">Writing multiple output values</span></span>

<span data-ttu-id="5ddb7-126">Para gravar vários valores em uma associação de saída, use os tipos [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="5ddb7-127">Esses tipos são coleções somente gravação que são gravadas na associação de saída quando o método é concluído.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="5ddb7-128">Este exemplo grava várias mensagens de fila usando `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="5ddb7-129">Registro em log</span><span class="sxs-lookup"><span data-stu-id="5ddb7-129">Logging</span></span>
<span data-ttu-id="5ddb7-130">Para registrar a saída nos logs de streaming em C#, inclua um argumento do tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="5ddb7-131">Recomendamos nomeá-lo como `log`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="5ddb7-132">Evite usar `Console.Write` no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="5ddb7-133">`TraceWriter` é definido no [SDK do Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="5ddb7-134">O nível de log para `TraceWriter` pode ser configurado em [host\.json].</span><span class="sxs-lookup"><span data-stu-id="5ddb7-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="5ddb7-135">Assíncrono</span><span class="sxs-lookup"><span data-stu-id="5ddb7-135">Async</span></span>
<span data-ttu-id="5ddb7-136">Para tornar uma função assíncrona, use a palavra-chave `async` e retorne um objeto `Task`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="5ddb7-137">Token de cancelamento</span><span class="sxs-lookup"><span data-stu-id="5ddb7-137">Cancellation Token</span></span>
<span data-ttu-id="5ddb7-138">Algumas operações exigem um desligamento normal.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="5ddb7-139">Embora seja sempre melhor escrever um código que possa lidar com falhas, nos casos em que você desejar lidar com solicitações de desligamento normal, defina um argumento tipado [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="5ddb7-140">Um `CancellationToken` é fornecido para sinalizar que um desligamento de host é disparado.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="5ddb7-141">Importando namespaces</span><span class="sxs-lookup"><span data-stu-id="5ddb7-141">Importing namespaces</span></span>
<span data-ttu-id="5ddb7-142">Se precisar importar namespaces, você poderá fazer como geralmente faz, com a cláusula `using` .</span><span class="sxs-lookup"><span data-stu-id="5ddb7-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="5ddb7-143">Os seguintes namespaces são automaticamente importados e, portanto, são opcionais:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="5ddb7-144">Referenciando Assemblies Externos</span><span class="sxs-lookup"><span data-stu-id="5ddb7-144">Referencing External Assemblies</span></span>
<span data-ttu-id="5ddb7-145">Para assemblies da estrutura, adicione referências usando a diretiva `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="5ddb7-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="5ddb7-146">Os seguintes assemblies são adicionados automaticamente pelo ambiente de hospedagem do Azure Functions:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="5ddb7-147">Os seguintes assemblies podem ser referenciados por um nome simples (por exemplo, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="5ddb7-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="5ddb7-148">Referenciando assemblies personalizados</span><span class="sxs-lookup"><span data-stu-id="5ddb7-148">Referencing custom assemblies</span></span>

<span data-ttu-id="5ddb7-149">Para referenciar um assembly personalizado, use um assembly *compartilhado* ou *particular*:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="5ddb7-150">Assemblies compartilhados são compartilhados entre todas as funções em um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="5ddb7-151">Para referenciar um assembly personalizado, carregue o assembly no aplicativo de funções, como em uma pasta `bin` na raiz do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="5ddb7-152">Assemblies particulares fazem parte do contexto de determinada função e dão suporte ao sideload de versões diferentes.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="5ddb7-153">Os assemblies particulares devem ser carregados em uma pasta `bin` do diretório da função.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="5ddb7-154">Referencie usando o nome do arquivo, como `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="5ddb7-155">Para obter informações sobre como carregar arquivos na pasta da função, consulte a seção a seguir sobre gerenciamento de pacotes.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="5ddb7-156">Diretórios inspecionados</span><span class="sxs-lookup"><span data-stu-id="5ddb7-156">Watched directories</span></span>

<span data-ttu-id="5ddb7-157">O diretório que contém o arquivo de script da função é inspecionado automaticamente quanto às alterações nos assemblies.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="5ddb7-158">Para inspecionar alterações de assembly em outros diretórios, adicione-os à lista `watchDirectories` em [host\.json].</span><span class="sxs-lookup"><span data-stu-id="5ddb7-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="5ddb7-159">Usando pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="5ddb7-159">Using NuGet packages</span></span>
<span data-ttu-id="5ddb7-160">Para usar pacotes NuGet em uma função C#, carregue um arquivo *project.json* na pasta da função, no sistema de arquivos do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="5ddb7-161">Aqui está um arquivo *project.json* de exemplo que adiciona uma referência à versão 1.1.0 do Microsoft.ProjectOxford.Face:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="5ddb7-162">Somente o .NET Framework 4.6 tem suporte. Desse modo, tenha certeza de que o arquivo *project.json* especifica `net46`, como mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="5ddb7-163">Quando você carrega um arquivo *project.json* , o tempo de execução obtém os pacotes e adiciona referências automaticamente aos assemblies do pacote.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="5ddb7-164">Você não precisa adicionar diretivas `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="5ddb7-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="5ddb7-165">Para usar os tipos definidos nos pacotes NuGet, adicione as instruções `using` obrigatórias ao arquivo *run.csx*</span><span class="sxs-lookup"><span data-stu-id="5ddb7-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="5ddb7-166">No tempo de execução do Functions, a restauração do NuGet funciona comparando `project.json` e `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="5ddb7-167">Se os carimbos de data/hora dos arquivos **não** forem correspondentes, uma restauração do NuGet será executada e o NuGet baixará os pacotes atualizados.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="5ddb7-168">No entanto, se os carimbos de data/hora dos arquivos **forem** correspondentes, o NuGet não executará nenhuma restauração.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="5ddb7-169">Portanto, `project.lock.json` não deve ser implantado, pois faz com que o NuGet ignore a restauração do pacote.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="5ddb7-170">Para evitar a implantação do arquivo de bloqueio, adicione o `project.lock.json` ao arquivo `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="5ddb7-171">Para usar um feed do NuGet personalizado, especifique o feed em um arquivo *Nuget.Config* na raiz do Aplicativo de Funções.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="5ddb7-172">Para obter mais informações, consulte [Configurando o comportamento do NuGet](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="5ddb7-173">Usando um arquivo project.json</span><span class="sxs-lookup"><span data-stu-id="5ddb7-173">Using a project.json file</span></span>
1. <span data-ttu-id="5ddb7-174">Abra a função no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="5ddb7-175">A guia logs exibe o resultado da instalação do pacote.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="5ddb7-176">Para carregar um arquivo project.json, use um dos métodos descritos em [Como atualizar os arquivos do aplicativo de funções](functions-reference.md#fileupdate) no tópico Referência do desenvolvedor do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="5ddb7-177">Depois que o arquivo *project.json* for carregado, você verá a saída como o exemplo a seguir no log de streaming da sua função:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="5ddb7-178">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="5ddb7-178">Environment variables</span></span>
<span data-ttu-id="5ddb7-179">Para obter uma variável de ambiente ou um valor de configuração do aplicativo, use `System.Environment.GetEnvironmentVariable`, conforme mostrado no exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="5ddb7-180">Reutilização de código .csx</span><span class="sxs-lookup"><span data-stu-id="5ddb7-180">Reusing .csx code</span></span>
<span data-ttu-id="5ddb7-181">Você pode usar classes e métodos definidos em outros arquivos *.csx* no seu arquivo *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="5ddb7-182">Para fazer isso, use diretivas `#load` no arquivo *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="5ddb7-183">No exemplo a seguir, uma rotina de log chamada `MyLogger` é compartilhada em *myLogger.csx* e carregada em *run.csx* usando a diretiva `#load`:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="5ddb7-184">Exemplo de *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="5ddb7-185">Exemplo de *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="5ddb7-186">Usar um *.csx* compartilhado é um padrão comum quando você desejar tipar fortemente os argumentos entre as funções usando um objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="5ddb7-187">No seguinte exemplo simplificado, um gatilho HTTP e um gatilho de fila compartilham um objeto POCO chamado `Order` para tipar fortemente os dados do pedido:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="5ddb7-188">Exemplo *run.csx* para o gatilho HTTP:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

<span data-ttu-id="5ddb7-189">Exemplo *run.csx* para o gatilho da fila:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="5ddb7-190">Exemplo *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="5ddb7-191">Você pode usar um caminho relativo com a diretiva `#load` :</span><span class="sxs-lookup"><span data-stu-id="5ddb7-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="5ddb7-192">`#load "mylogger.csx"` carrega um arquivo localizado na pasta de função.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="5ddb7-193">`#load "loadedfiles\mylogger.csx"` carrega um arquivo localizado em uma pasta na pasta de função.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="5ddb7-194">`#load "..\shared\mylogger.csx"` carrega um arquivo localizado em uma pasta no mesmo nível que a pasta de função, ou seja, diretamente em *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="5ddb7-195">A diretiva `#load` só funciona com arquivos *.csx* (script C#), e não com arquivos *.cs*.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="5ddb7-196">Associação em tempo de execução por meio de associações obrigatórias</span><span class="sxs-lookup"><span data-stu-id="5ddb7-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="5ddb7-197">No C#, e em outras linguagens .NET, você pode usar um padrão de associação [obrigatório](https://en.wikipedia.org/wiki/Imperative_programming), em vez de associações [*declarativas*](https://en.wikipedia.org/wiki/Declarative_programming) em *function.json*.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="5ddb7-198">A associação obrigatória é útil quando os parâmetros de associação precisam ser calculado no tempo de execução, em vez do tempo de design.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="5ddb7-199">Com esse padrão, é possível associar à associação de entrada e saída com suporte instantaneamente no código da função.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="5ddb7-200">Defina uma associação obrigatória da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="5ddb7-201">**Não** inclua uma entrada em *function.json* para as associações obrigatórias desejadas.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="5ddb7-202">Passe um parâmetro de entrada [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) ou [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="5ddb7-203">Use o padrão de C# a seguir para realizar a associação de dados.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="5ddb7-204">em que `BindingTypeAttribute` é o atributo do .NET que define a associação e `T` é o tipo de entrada ou saída com suporte nesse tipo de associação.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="5ddb7-205">`T` também não pode ser um tipo de parâmetro `out` (como `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="5ddb7-206">Por exemplo, a associação de saída de tabela dos Aplicativos Móveis dá suporte a [seis tipos de saída](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), mas você só pode usar [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) para `T`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="5ddb7-207">O código de exemplo a seguir cria uma [associação de saída do Armazenamento de Blobs](functions-bindings-storage-blob.md#using-a-blob-output-binding) com o caminho do blob definido em tempo de execução e grava uma cadeia de caracteres no blob.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="5ddb7-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) define a associação de entrada ou saída do [Armazenamento de Blobs](functions-bindings-storage-blob.md) e [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) é um tipo de associação de saída com suporte.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="5ddb7-209">No estado em que se encontra, o código obtém a configuração de aplicativo padrão para a cadeia de conexão da conta de armazenamento (`AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="5ddb7-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="5ddb7-210">Especifique uma configuração de aplicativo personalizada a ser usada adicionando [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) e passando a matriz de atributo para `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="5ddb7-211">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="5ddb7-211">For example,</span></span>

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

<span data-ttu-id="5ddb7-212">A tabela a seguir lista os atributos .NET para cada tipo de associação e os pacotes no qual eles são definidos.</span><span class="sxs-lookup"><span data-stu-id="5ddb7-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="5ddb7-213">Associação</span><span class="sxs-lookup"><span data-stu-id="5ddb7-213">Binding</span></span> | <span data-ttu-id="5ddb7-214">Atributo</span><span class="sxs-lookup"><span data-stu-id="5ddb7-214">Attribute</span></span> | <span data-ttu-id="5ddb7-215">Adicionar referência</span><span class="sxs-lookup"><span data-stu-id="5ddb7-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="5ddb7-216">Banco de Dados Cosmos</span><span class="sxs-lookup"><span data-stu-id="5ddb7-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="5ddb7-217">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5ddb7-217">Event Hubs</span></span> | <span data-ttu-id="5ddb7-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5ddb7-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="5ddb7-219">Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="5ddb7-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="5ddb7-220">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="5ddb7-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="5ddb7-221">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="5ddb7-221">Service Bus</span></span> | <span data-ttu-id="5ddb7-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5ddb7-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="5ddb7-223">Fila de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5ddb7-223">Storage queue</span></span> | <span data-ttu-id="5ddb7-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5ddb7-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="5ddb7-225">Armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="5ddb7-225">Storage blob</span></span> | <span data-ttu-id="5ddb7-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5ddb7-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="5ddb7-227">Tabela de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5ddb7-227">Storage table</span></span> | <span data-ttu-id="5ddb7-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="5ddb7-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="5ddb7-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="5ddb7-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="5ddb7-230">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5ddb7-230">Next steps</span></span>
<span data-ttu-id="5ddb7-231">Para saber mais, consulte os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ddb7-231">For more information, see the following resources:</span></span>

* [<span data-ttu-id="5ddb7-232">Práticas recomendadas para o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5ddb7-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="5ddb7-233">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5ddb7-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="5ddb7-234">Referência do desenvolvedor em F# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5ddb7-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="5ddb7-235">Referência do desenvolvedor de NodeJS do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5ddb7-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="5ddb7-236">Gatilhos e associações de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5ddb7-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
