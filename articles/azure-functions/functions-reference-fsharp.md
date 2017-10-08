---
title: "aaaAzure funções F # referência do desenvolvedor | Microsoft Docs"
description: "Entender como toodevelop funções do Azure usando F #."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor, F#"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="1eba8-104">Referência do desenvolvedor em F# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1eba8-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="1eba8-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="1eba8-106">Script em F#</span><span class="sxs-lookup"><span data-stu-id="1eba8-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="1eba8-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="1eba8-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="1eba8-108">F # para funções do Azure é uma solução para executar facilmente pequenos pedaços de código ou "funções", na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="1eba8-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="1eba8-109">Fluxos de dados em sua função F# por meio de argumentos de função.</span><span class="sxs-lookup"><span data-stu-id="1eba8-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="1eba8-110">Os nomes de argumento são especificados em `function.json`, e existem nomes predefinidos para acessar as coisas como Olá tokens de agente e o cancelamento de função.</span><span class="sxs-lookup"><span data-stu-id="1eba8-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="1eba8-111">Este artigo pressupõe que você já leu Olá [referência do desenvolvedor do Azure funções](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1eba8-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="1eba8-112">Como funciona o .fsx</span><span class="sxs-lookup"><span data-stu-id="1eba8-112">How .fsx works</span></span>
<span data-ttu-id="1eba8-113">Um arquivo `.fsx` é um script de F#.</span><span class="sxs-lookup"><span data-stu-id="1eba8-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="1eba8-114">Ele pode ser considerado um projeto em F# contido em um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="1eba8-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="1eba8-115">arquivo Hello contém ambos código Olá para o programa (nesse caso, a função do Azure) e diretivas para gerenciar as dependências.</span><span class="sxs-lookup"><span data-stu-id="1eba8-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="1eba8-116">Quando você usa um `.fsx` para uma função do Azure, normalmente requeridos assemblies serão incluídos automaticamente para você, permitindo que você toofocus no código de função em vez de "boilerplate" hello.</span><span class="sxs-lookup"><span data-stu-id="1eba8-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="1eba8-117">Associação tooarguments</span><span class="sxs-lookup"><span data-stu-id="1eba8-117">Binding tooarguments</span></span>
<span data-ttu-id="1eba8-118">Cada associação oferece suporte a um conjunto de argumentos, como detalhado no hello [gatilhos e associações de referência do desenvolvedor do Azure funções](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="1eba8-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="1eba8-119">Por exemplo, uma das associações de argumento Olá dá suporte a um gatilho de blob é um POCO, que pode ser expressada usando um registro F #.</span><span class="sxs-lookup"><span data-stu-id="1eba8-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="1eba8-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="1eba8-121">O Azure Function em F# usará um ou mais argumentos.</span><span class="sxs-lookup"><span data-stu-id="1eba8-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="1eba8-122">Quando falamos sobre os argumentos de funções do Azure, nós nos referimos muito*entrada* argumentos e *saída* argumentos.</span><span class="sxs-lookup"><span data-stu-id="1eba8-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="1eba8-123">Um argumento de entrada é exatamente o que parece: entrada tooyour função do Azure F #.</span><span class="sxs-lookup"><span data-stu-id="1eba8-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="1eba8-124">Um *saída* argumento é mutáveis dados ou um `byref<>` argumento serve como uma maneira toopass de dados volta *out* de sua função.</span><span class="sxs-lookup"><span data-stu-id="1eba8-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="1eba8-125">No exemplo acima, a saudação `blob` é um argumento de entrada, e `output` é um argumento de saída.</span><span class="sxs-lookup"><span data-stu-id="1eba8-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="1eba8-126">Observe que usamos `byref<>` para `output` (não há nenhum Olá de tooadd necessidade `[<Out>]` anotação).</span><span class="sxs-lookup"><span data-stu-id="1eba8-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="1eba8-127">Usando um `byref<>` tipo permite que seu toochange de função que o argumento de saudação do registro ou objeto refere-se a.</span><span class="sxs-lookup"><span data-stu-id="1eba8-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="1eba8-128">Quando um registro F # é usado como um tipo de entrada, a definição de registro Olá deve ser marcada com `[<CLIMutable>]` em ordem tooallow hello Azure funções framework tooset campos Olá adequadamente antes passando Olá tooyour registro função.</span><span class="sxs-lookup"><span data-stu-id="1eba8-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="1eba8-129">Bastidores hello, `[<CLIMutable>]` gera setters de propriedades de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="1eba8-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="1eba8-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="1eba8-131">Uma classe de F# também pode ser usada para ambos os argumentos.</span><span class="sxs-lookup"><span data-stu-id="1eba8-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="1eba8-132">Para uma classe, as propriedades geralmente exigirão getters e setters.</span><span class="sxs-lookup"><span data-stu-id="1eba8-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="1eba8-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="1eba8-134">Registro em log</span><span class="sxs-lookup"><span data-stu-id="1eba8-134">Logging</span></span>
<span data-ttu-id="1eba8-135">saída de toolog tooyour [os logs de streaming](../app-service-web/web-sites-streaming-logs-and-console.md) em F #, a função deve levar um argumento de tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="1eba8-136">Para manter a consistência, recomendamos que esse argumento seja denominado `log`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="1eba8-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="1eba8-138">Assíncrono</span><span class="sxs-lookup"><span data-stu-id="1eba8-138">Async</span></span>
<span data-ttu-id="1eba8-139">Olá `async` fluxo de trabalho pode ser usado, mas o resultado de saudação precisa tooreturn um `Task`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="1eba8-140">Isso pode ser feito com `Async.StartAsTask`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="1eba8-141">Token de cancelamento</span><span class="sxs-lookup"><span data-stu-id="1eba8-141">Cancellation Token</span></span>
<span data-ttu-id="1eba8-142">Se a função precisa desligar toohandle normalmente, você pode atribuir um [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumento.</span><span class="sxs-lookup"><span data-stu-id="1eba8-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="1eba8-143">Isso pode ser combinado com `async`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="1eba8-144">Importando namespaces</span><span class="sxs-lookup"><span data-stu-id="1eba8-144">Importing namespaces</span></span>
<span data-ttu-id="1eba8-145">Namespaces podem ser abertos no hello maneira normal:</span><span class="sxs-lookup"><span data-stu-id="1eba8-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="1eba8-146">Olá namespaces a seguir é aberto automaticamente:</span><span class="sxs-lookup"><span data-stu-id="1eba8-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="1eba8-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="1eba8-148">Referenciando Assemblies Externos</span><span class="sxs-lookup"><span data-stu-id="1eba8-148">Referencing External Assemblies</span></span>
<span data-ttu-id="1eba8-149">Da mesma forma, o assembly do framework possível adicionar referências com hello `#r "AssemblyName"` diretiva.</span><span class="sxs-lookup"><span data-stu-id="1eba8-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="1eba8-150">Hello assemblies a seguir são automaticamente adicionados pelas funções do Azure Olá ambiente de hospedagem:</span><span class="sxs-lookup"><span data-stu-id="1eba8-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="1eba8-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="1eba8-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="1eba8-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="1eba8-153">Além disso, a saudação assemblies a seguir é especial de maiusculas e minúsculas e pode ser referenciada por simplename (por exemplo, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="1eba8-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="1eba8-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="1eba8-155">Se você precisar tooreference um assembly privado, você pode carregar o arquivo de assembly de saudação em um `bin` referência usando hello (por exemplo, o nome de arquivo e função de tooyour relativo da pasta  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="1eba8-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="1eba8-156">Para obter informações sobre como tooupload arquivos de pasta de função tooyour, consulte Olá seção Gerenciamento de pacotes a seguir.</span><span class="sxs-lookup"><span data-stu-id="1eba8-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="1eba8-157">Prelúdio do editor</span><span class="sxs-lookup"><span data-stu-id="1eba8-157">Editor Prelude</span></span>
<span data-ttu-id="1eba8-158">Um editor que oferece suporte a serviços de compilador F # não estarão ciente dessas Olá namespaces e assemblies que funções do Azure inclui automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1eba8-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="1eba8-159">Como tal, ele pode ser útil tooinclude um prelude que ajuda a editor Olá localizar assemblies Olá que você está usando e tooexplicitly abrir namespaces.</span><span class="sxs-lookup"><span data-stu-id="1eba8-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="1eba8-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-160">For example:</span></span>

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

<span data-ttu-id="1eba8-161">Quando seu código é executado funções do Azure, ele processa fonte Olá com `COMPILED` definidos, para que prelude de editor hello será ignorada.</span><span class="sxs-lookup"><span data-stu-id="1eba8-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="1eba8-162">Gerenciamento de pacote</span><span class="sxs-lookup"><span data-stu-id="1eba8-162">Package management</span></span>
<span data-ttu-id="1eba8-163">pacotes do NuGet toouse em uma função de F #, adicione um `project.json` pasta da função de saudação toohello de arquivo no sistema de arquivos do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="1eba8-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="1eba8-164">Aqui está um exemplo `project.json` arquivo que adiciona uma referência de pacote do NuGet muito`Microsoft.ProjectOxford.Face` versão 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="1eba8-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="1eba8-165">Apenas hello do .NET Framework 4.6 tem suporte, portanto certifique-se que seu `project.json` arquivo especifica `net46` conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="1eba8-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="1eba8-166">Quando você carrega um `project.json` de arquivos, hello em tempo de execução obtém os pacotes de saudação e adiciona automaticamente os assemblies do pacote toohello referências.</span><span class="sxs-lookup"><span data-stu-id="1eba8-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="1eba8-167">Você não precisa tooadd `#r "AssemblyName"` diretivas.</span><span class="sxs-lookup"><span data-stu-id="1eba8-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="1eba8-168">Basta adicionar Olá necessário `open` instruções tooyour `.fsx` arquivo.</span><span class="sxs-lookup"><span data-stu-id="1eba8-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="1eba8-169">Talvez você queira tooput automaticamente faz referência a assemblies no seu prelude editor, tooimprove interação do editor com serviços de compilação do F #.</span><span class="sxs-lookup"><span data-stu-id="1eba8-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="1eba8-170">Como tooadd uma `project.json` arquivo tooyour função do Azure</span><span class="sxs-lookup"><span data-stu-id="1eba8-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="1eba8-171">Begin, certificando-se seu aplicativo de função está em execução, que pode ser feito através da abertura de sua função no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1eba8-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="1eba8-172">Isso também permite acesso os logs de streaming toohello qual saída de instalação do pacote será exibida.</span><span class="sxs-lookup"><span data-stu-id="1eba8-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="1eba8-173">tooupload um `project.json` de arquivos, use um dos métodos de saudação descritos em [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="1eba8-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="1eba8-174">Se você estiver usando [implantação contínua para funções do Azure](functions-continuous-deployment.md), você pode adicionar um `project.json` tooyour branch no tooexperiment de ordem com ele antes de adicioná-lo tooyour ramificação de implantação de preparo de arquivos.</span><span class="sxs-lookup"><span data-stu-id="1eba8-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="1eba8-175">Depois de saudação `project.json` arquivo é adicionado, você verá a saída toohello semelhante exemplo em sua função a seguir do fluxo de log:</span><span class="sxs-lookup"><span data-stu-id="1eba8-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="1eba8-176">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="1eba8-176">Environment variables</span></span>
<span data-ttu-id="1eba8-177">tooget uma variável de ambiente ou um valor de configuração do aplicativo, use `System.Environment.GetEnvironmentVariable`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="1eba8-178">Reutilizar o código .fsx</span><span class="sxs-lookup"><span data-stu-id="1eba8-178">Reusing .fsx code</span></span>
<span data-ttu-id="1eba8-179">Você pode usar código de outros arquivos `.fsx` usando uma diretiva `#load`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="1eba8-180">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1eba8-180">For example:</span></span>

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

<span data-ttu-id="1eba8-181">Caminhos fornece toohello `#load` diretiva são toohello relativo local do seu `.fsx` arquivo.</span><span class="sxs-lookup"><span data-stu-id="1eba8-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="1eba8-182">`#load "logger.fsx"`carrega um arquivo localizado na pasta de função hello.</span><span class="sxs-lookup"><span data-stu-id="1eba8-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="1eba8-183">`#load "package\logger.fsx"`carrega um arquivo localizado no hello `package` na pasta de função hello.</span><span class="sxs-lookup"><span data-stu-id="1eba8-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="1eba8-184">`#load "..\shared\mylogger.fsx"`carrega um arquivo localizado no hello `shared` pasta no mesmo nível como pasta de função hello, ou seja, de saudação diretamente sob `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="1eba8-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="1eba8-185">Olá `#load` diretiva só funciona com `.fsx` arquivos (F # script) e não com `.fs` arquivos.</span><span class="sxs-lookup"><span data-stu-id="1eba8-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1eba8-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1eba8-186">Next steps</span></span>
<span data-ttu-id="1eba8-187">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1eba8-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="1eba8-188">Guia de F#</span><span class="sxs-lookup"><span data-stu-id="1eba8-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="1eba8-189">Práticas recomendadas para o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="1eba8-190">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="1eba8-191">Referência do desenvolvedor de C# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="1eba8-192">Referência do desenvolvedor de NodeJS do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="1eba8-193">Gatilhos e de associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="1eba8-194">Teste do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="1eba8-195">Dimensionamento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1eba8-195">Azure Functions scaling</span></span>](functions-scale.md)

