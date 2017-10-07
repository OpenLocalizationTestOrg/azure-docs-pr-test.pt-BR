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
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="ebb85-104">Usando bibliotecas de classes .NET com o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ebb85-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="ebb85-105">Além disso tooscript arquivos, funções do Azure oferece suporte a uma biblioteca de classe de publicação como implementação Olá para uma ou mais funções.</span><span class="sxs-lookup"><span data-stu-id="ebb85-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="ebb85-106">Recomendamos que você use Olá [ferramentas do Azure funções Visual Studio 2017](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="ebb85-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebb85-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ebb85-107">Prerequisites</span></span> 

<span data-ttu-id="ebb85-108">Este artigo possui Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebb85-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="ebb85-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="ebb85-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="ebb85-110">Instalar as cargas de trabalho Olá **desenvolvimento ASP.NET e web** e **desenvolvimento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ebb85-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="ebb85-111">Ferramentas do Azure Functions para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ebb85-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="ebb85-112">Projeto de biblioteca de classes de funções</span><span class="sxs-lookup"><span data-stu-id="ebb85-112">Functions class library project</span></span>

<span data-ttu-id="ebb85-113">No Visual Studio, crie um novo projeto do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ebb85-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="ebb85-114">novo modelo de projeto Olá cria arquivos Olá *host.json* e *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="ebb85-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="ebb85-115">Você pode [personalizar as configurações de tempo de execução do Azure Functions no host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="ebb85-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="ebb85-116">arquivo Hello *local.settings.json* armazena configurações do aplicativo, cadeias de caracteres de conexão e as configurações para as ferramentas de núcleo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb85-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="ebb85-117">toolearn mais sobre a estrutura, consulte [código e teste do Azure funciona localmente](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="ebb85-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="ebb85-118">Atributo FunctionName</span><span class="sxs-lookup"><span data-stu-id="ebb85-118">FunctionName attribute</span></span>

<span data-ttu-id="ebb85-119">atributo Olá [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marca um método como um ponto de entrada da função.</span><span class="sxs-lookup"><span data-stu-id="ebb85-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="ebb85-120">Ele deve ser usado com exatamente um gatilho e 0 ou mais associações de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ebb85-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="ebb85-121">Toofunction.json de conversão</span><span class="sxs-lookup"><span data-stu-id="ebb85-121">Conversion toofunction.json</span></span>

<span data-ttu-id="ebb85-122">Quando um projeto de funções do Azure é criado, ele produz um arquivo `function.json` no diretório de saudação correspondente Olá nome de função definido pelo `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="ebb85-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="ebb85-123">Especifica os disparadores e associações e arquivo de assembly do projeto de toohello de pontos.</span><span class="sxs-lookup"><span data-stu-id="ebb85-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="ebb85-124">Essa conversão é executada pelo pacote do NuGet Olá [Microsoft\.NET\.Sdk\.funções](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="ebb85-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="ebb85-125">origem Hello está disponível no repositório do GitHub Olá [azure\-funções\-vs\-criar\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="ebb85-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="ebb85-126">Gatilhos e associações</span><span class="sxs-lookup"><span data-stu-id="ebb85-126">Triggers and bindings</span></span>

<span data-ttu-id="ebb85-127">Olá tabela a seguir lista os gatilhos de saudação e associações que estão disponíveis em um projeto de biblioteca de classe de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb85-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="ebb85-128">Todos os atributos estão no namespace de saudação `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="ebb85-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="ebb85-129">Associação</span><span class="sxs-lookup"><span data-stu-id="ebb85-129">Binding</span></span> | <span data-ttu-id="ebb85-130">Atributo</span><span class="sxs-lookup"><span data-stu-id="ebb85-130">Attribute</span></span> | <span data-ttu-id="ebb85-131">Pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="ebb85-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="ebb85-132">Gatilho de armazenamento de blobs, entrada, saída</span><span class="sxs-lookup"><span data-stu-id="ebb85-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="ebb85-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ebb85-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ebb85-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="ebb85-135">[O armazenamento de blobs]</span><span class="sxs-lookup"><span data-stu-id="ebb85-135">[Blob storage]</span></span> |
| [<span data-ttu-id="ebb85-136">Associação de entrada e saída do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ebb85-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="ebb85-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="ebb85-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="ebb85-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="ebb85-139">Gatilho de Hubs de Eventos e saída</span><span class="sxs-lookup"><span data-stu-id="ebb85-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="ebb85-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="ebb85-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="ebb85-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="ebb85-142">Entrada e saída do arquivo externo</span><span class="sxs-lookup"><span data-stu-id="ebb85-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="ebb85-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="ebb85-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="ebb85-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="ebb85-145">Gatilho HTTP e webhook</span><span class="sxs-lookup"><span data-stu-id="ebb85-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="ebb85-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="ebb85-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="ebb85-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="ebb85-148">Entrada e saída dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="ebb85-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="ebb85-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="ebb85-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="ebb85-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="ebb85-151">Saída dos Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="ebb85-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="ebb85-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="ebb85-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="ebb85-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="ebb85-154">Gatilho de armazenamento de filas e saída</span><span class="sxs-lookup"><span data-stu-id="ebb85-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="ebb85-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ebb85-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ebb85-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="ebb85-157">Saída do SendGrid</span><span class="sxs-lookup"><span data-stu-id="ebb85-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="ebb85-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-158">[SendGridAttribute]</span></span> | <span data-ttu-id="ebb85-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="ebb85-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="ebb85-160">Gatilho e saída do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ebb85-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="ebb85-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="ebb85-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="ebb85-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="ebb85-163">Entrada e saída de armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="ebb85-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="ebb85-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="ebb85-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="ebb85-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="ebb85-166">Gatilho de temporizador</span><span class="sxs-lookup"><span data-stu-id="ebb85-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="ebb85-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="ebb85-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="ebb85-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="ebb85-169">Saída do Twilio</span><span class="sxs-lookup"><span data-stu-id="ebb85-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="ebb85-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="ebb85-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="ebb85-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="ebb85-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="ebb85-172">Associações de entrada, saída e gatilho armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="ebb85-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="ebb85-173">O Azure Functions dá suporte a associações de entrada, saída e gatilho para o Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ebb85-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="ebb85-174">Para obter mais informações sobre expressões de associação e os metadados, consulte [Associações de armazenamento de blobs do Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="ebb85-175">Um gatilho de blob é definido com hello `[BlobTrigger]` atributo.</span><span class="sxs-lookup"><span data-stu-id="ebb85-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="ebb85-176">Você pode usar o atributo Olá `[StorageAccount]` toodefine conta de armazenamento de saudação que é usada por uma classe ou função inteira.</span><span class="sxs-lookup"><span data-stu-id="ebb85-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="ebb85-177">Blob de entrada e saída são definidos usando Olá `[Blob]` atributo, junto com um `FileAccess` parâmetro que indica a leitura ou gravação.</span><span class="sxs-lookup"><span data-stu-id="ebb85-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="ebb85-178">Olá seguinte exemplo usa um gatilho de blob e associação de saída de blob.</span><span class="sxs-lookup"><span data-stu-id="ebb85-178">hello following example uses a blob trigger and blob output binding.</span></span>

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

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="ebb85-179">Associações de entrada e saída do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ebb85-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="ebb85-180">O Azure Functions dá suporte a associações de entrada e saída para o Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ebb85-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="ebb85-181">toolearn mais sobre os recursos de saudação de associação de banco de dados do Cosmos hello, consulte [associações de banco de dados do Azure funções Cosmos](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="ebb85-182">toobind tooa Cosmos banco de dados de documento, use o atributo de saudação `[DocumentDB]` no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="ebb85-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="ebb85-183">saudação de exemplo a seguir tem um gatilho de fila e uma API DocumentDB associação de saída:</span><span class="sxs-lookup"><span data-stu-id="ebb85-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

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

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="ebb85-184">Gatilho de Hubs de Eventos e saída</span><span class="sxs-lookup"><span data-stu-id="ebb85-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="ebb85-185">O Azure Functions dá suporte a associações de gatilho e de saída para os Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ebb85-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="ebb85-186">Para obter mais informações, consulte [Associações do Hub de Eventos do Azure Functions](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="ebb85-187">Olá tipos `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` e `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` são definidos no pacote do NuGet Olá [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="ebb85-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="ebb85-188">Olá, exemplo a seguir usa um gatilho de Hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="ebb85-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="ebb85-189">Olá, exemplo a seguir tem um Hub de eventos de saída, usando o valor de retorno do método hello como saída de hello:</span><span class="sxs-lookup"><span data-stu-id="ebb85-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

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

### <a name="external-file-input-and-output"></a><span data-ttu-id="ebb85-190">Entrada e saída do arquivo externo</span><span class="sxs-lookup"><span data-stu-id="ebb85-190">External file input and output</span></span>

<span data-ttu-id="ebb85-191">O Azure Functions dá suporte a associações de gatilho, entrada e saída para arquivos externos, tais como Google Drive, Dropbox e OneDrive.</span><span class="sxs-lookup"><span data-stu-id="ebb85-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="ebb85-192">mais, consulte toolearn [associações de arquivo externo de funções do Azure](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="ebb85-193">Olá atributos `[ExternalFileTrigger]` e `[ExternalFile]` são definidos no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="ebb85-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="ebb85-194">Olá c# de exemplo a seguir demonstra um arquivo externo de entrada e saída de associação.</span><span class="sxs-lookup"><span data-stu-id="ebb85-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="ebb85-195">cópias de código Olá Olá arquivo de saída do arquivo de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="ebb85-195">hello code copies hello input file toohello output file.</span></span>

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

### <a name="http-and-webhooks"></a><span data-ttu-id="ebb85-196">HTTP e webhooks</span><span class="sxs-lookup"><span data-stu-id="ebb85-196">HTTP and webhooks</span></span>

<span data-ttu-id="ebb85-197">Saudação de uso `HttpTrigger` gatilho do atributo toodefine um HTTP ou webhook.</span><span class="sxs-lookup"><span data-stu-id="ebb85-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="ebb85-198">Esse atributo é definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="ebb85-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="ebb85-199">Você pode personalizar o nível de autorização hello, tipo de webhook, rota e métodos.</span><span class="sxs-lookup"><span data-stu-id="ebb85-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="ebb85-200">Olá, exemplo a seguir define um gatilho HTTP com a autenticação anônima e _genericJson_ webhook tipo.</span><span class="sxs-lookup"><span data-stu-id="ebb85-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="ebb85-201">Entrada e saída dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="ebb85-201">Mobile Apps input and output</span></span>

<span data-ttu-id="ebb85-202">O Azure Functions dá suporte a associações de entrada e saída para os Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="ebb85-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="ebb85-203">mais, consulte toolearn [associações de aplicativos do Azure funções móveis](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="ebb85-204">atributo Olá `[MobileTable]` está definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="ebb85-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="ebb85-205">Olá, exemplo a seguir demonstra um aplicativos móveis associação de saída:</span><span class="sxs-lookup"><span data-stu-id="ebb85-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="ebb85-206">Saída dos Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="ebb85-206">Notification Hubs output</span></span>

<span data-ttu-id="ebb85-207">O Azure Functions oferece suporte a uma associação de saída para Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="ebb85-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="ebb85-208">mais, consulte toolearn [associação de saída do Hub de notificação do Azure funções](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="ebb85-209">atributo Olá `[NotificationHub]` está definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="ebb85-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="ebb85-210">Gatilho de armazenamento de filas e saída</span><span class="sxs-lookup"><span data-stu-id="ebb85-210">Queue storage trigger and output</span></span>

<span data-ttu-id="ebb85-211">O Azure Functions dá suporte a associações de gatilho e de saída para filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb85-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="ebb85-212">Para obter mais informações, consulte [Associações do Armazenamento de Filas do Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="ebb85-213">Olá exemplo a seguir mostra como função de hello toouse tipo de retorno com uma saída de fila de associação, usando Olá `[Queue]` atributo.</span><span class="sxs-lookup"><span data-stu-id="ebb85-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="ebb85-214">toodefine um gatilho de fila, use Olá `[QueueTrigger]` atributo.</span><span class="sxs-lookup"><span data-stu-id="ebb85-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

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

### <a name="sendgrid-output"></a><span data-ttu-id="ebb85-215">Saída do SendGrid</span><span class="sxs-lookup"><span data-stu-id="ebb85-215">SendGrid output</span></span>

<span data-ttu-id="ebb85-216">O Azure Functions oferece suporte a uma associação de saída do SendGrid para enviar email programaticamente.</span><span class="sxs-lookup"><span data-stu-id="ebb85-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="ebb85-217">mais, consulte toolearn [SendGrid de funções do Azure associações](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="ebb85-218">atributo Olá `[SendGrid]` está definido no pacote do NuGet Olá [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="ebb85-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="ebb85-219">Olá, a seguir é um exemplo de usando um gatilho de fila do barramento de serviço e uma associação de saída SendGrid usando `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="ebb85-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

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

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="ebb85-220">Gatilho e saída do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ebb85-220">Service Bus trigger and output</span></span>

<span data-ttu-id="ebb85-221">O Azure Functions dá suporte a gatilhos e a associações de saída para filas e tópicos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="ebb85-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="ebb85-222">Para obter mais informações sobre como configurar associações, consulte [Associações do Barramento de Serviço do Azure Functions](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="ebb85-223">Olá atributos `[ServiceBusTrigger]` e `[ServiceBus]` são definidos no pacote do NuGet Olá [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="ebb85-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="ebb85-224">Olá seguinte é um exemplo de um gatilho de fila do barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="ebb85-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="ebb85-225">a seguir Olá é um exemplo de uma saída de barramento de serviço de associação, usando o tipo de retorno do método hello como saída de hello:</span><span class="sxs-lookup"><span data-stu-id="ebb85-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

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

### <a name="table-storage-input-and-output"></a><span data-ttu-id="ebb85-226">Entrada e saída de armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="ebb85-226">Table storage input and output</span></span>

<span data-ttu-id="ebb85-227">O Azure Functions dá suporte a associações de entrada e saída para armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb85-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="ebb85-228">mais, consulte toolearn [associações de armazenamento de tabela de funções do Azure](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="ebb85-229">Olá, exemplo a seguir é uma classe com duas funções, demonstrando associações de entrada e saída de armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="ebb85-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

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

### <a name="timer-trigger"></a><span data-ttu-id="ebb85-230">Gatilho de temporizador</span><span class="sxs-lookup"><span data-stu-id="ebb85-230">Timer trigger</span></span>

<span data-ttu-id="ebb85-231">O Azure Functions tem uma associação de gatilho de timer que permite executar o código de função com base em um agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="ebb85-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="ebb85-232">toolearn mais sobre os recursos de saudação da associação hello, consulte [agendar a execução de código com funções do Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="ebb85-233">Plano de consumo hello, você pode definir agendas com um [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="ebb85-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="ebb85-234">Se você estiver usando um Plano do Serviço de Aplicativo, você também pode usar uma cadeia de caracteres do período de tempo.</span><span class="sxs-lookup"><span data-stu-id="ebb85-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="ebb85-235">saudação de exemplo a seguir define um gatilho de timer que é executado a cada 5 minutos:</span><span class="sxs-lookup"><span data-stu-id="ebb85-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="ebb85-236">Saída do Twilio</span><span class="sxs-lookup"><span data-stu-id="ebb85-236">Twilio output</span></span>

<span data-ttu-id="ebb85-237">Suporte de funções do Azure Twilio saída associações tooenable suas mensagens de texto SMS funções toosend.</span><span class="sxs-lookup"><span data-stu-id="ebb85-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="ebb85-238">mais, consulte toolearn [associação de saída de mensagens de enviar SMS das funções do Azure usando Olá Twilio](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="ebb85-239">atributo Olá `[TwilioSms]` está definido no pacote de saudação [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="ebb85-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="ebb85-240">Olá, c# de exemplo seguinte usa uma fila gatilho e uma Twilio associação de saída:</span><span class="sxs-lookup"><span data-stu-id="ebb85-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ebb85-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebb85-241">Next steps</span></span>

<span data-ttu-id="ebb85-242">Para obter mais informações sobre como usar funções do Azure no script de C#, consulte a [referência para o desenvolvedor de script \#C no Azure Functions](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="ebb85-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

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
