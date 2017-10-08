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
# <a name="azure-functions-f-developer-reference"></a>Referência do desenvolvedor em F# do Azure Functions
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script em F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # para funções do Azure é uma solução para executar facilmente pequenos pedaços de código ou "funções", na nuvem de saudação. Fluxos de dados em sua função F# por meio de argumentos de função. Os nomes de argumento são especificados em `function.json`, e existem nomes predefinidos para acessar as coisas como Olá tokens de agente e o cancelamento de função.

Este artigo pressupõe que você já leu Olá [referência do desenvolvedor do Azure funções](functions-reference.md).

## <a name="how-fsx-works"></a>Como funciona o .fsx
Um arquivo `.fsx` é um script de F#. Ele pode ser considerado um projeto em F# contido em um único arquivo. arquivo Hello contém ambos código Olá para o programa (nesse caso, a função do Azure) e diretivas para gerenciar as dependências.

Quando você usa um `.fsx` para uma função do Azure, normalmente requeridos assemblies serão incluídos automaticamente para você, permitindo que você toofocus no código de função em vez de "boilerplate" hello.

## <a name="binding-tooarguments"></a>Associação tooarguments
Cada associação oferece suporte a um conjunto de argumentos, como detalhado no hello [gatilhos e associações de referência do desenvolvedor do Azure funções](functions-triggers-bindings.md). Por exemplo, uma das associações de argumento Olá dá suporte a um gatilho de blob é um POCO, que pode ser expressada usando um registro F #. Por exemplo:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

O Azure Function em F# usará um ou mais argumentos. Quando falamos sobre os argumentos de funções do Azure, nós nos referimos muito*entrada* argumentos e *saída* argumentos. Um argumento de entrada é exatamente o que parece: entrada tooyour função do Azure F #. Um *saída* argumento é mutáveis dados ou um `byref<>` argumento serve como uma maneira toopass de dados volta *out* de sua função.

No exemplo acima, a saudação `blob` é um argumento de entrada, e `output` é um argumento de saída. Observe que usamos `byref<>` para `output` (não há nenhum Olá de tooadd necessidade `[<Out>]` anotação). Usando um `byref<>` tipo permite que seu toochange de função que o argumento de saudação do registro ou objeto refere-se a.

Quando um registro F # é usado como um tipo de entrada, a definição de registro Olá deve ser marcada com `[<CLIMutable>]` em ordem tooallow hello Azure funções framework tooset campos Olá adequadamente antes passando Olá tooyour registro função. Bastidores hello, `[<CLIMutable>]` gera setters de propriedades de registro de saudação. Por exemplo:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

