---
title: "classe de aaaUsing .NET bibliotecas com funções do Azure | Microsoft Docs"
description: "Saiba como bibliotecas de classes do .NET tooauthor para usam com as funções do Azure"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a>Usando bibliotecas de classes .NET com o Azure Functions

Além disso tooscript arquivos, funções do Azure oferece suporte a uma biblioteca de classe de publicação como implementação Olá para uma ou mais funções. Recomendamos que você use Olá [ferramentas do Azure funções Visual Studio 2017](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).

## <a name="prerequisites"></a>Pré-requisitos 

Este artigo possui Olá pré-requisitos a seguir:

- [Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/). Instalar as cargas de trabalho Olá **desenvolvimento ASP.NET e web** e **desenvolvimento do Azure**.
- [Ferramentas do Azure Functions para Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Projeto de biblioteca de classes de funções

No Visual Studio, crie um novo projeto do Azure Functions. novo modelo de projeto Olá cria arquivos Olá *host.json* e *local.settings.json*. Você pode [personalizar as configurações de tempo de execução do Azure Functions no host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json). 

arquivo Hello *local.settings.json* armazena configurações do aplicativo, cadeias de caracteres de conexão e as configurações para as ferramentas de núcleo de funções do Azure. toolearn mais sobre a estrutura, consulte [código e teste do Azure funciona localmente](functions-run-local.md#local-settings).

### <a name="functionname-attribute"></a>Atributo FunctionName

atributo Olá [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marca um método como um ponto de entrada da função. Ele deve ser usado com exatamente um gatilho e 0 ou mais associações de entrada e saída.

### <a name="conversion-toofunctionjson"></a>Toofunction.json de conversão

Quando um projeto de funções do Azure é criado, ele produz um arquivo `function.json` no diretório de saudação correspondente Olá nome de função definido pelo `[FunctionName]`. Especifica os disparadores e associações e arquivo de assembly do projeto de toohello de pontos.

Essa conversão é executada pelo pacote do NuGet Olá [Microsoft\.NET\.Sdk\.funções](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). origem Hello está disponível no repositório do GitHub Olá [azure\-funções\-vs\-criar\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="triggers-and-bindings"></a>Gatilhos e associações

Olá tabela a seguir lista os gatilhos de saudação e associações que estão disponíveis em um projeto de biblioteca de classe de funções do Azure. Todos os atributos estão no namespace de saudação `Microsoft.Azure.WebJobs`.

| Associação | Atributo | Pacote NuGet |
|------   | ------    | ------        |
| [Gatilho de armazenamento de blobs, entrada, saída](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [O armazenamento de blobs] |
| [Associação de entrada e saída do Cosmos DB](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Gatilho de Hubs de Eventos e saída](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [Entrada e saída do arquivo externo](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [Gatilho HTTP e webhook](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Entrada e saída dos Aplicativos Móveis](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Saída dos Hubs de Notificação](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [Gatilho de armazenamento de filas e saída](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Saída do SendGrid](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Gatilho e saída do Barramento de Serviço](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [Entrada e saída de armazenamento de tabelas](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Gatilho de temporizador](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Saída do Twilio](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Associações de entrada, saída e gatilho armazenamento de blobs

O Azure Functions dá suporte a associações de entrada, saída e gatilho para o Azure Blob Storage. Para obter mais informações sobre expressões de associação e os metadados, consulte [Associações de armazenamento de blobs do Azure Functions](functions-bindings-storage-blob.md).

Um gatilho de blob é definido com hello `[BlobTrigger]` atributo. Você pode usar o atributo Olá `[StorageAccount]` toodefine conta de armazenamento de saudação que é usada por uma classe ou função inteira.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

Blob de entrada e saída são definidos usando Olá `[Blob]` atributo, junto com um `FileAccess` parâmetro que indica a leitura ou gravação. Olá seguinte exemplo usa um gatilho de blob e associação de saída de blob.

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a>Associações de entrada e saída do Cosmos DB

O Azure Functions dá suporte a associações de entrada e saída para o Cosmos DB. toolearn mais sobre os recursos de saudação de associação de banco de dados do Cosmos hello, consulte [associações de banco de dados do Azure funções Cosmos](functions-bindings-documentdb.md).

toobind tooa Cosmos banco de dados de documento, use o atributo de saudação `[DocumentDB]` no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.DocumentDB]. saudação de exemplo a seguir tem um gatilho de fila e uma API DocumentDB associação de saída:

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a>Gatilho de Hubs de Eventos e saída

O Azure Functions dá suporte a associações de gatilho e de saída para os Hubs de Eventos. Para obter mais informações, consulte [Associações do Hub de Eventos do Azure Functions](functions-bindings-event-hubs.md).

Olá tipos `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` e `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` são definidos no pacote do NuGet Olá [Microsoft.Azure.WebJobs.ServiceBus]. 

Olá, exemplo a seguir usa um gatilho de Hub de eventos:

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Olá, exemplo a seguir tem um Hub de eventos de saída, usando o valor de retorno do método hello como saída de hello:

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a>Entrada e saída do arquivo externo

O Azure Functions dá suporte a associações de gatilho, entrada e saída para arquivos externos, tais como Google Drive, Dropbox e OneDrive. mais, consulte toolearn [associações de arquivo externo de funções do Azure](functions-bindings-external-file.md). Olá atributos `[ExternalFileTrigger]` e `[ExternalFile]` são definidos no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.ApiHub].

Olá c# de exemplo a seguir demonstra um arquivo externo de entrada e saída de associação. cópias de código Olá Olá arquivo de saída do arquivo de entrada toohello.

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a>HTTP e webhooks

Saudação de uso `HttpTrigger` gatilho do atributo toodefine um HTTP ou webhook. Esse atributo é definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.Http]. Você pode personalizar o nível de autorização hello, tipo de webhook, rota e métodos. Olá, exemplo a seguir define um gatilho HTTP com a autenticação anônima e _genericJson_ webhook tipo.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Entrada e saída dos Aplicativos Móveis

O Azure Functions dá suporte a associações de entrada e saída para os Aplicativos Móveis. mais, consulte toolearn [associações de aplicativos do Azure funções móveis](functions-bindings-mobile-apps.md). atributo Olá `[MobileTable]` está definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.MobileApps].

Olá, exemplo a seguir demonstra um aplicativos móveis associação de saída:

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Saída dos Hubs de Notificação

O Azure Functions oferece suporte a uma associação de saída para Hubs de Notificação. mais, consulte toolearn [associação de saída do Hub de notificação do Azure funções](functions-bindings-notification-hubs.md). atributo Olá `[NotificationHub]` está definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>Gatilho de armazenamento de filas e saída

O Azure Functions dá suporte a associações de gatilho e de saída para filas do Azure. Para obter mais informações, consulte [Associações do Armazenamento de Filas do Azure Functions](functions-bindings-storage-queue.md).

Olá exemplo a seguir mostra como função de hello toouse tipo de retorno com uma saída de fila de associação, usando Olá `[Queue]` atributo. toodefine um gatilho de fila, use Olá `[QueueTrigger]` atributo.

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a>Saída do SendGrid

O Azure Functions oferece suporte a uma associação de saída do SendGrid para enviar email programaticamente. mais, consulte toolearn [SendGrid de funções do Azure associações](functions-bindings-sendgrid.md).

atributo Olá `[SendGrid]` está definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.SendGrid].

Olá, a seguir é um exemplo de usando um gatilho de fila do barramento de serviço e uma associação de saída SendGrid usando `SendGridMessage`:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a>Gatilho e saída do Barramento de Serviço

O Azure Functions dá suporte a gatilhos e a associações de saída para filas e tópicos do Barramento de Serviço. Para obter mais informações sobre como configurar associações, consulte [Associações do Barramento de Serviço do Azure Functions](functions-bindings-service-bus.md).

Olá atributos `[ServiceBusTrigger]` e `[ServiceBus]` são definidos no pacote do NuGet Olá [Microsoft.Azure.WebJobs.ServiceBus]. 

Olá seguinte é um exemplo de um gatilho de fila do barramento de serviço:

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

a seguir Olá é um exemplo de uma saída de barramento de serviço de associação, usando o tipo de retorno do método hello como saída de hello:

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a>Entrada e saída de armazenamento de tabelas

O Azure Functions dá suporte a associações de entrada e saída para armazenamento de Tabelas do Azure. mais, consulte toolearn [associações de armazenamento de tabela de funções do Azure](functions-bindings-storage-table.md).

Olá, exemplo a seguir é uma classe com duas funções, demonstrando associações de entrada e saída de armazenamento de tabela. 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a>Gatilho de temporizador

O Azure Functions tem uma associação de gatilho de timer que permite executar o código de função com base em um agendamento definido. toolearn mais sobre os recursos de saudação da associação hello, consulte [agendar a execução de código com funções do Azure](functions-bindings-timer.md).

Plano de consumo hello, você pode definir agendas com um [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression). Se você estiver usando um Plano do Serviço de Aplicativo, você também pode usar uma cadeia de caracteres do período de tempo. 

saudação de exemplo a seguir define um gatilho de timer que é executado a cada 5 minutos:

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Saída do Twilio

Suporte de funções do Azure Twilio saída associações tooenable suas mensagens de texto SMS funções toosend. mais, consulte toolearn [associação de saída de mensagens de enviar SMS das funções do Azure usando Olá Twilio](functions-bindings-twilio.md). 

atributo Olá `[TwilioSms]` está definido no pacote de saudação [Microsoft.Azure.WebJobs.Extensions.Twilio].

Olá, c# de exemplo seguinte usa uma fila gatilho e uma Twilio associação de saída:

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar funções do Azure no script de C#, consulte a [referência para o desenvolvedor de script \#C no Azure Functions](functions-reference-csharp.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
