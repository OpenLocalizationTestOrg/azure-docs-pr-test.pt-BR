---
title: Como usar o armazenamento de fila do Azure com o SDK de Trabalhos Web
description: Saiba como usar o armazenamento de fila do Azure com o SDK de Trabalhos Web. Criar e excluir filas; Inserir, inspecionar, obter e excluir a fila de mensagens e muito mais.
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
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="c891f-104">Como usar o armazenamento de fila do Azure com o SDK de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="c891f-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="c891f-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c891f-105">Overview</span></span>
<span data-ttu-id="c891f-106">Este guia fornece exemplos de código em C# que mostram como usar o SDK de Trabalhos Web do Azure versão 1.x com o serviço de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="c891f-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="c891f-107">Esse guia pressupõe que você sabe [como criar um projeto do Trabalho Web no Visual Studio com cadeias de conexão que apontam para sua conta de armazenamento](websites-dotnet-webjobs-sdk-get-started.md) ou para [várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="c891f-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="c891f-108">A maioria dos trechos de código mostra somente funções, não o código que cria o `JobHost` objeto como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="c891f-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="c891f-109">O guia inclui os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="c891f-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="c891f-110">Como acionar uma função quando uma mensagem da fila é recebida</span><span class="sxs-lookup"><span data-stu-id="c891f-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="c891f-111">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="c891f-111">String queue messages</span></span>
  * <span data-ttu-id="c891f-112">Mensagem de fila POCO</span><span class="sxs-lookup"><span data-stu-id="c891f-112">POCO queue messages</span></span>
  * <span data-ttu-id="c891f-113">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="c891f-113">Async functions</span></span>
  * <span data-ttu-id="c891f-114">Tipos com os quais o atributo QueueTrigger funciona</span><span class="sxs-lookup"><span data-stu-id="c891f-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="c891f-115">Algoritmo de sondagem</span><span class="sxs-lookup"><span data-stu-id="c891f-115">Polling algorithm</span></span>
  * <span data-ttu-id="c891f-116">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="c891f-116">Multiple instances</span></span>
  * <span data-ttu-id="c891f-117">Execução paralela</span><span class="sxs-lookup"><span data-stu-id="c891f-117">Parallel execution</span></span>
  * <span data-ttu-id="c891f-118">Obter fila ou metadados de mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="c891f-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="c891f-119">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="c891f-119">Graceful shutdown</span></span>
