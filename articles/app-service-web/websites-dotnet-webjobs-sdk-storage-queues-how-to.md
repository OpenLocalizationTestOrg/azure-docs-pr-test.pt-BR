---
title: aaaHow toouse armazenamento de fila do Azure com hello SDK do WebJobs
description: Saiba como o armazenamento com hello SDK do WebJobs de fila toouse do Azure. Criar e excluir filas; Inserir, inspecionar, obter e excluir a fila de mensagens e muito mais.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="f9a23-104">Como o armazenamento com hello SDK do WebJobs de fila toouse do Azure</span><span class="sxs-lookup"><span data-stu-id="f9a23-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="f9a23-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f9a23-105">Overview</span></span>
<span data-ttu-id="f9a23-106">Este guia fornece c# exemplos de código que mostram como toouse Olá versão do SDK do Azure WebJobs 1. x com hello serviço de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a23-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="f9a23-107">Guia de saudação pressupõe que você sabe [como toocreate um projeto do WebJob no Visual Studio com conexão cadeias de caracteres essa conta de armazenamento de ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou muito[várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="f9a23-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="f9a23-108">Maioria dos trechos de código Olá mostra apenas as funções, hello não código que cria Olá `JobHost` objeto como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="f9a23-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="f9a23-109">Guia de saudação inclui Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="f9a23-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="f9a23-110">Como tootrigger uma função quando é recebida uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="f9a23-111">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="f9a23-111">String queue messages</span></span>
  * <span data-ttu-id="f9a23-112">Mensagem de fila POCO</span><span class="sxs-lookup"><span data-stu-id="f9a23-112">POCO queue messages</span></span>
  * <span data-ttu-id="f9a23-113">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="f9a23-113">Async functions</span></span>
  * <span data-ttu-id="f9a23-114">Atributo de QueueTrigger Olá tipos funciona com</span><span class="sxs-lookup"><span data-stu-id="f9a23-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="f9a23-115">Algoritmo de sondagem</span><span class="sxs-lookup"><span data-stu-id="f9a23-115">Polling algorithm</span></span>
  * <span data-ttu-id="f9a23-116">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="f9a23-116">Multiple instances</span></span>
  * <span data-ttu-id="f9a23-117">Execução paralela</span><span class="sxs-lookup"><span data-stu-id="f9a23-117">Parallel execution</span></span>
  * <span data-ttu-id="f9a23-118">Obter fila ou metadados de mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="f9a23-119">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="f9a23-119">Graceful shutdown</span></span>