Uma classe de F# também pode ser usada para ambos os argumentos. Para uma classe, as propriedades geralmente exigirão getters e setters. Por exemplo:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Registro em log
saída de toolog tooyour [os logs de streaming](../app-service-web/web-sites-streaming-logs-and-console.md) em F #, a função deve levar um argumento de tipo `TraceWriter`. Para manter a consistência, recomendamos que esse argumento seja denominado `log`. Por exemplo:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Assíncrono
Olá `async` fluxo de trabalho pode ser usado, mas o resultado de saudação precisa tooreturn um `Task`. Isso pode ser feito com `Async.StartAsTask`, por exemplo:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>Token de cancelamento
Se a função precisa desligar toohandle normalmente, você pode atribuir um [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumento. Isso pode ser combinado com `async`, por exemplo:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Importando namespaces
Namespaces podem ser abertos no hello maneira normal:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Olá namespaces a seguir é aberto automaticamente:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Referenciando Assemblies Externos
Da mesma forma, o assembly do framework possível adicionar referências com hello `#r "AssemblyName"` diretiva.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hello assemblies a seguir são automaticamente adicionados pelas funções do Azure Olá ambiente de hospedagem:

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`.

Além disso, a saudação assemblies a seguir é especial de maiusculas e minúsculas e pode ser referenciada por simplename (por exemplo, `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Se você precisar tooreference um assembly privado, você pode carregar o arquivo de assembly de saudação em um `bin` referência usando hello (por exemplo, o nome de arquivo e função de tooyour relativo da pasta  `#r "MyAssembly.dll"`). Para obter informações sobre como tooupload arquivos de pasta de função tooyour, consulte Olá seção Gerenciamento de pacotes a seguir.

## <a name="editor-prelude"></a>Prelúdio do editor
Um editor que oferece suporte a serviços de compilador F # não estarão ciente dessas Olá namespaces e assemblies que funções do Azure inclui automaticamente. Como tal, ele pode ser útil tooinclude um prelude que ajuda a editor Olá localizar assemblies Olá que você está usando e tooexplicitly abrir namespaces. Por exemplo:

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

Quando seu código é executado funções do Azure, ele processa fonte Olá com `COMPILED` definidos, para que prelude de editor hello será ignorada.

<a name="package"></a>

## <a name="package-management"></a>Gerenciamento de pacote
pacotes do NuGet toouse em uma função de F #, adicione um `project.json` pasta da função de saudação toohello de arquivo no sistema de arquivos do aplicativo de função hello. Aqui está um exemplo `project.json` arquivo que adiciona uma referência de pacote do NuGet muito`Microsoft.ProjectOxford.Face` versão 1.1.0:

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

Apenas hello do .NET Framework 4.6 tem suporte, portanto certifique-se que seu `project.json` arquivo especifica `net46` conforme mostrado aqui.

Quando você carrega um `project.json` de arquivos, hello em tempo de execução obtém os pacotes de saudação e adiciona automaticamente os assemblies do pacote toohello referências. Você não precisa tooadd `#r "AssemblyName"` diretivas. Basta adicionar Olá necessário `open` instruções tooyour `.fsx` arquivo.

Talvez você queira tooput automaticamente faz referência a assemblies no seu prelude editor, tooimprove interação do editor com serviços de compilação do F #.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>Como tooadd uma `project.json` arquivo tooyour função do Azure
1. Begin, certificando-se seu aplicativo de função está em execução, que pode ser feito através da abertura de sua função no hello portal do Azure. Isso também permite acesso os logs de streaming toohello qual saída de instalação do pacote será exibida.
2. tooupload um `project.json` de arquivos, use um dos métodos de saudação descritos em [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate). Se você estiver usando [implantação contínua para funções do Azure](functions-continuous-deployment.md), você pode adicionar um `project.json` tooyour branch no tooexperiment de ordem com ele antes de adicioná-lo tooyour ramificação de implantação de preparo de arquivos.
3. Depois de saudação `project.json` arquivo é adicionado, você verá a saída toohello semelhante exemplo em sua função a seguir do fluxo de log:

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

## <a name="environment-variables"></a>Variáveis de ambiente
tooget uma variável de ambiente ou um valor de configuração do aplicativo, use `System.Environment.GetEnvironmentVariable`, por exemplo:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>Reutilizar o código .fsx
Você pode usar código de outros arquivos `.fsx` usando uma diretiva `#load`. Por exemplo:

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

Caminhos fornece toohello `#load` diretiva são toohello relativo local do seu `.fsx` arquivo.

* `#load "logger.fsx"`carrega um arquivo localizado na pasta de função hello.
* `#load "package\logger.fsx"`carrega um arquivo localizado no hello `package` na pasta de função hello.
* `#load "..\shared\mylogger.fsx"`carrega um arquivo localizado no hello `shared` pasta no mesmo nível como pasta de função hello, ou seja, de saudação diretamente sob `wwwroot`.

Olá `#load` diretiva só funciona com `.fsx` arquivos (F # script) e não com `.fs` arquivos.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir:

* [Guia de F#](/dotnet/articles/fsharp/index)
* [Práticas recomendadas para o Azure Functions](functions-best-practices.md)
* [Referência do desenvolvedor do Azure Functions](functions-reference.md)
* [Referência do desenvolvedor de C# do Azure Functions](functions-reference-csharp.md)
* [Referência do desenvolvedor de NodeJS do Azure Functions](functions-reference-node.md)
* [Gatilhos e de associações do Azure Functions](functions-triggers-bindings.md)
* [Teste do Azure Functions](functions-test-a-function.md)
* [Dimensionamento do Azure Functions](functions-scale.md)