* [<span data-ttu-id="c891f-120">Como criar uma mensagem da fila durante o processamento de uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="c891f-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="c891f-121">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="c891f-121">String queue messages</span></span>
  * <span data-ttu-id="c891f-122">Mensagem de fila POCO</span><span class="sxs-lookup"><span data-stu-id="c891f-122">POCO queue messages</span></span>
  * <span data-ttu-id="c891f-123">Criar várias mensagens ou em funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="c891f-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="c891f-124">Tipos com os quais o atributo Queue funciona</span><span class="sxs-lookup"><span data-stu-id="c891f-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="c891f-125">Usar atributos do SDK de Trabalhos Web no corpo de uma função</span><span class="sxs-lookup"><span data-stu-id="c891f-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="c891f-126">Como ler e gravar blobs ao processar uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="c891f-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="c891f-127">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="c891f-127">String queue messages</span></span>
  * <span data-ttu-id="c891f-128">Mensagem de fila POCO</span><span class="sxs-lookup"><span data-stu-id="c891f-128">POCO queue messages</span></span>
  * <span data-ttu-id="c891f-129">Tipos com os quais o atributo Blob funciona</span><span class="sxs-lookup"><span data-stu-id="c891f-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="c891f-130">Como tratar mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="c891f-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="c891f-131">Manipulação automática de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="c891f-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="c891f-132">Manipulação manual de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="c891f-132">Manual poison message handling</span></span>
* [<span data-ttu-id="c891f-133">Como definir as opções de configuração</span><span class="sxs-lookup"><span data-stu-id="c891f-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="c891f-134">Definir cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="c891f-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="c891f-135">Definir configurações de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="c891f-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="c891f-136">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="c891f-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="c891f-137">Como acionar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="c891f-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="c891f-138">Como gravar logs</span><span class="sxs-lookup"><span data-stu-id="c891f-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="c891f-139">Como tratar erros e configurar tempos limite</span><span class="sxs-lookup"><span data-stu-id="c891f-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="c891f-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c891f-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="c891f-141"><a id="trigger"></a> Como acionar uma função quando uma mensagem da fila é recebida</span><span class="sxs-lookup"><span data-stu-id="c891f-141"><a id="trigger"></a> How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="c891f-142">Para gravar uma função que o SDK de Trabalhos Web chama quando uma mensagem da fila é recebida, use o atributo `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="c891f-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="c891f-143">O construtor de atributo tem um parâmetro de cadeia que especifica o nome da fila para sondagem.</span><span class="sxs-lookup"><span data-stu-id="c891f-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="c891f-144">Você também pode [definir dinamicamente o nome da fila](#config).</span><span class="sxs-lookup"><span data-stu-id="c891f-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c891f-145">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="c891f-145">String queue messages</span></span>
<span data-ttu-id="c891f-146">No exemplo a seguir, a fila contém uma mensagem de cadeia. Portanto, `QueueTrigger` é aplicado a um parâmetro de cadeia chamado `logMessage`, o qual contém o conteúdo da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="c891f-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="c891f-147">A função [grava uma mensagem de log no painel](#logs).</span><span class="sxs-lookup"><span data-stu-id="c891f-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="c891f-148">Além de `string`, o parâmetro pode ser uma matriz de bytes, um objeto `CloudQueueMessage` ou um POCO que você define.</span><span class="sxs-lookup"><span data-stu-id="c891f-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c891f-149">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c891f-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c891f-150">No exemplo a seguir, a mensagem da fila contém JSON para um objeto `BlobInformation` que inclui uma propriedade `BlobName`.</span><span class="sxs-lookup"><span data-stu-id="c891f-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="c891f-151">O SDK automaticamente desserializa o objeto.</span><span class="sxs-lookup"><span data-stu-id="c891f-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="c891f-152">O SDK usa o [pacote NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) para serializar e desserializar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="c891f-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="c891f-153">Se criar mensagens de fila em um programa que não usa o SDK de Trabalhos Web, você poderá escrever código como o exemplo a seguir para criar uma mensagem de fila POCO que o SDK possa analisar.</span><span class="sxs-lookup"><span data-stu-id="c891f-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="c891f-154">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="c891f-154">Async functions</span></span>
<span data-ttu-id="c891f-155">A seguinte função assíncrona [grava um log no painel](#logs).</span><span class="sxs-lookup"><span data-stu-id="c891f-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="c891f-156">As funções assíncronas podem levar um [token de cancelamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), conforme mostrado no exemplo a seguir, que copia um blob.</span><span class="sxs-lookup"><span data-stu-id="c891f-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="c891f-157">(Para obter uma explicação sobre o espaço reservado `queueTrigger` , consulte a seção [Blobs](#blobs) .)</span><span class="sxs-lookup"><span data-stu-id="c891f-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="c891f-158"><a id="qtattributetypes"></a> Tipos com os quais o atributo QueueTrigger funciona</span><span class="sxs-lookup"><span data-stu-id="c891f-158"><a id="qtattributetypes"></a> Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="c891f-159">Você pode usar `QueueTrigger` com os seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="c891f-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="c891f-160">Um tipo POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="c891f-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="c891f-161"><a id="polling"></a> Algoritmo de sondagem</span><span class="sxs-lookup"><span data-stu-id="c891f-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="c891f-162">O SDK implementa um algoritmo exponencial aleatório de retirada para reduzir o efeito de sondagem de fila ociosa nos custos das transações de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c891f-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="c891f-163">Quando uma mensagem for encontrada, o SDK aguarda dois segundos e, em seguida, verifica outra mensagem; quando nenhuma mensagem for encontrada, ele aguarda cerca de quatro segundos antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="c891f-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="c891f-164">Após subsequentes tentativas falhas para obter uma mensagem da fila, o tempo de espera continua a aumentar até atingir o tempo de espera máximo, cujo padrão é um minuto.</span><span class="sxs-lookup"><span data-stu-id="c891f-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="c891f-165">[O tempo de espera máximo é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="c891f-165">[The maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="c891f-166"><a id="instances"></a> Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="c891f-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="c891f-167">Se seu aplicativo Web for executado em várias instâncias, um Trabalho Web contínuo será executado em todos os computadores, e cada computador aguardará os gatilhos e tentará executar as funções.</span><span class="sxs-lookup"><span data-stu-id="c891f-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="c891f-168">O gatilho de fila do SDK dos Trabalhos Web impede automaticamente que uma função processe uma mensagem da fila várias vezes; as funções não precisam ser escritas para ser idempotentes.</span><span class="sxs-lookup"><span data-stu-id="c891f-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="c891f-169">No entanto, se desejar garantir que apenas uma instância de uma função é executada, mesmo quando houver várias instâncias do aplicativo Web host, é possível usar o atributo `Singleton` .</span><span class="sxs-lookup"><span data-stu-id="c891f-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <span data-ttu-id="c891f-170"><a id="parallel"></a> Execução paralela</span><span class="sxs-lookup"><span data-stu-id="c891f-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="c891f-171">Se você tiver várias funções escutando em filas diferentes, o SDK as chamará em paralelo quando as mensagens forem recebidas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="c891f-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="c891f-172">O mesmo é verdadeiro quando várias mensagens são recebidas para uma única fila.</span><span class="sxs-lookup"><span data-stu-id="c891f-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="c891f-173">Por padrão, o SDK obtém um lote de 16 mensagens de fila por vez e executa a função que as processa em paralelo.</span><span class="sxs-lookup"><span data-stu-id="c891f-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="c891f-174">[O tamanho do lote é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="c891f-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="c891f-175">Quando o número que está sendo processado chega até a metade do tamanho do lote, o SDK obtém outro lote e começa a processar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="c891f-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="c891f-176">Portanto, o número máximo de mensagens simultâneas que estão sendo processadas por função é uma vez e meia o tamanho do lote.</span><span class="sxs-lookup"><span data-stu-id="c891f-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="c891f-177">Esse limite se aplica separadamente a cada função que tem um atributo `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="c891f-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="c891f-178">Se não desejar uma execução paralela para mensagens recebidas em uma fila, é possível definir o tamanho do lote como 1.</span><span class="sxs-lookup"><span data-stu-id="c891f-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="c891f-179">Veja também **Mais controle sobre o processamento de fila** no [RTM 1.1.0 do SDK dos Trabalhos Web do Azure](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="c891f-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="c891f-180"><a id="queuemetadata"></a>Obter fila ou metadados de mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="c891f-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="c891f-181">Você pode obter as propriedades da mensagem a seguir adicionando parâmetros à assinatura do método:</span><span class="sxs-lookup"><span data-stu-id="c891f-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="c891f-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="c891f-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="c891f-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="c891f-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="c891f-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="c891f-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="c891f-185">`string` queueTrigger (contém o texto da mensagem)</span><span class="sxs-lookup"><span data-stu-id="c891f-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="c891f-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="c891f-186">`string` id</span></span>
* <span data-ttu-id="c891f-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="c891f-187">`string` popReceipt</span></span>
* <span data-ttu-id="c891f-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="c891f-188">`int` dequeueCount</span></span>

<span data-ttu-id="c891f-189">Se desejar trabalhar diretamente com a API de armazenamento do Azure, também é possível adicionar um parâmetro `CloudStorageAccount` .</span><span class="sxs-lookup"><span data-stu-id="c891f-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="c891f-190">O exemplo a seguir grava todos os metadados em um log de aplicativo de informações.</span><span class="sxs-lookup"><span data-stu-id="c891f-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="c891f-191">No exemplo, tanto logMessage quanto queueTrigger contém o conteúdo da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="c891f-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="c891f-192">Este é um log de exemplo gravado pelo código de exemplo:</span><span class="sxs-lookup"><span data-stu-id="c891f-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="c891f-193"><a id="graceful"></a>Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="c891f-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="c891f-194">Uma função que é executada em um trabalho Web contínuo pode aceitar um parâmetro `CancellationToken` , que permite ao sistema operacional notificar a função quando o trabalho Web está prestes a ser encerrado.</span><span class="sxs-lookup"><span data-stu-id="c891f-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="c891f-195">Você pode usar essa notificação para certificar-se de que a função não finalize inesperadamente de uma maneira que os dados fiquem em um estado inconsistente.</span><span class="sxs-lookup"><span data-stu-id="c891f-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="c891f-196">O exemplo a seguir mostra como verificar se há eminência de encerramento do trabalho Web em uma função.</span><span class="sxs-lookup"><span data-stu-id="c891f-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="c891f-197">**Observação:** o painel pode não mostrar corretamente o status e a saída das funções que foram desligadas.</span><span class="sxs-lookup"><span data-stu-id="c891f-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="c891f-198">Para obter mais informações, consulte [Desligamento normal dos trabalhos Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="c891f-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="c891f-199"><a id="createqueue"></a> Como criar uma mensagem da fila durante o processamento de uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="c891f-199"><a id="createqueue"></a> How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="c891f-200">Para gravar uma função que cria uma nova mensagem da fila, use o atributo `Queue` .</span><span class="sxs-lookup"><span data-stu-id="c891f-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="c891f-201">Como o `QueueTrigger`, você passa o nome da fila como uma cadeia de caracteres ou pode [definir o nome da fila dinamicamente](#config).</span><span class="sxs-lookup"><span data-stu-id="c891f-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c891f-202">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="c891f-202">String queue messages</span></span>
<span data-ttu-id="c891f-203">O exemplo de código não síncrono a seguir cria uma nova mensagem de fila na fila denominada "outputqueue" com o mesmo conteúdo que a mensagem da fila recebida na fila denominada "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="c891f-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="c891f-204">(Para funções assíncronas, use `IAsyncCollector<T>` , conforme mostrado posteriormente nesta seção.)</span><span class="sxs-lookup"><span data-stu-id="c891f-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c891f-205">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c891f-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c891f-206">Para criar uma mensagem da fila que contenha um POCO em vez de uma cadeia de caracteres, passe o tipo POCO como um parâmetro de saída para o construtor de atributo `Queue` .</span><span class="sxs-lookup"><span data-stu-id="c891f-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="c891f-207">O SDK serializa automaticamente o objeto em JSON.</span><span class="sxs-lookup"><span data-stu-id="c891f-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="c891f-208">Uma mensagem da fila sempre é criada, mesmo que o objeto seja nulo.</span><span class="sxs-lookup"><span data-stu-id="c891f-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="c891f-209">Criar várias mensagens ou em funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="c891f-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="c891f-210">Para criar várias mensagens, crie o tipo de parâmetro para a fila de saída `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c891f-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="c891f-211">Cada mensagem da fila é criada imediatamente quando o método `Add` é chamado.</span><span class="sxs-lookup"><span data-stu-id="c891f-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="c891f-212">Tipos com os quais o atributo Queue funciona</span><span class="sxs-lookup"><span data-stu-id="c891f-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="c891f-213">Você pode usar o atributo `Queue` nos seguintes tipos de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c891f-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="c891f-214">`out string` (criará a mensagem da fila se o valor do parâmetro não for nulo quando a função terminar)</span><span class="sxs-lookup"><span data-stu-id="c891f-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="c891f-215">`out byte[]` (funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="c891f-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="c891f-216">`out CloudQueueMessage` (funciona como `string`)</span><span class="sxs-lookup"><span data-stu-id="c891f-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="c891f-217">`out POCO` (um tipo serializável criará uma mensagem com um objeto nulo se o parâmetro for nulo quando a função terminar)</span><span class="sxs-lookup"><span data-stu-id="c891f-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="c891f-218">`CloudQueue` (para criar mensagens manualmente usando a API de Armazenamento do Azure diretamente)</span><span class="sxs-lookup"><span data-stu-id="c891f-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <span data-ttu-id="c891f-219"><a id="ibinder"></a>Usar atributos do SDK de Trabalhos Web no corpo de uma função</span><span class="sxs-lookup"><span data-stu-id="c891f-219"><a id="ibinder"></a>Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="c891f-220">Se precisar realizar algum trabalho em sua função antes de usar um atributo do SDK de Trabalhos Web como `Queue`, `Blob`, ou `Table`, você poderá usar a interface `IBinder`.</span><span class="sxs-lookup"><span data-stu-id="c891f-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="c891f-221">O exemplo a seguir usa uma mensagem da fila de entrada e cria uma nova mensagem com o mesmo conteúdo em uma fila de saída.</span><span class="sxs-lookup"><span data-stu-id="c891f-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="c891f-222">O nome da fila de saída é definido pelo código no corpo da função.</span><span class="sxs-lookup"><span data-stu-id="c891f-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="c891f-223">A interface `IBinder` também pode ser usada com os atributos `Table` e `Blob`.</span><span class="sxs-lookup"><span data-stu-id="c891f-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="c891f-224"><a id="blobs"></a> Como ler e gravar blobs e tabelas durante o processamento de uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="c891f-224"><a id="blobs"></a> How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="c891f-225">Os atributos `Blob` e `Table` permitem que você leia e grave os blobs e tabelas.</span><span class="sxs-lookup"><span data-stu-id="c891f-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="c891f-226">Os exemplos nesta seção se aplicam a blobs.</span><span class="sxs-lookup"><span data-stu-id="c891f-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="c891f-227">Para obter exemplos de código que mostram como disparar processos quando blobs são criados ou atualizados, consulte [Como usar o armazenamento de blobs do Azure com o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) e para obter exemplos de código que leem e gravam as tabelas, consulte [Como usar o armazenamento de tabelas do Azure com o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c891f-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="c891f-228">Mensagens da fila de cadeia de caracteres que disparam operações de blob</span><span class="sxs-lookup"><span data-stu-id="c891f-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="c891f-229">Para uma mensagem da fila que contém uma cadeia de caracteres, `queueTrigger` é um espaço reservado que você pode usar no parâmetro do `Blob` atributo `blobPath` que tem o conteúdo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="c891f-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="c891f-230">O exemplo a seguir usa objetos `Stream` para ler e gravar os blobs.</span><span class="sxs-lookup"><span data-stu-id="c891f-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="c891f-231">A mensagem da fila é o nome de um blob localizado no contêiner de textblobs.</span><span class="sxs-lookup"><span data-stu-id="c891f-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="c891f-232">Uma cópia de blob com "-new" acrescentado ao nome é criada no mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="c891f-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c891f-233">O atributo construtor `Blob` aceita um parâmetro `blobPath` que especifica o nome do blob e contêiner.</span><span class="sxs-lookup"><span data-stu-id="c891f-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="c891f-234">Para obter mais informações sobre esse espaço reservado, consulte [Como usar o armazenamento de blob do Azure com o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="c891f-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="c891f-235">Quando o atributo decora um objeto `Stream`, outro parâmetro de construtor especifica o modo `FileAccess` como leitura, gravação ou leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="c891f-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="c891f-236">O exemplo a seguir usa um objeto `CloudBlockBlob` para excluir um blob.</span><span class="sxs-lookup"><span data-stu-id="c891f-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="c891f-237">A mensagem da fila é o nome do blob.</span><span class="sxs-lookup"><span data-stu-id="c891f-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="c891f-238"><a id="pocoblobs"></a> Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c891f-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c891f-239">Para um POCO armazenado como JSON na mensagem da fila, você pode usar espaços reservados que nomeiam as propriedades do objeto no parâmetro do `Queue` atributo `blobPath`.</span><span class="sxs-lookup"><span data-stu-id="c891f-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="c891f-240">Também é possível utilizar os [nomes de propriedade de metadados de fila](#queuemetadata) como espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="c891f-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="c891f-241">O exemplo a seguir copia um blob para um novo blob com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="c891f-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="c891f-242">A mensagem da fila é um objeto `BlobInformation` que inclui `BlobName` e as propriedades `BlobNameWithoutExtension`.</span><span class="sxs-lookup"><span data-stu-id="c891f-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="c891f-243">Os nomes de propriedade são usados como espaços reservados no caminho de blob para os atributos `Blob` .</span><span class="sxs-lookup"><span data-stu-id="c891f-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c891f-244">O SDK usa o [pacote NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) para serializar e desserializar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="c891f-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="c891f-245">Se criar mensagens de fila em um programa que não usa o SDK de Trabalhos Web, você poderá escrever código como o exemplo a seguir para criar uma mensagem de fila POCO que o SDK possa analisar.</span><span class="sxs-lookup"><span data-stu-id="c891f-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="c891f-246">Se você precisar fazer algum trabalho em sua função antes de vincular um blob a um objeto, você pode usar o atributo no corpo da função, [conforme mostrado anteriormente para o atributo da fila](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="c891f-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="c891f-247"><a id="blobattributetypes"></a> Tipos com os quais você pode usar o atributo Blob</span><span class="sxs-lookup"><span data-stu-id="c891f-247"><a id="blobattributetypes"></a> Types you can use the Blob attribute with</span></span>
<span data-ttu-id="c891f-248">O atributo `Blob` pode ser usado com os seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="c891f-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="c891f-249">`Stream` (leitura ou gravação, especificadas usando o parâmetro de construtor FileAccess)</span><span class="sxs-lookup"><span data-stu-id="c891f-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="c891f-250">`string` (leitura)</span><span class="sxs-lookup"><span data-stu-id="c891f-250">`string` (read)</span></span>
* <span data-ttu-id="c891f-251">`out string` (gravação; criará um blob somente se o parâmetro de cadeia de caracteres não for nulo quando a função retornar)</span><span class="sxs-lookup"><span data-stu-id="c891f-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="c891f-252">POCO (leitura)</span><span class="sxs-lookup"><span data-stu-id="c891f-252">POCO (read)</span></span>
* <span data-ttu-id="c891f-253">out POCO (gravação; sempre cria um blob; criará como objeto nulo se o parâmetro POCO for nulo quando a função retornar)</span><span class="sxs-lookup"><span data-stu-id="c891f-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="c891f-254">`CloudBlobStream` (gravação)</span><span class="sxs-lookup"><span data-stu-id="c891f-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="c891f-255">`ICloudBlob` (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="c891f-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="c891f-256">`CloudBlockBlob` (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="c891f-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="c891f-257">`CloudPageBlob` (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="c891f-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="c891f-258"><a id="poison"></a> Como tratar mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="c891f-258"><a id="poison"></a> How to handle poison messages</span></span>
<span data-ttu-id="c891f-259">As mensagens cujo conteúdo faz com que uma função falhe são chamadas de *mensagens suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="c891f-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="c891f-260">Quando a função falhar, a mensagem da fila não é excluída e eventualmente é captada novamente, fazendo com que o ciclo seja repetido.</span><span class="sxs-lookup"><span data-stu-id="c891f-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="c891f-261">O SDK pode interromper automaticamente o ciclo após algumas iterações, ou você fazê-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="c891f-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="c891f-262">Manipulação automática de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="c891f-262">Automatic poison message handling</span></span>
<span data-ttu-id="c891f-263">O SDK chamará uma função até 5 vezes para processar uma mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="c891f-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="c891f-264">Se a quinta tentativa falhar, a mensagem é movida para uma fila de mensagens suspeitas.</span><span class="sxs-lookup"><span data-stu-id="c891f-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="c891f-265">[O número máximo de novas tentativas é configurável](#config).</span><span class="sxs-lookup"><span data-stu-id="c891f-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="c891f-266">A fila de mensagens suspeita é denominada *{originalqueuename}*-suspeita.</span><span class="sxs-lookup"><span data-stu-id="c891f-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="c891f-267">Você pode gravar uma função para processar as mensagens da fila de mensagens suspeitas registrando-as ou enviando uma notificação de que a atenção manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="c891f-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="c891f-268">No exemplo a seguir, a função `CopyBlob` falhará quando uma mensagem da fila contiver o nome de um blob que não existe.</span><span class="sxs-lookup"><span data-stu-id="c891f-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="c891f-269">Quando isso acontece, a mensagem será movida da fila copyblobqueue para a fila copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="c891f-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="c891f-270">O `ProcessPoisonMessage` registra então a mensagem suspeita.</span><span class="sxs-lookup"><span data-stu-id="c891f-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

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
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="c891f-271">A ilustração a seguir mostra a saída do console dessas funções quando uma mensagem suspeita é processada.</span><span class="sxs-lookup"><span data-stu-id="c891f-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Saída do console para tratamento de mensagens suspeitas](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="c891f-273">Manipulação manual de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="c891f-273">Manual poison message handling</span></span>
<span data-ttu-id="c891f-274">Você pode obter o número de vezes que uma mensagem foi selecionada para processamento adicionando um parâmetro `int` chamado `dequeueCount` à sua função.</span><span class="sxs-lookup"><span data-stu-id="c891f-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="c891f-275">Você pode, então, verificar a contagem de remoção da fila no código de função e realizar seu próprio tratamento de mensagem suspeita quando o número exceder um limite, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c891f-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <span data-ttu-id="c891f-276"><a id="config"></a> Como definir as opções de configuração</span><span class="sxs-lookup"><span data-stu-id="c891f-276"><a id="config"></a> How to set configuration options</span></span>
<span data-ttu-id="c891f-277">Você pode usar o tipo `JobHostConfiguration` para definir as seguintes opções de configuração:</span><span class="sxs-lookup"><span data-stu-id="c891f-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="c891f-278">Definir as cadeias de conexão do SDK no código.</span><span class="sxs-lookup"><span data-stu-id="c891f-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="c891f-279">Defina as configurações `QueueTrigger` de como a contagem máxima de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="c891f-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="c891f-280">Obtenha nomes de fila por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="c891f-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="c891f-281"><a id="setconnstr"></a>Definir as cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="c891f-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="c891f-282">A definição das cadeias de conexão do SDK no código lhe permite usar seus próprios nomes de cadeia de conexão em arquivos de configuração ou variáveis de ambiente, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c891f-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <span data-ttu-id="c891f-283"><a id="configqueue"></a>Configurar definições de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="c891f-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="c891f-284">Você pode definir as seguintes configurações que se aplicam ao processamento de mensagem de fila:</span><span class="sxs-lookup"><span data-stu-id="c891f-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="c891f-285">O número máximo de mensagens da fila que são recebidas simultaneamente a serem executadas em paralelo (o padrão é 16).</span><span class="sxs-lookup"><span data-stu-id="c891f-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="c891f-286">O número máximo de tentativas antes de uma mensagem da fila ser enviada para uma fila de suspeita (o padrão é 5).</span><span class="sxs-lookup"><span data-stu-id="c891f-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="c891f-287">O tempo máximo de espera antes de sondar novamente quando uma fila está vazia (o padrão é 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="c891f-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="c891f-288">O exemplo a seguir mostra como definir essas configurações:</span><span class="sxs-lookup"><span data-stu-id="c891f-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="c891f-289"><a id="setnamesincode"></a>Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="c891f-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="c891f-290">Às vezes você deseja especificar um nome de fila, um nome de blob ou contêiner ou um nome de tabela no código em vez de embuti-lo no código.</span><span class="sxs-lookup"><span data-stu-id="c891f-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="c891f-291">Por exemplo, você talvez queira especificar o nome da fila para `QueueTrigger` em um arquivo de configuração ou variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="c891f-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="c891f-292">Você pode fazer isso passando um objeto `NameResolver` para o tipo `JobHostConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="c891f-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="c891f-293">Você inclui espaços reservados especiais entre sinais de percentual (%) em parâmetros do construtor de atributos do SDK de e o código `NameResolver` especifica os valores reais a serem usados no lugar desses espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="c891f-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="c891f-294">Por exemplo, suponha que você deseje usar uma fila denominada logqueuetest no ambiente de teste e uma denominada logqueueprod na produção.</span><span class="sxs-lookup"><span data-stu-id="c891f-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="c891f-295">Em vez de um nome de fila embutido em código, você deseja especificar o nome de uma entrada na coleção `appSettings` que teria o nome da fila real.</span><span class="sxs-lookup"><span data-stu-id="c891f-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="c891f-296">Se a chave `appSettings` for logqueue, sua função será semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c891f-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="c891f-297">Sua classe `NameResolver` poderia, então, obter o nome da fila de `appSettings`, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c891f-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="c891f-298">Você passa a classe `NameResolver` ao objeto `JobHost`, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c891f-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="c891f-299">**Observação:** os nomes de fila, tabela e blob são resolvidos sempre que uma função é chamada, mas os nomes de contêineres de blob são resolvidos somente quando o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="c891f-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="c891f-300">Você não pode alterar o nome do contêiner de blob enquanto o trabalho está em execução.</span><span class="sxs-lookup"><span data-stu-id="c891f-300">You can't change blob container name while the job is running.</span></span>

## <span data-ttu-id="c891f-301"><a id="manual"></a>Como acionar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="c891f-301"><a id="manual"></a>How to trigger a function manually</span></span>
<span data-ttu-id="c891f-302">Para disparar uma função manualmente, use o método `Call` ou `CallAsync` no objeto `JobHost` e o atributo `NoAutomaticTrigger` na função, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c891f-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

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

## <span data-ttu-id="c891f-303"><a id="logs"></a>Como gravar logs</span><span class="sxs-lookup"><span data-stu-id="c891f-303"><a id="logs"></a>How to write logs</span></span>
<span data-ttu-id="c891f-304">O painel mostra logs em dois lugares: na página do Trabalho Web e na página de determinada invocação do Trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="c891f-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Logs na página do Trabalho Web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Logs na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="c891f-307">A saída de métodos de console que você chama em uma função ou no método `Main()` aparece na página Painel para o trabalho Web, não na página de uma invocação de método específica.</span><span class="sxs-lookup"><span data-stu-id="c891f-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="c891f-308">A saída do objeto TextWriter obtido de um parâmetro na assinatura do método é exibida na página Painel para uma invocação de método.</span><span class="sxs-lookup"><span data-stu-id="c891f-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="c891f-309">A saída do console não pode ser vinculada a uma invocação de método específica porque o console é single-threaded, embora muitas funções de trabalho possam estar sendo executadas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="c891f-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="c891f-310">É por isso que o SDK fornece a cada invocação de função seu próprio objeto de gravador de log exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c891f-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="c891f-311">Para gravar [logs de rastreamento do aplicativo](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilize `Console.Out` (cria registros marcados como INFO) e `Console.Error` (cria registros marcados como ERROR).</span><span class="sxs-lookup"><span data-stu-id="c891f-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="c891f-312">Uma alternativa é usar [Rastreamento ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que fornece os níveis Detalhado, de Aviso e Crítico, além de Informações e Erro.</span><span class="sxs-lookup"><span data-stu-id="c891f-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="c891f-313">Os logs de rastreamento de aplicativo aparecem nos arquivos de log de aplicativo Web, nas tabelas do Azure ou nos blobs do Azure, dependendo de como você configura seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="c891f-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="c891f-314">Assim como ocorre com toda a saída do console, os 100 logs de aplicativos mais recentes também são exibidos na página Painel do Trabalho Web, não na página de uma invocação de função.</span><span class="sxs-lookup"><span data-stu-id="c891f-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="c891f-315">A saída do console aparecerá no painel somente se o programa estiver em execução em um Trabalho Web do Azure, não se o programa estiver em execução localmente ou em outro ambiente.</span><span class="sxs-lookup"><span data-stu-id="c891f-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="c891f-316">Desabilite o log de painel para cenários de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="c891f-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="c891f-317">Por padrão, o SDK grava logs no armazenamento e essa atividade pode degradar o desempenho durante o processamento de várias mensagens.</span><span class="sxs-lookup"><span data-stu-id="c891f-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="c891f-318">Para desabilitar o log, defina a cadeia de conexão do painel de controle como nula, como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c891f-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="c891f-319">O exemplo a seguir mostra várias maneiras de gravar logs:</span><span class="sxs-lookup"><span data-stu-id="c891f-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="c891f-320">No painel do SDK de Trabalhos Web, a saída do objeto `TextWriter` aparece quando você vai até a página para uma invocação de função específica e clica em **Alternar Saída**:</span><span class="sxs-lookup"><span data-stu-id="c891f-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![Clique no link de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Logs na página de invocação de função](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="c891f-323">No painel do SDK de Trabalhos Web, as 100 linhas da saída do console mais recentes são mostradas quando você vai até a página do Trabalho Web (não da invocação de função) e clica em **Alternar Saída**.</span><span class="sxs-lookup"><span data-stu-id="c891f-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![Clique em Alternar Saída](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="c891f-325">Em um Trabalho Web contínuo, os logs de aplicativo são mostrados em /data/jobs/continuous/*{nomedowebjob}*/job_log.txt no sistema de arquivos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c891f-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="c891f-326">Em um blob do Azure, os logs de aplicativo se parecem com este: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Olá, mundo!,</span><span class="sxs-lookup"><span data-stu-id="c891f-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="c891f-327">E em uma tabela do Azure, os logs `Console.Out` e `Console.Error` têm esta aparência:</span><span class="sxs-lookup"><span data-stu-id="c891f-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![Log de informações na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Log de erros na tabela](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="c891f-330">Se você desejar conectar seu próprio agente, veja [este exemplo](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c891f-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="c891f-331"><a id="errors"></a>Como tratar erros e configurar tempos limite</span><span class="sxs-lookup"><span data-stu-id="c891f-331"><a id="errors"></a>How to handle errors and configure timeouts</span></span>
<span data-ttu-id="c891f-332">O SDK dos Trabalhos Web também inclui um atributo [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) que pode ser usado para fazer com que uma função seja cancelada se não for concluída em um período especificado.</span><span class="sxs-lookup"><span data-stu-id="c891f-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="c891f-333">E se você desejar gerar um alerta quando um número excessivo de erros ocorrerem em um período especificado, é possível usar o atributo `ErrorTrigger` .</span><span class="sxs-lookup"><span data-stu-id="c891f-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="c891f-334">Este é um [exemplo de ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="c891f-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="c891f-335">Você também pode desabilitar e habilitar de modo dinâmico funções para controlar se eles podem ser disparados, usando uma opção de configuração que pode ser uma configuração de aplicativo ou um nome de variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="c891f-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="c891f-336">Para obter o código de exemplo, veja o atributo `Disable` no [repositório de exemplos de SDK dos Trabalhos Web](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="c891f-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="c891f-337"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c891f-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="c891f-338">Este guia forneceu exemplos de código que mostram como lidar com cenários comuns para trabalhar com filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="c891f-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="c891f-339">Para obter mais informações sobre como usar os Trabalhos Web do Azure e o SDK de Trabalhos Web, consulte [Trabalhos Web do Azure – Recursos recomendados](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c891f-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
