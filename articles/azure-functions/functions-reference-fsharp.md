---
title: "Referência do desenvolvedor em F# do Azure Functions | Microsoft Docs"
description: Entenda como desenvolver no Azure Functions usando F#.
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure funções, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura serverless, F #"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="b264e-104">Referência do desenvolvedor em F# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b264e-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="b264e-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="b264e-106">Script em F#</span><span class="sxs-lookup"><span data-stu-id="b264e-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="b264e-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="b264e-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="b264e-108">F# para Azure Functions é uma solução para executar facilmente pequenos trechos de código, ou "funções", na nuvem.</span><span class="sxs-lookup"><span data-stu-id="b264e-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="b264e-109">Fluxos de dados em sua função F# por meio de argumentos de função.</span><span class="sxs-lookup"><span data-stu-id="b264e-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="b264e-110">Os nomes de argumentos são especificados em `function.json`e há nomes predefinidos para acessar itens como a função logger e os tokens de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="b264e-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="b264e-111">Este artigo pressupõe que você já tenha lido a [referência do desenvolvedor do Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b264e-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="b264e-112">Como funciona o .fsx</span><span class="sxs-lookup"><span data-stu-id="b264e-112">How .fsx works</span></span>
<span data-ttu-id="b264e-113">Um arquivo `.fsx` é um script de F#.</span><span class="sxs-lookup"><span data-stu-id="b264e-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="b264e-114">Ele pode ser considerado um projeto em F# contido em um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="b264e-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="b264e-115">O arquivo contém o código para seu programa (nesse caso, o Azure Function) e diretivas para gerenciar as dependências.</span><span class="sxs-lookup"><span data-stu-id="b264e-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="b264e-116">Quando você usa um `.fsx` para um Azure Function, os assemblies normalmente exibidos são incluídos automaticamente, permitindo que você se concentre na função em vez do código "clichê".</span><span class="sxs-lookup"><span data-stu-id="b264e-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="b264e-117">Binding para argumentos</span><span class="sxs-lookup"><span data-stu-id="b264e-117">Binding to arguments</span></span>
<span data-ttu-id="b264e-118">Cada associação oferece suporte a um conjunto de argumentos, conforme detalhado na [Referências de gatilhos e de associações do Azure Functions para desenvolvedores](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="b264e-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="b264e-119">Por exemplo, uma das associações de argumento com suporte de um gatilho de blob é um POCO, que pode ser expresso usando um registro em F#.</span><span class="sxs-lookup"><span data-stu-id="b264e-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="b264e-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="b264e-121">O Azure Function em F# usará um ou mais argumentos.</span><span class="sxs-lookup"><span data-stu-id="b264e-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="b264e-122">Quando falamos sobre os argumentos do Azure Functions, nos referimos a argumentos de *entrada* e argumentos de *saída*.</span><span class="sxs-lookup"><span data-stu-id="b264e-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="b264e-123">Um argumento de entrada é exatamente o que parece: uma entrada para o Azure Function em F#.</span><span class="sxs-lookup"><span data-stu-id="b264e-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="b264e-124">Um argumento de *saída* são dados mutáveis ou um argumento `byref<>` que serve como uma maneira de passar dados de volta *saindo* de sua função.</span><span class="sxs-lookup"><span data-stu-id="b264e-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="b264e-125">No exemplo acima, `blob` é um argumento de entrada e `output` é um argumento de saída.</span><span class="sxs-lookup"><span data-stu-id="b264e-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="b264e-126">Observe que utilizamos `byref<>` para `output` (não é necessário adicionar a anotação `[<Out>]`).</span><span class="sxs-lookup"><span data-stu-id="b264e-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="b264e-127">O uso de um tipo `byref<>` permite que sua função altere o registro ou o objeto ao qual o argumento se refere.</span><span class="sxs-lookup"><span data-stu-id="b264e-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="b264e-128">Quando um registro em F# é usado como um tipo de entrada, a definição de registro deve ser marcada com `[<CLIMutable>]` para permitir que a estrutura do Azure Functions defina os campos adequadamente antes de passar o registro para a função.</span><span class="sxs-lookup"><span data-stu-id="b264e-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="b264e-129">Nos bastidores, `[<CLIMutable>]` gera setters para as propriedades de registro.</span><span class="sxs-lookup"><span data-stu-id="b264e-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="b264e-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="b264e-131">Uma classe de F# também pode ser usada para ambos os argumentos.</span><span class="sxs-lookup"><span data-stu-id="b264e-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="b264e-132">Para uma classe, as propriedades geralmente exigirão getters e setters.</span><span class="sxs-lookup"><span data-stu-id="b264e-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="b264e-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="b264e-134">Registro em log</span><span class="sxs-lookup"><span data-stu-id="b264e-134">Logging</span></span>
<span data-ttu-id="b264e-135">Para registrar a saída em seus [logs de streaming](../app-service-web/web-sites-streaming-logs-and-console.md) em F#, sua função deve usar um argumento do tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="b264e-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="b264e-136">Para manter a consistência, recomendamos que esse argumento seja denominado `log`.</span><span class="sxs-lookup"><span data-stu-id="b264e-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="b264e-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="b264e-138">Assíncrono</span><span class="sxs-lookup"><span data-stu-id="b264e-138">Async</span></span>
<span data-ttu-id="b264e-139">O fluxo de trabalho de `async` pode ser usado, mas o resultado precisa retornar um `Task`.</span><span class="sxs-lookup"><span data-stu-id="b264e-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="b264e-140">Isso pode ser feito com `Async.StartAsTask`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="b264e-141">Token de cancelamento</span><span class="sxs-lookup"><span data-stu-id="b264e-141">Cancellation Token</span></span>
<span data-ttu-id="b264e-142">Se a sua função precisar manipular o desligamento com cuidado, atribua um argumento [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b264e-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="b264e-143">Isso pode ser combinado com `async`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="b264e-144">Importando namespaces</span><span class="sxs-lookup"><span data-stu-id="b264e-144">Importing namespaces</span></span>
<span data-ttu-id="b264e-145">É possível abrir os namespaces como de costume:</span><span class="sxs-lookup"><span data-stu-id="b264e-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="b264e-146">Os namespaces a seguir são abertos automaticamente:</span><span class="sxs-lookup"><span data-stu-id="b264e-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="b264e-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="b264e-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="b264e-148">Referenciando Assemblies Externos</span><span class="sxs-lookup"><span data-stu-id="b264e-148">Referencing External Assemblies</span></span>
<span data-ttu-id="b264e-149">Da mesma forma, as referências à estrutura do assembly podem ser adicionadas com a diretiva `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="b264e-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="b264e-150">Os seguintes assemblies são adicionados automaticamente pelo ambiente de hospedagem do Azure Functions:</span><span class="sxs-lookup"><span data-stu-id="b264e-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="b264e-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="b264e-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="b264e-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="b264e-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="b264e-153">Além disso, os seguintes assemblies têm regras de maiúsculas e minúsculas especiais e podem ser referenciados por simplename (por exemplo, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="b264e-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="b264e-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="b264e-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="b264e-155">Se precisar fazer referência a um assembly particular, carregue o arquivo do assembly em uma pasta `bin` relativa à sua função e faça referência a ela usando o nome do arquivo (por exemplo, `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="b264e-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="b264e-156">Para obter informações sobre como carregar arquivos na pasta da função, consulte a seção a seguir sobre gerenciamento de pacotes.</span><span class="sxs-lookup"><span data-stu-id="b264e-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="b264e-157">Prelúdio do editor</span><span class="sxs-lookup"><span data-stu-id="b264e-157">Editor Prelude</span></span>
<span data-ttu-id="b264e-158">Um editor que oferece suporte aos Serviços de compilador em F# não estará ciente dos namespaces e assemblies que o Azure Functions inclui automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b264e-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="b264e-159">Dessa forma, pode ser útil incluir um prelúdio que ajuda o editor a encontrar os assemblies que você está usando e a abrir explicitamente os namespaces.</span><span class="sxs-lookup"><span data-stu-id="b264e-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="b264e-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="b264e-161">Quando o Azure Functions executa seu código, ele processa o código-fonte com `COMPILED` definido, e o prelúdio do editor é ignorado.</span><span class="sxs-lookup"><span data-stu-id="b264e-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="b264e-162">Gerenciamento de pacote</span><span class="sxs-lookup"><span data-stu-id="b264e-162">Package management</span></span>
<span data-ttu-id="b264e-163">Para usar os pacotes do NuGet em uma função F#, adicione um arquivo `project.json` à pasta da função, no sistema de arquivos do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="b264e-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="b264e-164">Veja um exemplo de arquivo `project.json` que adiciona uma referência do pacote NuGet ao `Microsoft.ProjectOxford.Face` versão 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="b264e-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="b264e-165">Somente o .NET Framework 4.6 tem suporte. Desse modo, tenha certeza de que o arquivo `project.json` especifica `net46`, como mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="b264e-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="b264e-166">Quando você carrega um arquivo `project.json` , o tempo de execução obtém os pacotes e adiciona referências automaticamente aos assemblies do pacote.</span><span class="sxs-lookup"><span data-stu-id="b264e-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="b264e-167">Você não precisa adicionar diretivas `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="b264e-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="b264e-168">Basta adicionar as instruções `open` necessárias ao seu arquivo `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="b264e-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="b264e-169">Talvez você queira colocar automaticamente assemblies de referência no prelúdio de seu editor, para melhorar a interação do editor com os Serviços de compilação em F#.</span><span class="sxs-lookup"><span data-stu-id="b264e-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="b264e-170">Como adicionar um arquivo `project.json` ao Azure Function</span><span class="sxs-lookup"><span data-stu-id="b264e-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="b264e-171">Comece verificando se o aplicativo está em execução, o que pode ser feito abrindo a função no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b264e-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="b264e-172">Isso também permite acessar os logs de streaming nos quais a saída da instalação do pacote será exibida.</span><span class="sxs-lookup"><span data-stu-id="b264e-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="b264e-173">Para carregar um arquivo `project.json` , use um dos métodos descritos em [Como atualizar os arquivos de aplicativo de funções](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="b264e-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="b264e-174">Se você estiver usando a [Implantação contínua para o Azure Functions](functions-continuous-deployment.md), adicione um arquivo `project.json` à sua ramificação de preparo a fim de testar antes de adicioná-lo à sua ramificação de implantação.</span><span class="sxs-lookup"><span data-stu-id="b264e-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="b264e-175">Depois que o arquivo `project.json` for adicionado, você verá uma saída semelhante ao exemplo a seguir em seu log de streaming da função:</span><span class="sxs-lookup"><span data-stu-id="b264e-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="b264e-176">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="b264e-176">Environment variables</span></span>
<span data-ttu-id="b264e-177">Para obter uma variável de ambiente ou um valor de configuração do aplicativo, use `System.Environment.GetEnvironmentVariable`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="b264e-178">Reutilizar o código .fsx</span><span class="sxs-lookup"><span data-stu-id="b264e-178">Reusing .fsx code</span></span>
<span data-ttu-id="b264e-179">Você pode usar código de outros arquivos `.fsx` usando uma diretiva `#load`.</span><span class="sxs-lookup"><span data-stu-id="b264e-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="b264e-180">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b264e-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="b264e-181">Os caminhos fornecidos para a diretiva `#load` são relativos ao local de seu arquivo `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="b264e-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="b264e-182">`#load "logger.fsx"` carrega um arquivo localizado na pasta de função.</span><span class="sxs-lookup"><span data-stu-id="b264e-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="b264e-183">`#load "package\logger.fsx"` carrega um arquivo localizado na pasta `package`na pasta da função.</span><span class="sxs-lookup"><span data-stu-id="b264e-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="b264e-184">`#load "..\shared\mylogger.fsx"` carrega um arquivo localizado em uma pasta `shared`no mesmo nível que a pasta de função, ou seja, diretamente em `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="b264e-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="b264e-185">A diretiva `#load` só funciona com arquivos `.fsx` (script em F#) e não com arquivos `.fs`.</span><span class="sxs-lookup"><span data-stu-id="b264e-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b264e-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b264e-186">Next steps</span></span>
<span data-ttu-id="b264e-187">Para saber mais, consulte os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b264e-187">For more information, see the following resources:</span></span>

* [<span data-ttu-id="b264e-188">Guia de F#</span><span class="sxs-lookup"><span data-stu-id="b264e-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="b264e-189">Práticas recomendadas para o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="b264e-190">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="b264e-191">Referência do desenvolvedor de C# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="b264e-192">Referência do desenvolvedor de NodeJS do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="b264e-193">Gatilhos e de associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="b264e-194">Teste do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="b264e-195">Dimensionamento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b264e-195">Azure Functions scaling</span></span>](functions-scale.md)