* [<span data-ttu-id="f9a23-120">Como toocreate uma fila de mensagens ao processar uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="f9a23-121">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="f9a23-121">String queue messages</span></span>
  * <span data-ttu-id="f9a23-122">Mensagem de fila POCO</span><span class="sxs-lookup"><span data-stu-id="f9a23-122">POCO queue messages</span></span>
  * <span data-ttu-id="f9a23-123">Criar várias mensagens ou em funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="f9a23-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="f9a23-124">Atributo de fila Olá tipos funciona com</span><span class="sxs-lookup"><span data-stu-id="f9a23-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="f9a23-125">Usar atributos de SDK do WebJobs no corpo de saudação de uma função</span><span class="sxs-lookup"><span data-stu-id="f9a23-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="f9a23-126">Como blobs de tooread e gravação ao processar uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="f9a23-127">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="f9a23-127">String queue messages</span></span>
  * <span data-ttu-id="f9a23-128">Mensagem de fila POCO</span><span class="sxs-lookup"><span data-stu-id="f9a23-128">POCO queue messages</span></span>
  * <span data-ttu-id="f9a23-129">Atributo de Blob Olá tipos funciona com</span><span class="sxs-lookup"><span data-stu-id="f9a23-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="f9a23-130">Como o toohandle mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="f9a23-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="f9a23-131">Manipulação automática de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="f9a23-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="f9a23-132">Manipulação manual de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="f9a23-132">Manual poison message handling</span></span>
* [<span data-ttu-id="f9a23-133">Como as opções de configuração de tooset</span><span class="sxs-lookup"><span data-stu-id="f9a23-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="f9a23-134">Defina as cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="f9a23-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="f9a23-135">Definir configurações de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="f9a23-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="f9a23-136">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="f9a23-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="f9a23-137">Como uma função de tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="f9a23-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="f9a23-138">Como os logs de toowrite</span><span class="sxs-lookup"><span data-stu-id="f9a23-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="f9a23-139">Como toohandle erros e definir tempos limite</span><span class="sxs-lookup"><span data-stu-id="f9a23-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="f9a23-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9a23-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="f9a23-141"><a id="trigger"></a>Como tootrigger uma função quando é recebida uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="f9a23-142">toowrite uma função que Olá SDK do WebJobs chama quando é recebida uma mensagem da fila, use Olá `QueueTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="f9a23-143">o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome de saudação do hello toopoll de fila.</span><span class="sxs-lookup"><span data-stu-id="f9a23-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="f9a23-144">Você também pode [definir dinamicamente o nome da fila Olá](#config).</span><span class="sxs-lookup"><span data-stu-id="f9a23-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="f9a23-145">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="f9a23-145">String queue messages</span></span>
<span data-ttu-id="f9a23-146">Olá exemplo a seguir, fila Olá contém uma mensagem de cadeia de caracteres, portanto `QueueTrigger` parâmetro de cadeia de caracteres tooa aplicada denominado `logMessage` que contém o conteúdo de saudação de mensagem da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="f9a23-147">Olá função [grava uma mensagem de log toohello painel](#logs).</span><span class="sxs-lookup"><span data-stu-id="f9a23-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="f9a23-148">Além disso `string`, parâmetro hello pode ser uma matriz de bytes, um `CloudQueueMessage` objeto ou um POCO que você definir.</span><span class="sxs-lookup"><span data-stu-id="f9a23-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="f9a23-149">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="f9a23-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f9a23-150">Olá exemplo a seguir, mensagem de saudação do fila contém JSON para um `BlobInformation` objeto que inclui um `BlobName` propriedade.</span><span class="sxs-lookup"><span data-stu-id="f9a23-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="f9a23-151">Olá SDK automaticamente desserializa o objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="f9a23-152">Olá SDK usa Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e desserializar de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f9a23-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="f9a23-153">Se você criar a fila de mensagens em um programa que não usa o SDK do WebJobs do hello, você pode escrever código como Olá seguindo o exemplo toocreate uma mensagem da fila POCO que Olá que SDK pode ser analisado.</span><span class="sxs-lookup"><span data-stu-id="f9a23-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="f9a23-154">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="f9a23-154">Async functions</span></span>
<span data-ttu-id="f9a23-155">Olá seguinte função assíncrona [grava um log toohello painel](#logs).</span><span class="sxs-lookup"><span data-stu-id="f9a23-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="f9a23-156">Funções assíncronas podem levar uma [token de cancelamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), conforme mostrado no hello exemplo que copia um blob a seguir.</span><span class="sxs-lookup"><span data-stu-id="f9a23-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="f9a23-157">(Para obter uma explicação da saudação `queueTrigger` espaço reservado, consulte Olá [Blobs](#blobs) seção.)</span><span class="sxs-lookup"><span data-stu-id="f9a23-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="f9a23-158"><a id="qtattributetypes"></a>Atributo de QueueTrigger Olá tipos funciona com</span><span class="sxs-lookup"><span data-stu-id="f9a23-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="f9a23-159">Você pode usar `QueueTrigger` com hello tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9a23-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="f9a23-160">Um tipo POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="f9a23-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="f9a23-161"><a id="polling"></a> Algoritmo de sondagem</span><span class="sxs-lookup"><span data-stu-id="f9a23-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="f9a23-162">Olá SDK implementa um efeito de saudação tooreduce aleatória exponencial algoritmo de retirada da fila ociosa em custos de transações de armazenamento de sondagem.</span><span class="sxs-lookup"><span data-stu-id="f9a23-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="f9a23-163">Quando uma mensagem é encontrada, Olá SDK espera 2 segundos e, em seguida, verifica a outra mensagem; Quando nenhuma mensagem for encontrada, ele aguarda cerca de quatro segundos antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="f9a23-164">Depois de tentativas subsequentes tooget uma mensagem da fila, o tempo de espera Olá continua tooincrease até atingir o tempo de espera máximo Olá, quais minuto de tooone padrões.</span><span class="sxs-lookup"><span data-stu-id="f9a23-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="f9a23-165">[Olá tempo de espera máximo é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="f9a23-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="f9a23-166"><a id="instances"></a> Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="f9a23-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="f9a23-167">Se seu aplicativo web é executado em várias instâncias, um trabalho Web contínuo é executado em cada computador, e cada computador aguardará para gatilhos e tentar toorun funções.</span><span class="sxs-lookup"><span data-stu-id="f9a23-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="f9a23-168">Olá gatilho de fila do SDK do WebJobs impede automaticamente uma função de uma mensagem da fila de processamento várias vezes; funções não têm toobe gravado toobe idempotentes.</span><span class="sxs-lookup"><span data-stu-id="f9a23-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="f9a23-169">No entanto, se você quiser tooensure que apenas uma instância de uma função é executada mesmo quando há várias instâncias do aplicativo de web host hello, você pode usar o hello `Singleton` atributo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="f9a23-170"><a id="parallel"></a> Execução paralela</span><span class="sxs-lookup"><span data-stu-id="f9a23-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="f9a23-171">Se você tiver várias funções diferentes filas escutando, Olá SDK ligá-los em paralelo quando as mensagens são recebidas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="f9a23-172">Olá mesmo é verdadeiro quando várias mensagens são recebidas para uma única fila.</span><span class="sxs-lookup"><span data-stu-id="f9a23-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="f9a23-173">Por padrão, hello SDK obtém um lote de mensagens de fila de 16 por vez e executa a função hello processa-los em paralelo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="f9a23-174">[tamanho do lote Olá é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="f9a23-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="f9a23-175">Quando o número Olá processado chega toohalf de tamanho de lote hello, Olá SDK obtém outro lote e começa a processar essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="f9a23-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="f9a23-176">Portanto o número de máximo de saudação simultâneas mensagens processadas por função é tamanho de lote de saudação de uma vez e meia.</span><span class="sxs-lookup"><span data-stu-id="f9a23-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="f9a23-177">Esse limite se aplica separadamente função tooeach que tem um `QueueTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="f9a23-178">Se não quiser que a execução paralela para mensagens recebidas em uma fila, você pode definir Olá too1 de tamanho de lote.</span><span class="sxs-lookup"><span data-stu-id="f9a23-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="f9a23-179">Veja também **Mais controle sobre o processamento de fila** no [RTM 1.1.0 do SDK dos Trabalhos Web do Azure](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="f9a23-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="f9a23-180"><a id="queuemetadata"></a>Obter fila ou metadados de mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="f9a23-181">Você pode obter Olá propriedades de mensagem a seguir, adicionando a assinatura do método toohello parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f9a23-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="f9a23-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="f9a23-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="f9a23-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="f9a23-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="f9a23-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="f9a23-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="f9a23-185">`string` queueTrigger (contém o texto da mensagem)</span><span class="sxs-lookup"><span data-stu-id="f9a23-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="f9a23-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="f9a23-186">`string` id</span></span>
* <span data-ttu-id="f9a23-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="f9a23-187">`string` popReceipt</span></span>
* <span data-ttu-id="f9a23-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="f9a23-188">`int` dequeueCount</span></span>

<span data-ttu-id="f9a23-189">Se você desejar toowork diretamente com hello API de armazenamento do Azure, você também pode adicionar um `CloudStorageAccount` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f9a23-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="f9a23-190">Olá exemplo a seguir grava todos os este metadados tooan informações do log de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="f9a23-191">No exemplo hello, logMessage e queueTrigger contêm conteúdo Olá de mensagem da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="f9a23-192">Aqui está um exemplo de log gravado pelo código de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="f9a23-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="f9a23-193"><a id="graceful"></a>Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="f9a23-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="f9a23-194">Uma função que é executado em um trabalho Web contínuo pode aceitar um `CancellationToken` parâmetro que permite Olá toonotify Olá função do sistema operacional quando hello WebJob é sobre toobe encerrada.</span><span class="sxs-lookup"><span data-stu-id="f9a23-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="f9a23-195">Você pode usar este toomake notificação se a função hello não finalização inesperada de forma que deixa os dados em um estado inconsistente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="f9a23-196">Olá mostrado no exemplo a seguir como toocheck iminente encerramento do trabalho Web em uma função.</span><span class="sxs-lookup"><span data-stu-id="f9a23-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="f9a23-197">**Observação:** Olá painel não pode mostrar corretamente o status de saudação e a saída de funções que ter sido desligado.</span><span class="sxs-lookup"><span data-stu-id="f9a23-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="f9a23-198">Para obter mais informações, consulte [Desligamento normal dos trabalhos Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="f9a23-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="f9a23-199"><a id="createqueue"></a>Como toocreate uma fila de mensagens ao processar uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="f9a23-200">toowrite uma função que cria uma nova mensagem da fila, use Olá `Queue` atributo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="f9a23-201">Como `QueueTrigger`, passar no nome da fila hello como uma cadeia de caracteres, ou você pode [definir dinamicamente o nome da fila Olá](#config).</span><span class="sxs-lookup"><span data-stu-id="f9a23-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="f9a23-202">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="f9a23-202">String queue messages</span></span>
<span data-ttu-id="f9a23-203">Olá async não exemplo de código a seguir cria uma nova mensagem de fila na fila de saudação denominada "outputqueue" com hello mesmo conteúdo como mensagem de saudação do fila recebidos na fila de saudação denominada "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="f9a23-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="f9a23-204">(Para funções assíncronas, use `IAsyncCollector<T>` , conforme mostrado posteriormente nesta seção.)</span><span class="sxs-lookup"><span data-stu-id="f9a23-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="f9a23-205">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="f9a23-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f9a23-206">tipo de uma mensagem da fila que contém um POCO em vez de uma cadeia de caracteres, passagem Olá POCO toocreate como um toohello de parâmetro de saída `Queue` construtor de atributo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="f9a23-207">Olá SDK automaticamente serializa Olá tooJSON de objeto.</span><span class="sxs-lookup"><span data-stu-id="f9a23-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="f9a23-208">Uma mensagem da fila é sempre criada, mesmo se o objeto de saudação é nulo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="f9a23-209">Criar várias mensagens ou em funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="f9a23-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="f9a23-210">toocreate várias mensagens, verifique o tipo de parâmetro de saudação para fila de saída de hello `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="f9a23-211">Cada mensagem de fila é criada imediatamente quando hello `Add` método é chamado.</span><span class="sxs-lookup"><span data-stu-id="f9a23-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="f9a23-212">Tipos de atributo fila Olá funciona com</span><span class="sxs-lookup"><span data-stu-id="f9a23-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="f9a23-213">Você pode usar o hello `Queue` atributo Olá tipos de parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9a23-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="f9a23-214">`out string`(cria a mensagem da fila se o valor do parâmetro é não nulo quando a função hello termina)</span><span class="sxs-lookup"><span data-stu-id="f9a23-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="f9a23-215">`out byte[]` (funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="f9a23-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="f9a23-216">`out CloudQueueMessage` (funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="f9a23-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="f9a23-217">`out POCO`(um tipo serializável, cria uma mensagem com um objeto nulo se o parâmetro hello é nulo quando termina de função hello)</span><span class="sxs-lookup"><span data-stu-id="f9a23-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="f9a23-218">`CloudQueue`(para criar manualmente usando Olá API de armazenamento do Azure diretamente de mensagens)</span><span class="sxs-lookup"><span data-stu-id="f9a23-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="f9a23-219"><a id="ibinder"></a>Usar atributos de SDK do WebJobs no corpo de saudação de uma função</span><span class="sxs-lookup"><span data-stu-id="f9a23-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="f9a23-220">Se você precisar toodo alguns funcionar na sua função antes de usar um atributo do SDK do WebJobs como `Queue`, `Blob`, ou `Table`, você pode usar o hello `IBinder` interface.</span><span class="sxs-lookup"><span data-stu-id="f9a23-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="f9a23-221">saudação de exemplo a seguir usa uma mensagem da fila de entrada e cria uma nova mensagem com hello mesmo conteúdo em uma fila de saída.</span><span class="sxs-lookup"><span data-stu-id="f9a23-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="f9a23-222">nome de fila de saída de saudação é definido pelo código no corpo de saudação do função hello.</span><span class="sxs-lookup"><span data-stu-id="f9a23-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="f9a23-223">Olá `IBinder` interface também pode ser usada com hello `Table` e `Blob` atributos.</span><span class="sxs-lookup"><span data-stu-id="f9a23-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="f9a23-224"><a id="blobs"></a>Como tooread e gravar os blobs e tabelas durante o processamento de uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="f9a23-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="f9a23-225">Olá `Blob` e `Table` atributos permitem que você tooread e gravar os blobs e tabelas.</span><span class="sxs-lookup"><span data-stu-id="f9a23-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="f9a23-226">exemplos de saudação nesta seção se aplicam a tooblobs.</span><span class="sxs-lookup"><span data-stu-id="f9a23-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="f9a23-227">Para obter exemplos de código que mostram como tootrigger processa quando blobs são criados ou atualizados, consulte [como toouse Azure blob storage com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e para obter exemplos de código que leem e gravam tabelas, consulte [como toouse tabela do Azure armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="f9a23-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="f9a23-228">Mensagens da fila de cadeia de caracteres que disparam operações de blob</span><span class="sxs-lookup"><span data-stu-id="f9a23-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="f9a23-229">Para uma mensagem da fila que contém uma cadeia de caracteres, `queueTrigger` é um espaço reservado que você pode usar em Olá `Blob` do atributo `blobPath` parâmetro hello com conteúdo de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="f9a23-230">Olá exemplo a seguir usa `Stream` objetos blobs tooread e gravação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="f9a23-231">mensagem de saudação do fila é o nome de saudação de um blob localizado no contêiner de textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="f9a23-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="f9a23-232">Uma cópia de blob Olá com "-novo" acrescentada toohello nome é criado no hello mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="f9a23-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="f9a23-233">Olá `Blob` atributo construtor usa um `blobPath` parâmetro que especifica o contêiner de saudação e nome do blob.</span><span class="sxs-lookup"><span data-stu-id="f9a23-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="f9a23-234">Para obter mais informações sobre esse espaço reservado, consulte [como toouse Azure blob storage com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="f9a23-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="f9a23-235">Quando o atributo Olá decora uma `Stream` do objeto, outro parâmetro de construtor Especifica Olá `FileAccess` modo como leitura, gravação ou leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="f9a23-236">Olá exemplo a seguir usa uma `CloudBlockBlob` toodelete um blob do objeto.</span><span class="sxs-lookup"><span data-stu-id="f9a23-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="f9a23-237">mensagem da fila de saudação é o nome de saudação do blob hello.</span><span class="sxs-lookup"><span data-stu-id="f9a23-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="f9a23-238"><a id="pocoblobs"></a> Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="f9a23-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f9a23-239">Para um POCO armazenada como JSON na mensagem de saudação do fila, você pode usar espaços reservados que propriedades de objeto Olá Olá nomes `Queue` do atributo `blobPath` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f9a23-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="f9a23-240">Também é possível utilizar os [nomes de propriedade de metadados de fila](#queuemetadata) como espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="f9a23-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="f9a23-241">Olá, exemplo a seguir copia um blob tooa novo blob com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="f9a23-242">mensagem de saudação do fila é um `BlobInformation` objeto inclui `BlobName` e `BlobNameWithoutExtension` propriedades.</span><span class="sxs-lookup"><span data-stu-id="f9a23-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="f9a23-243">nomes de propriedade Olá são usados como espaços reservados no caminho de blob Olá Olá `Blob` atributos.</span><span class="sxs-lookup"><span data-stu-id="f9a23-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="f9a23-244">Olá SDK usa Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e desserializar de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f9a23-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="f9a23-245">Se você criar a fila de mensagens em um programa que não usa o SDK do WebJobs do hello, você pode escrever código como Olá seguindo o exemplo toocreate uma mensagem da fila POCO que Olá que SDK pode ser analisado.</span><span class="sxs-lookup"><span data-stu-id="f9a23-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="f9a23-246">Se você precisar toodo alguns funcionar na sua função antes de associar um objeto de tooan de blob, você pode usar o atributo de saudação no corpo de saudação do função hello, [conforme mostrado anteriormente para o atributo de fila Olá](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="f9a23-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="f9a23-247"><a id="blobattributetypes"></a>Tipos que você pode usar o hello Blob de atributo com</span><span class="sxs-lookup"><span data-stu-id="f9a23-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="f9a23-248">Olá `Blob` atributo pode ser usado com hello tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9a23-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="f9a23-249">`Stream`(leitura ou gravação, especificadas usando o parâmetro de construtor FileAccess Olá)</span><span class="sxs-lookup"><span data-stu-id="f9a23-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="f9a23-250">`string` (leitura)</span><span class="sxs-lookup"><span data-stu-id="f9a23-250">`string` (read)</span></span>
* <span data-ttu-id="f9a23-251">`out string`(gravação; cria um blob somente se o parâmetro de cadeia de caracteres de saudação for não nulo quando a função hello retorna)</span><span class="sxs-lookup"><span data-stu-id="f9a23-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="f9a23-252">POCO (leitura)</span><span class="sxs-lookup"><span data-stu-id="f9a23-252">POCO (read)</span></span>
* <span data-ttu-id="f9a23-253">limite POCO (gravação; sempre cria um blob, cria como objeto nulo se o parâmetro POCO é nulo quando a função hello retorna)</span><span class="sxs-lookup"><span data-stu-id="f9a23-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="f9a23-254">`CloudBlobStream` (gravação)</span><span class="sxs-lookup"><span data-stu-id="f9a23-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="f9a23-255">`ICloudBlob` (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="f9a23-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="f9a23-256">`CloudBlockBlob` (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="f9a23-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="f9a23-257">`CloudPageBlob` (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="f9a23-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="f9a23-258"><a id="poison"></a>Como o toohandle mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="f9a23-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="f9a23-259">São chamadas de mensagens cujo conteúdo faz com que uma função toofail *mensagens suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="f9a23-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="f9a23-260">Quando a função hello falha, mensagem de saudação do fila não é excluída e eventualmente é obtida novamente, causando toobe de ciclo de saudação repetido.</span><span class="sxs-lookup"><span data-stu-id="f9a23-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="f9a23-261">Olá SDK automaticamente pode interromper o ciclo de saudação após um número limitado de iterações ou você pode fazer isso manualmente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="f9a23-262">Manipulação automática de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="f9a23-262">Automatic poison message handling</span></span>
<span data-ttu-id="f9a23-263">Olá SDK chamará uma função de backup too5 vezes tooprocess uma mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="f9a23-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="f9a23-264">Se tentar quinto Olá falhar, mensagem de saudação é fila inviabilização movida tooa.</span><span class="sxs-lookup"><span data-stu-id="f9a23-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="f9a23-265">[Olá o número máximo de repetições é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="f9a23-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="f9a23-266">fila suspeitas Olá é denominada *{originalqueuename}*-suspeitas.</span><span class="sxs-lookup"><span data-stu-id="f9a23-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="f9a23-267">Você pode escrever uma função tooprocess mensagens da fila de suspeitas Olá registrá-los ou enviar uma notificação que atenção manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="f9a23-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="f9a23-268">Em Olá Olá de exemplo a seguir `CopyBlob` função falhará quando uma mensagem da fila contém nome de saudação de um blob que não existe.</span><span class="sxs-lookup"><span data-stu-id="f9a23-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="f9a23-269">Quando isso acontece, a mensagem de saudação é movida da fila de suspeitas copyblobqueue Olá copyblobqueue fila toohello.</span><span class="sxs-lookup"><span data-stu-id="f9a23-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="f9a23-270">Olá `ProcessPoisonMessage` e logs Olá mensagens suspeitas.</span><span class="sxs-lookup"><span data-stu-id="f9a23-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="f9a23-271">Olá ilustração a seguir mostra a saída de console dessas funções quando uma mensagem suspeita é processada.</span><span class="sxs-lookup"><span data-stu-id="f9a23-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Saída do console para tratamento de mensagens suspeitas](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="f9a23-273">Manipulação manual de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="f9a23-273">Manual poison message handling</span></span>
<span data-ttu-id="f9a23-274">Você pode obter o número de saudação de vezes que uma mensagem tem foram coletada para processamento, adicionando um `int` parâmetro denominado `dequeueCount` tooyour função.</span><span class="sxs-lookup"><span data-stu-id="f9a23-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="f9a23-275">Você pode então seleção Olá contagem no código da função de remoção da fila e executar seu próprio tratamento de mensagens suspeitas quando o número de saudação excede um limite, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <span data-ttu-id="f9a23-276"><a id="config"></a>Como as opções de configuração de tooset</span><span class="sxs-lookup"><span data-stu-id="f9a23-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="f9a23-277">Você pode usar o hello `JobHostConfiguration` saudação do tipo tooset as opções de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9a23-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="f9a23-278">Defina cadeias de caracteres de conexão do hello SDK no código.</span><span class="sxs-lookup"><span data-stu-id="f9a23-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="f9a23-279">Defina as configurações `QueueTrigger` de como a contagem máxima de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="f9a23-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="f9a23-280">Obtenha nomes de fila por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="f9a23-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="f9a23-281"><a id="setconnstr"></a>Definir as cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="f9a23-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="f9a23-282">Definindo cadeias de caracteres de conexão do hello SDK no código permite que você toouse seus próprios nomes de cadeia de caracteres de conexão em arquivos de configuração ou variáveis de ambiente, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="f9a23-283"><a id="configqueue"></a>Configurar definições de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="f9a23-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="f9a23-284">Você pode configurar Olá configurações que se aplicam a toohello processamento de mensagens de fila a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9a23-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="f9a23-285">Olá número máximo de fila de mensagens que são aplicadas simultaneamente toobe executado em paralelo (o padrão é 16).</span><span class="sxs-lookup"><span data-stu-id="f9a23-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="f9a23-286">Olá número máximo de tentativas antes de uma mensagem da fila é enviada a fila de suspeitas tooa (o padrão é 5).</span><span class="sxs-lookup"><span data-stu-id="f9a23-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="f9a23-287">tempo de espera máximo Olá antes de sondar novamente quando uma fila está vazia (o padrão é 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="f9a23-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="f9a23-288">Olá mostrado no exemplo a seguir como tooconfigure essas configurações:</span><span class="sxs-lookup"><span data-stu-id="f9a23-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="f9a23-289"><a id="setnamesincode"></a>Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="f9a23-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="f9a23-290">Às vezes, você deseja toospecify um nome de fila, um nome de blob ou contêiner ou nome de uma tabela no código em vez de embuti-lo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="f9a23-291">Por exemplo, convém toospecify Olá nome `QueueTrigger` em uma variável de ambiente ou arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="f9a23-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="f9a23-292">Você pode fazer isso, passando um `NameResolver` toohello do objeto `JobHostConfiguration` tipo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="f9a23-293">Incluir espaços reservados especiais entre sinais de porcentagem (%)) nos parâmetros de construtor de atributo do SDK do WebJobs e sua `NameResolver` código especifica Olá toobe de valores reais usado no lugar desses espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="f9a23-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="f9a23-294">Por exemplo, suponha que você queira toouse uma fila denominada logqueuetest no ambiente de teste hello e um logqueueprod nomeado na produção.</span><span class="sxs-lookup"><span data-stu-id="f9a23-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="f9a23-295">Em vez de um nome de fila embutidos, você deseja que o nome de saudação toospecify da entrada hello `appSettings` coleção que tem nome de fila real hello.</span><span class="sxs-lookup"><span data-stu-id="f9a23-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="f9a23-296">Se hello `appSettings` chave é logqueue, sua função pode parecer com o exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="f9a23-297">O `NameResolver` classe, em seguida, foi possível obter o nome da fila de saudação do `appSettings` conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f9a23-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="f9a23-298">Você passa Olá `NameResolver` classe toohello `JobHost` conforme mostrado no exemplo a seguir de saudação do objeto.</span><span class="sxs-lookup"><span data-stu-id="f9a23-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="f9a23-299">**Observação:** nomes de blob, tabela e fila são resolvidos sempre que uma função é chamada, mas os nomes de contêiner de blob são resolvidos somente quando o aplicativo hello inicia.</span><span class="sxs-lookup"><span data-stu-id="f9a23-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="f9a23-300">Você não pode alterar o nome do contêiner de blob enquanto Olá trabalho está em execução.</span><span class="sxs-lookup"><span data-stu-id="f9a23-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="f9a23-301"><a id="manual"></a>Como uma função de tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="f9a23-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="f9a23-302">tootrigger uma função manualmente, use Olá `Call` ou `CallAsync` método hello `JobHost` objeto e hello `NoAutomaticTrigger` atributo na função hello, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <span data-ttu-id="f9a23-303"><a id="logs"></a>Como os logs de toowrite</span><span class="sxs-lookup"><span data-stu-id="f9a23-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="f9a23-304">Olá painel mostra logs em dois lugares: página Olá Olá trabalho Web e página Olá para determinada invocação WebJob.</span><span class="sxs-lookup"><span data-stu-id="f9a23-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Logs na página do Trabalho Web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Logs na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="f9a23-307">Saída de métodos de Console que você chama uma função ou de saudação `Main()` método aparece na página painel Olá Olá WebJob, não na página de saudação para uma invocação de método específico.</span><span class="sxs-lookup"><span data-stu-id="f9a23-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="f9a23-308">Saída do objeto de TextWriter Olá que você obteve de um parâmetro na sua assinatura do método aparece na página do painel de saudação de uma invocação de método.</span><span class="sxs-lookup"><span data-stu-id="f9a23-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="f9a23-309">Saída do console não pode ser vinculado tooa da invocação do método particular porque Olá Console é de thread único, enquanto muitas funções de trabalho podem ser executadas ao Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="f9a23-310">É por isso que Olá SDK fornece cada invocação de função com seu próprio objeto do gravador de log exclusivo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="f9a23-311">toowrite [logs de rastreamento de aplicativo](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (cria marcados como informações de logs) e `Console.Error` (cria logs marcados como erro).</span><span class="sxs-lookup"><span data-stu-id="f9a23-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="f9a23-312">Uma alternativa é toouse [rastreamento ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que fornece detalhado, aviso e crítico níveis em adição tooInfo e erro.</span><span class="sxs-lookup"><span data-stu-id="f9a23-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="f9a23-313">Logs de rastreamento do aplicativo aparecem nos arquivos de log de aplicativo da web hello, as tabelas do Azure, ou blobs do Azure dependendo de como você configura seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a23-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="f9a23-314">Assim como de toda a saída de Console, logs de aplicativo 100 mais recentes Olá também aparecem na página painel Olá Olá WebJob, não a página Olá para uma invocação de função.</span><span class="sxs-lookup"><span data-stu-id="f9a23-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="f9a23-315">Saída do console é exibida em Olá painel somente se o programa hello está sendo executado em um trabalho de Web do Azure, não se programa hello está sendo executado localmente ou em algum outro ambiente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="f9a23-316">Desabilite o log de painel para cenários de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="f9a23-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="f9a23-317">Por padrão, Olá SDK grava logs toostorage e essa atividade pode degradar o desempenho quando você estiver processando várias mensagens.</span><span class="sxs-lookup"><span data-stu-id="f9a23-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="f9a23-318">toodisable log, defina Olá toonull de cadeia de caracteres de conexão de painel conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9a23-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="f9a23-319">Olá, exemplo a seguir mostra várias maneiras toowrite logs:</span><span class="sxs-lookup"><span data-stu-id="f9a23-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="f9a23-320">Em Olá painel do SDK do WebJobs, Olá saída de hello `TextWriter` mostra backup quando você entrar toohello página para uma determinada chamada de função e clique em objeto **alternar saída**:</span><span class="sxs-lookup"><span data-stu-id="f9a23-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![Clique no link de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Logs na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="f9a23-323">Em Olá painel do SDK do WebJobs, linhas Olá 100 mais recente do Console de saída mostrar backup quando você vá para a página toohello para Olá WebJob (não para invocação de função hello) e clique em **alternar saída**.</span><span class="sxs-lookup"><span data-stu-id="f9a23-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Clique em Alternar Saída](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="f9a23-325">Em um trabalho Web contínuo, logs de aplicativo exibido no/dados/trabalhos/contínua/*{webjobname}*/job_log.txt no sistema de arquivos de aplicativo de web hello.</span><span class="sxs-lookup"><span data-stu-id="f9a23-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="f9a23-326">Em um aplicativo hello de BLOBs do Azure logs ter esta aparência: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Olá, mundo!, 2014-09-26T21:01:13, erro, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Olá, mundo!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Olá, mundo!,</span><span class="sxs-lookup"><span data-stu-id="f9a23-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="f9a23-327">Em uma saudação de tabela do Azure `Console.Out` e `Console.Error` logs ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="f9a23-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Log de informações na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Log de erros na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="f9a23-330">Se você quiser tooplug no seu próprio agente de log, consulte [Este exemplo](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="f9a23-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="f9a23-331"><a id="errors"></a>Como toohandle erros e definir tempos limite</span><span class="sxs-lookup"><span data-stu-id="f9a23-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="f9a23-332">Olá WebJobs SDK também inclui um [tempo limite](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) atributo que você pode usar toocause toobe uma função cancelada se não for concluída dentro de um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="f9a23-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="f9a23-333">E se você quiser tooraise um alerta quando muitos erros ocorrem dentro de um período de tempo especificado, você pode usar o hello `ErrorTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="f9a23-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="f9a23-334">Este é um [exemplo de ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="f9a23-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="f9a23-335">Você pode desabilitar e habilitar funções toocontrol se eles podem ser acionados, usando uma opção de configuração que pode ser uma configuração de aplicativo ou o nome de variável de ambiente também dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="f9a23-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="f9a23-336">Para exemplo de código, consulte Olá `Disable` atributo em [Olá SDK do WebJobs exemplos repositório](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="f9a23-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="f9a23-337"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9a23-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="f9a23-338">Este guia fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a23-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="f9a23-339">Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos recomendada do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="f9a23-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
