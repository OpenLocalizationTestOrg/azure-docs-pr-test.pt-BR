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
# <a name="azure-functions-c-script-developer-reference"></a>Referência do desenvolvedor de scripts C# do Azure Functions
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script em F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

Olá c# experiência de script para funções do Azure baseia-se em Olá SDK do Azure WebJobs. Fluxos de dados na sua função C# por meio de argumentos de método. Os nomes de argumento são especificados em `function.json`, e existem nomes predefinidos para acessar as coisas como Olá tokens de agente e o cancelamento de função.

Este artigo pressupõe que você já leu Olá [referência do desenvolvedor do Azure funções](functions-reference.md).

Para obter informações sobre como usar as bibliotecas de classes C#, consulte [Usando bibliotecas de classes do .NET com o Azure Functions](functions-dotnet-class-library.md).

## <a name="how-csx-works"></a>Como o .csx funciona
Olá `.csx` formato permite que você toowrite menos "boilerplate" e foco sobre a escrita de apenas uma função c#. Inclua todos os namespaces no início de saudação do arquivo hello e referências de assembly como de costume. Em vez de encapsular tudo em um namespace e uma classe, basta definir um método `Run`. Se você precisar tooinclude todas as classes, para a instância toodefine simples objetos antigo objeto CLR (POCO), você pode incluir uma classe em Olá mesmo arquivo.   

## <a name="binding-tooarguments"></a>Associação tooarguments
Olá, várias associações são associados tooa c# função via Olá `name` propriedade Olá *function.json* configuração. Cada associação tem seus próprios tipos com suporte; por exemplo, um gatilho de blob pode dar suporte a uma cadeia de caracteres, um POCO ou um CloudBlockBlob. tipos de saudação com suporte são documentados na referência de Olá para cada associação. Um objeto POCO deve ter um getter e setter definido para cada propriedade.

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

## <a name="using-method-return-value-for-output-binding"></a>Usando o valor retornado de um método em uma associação de saída

Você pode usar um valor de retorno do método para uma associação de saída, usando o nome da saudação `$return` na *function.json*:

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

## <a name="writing-multiple-output-values"></a>Gravando vários valores de saída

toowrite tooan de vários valores de saída de associação, use Olá [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) tipos. Esses tipos são coleções de somente gravação que são a associação de saída toohello escrito quando o método hello for concluída.

Este exemplo grava várias mensagens de fila usando `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Registro em log
toolog saída tooyour os logs de streaming em c#, incluir um argumento do tipo `TraceWriter`. Recomendamos nomeá-lo como `log`. Evite usar `Console.Write` no Azure Functions. 

`TraceWriter`é definido em Olá [SDK do Azure WebJobs](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Olá o nível de log para `TraceWriter` podem ser configurados em [host\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Assíncrono
toomake uma função assíncrona, use Olá `async` palavra-chave e retornar um `Task` objeto.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>Token de cancelamento
Algumas operações exigem um desligamento normal. Embora sempre seja melhor código toowrite que pode lidar com falha, em casos onde você deseja toohandle solicitações de desligamento normal, você define uma [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumento de tipo.  Um `CancellationToken` é fornecida toosignal que um desligamento de host é disparado.

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

## <a name="importing-namespaces"></a>Importando namespaces
Se você precisar tooimport namespaces, você pode fazer isso como de costume, com hello `using` cláusula.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Olá namespaces a seguir são automaticamente importados e, portanto, são opcionais:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Referenciando Assemblies Externos
Para assemblies do framework, adicione referências usando Olá `#r "AssemblyName"` diretiva.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello assemblies a seguir são automaticamente adicionados pelas funções do Azure Olá ambiente de hospedagem:

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

Olá assemblies a seguir podem ser referenciados por nome simples (por exemplo, `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Referenciando assemblies personalizados

tooreference um assembly personalizado, você pode usar um *compartilhado* assembly ou um *privada* assembly:
- Assemblies compartilhados são compartilhados entre todas as funções em um aplicativo de funções. tooreference um assembly personalizado, carregar o aplicativo de função tooyour do assembly hello, como em um `bin` pasta na raiz do aplicativo de função hello. 
- Assemblies particulares fazem parte do contexto de determinada função e dão suporte ao sideload de versões diferentes. Assemblies privados devem ser carregados em um `bin` pasta no diretório de função hello. Referência usando o nome do arquivo hello, como `#r "MyAssembly.dll"`. 

Para obter informações sobre como tooupload arquivos de pasta de função tooyour, consulte Olá seção Gerenciamento de pacotes a seguir.

### <a name="watched-directories"></a>Diretórios inspecionados

diretório Olá que contém o arquivo de script de função hello automaticamente é inspecionado tooassemblies de alterações. toowatch alterações de assembly em outros diretórios, adicioná-las toohello `watchDirectories` lista [host\.json].

## <a name="using-nuget-packages"></a>Usando pacotes NuGet
pacotes do NuGet toouse em uma função c#, carregar uma *Project* pasta toohello da função de arquivo no sistema de arquivos do aplicativo de função hello. Aqui está um exemplo *Project* arquivo que adiciona uma referência tooMicrosoft.ProjectOxford.Face versão 1.1.0:

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

Apenas hello do .NET Framework 4.6 tem suporte, portanto certifique-se que seu *Project* arquivo especifica `net46` conforme mostrado aqui.

Quando você carrega um *Project* de arquivos, hello em tempo de execução obtém os pacotes de saudação e adiciona automaticamente os assemblies do pacote toohello referências. Você não precisa tooadd `#r "AssemblyName"` diretivas. tipos de saudação toouse definidos em pacotes do NuGet hello, adicionar Olá necessário `using` instruções tooyour *run.csx* arquivo 

Em tempo de execução de funções hello, a restauração do NuGet funciona comparando `project.json` e `project.lock.json`. Se Olá carimbos de data e hora dos arquivos de saudação **não** correspondência, uma restauração do NuGet executa e pacotes de atualização de downloads do NuGet. No entanto, se hello carimbos de data e hora dos arquivos de saudação **fazer** correspondência, o NuGet não realizar uma restauração. Portanto, `project.lock.json` não deve ser implantado porque ele faz com que a restauração do pacote do NuGet tooskip. tooavoid Implantando o bloqueio de saudação do arquivo, adicione Olá `project.lock.json` toohello `.gitignore` arquivo.

toouse um feed personalizado do NuGet, especifique Olá feed em uma *config* arquivo na raiz do aplicativo de função hello. Para obter mais informações, consulte [Configurando o comportamento do NuGet](/nuget/consume-packages/configuring-nuget-behavior).

### <a name="using-a-projectjson-file"></a>Usando um arquivo project.json
1. Abra a função hello no hello portal do Azure. Olá registra a saída de instalação do pacote do guia exibe hello.
2. tooupload um arquivo Project. JSON, use um dos métodos de saudação descritos em Olá [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate) no tópico de referência de desenvolvedor Olá funções do Azure.
3. Depois de saudação *Project* arquivo é carregado, você verá a saída como Olá exemplo em sua função a seguir do fluxo de log:

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
tooget uma variável de ambiente ou um valor de configuração do aplicativo, use `System.Environment.GetEnvironmentVariable`, conforme mostrado no hello exemplo de código a seguir:

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

## <a name="reusing-csx-code"></a>Reutilização de código .csx
Você pode usar classes e métodos definidos em outros arquivos *.csx* no seu arquivo *run.csx*. toodo que usam `#load` diretivas em seu *run.csx* arquivo. Saudação de exemplo a seguir, uma rotina de log denominado `MyLogger` é compartilhado em *myLogger.csx* e carregados na *run.csx* usando Olá `#load` diretiva:

Exemplo de *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Exemplo de *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

Usando um compartilhado *. CSx* é um padrão comum quando desejar toostrongly seus argumentos entre funções usando um objeto POCO de tipo. Em Olá simplificada de exemplo a seguir, um gatilho HTTP e o gatilho de fila compartilham um objeto POCO chamado `Order` toostrongly dados de pedidos de saudação de tipo:

Exemplo *run.csx* para o gatilho HTTP:

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

Exemplo *run.csx* para o gatilho da fila:

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

Exemplo *order.csx*:

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

Você pode usar um caminho relativo com hello `#load` diretiva:

* `#load "mylogger.csx"`carrega um arquivo localizado na pasta de função hello.
* `#load "loadedfiles\mylogger.csx"`carrega um arquivo localizado em uma pasta na pasta de função hello.
* `#load "..\shared\mylogger.csx"`carrega um arquivo localizado em uma pasta no mesmo nível como pasta de função hello, ou seja, de saudação diretamente sob *wwwroot*.

Olá `#load` diretiva só funciona com *. CSx* arquivos (c# script), não com *. CS* arquivos.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Associação em tempo de execução por meio de associações obrigatórias

Em c# e outras linguagens .NET, você pode usar um [fundamental](https://en.wikipedia.org/wiki/Imperative_programming) padrão de associação, como contrário toohello [ *declarativa* ](https://en.wikipedia.org/wiki/Declarative_programming) associações em *function.json*. Associação fundamental é útil quando precisam de parâmetros de ligação toobe computado em tempo de execução, em vez de design. Com esse padrão, você pode associar toosupported entrada e saída associação em interrupções no seu código de função.

Defina uma associação obrigatória da seguinte maneira:

- **Não** inclua uma entrada em *function.json* para as associações obrigatórias desejadas.
- Passe um parâmetro de entrada [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) ou [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Use Olá c# padrão tooperform Olá associação de dados a seguir.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

onde `BindingTypeAttribute` é Olá .NET atributo que define a associação e `T` é Olá o tipo de entrada ou saído que é suportado por este tipo de associação. `T` também não pode ser um tipo de parâmetro `out` (como `out JObject`). Por exemplo, a associação de saída de tabela dos Aplicativos Móveis dá suporte a [seis tipos de saída](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), mas você só pode usar [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) ou [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) para `T`.

Olá, código de exemplo a seguir cria um [associação de saída blob de armazenamento](functions-bindings-storage-blob.md#using-a-blob-output-binding) com blob caminho que é definido em tempo de execução, em seguida, grava um blob de toohello de cadeia de caracteres.

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) define Olá [blob de armazenamento](functions-bindings-storage-blob.md) de entrada ou saída de associação, e [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) é um tipo de associação de saída com suporte.
Como é, o código de saudação obtém configuração de aplicativo padrão Olá para Olá cadeia de conexão da conta de armazenamento (que é `AzureWebJobsStorage`). Você pode especificar um toouse de configuração de aplicativo personalizado adicionando o [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) e passar a matriz de atributos de saudação em `BindAsync<T>()`. Por exemplo,

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

Olá tabela a seguir lista atributos de .NET Olá para cada pacotes de tipo e hello de associação no qual eles são definidos.

> [!div class="mx-codeBreakAll"]
| Associação | Atributo | Adicionar referência |
|------|------|------|
| Banco de Dados Cosmos | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Hubs de Eventos | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Aplicativos Móveis | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Hubs de Notificação | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Barramento de Serviço | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Fila de armazenamento | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Armazenamento de blobs | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Tabela de armazenamento | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir:

* [Práticas recomendadas para o Azure Functions](functions-best-practices.md)
* [Referência do desenvolvedor do Azure Functions](functions-reference.md)
* [Referência do desenvolvedor em F# do Azure Functions](functions-reference-fsharp.md)
* [Referência do desenvolvedor de NodeJS do Azure Functions](functions-reference-node.md)
* [Gatilhos e associações de Azure Functions](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
