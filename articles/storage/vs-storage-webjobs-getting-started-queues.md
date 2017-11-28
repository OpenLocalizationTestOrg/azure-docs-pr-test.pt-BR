---
title: "aaaGetting de Introdução ao armazenamento de fila e o Visual Studio serviços conectados (projetos WebJob) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de fila do Azure em um projeto do WebJob depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="3c06d-103">Introdução ao Armazenamento de Fila do Azure e aos Serviços Conectados do Visual Studio (Projetos WebJob)</span><span class="sxs-lookup"><span data-stu-id="3c06d-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="3c06d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3c06d-104">Overview</span></span>
<span data-ttu-id="3c06d-105">Este artigo descreve como obter iniciado usando a fila do Azure Olá de armazenamento em um projeto de trabalho de Web do Visual Studio Azure depois que você criou ou referenciados de uma conta de armazenamento do Azure usando o Visual Studio **adicionar serviços conectados** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="3c06d-106">Quando você adiciona um projeto WebJob de tooa de conta de armazenamento usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo, pacotes do NuGet do armazenamento do Azure apropriados Olá estiverem instalados, referências de .NET apropriadas Olá são toohello adicionado projeto e cadeias de caracteres de conexão para a conta de armazenamento Olá são atualizadas no arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="3c06d-107">Este artigo fornece c# exemplos de código que mostram como toouse Olá versão do SDK do Azure WebJobs 1. x com hello serviço de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c06d-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="3c06d-108">Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3c06d-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="3c06d-109">Uma mensagem da fila única pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3c06d-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="3c06d-110">Consulte a [Introdução ao Armazenamento de Filas do Azure usando o .NET](storage-dotnet-how-to-use-queues.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="3c06d-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="3c06d-111">Para saber mais sobre ASP.NET, confira [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="3c06d-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="3c06d-112">Como tootrigger uma função quando é recebida uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="3c06d-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="3c06d-113">toowrite uma função que Olá SDK do WebJobs chama quando é recebida uma mensagem da fila, use Olá **QueueTrigger** atributo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="3c06d-114">o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome de saudação do hello toopoll de fila.</span><span class="sxs-lookup"><span data-stu-id="3c06d-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="3c06d-115">toosee como tooset Olá nome da fila dinamicamente, check-out [como tooset opções de configuração](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="3c06d-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="3c06d-116">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="3c06d-116">String queue messages</span></span>
<span data-ttu-id="3c06d-117">Olá exemplo a seguir, fila Olá contém uma mensagem de cadeia de caracteres, portanto **QueueTrigger** parâmetro de cadeia de caracteres tooa aplicada denominado **logMessage** que contém o conteúdo de saudação de mensagem da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="3c06d-118">Olá função [grava uma mensagem de log toohello painel](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="3c06d-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="3c06d-119">Além disso **cadeia de caracteres**, parâmetro hello pode ser uma matriz de bytes, um **CloudQueueMessage** objeto ou um POCO que você definir.</span><span class="sxs-lookup"><span data-stu-id="3c06d-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="3c06d-120">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="3c06d-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="3c06d-121">Olá exemplo a seguir, mensagem de saudação do fila contém JSON para um **BlobInformation** objeto que inclui um **BlobName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="3c06d-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="3c06d-122">Olá SDK automaticamente desserializa o objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="3c06d-123">Olá SDK usa Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e desserializar de mensagens.</span><span class="sxs-lookup"><span data-stu-id="3c06d-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="3c06d-124">Se você criar a fila de mensagens em um programa que não usa o SDK do WebJobs do hello, você pode escrever código como Olá seguindo o exemplo toocreate uma mensagem da fila POCO que Olá que SDK pode ser analisado.</span><span class="sxs-lookup"><span data-stu-id="3c06d-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="3c06d-125">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="3c06d-125">Async functions</span></span>
<span data-ttu-id="3c06d-126">Olá seguinte função assíncrona [grava um log toohello painel](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="3c06d-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="3c06d-127">Funções assíncronas podem levar uma [token de cancelamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), conforme mostrado no hello exemplo que copia um blob a seguir.</span><span class="sxs-lookup"><span data-stu-id="3c06d-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="3c06d-128">(Para obter uma explicação da saudação **queueTrigger** espaço reservado, consulte Olá [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) seção.)</span><span class="sxs-lookup"><span data-stu-id="3c06d-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="3c06d-129">Atributo de QueueTrigger Olá tipos funciona com</span><span class="sxs-lookup"><span data-stu-id="3c06d-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="3c06d-130">Você pode usar **QueueTrigger** com hello tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c06d-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="3c06d-131">**string**</span><span class="sxs-lookup"><span data-stu-id="3c06d-131">**string**</span></span>
* <span data-ttu-id="3c06d-132">Um tipo POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="3c06d-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="3c06d-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="3c06d-133">**byte[]**</span></span>
* <span data-ttu-id="3c06d-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="3c06d-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="3c06d-135">Algoritmo de sondagem</span><span class="sxs-lookup"><span data-stu-id="3c06d-135">Polling algorithm</span></span>
<span data-ttu-id="3c06d-136">Olá SDK implementa um efeito de saudação tooreduce aleatória exponencial algoritmo de retirada da fila ociosa em custos de transações de armazenamento de sondagem.</span><span class="sxs-lookup"><span data-stu-id="3c06d-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="3c06d-137">Quando uma mensagem é encontrada, Olá SDK espera 2 segundos e, em seguida, verifica a outra mensagem; Quando nenhuma mensagem for encontrada, ele aguarda cerca de quatro segundos antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="3c06d-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="3c06d-138">Depois de tentativas subsequentes tooget uma mensagem da fila, o tempo de espera Olá continua tooincrease até atingir o tempo de espera máximo Olá, quais minuto de tooone padrões.</span><span class="sxs-lookup"><span data-stu-id="3c06d-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="3c06d-139">[Olá tempo de espera máximo é configurável](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="3c06d-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="3c06d-140">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="3c06d-140">Multiple instances</span></span>
<span data-ttu-id="3c06d-141">Se seu aplicativo web é executado em várias instâncias, um trabalhos Web contínuos é executado em cada computador, e cada computador aguardará para gatilhos e tentar toorun funções.</span><span class="sxs-lookup"><span data-stu-id="3c06d-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="3c06d-142">Em alguns cenários, que isso pode levar funções toosome processamento Olá mesmo dados duas vezes, para que funções devem ser idempotentes (gravado de forma que chamando repetidamente com hello mesmos dados de entrada não produzem duplicar os resultados).</span><span class="sxs-lookup"><span data-stu-id="3c06d-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="3c06d-143">Execução paralela</span><span class="sxs-lookup"><span data-stu-id="3c06d-143">Parallel execution</span></span>
<span data-ttu-id="3c06d-144">Se você tiver várias funções diferentes filas escutando, Olá SDK ligá-los em paralelo quando as mensagens são recebidas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="3c06d-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="3c06d-145">Olá mesmo é verdadeiro quando várias mensagens são recebidas para uma única fila.</span><span class="sxs-lookup"><span data-stu-id="3c06d-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="3c06d-146">Por padrão, hello SDK obtém um lote de mensagens de fila de 16 por vez e executa a função hello processa-los em paralelo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="3c06d-147">[tamanho do lote Olá é configurável](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="3c06d-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="3c06d-148">Quando o número Olá processado chega toohalf de tamanho de lote hello, Olá SDK obtém outro lote e começa a processar essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="3c06d-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="3c06d-149">Portanto o número de máximo de saudação simultâneas mensagens processadas por função é tamanho de lote de saudação de uma vez e meia.</span><span class="sxs-lookup"><span data-stu-id="3c06d-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="3c06d-150">Esse limite se aplica separadamente função tooeach que tem um **QueueTrigger** atributo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="3c06d-151">Se não quiser que a execução paralela para mensagens recebidas em uma fila, defina Olá too1 de tamanho de lote.</span><span class="sxs-lookup"><span data-stu-id="3c06d-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="3c06d-152">Obter fila ou metadados de mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="3c06d-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="3c06d-153">Você pode obter Olá propriedades de mensagem a seguir, adicionando a assinatura do método toohello parâmetros:</span><span class="sxs-lookup"><span data-stu-id="3c06d-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="3c06d-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="3c06d-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="3c06d-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="3c06d-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="3c06d-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="3c06d-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="3c06d-157">**string** queueTrigger (contém o texto da mensagem)</span><span class="sxs-lookup"><span data-stu-id="3c06d-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="3c06d-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="3c06d-158">**string** id</span></span>
* <span data-ttu-id="3c06d-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="3c06d-159">**string** popReceipt</span></span>
* <span data-ttu-id="3c06d-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="3c06d-160">**int** dequeueCount</span></span>

<span data-ttu-id="3c06d-161">Se você desejar toowork diretamente com hello API de armazenamento do Azure, você também pode adicionar uma **CloudStorageAccount** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3c06d-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="3c06d-162">Olá exemplo a seguir grava todos os este metadados tooan informações do log de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="3c06d-163">No exemplo hello, logMessage e queueTrigger contêm conteúdo Olá de mensagem da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="3c06d-164">Aqui está um exemplo de log gravado pelo código de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="3c06d-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="3c06d-165">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="3c06d-165">Graceful shutdown</span></span>
<span data-ttu-id="3c06d-166">Uma função que é executado em um trabalho Web contínuo pode aceitar um **CancellationToken** parâmetro que permite Olá toonotify Olá função do sistema operacional quando hello WebJob é sobre toobe encerrada.</span><span class="sxs-lookup"><span data-stu-id="3c06d-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="3c06d-167">Você pode usar este toomake notificação se a função hello não finalização inesperada de forma que deixa os dados em um estado inconsistente.</span><span class="sxs-lookup"><span data-stu-id="3c06d-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="3c06d-168">Olá mostrado no exemplo a seguir como toocheck iminente encerramento do trabalho Web em uma função.</span><span class="sxs-lookup"><span data-stu-id="3c06d-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="3c06d-169">**Observação:** Olá painel não pode mostrar corretamente o status de saudação e a saída de funções que ter sido desligado.</span><span class="sxs-lookup"><span data-stu-id="3c06d-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="3c06d-170">Para obter mais informações, consulte [Desligamento normal dos trabalhos Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="3c06d-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="3c06d-171">Como toocreate uma fila de mensagens ao processar uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="3c06d-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="3c06d-172">toowrite uma função que cria uma nova mensagem da fila, use Olá **fila** atributo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="3c06d-173">Como **QueueTrigger**, passar no nome da fila hello como uma cadeia de caracteres, ou você pode [definir dinamicamente o nome da fila Olá](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="3c06d-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="3c06d-174">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="3c06d-174">String queue messages</span></span>
<span data-ttu-id="3c06d-175">Olá async não exemplo de código a seguir cria uma nova mensagem de fila na fila de saudação denominada "outputqueue" com hello mesmo conteúdo como mensagem de saudação do fila recebidos na fila de saudação denominada "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="3c06d-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="3c06d-176">(Para funções assíncronas, use **IAsyncCollector<T>** , conforme mostrado posteriormente nesta seção.)</span><span class="sxs-lookup"><span data-stu-id="3c06d-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="3c06d-177">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="3c06d-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="3c06d-178">tipo de uma mensagem da fila que contém um POCO em vez de uma cadeia de caracteres, passagem Olá POCO toocreate como um toohello de parâmetro de saída **fila** construtor de atributo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="3c06d-179">Olá SDK automaticamente serializa Olá tooJSON de objeto.</span><span class="sxs-lookup"><span data-stu-id="3c06d-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="3c06d-180">Uma mensagem da fila é sempre criada, mesmo se o objeto de saudação é nulo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="3c06d-181">Criar várias mensagens ou em funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="3c06d-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="3c06d-182">toocreate várias mensagens, verifique o tipo de parâmetro de saudação para fila de saída de hello **ICollector<T>**  ou **IAsyncCollector<T>**, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="3c06d-183">Cada mensagem de fila é criada imediatamente quando hello **adicionar** método é chamado.</span><span class="sxs-lookup"><span data-stu-id="3c06d-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="3c06d-184">Tipos de atributo fila Olá funciona com</span><span class="sxs-lookup"><span data-stu-id="3c06d-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="3c06d-185">Você pode usar o hello **fila** atributo Olá tipos de parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c06d-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="3c06d-186">**saída de cadeia de caracteres** (cria a mensagem da fila se o valor do parâmetro é não nulo quando a função hello termina)</span><span class="sxs-lookup"><span data-stu-id="3c06d-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="3c06d-187">**out byte[]** (funciona como **string**)</span><span class="sxs-lookup"><span data-stu-id="3c06d-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="3c06d-188">**out CloudQueueMessage** (funciona como **string**)</span><span class="sxs-lookup"><span data-stu-id="3c06d-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="3c06d-189">**limite POCO** (um tipo serializável, cria uma mensagem com um objeto nulo se o parâmetro hello é nulo quando termina de função hello)</span><span class="sxs-lookup"><span data-stu-id="3c06d-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="3c06d-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="3c06d-190">**ICollector**</span></span>
* <span data-ttu-id="3c06d-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="3c06d-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="3c06d-192">**CloudQueue** (para a criação de mensagens manualmente usando Olá API de armazenamento do Azure diretamente)</span><span class="sxs-lookup"><span data-stu-id="3c06d-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="3c06d-193">Usar atributos de SDK do WebJobs no corpo de saudação de uma função</span><span class="sxs-lookup"><span data-stu-id="3c06d-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="3c06d-194">Se você precisar toodo alguns funcionar na sua função antes de usar um atributo do SDK do WebJobs como **fila**, **Blob**, ou **tabela**, você pode usar o hello **IBinder** interface.</span><span class="sxs-lookup"><span data-stu-id="3c06d-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="3c06d-195">saudação de exemplo a seguir usa uma mensagem da fila de entrada e cria uma nova mensagem com hello mesmo conteúdo em uma fila de saída.</span><span class="sxs-lookup"><span data-stu-id="3c06d-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="3c06d-196">nome de fila de saída de saudação é definido pelo código no corpo de saudação do função hello.</span><span class="sxs-lookup"><span data-stu-id="3c06d-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="3c06d-197">Olá **IBinder** interface também pode ser usada com hello **tabela** e **Blob** atributos.</span><span class="sxs-lookup"><span data-stu-id="3c06d-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="3c06d-198">Como tooread e gravar os blobs e tabelas durante o processamento de uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="3c06d-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="3c06d-199">Olá **Blob** e **tabela** atributos permitem que você tooread e gravar os blobs e tabelas.</span><span class="sxs-lookup"><span data-stu-id="3c06d-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="3c06d-200">exemplos de saudação nesta seção se aplicam a tooblobs.</span><span class="sxs-lookup"><span data-stu-id="3c06d-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="3c06d-201">Para obter exemplos de código que mostram como tootrigger processa quando blobs são criados ou atualizados, consulte [como toouse Azure blob storage com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e para obter exemplos de código que leem e gravam tabelas, consulte [como toouse tabela do Azure armazenamento com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="3c06d-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="3c06d-202">Mensagens da fila de cadeia de caracteres que disparam operações de blob</span><span class="sxs-lookup"><span data-stu-id="3c06d-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="3c06d-203">Para uma mensagem da fila que contém uma cadeia de caracteres, **queueTrigger** é um espaço reservado que você pode usar em Olá **Blob** do atributo **blobPath** parâmetro que contém o conteúdo de saudação do mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="3c06d-204">Olá exemplo a seguir usa **fluxo** objetos blobs tooread e gravação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="3c06d-205">mensagem de saudação do fila é o nome de saudação de um blob localizado no contêiner de textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="3c06d-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="3c06d-206">Uma cópia de blob Olá com "-novo" acrescentada toohello nome é criado no hello mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="3c06d-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="3c06d-207">Olá **Blob** atributo construtor usa um **blobPath** parâmetro que especifica o contêiner de saudação e nome do blob.</span><span class="sxs-lookup"><span data-stu-id="3c06d-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="3c06d-208">Para obter mais informações sobre esse espaço reservado, consulte [como toouse Azure blob storage com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="3c06d-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="3c06d-209">Quando o atributo Olá decora uma **fluxo** do objeto, outro parâmetro de construtor Especifica Olá **FileAccess** modo como leitura, gravação ou leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="3c06d-210">Olá exemplo a seguir usa uma **CloudBlockBlob** toodelete um blob do objeto.</span><span class="sxs-lookup"><span data-stu-id="3c06d-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="3c06d-211">mensagem da fila de saudação é o nome de saudação do blob hello.</span><span class="sxs-lookup"><span data-stu-id="3c06d-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="3c06d-212">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="3c06d-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="3c06d-213">Para um POCO armazenada como JSON na mensagem de saudação do fila, você pode usar espaços reservados que propriedades de objeto Olá Olá nomes **fila** do atributo **blobPath** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3c06d-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="3c06d-214">Também é possível utilizar os nomes de propriedade de metadados de fila como espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="3c06d-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="3c06d-215">Consulte [Obter a fila ou os metadados de mensagem da fila](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="3c06d-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="3c06d-216">Olá, exemplo a seguir copia um blob tooa novo blob com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="3c06d-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="3c06d-217">mensagem de saudação do fila é um **BlobInformation** objeto inclui **BlobName** e **BlobNameWithoutExtension** propriedades.</span><span class="sxs-lookup"><span data-stu-id="3c06d-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="3c06d-218">nomes de propriedade Olá são usados como espaços reservados no caminho de blob Olá Olá **Blob** atributos.</span><span class="sxs-lookup"><span data-stu-id="3c06d-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="3c06d-219">Olá SDK usa Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e desserializar de mensagens.</span><span class="sxs-lookup"><span data-stu-id="3c06d-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="3c06d-220">Se você criar a fila de mensagens em um programa que não usa o SDK do WebJobs do hello, você pode escrever código como Olá seguindo o exemplo toocreate uma mensagem da fila POCO que Olá que SDK pode ser analisado.</span><span class="sxs-lookup"><span data-stu-id="3c06d-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="3c06d-221">Se você precisar toodo alguns funcionar na sua função antes de associar um objeto de tooan de blob, você pode usar o atributo de saudação no corpo de saudação do função hello, conforme mostrado no [atributos de usar o SDK do WebJobs no corpo de saudação de uma função](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="3c06d-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="3c06d-222">Tipos que você pode usar o hello Blob de atributo com</span><span class="sxs-lookup"><span data-stu-id="3c06d-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="3c06d-223">Olá **Blob** atributo pode ser usado com hello tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c06d-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="3c06d-224">**Fluxo** (leitura ou gravação, especificadas usando o parâmetro de construtor FileAccess Olá)</span><span class="sxs-lookup"><span data-stu-id="3c06d-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="3c06d-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="3c06d-225">**TextReader**</span></span>
* <span data-ttu-id="3c06d-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="3c06d-226">**TextWriter**</span></span>
* <span data-ttu-id="3c06d-227">**string** (leitura)</span><span class="sxs-lookup"><span data-stu-id="3c06d-227">**string** (read)</span></span>
* <span data-ttu-id="3c06d-228">**saída de cadeia de caracteres** (gravação; cria um blob somente se o parâmetro de cadeia de caracteres de saudação for não nulo quando a função hello retorna)</span><span class="sxs-lookup"><span data-stu-id="3c06d-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="3c06d-229">POCO (leitura)</span><span class="sxs-lookup"><span data-stu-id="3c06d-229">POCO (read)</span></span>
* <span data-ttu-id="3c06d-230">limite POCO (gravação; sempre cria um blob, cria como objeto nulo se o parâmetro POCO é nulo quando a função hello retorna)</span><span class="sxs-lookup"><span data-stu-id="3c06d-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="3c06d-231">**CloudBlobStream** (gravação)</span><span class="sxs-lookup"><span data-stu-id="3c06d-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="3c06d-232">**ICloudBlob** (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="3c06d-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="3c06d-233">**CloudBlockBlob** (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="3c06d-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="3c06d-234">**CloudPageBlob** (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="3c06d-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="3c06d-235">Como o toohandle mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="3c06d-235">How toohandle poison messages</span></span>
<span data-ttu-id="3c06d-236">São chamadas de mensagens cujo conteúdo faz com que uma função toofail *mensagens suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="3c06d-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="3c06d-237">Quando a função hello falha, mensagem de saudação do fila não é excluída e eventualmente é obtida novamente, causando toobe de ciclo de saudação repetido.</span><span class="sxs-lookup"><span data-stu-id="3c06d-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="3c06d-238">Olá SDK automaticamente pode interromper o ciclo de saudação após um número limitado de iterações ou você pode fazer isso manualmente.</span><span class="sxs-lookup"><span data-stu-id="3c06d-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="3c06d-239">Manipulação automática de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="3c06d-239">Automatic poison message handling</span></span>
<span data-ttu-id="3c06d-240">Olá SDK chamará uma função de backup too5 vezes tooprocess uma mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="3c06d-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="3c06d-241">Se tentar quinto Olá falhar, mensagem de saudação é fila inviabilização movida tooa.</span><span class="sxs-lookup"><span data-stu-id="3c06d-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="3c06d-242">Você pode ver como tooconfigure Olá número máximo de repetições em [como opções de configuração de tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="3c06d-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="3c06d-243">fila suspeitas Olá é denominada *{originalqueuename}*-suspeitas.</span><span class="sxs-lookup"><span data-stu-id="3c06d-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="3c06d-244">Você pode escrever uma função tooprocess mensagens da fila de suspeitas Olá registrá-los ou enviar uma notificação que atenção manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="3c06d-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="3c06d-245">Em Olá Olá de exemplo a seguir **CopyBlob** função falhará quando uma mensagem da fila contém nome de saudação de um blob que não existe.</span><span class="sxs-lookup"><span data-stu-id="3c06d-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="3c06d-246">Quando isso acontece, a mensagem de saudação é movida da fila de suspeitas copyblobqueue Olá copyblobqueue fila toohello.</span><span class="sxs-lookup"><span data-stu-id="3c06d-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="3c06d-247">Olá **ProcessPoisonMessage** e logs Olá mensagens suspeitas.</span><span class="sxs-lookup"><span data-stu-id="3c06d-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

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

<span data-ttu-id="3c06d-248">Olá ilustração a seguir mostra a saída de console dessas funções quando uma mensagem suspeita é processada.</span><span class="sxs-lookup"><span data-stu-id="3c06d-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Saída do console para tratamento de mensagens suspeitas](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="3c06d-250">Manipulação manual de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="3c06d-250">Manual poison message handling</span></span>
<span data-ttu-id="3c06d-251">Você pode obter o número de saudação de vezes que uma mensagem tem foram coletada para processamento, adicionando um **int** parâmetro denominado **dequeueCount** tooyour função.</span><span class="sxs-lookup"><span data-stu-id="3c06d-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="3c06d-252">Você pode então seleção Olá contagem no código da função de remoção da fila e executar seu próprio tratamento de mensagens suspeitas quando o número de saudação excede um limite, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="3c06d-253">Como as opções de configuração de tooset</span><span class="sxs-lookup"><span data-stu-id="3c06d-253">How tooset configuration options</span></span>
<span data-ttu-id="3c06d-254">Você pode usar o hello **JobHostConfiguration** saudação do tipo tooset as opções de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c06d-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="3c06d-255">Defina cadeias de caracteres de conexão do hello SDK no código.</span><span class="sxs-lookup"><span data-stu-id="3c06d-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="3c06d-256">Definir as configurações de **QueueTrigger** como contagem máxima de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="3c06d-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="3c06d-257">Obtenha nomes de fila por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="3c06d-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="3c06d-258">Defina as cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="3c06d-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="3c06d-259">Definindo cadeias de caracteres de conexão do hello SDK no código permite que você toouse seus próprios nomes de cadeia de caracteres de conexão em arquivos de configuração ou variáveis de ambiente, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="3c06d-260">Definir configurações de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="3c06d-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="3c06d-261">Você pode configurar Olá configurações que se aplicam a toohello processamento de mensagens de fila a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c06d-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="3c06d-262">Olá número máximo de fila de mensagens que são aplicadas simultaneamente toobe executado em paralelo (o padrão é 16).</span><span class="sxs-lookup"><span data-stu-id="3c06d-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="3c06d-263">Olá número máximo de tentativas antes de uma mensagem da fila é enviada a fila de suspeitas tooa (o padrão é 5).</span><span class="sxs-lookup"><span data-stu-id="3c06d-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="3c06d-264">tempo de espera máximo Olá antes de sondar novamente quando uma fila está vazia (o padrão é 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="3c06d-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="3c06d-265">Olá mostrado no exemplo a seguir como tooconfigure essas configurações:</span><span class="sxs-lookup"><span data-stu-id="3c06d-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="3c06d-266">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="3c06d-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="3c06d-267">Às vezes, você deseja toospecify um nome de fila, um nome de blob ou contêiner ou nome de uma tabela no código em vez de embuti-lo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="3c06d-268">Por exemplo, convém toospecify Olá nome **QueueTrigger** em uma variável de ambiente ou arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="3c06d-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="3c06d-269">Você pode fazer isso, passando um **NameResolver** objeto toohello **JobHostConfiguration** tipo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="3c06d-270">Incluir espaços reservados especiais entre sinais de porcentagem (%)) nos parâmetros de construtor de atributo do SDK do WebJobs e sua **NameResolver** código especifica Olá toobe de valores reais usado no lugar desses espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="3c06d-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="3c06d-271">Por exemplo, suponha que você queira toouse uma fila denominada logqueuetest no ambiente de teste hello e um logqueueprod nomeado na produção.</span><span class="sxs-lookup"><span data-stu-id="3c06d-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="3c06d-272">Em vez de um nome de fila embutidos, você deseja que o nome de saudação toospecify da entrada hello **appSettings** coleção que tem nome de fila real hello.</span><span class="sxs-lookup"><span data-stu-id="3c06d-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="3c06d-273">Se hello **appSettings** chave é logqueue, sua função pode parecer com o exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="3c06d-274">O **NameResolver** classe, em seguida, foi possível obter o nome da fila de saudação do **appSettings** conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="3c06d-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="3c06d-275">Você passa Olá **NameResolver** classe toohello **JobHost** conforme mostrado no exemplo a seguir de saudação do objeto.</span><span class="sxs-lookup"><span data-stu-id="3c06d-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="3c06d-276">**Observação:** nomes de blob, tabela e fila são resolvidos sempre que uma função é chamada, mas os nomes de contêiner de blob são resolvidos somente quando o aplicativo hello inicia.</span><span class="sxs-lookup"><span data-stu-id="3c06d-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="3c06d-277">Você não pode alterar o nome do contêiner de blob enquanto Olá trabalho está em execução.</span><span class="sxs-lookup"><span data-stu-id="3c06d-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="3c06d-278">Como uma função de tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="3c06d-278">How tootrigger a function manually</span></span>
<span data-ttu-id="3c06d-279">tootrigger uma função manualmente, use Olá **chamar** ou **CallAsync** método hello **JobHost** objeto e hello **NoAutomaticTrigger** atributo na função hello, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c06d-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

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

## <a name="how-toowrite-logs"></a><span data-ttu-id="3c06d-280">Como os logs de toowrite</span><span class="sxs-lookup"><span data-stu-id="3c06d-280">How toowrite logs</span></span>
<span data-ttu-id="3c06d-281">Olá painel mostra logs em dois lugares: página Olá Olá trabalho Web e página Olá para determinada invocação WebJob.</span><span class="sxs-lookup"><span data-stu-id="3c06d-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Logs na página do Trabalho Web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Logs na página de invocação de função](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="3c06d-284">Saída de métodos de Console que você chama uma função ou de saudação **Main** método aparece na página painel Olá Olá WebJob, não na página de saudação para uma invocação de método específico.</span><span class="sxs-lookup"><span data-stu-id="3c06d-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="3c06d-285">Saída do objeto de TextWriter Olá que você obteve de um parâmetro na sua assinatura do método aparece na página do painel de saudação de uma invocação de método.</span><span class="sxs-lookup"><span data-stu-id="3c06d-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="3c06d-286">Saída do console não pode ser vinculado tooa da invocação do método particular porque Olá Console é de thread único, enquanto muitas funções de trabalho podem ser executadas ao Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="3c06d-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="3c06d-287">É por isso que Olá SDK fornece cada invocação de função com seu próprio objeto do gravador de log exclusivo.</span><span class="sxs-lookup"><span data-stu-id="3c06d-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="3c06d-288">toowrite [logs de rastreamento de aplicativo](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (cria marcados como informações de logs) e **Console.Error** (cria logs marcados como erro).</span><span class="sxs-lookup"><span data-stu-id="3c06d-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="3c06d-289">Uma alternativa é toouse [rastreamento ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que fornece detalhado, aviso e crítico níveis em adição tooInfo e erro.</span><span class="sxs-lookup"><span data-stu-id="3c06d-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="3c06d-290">Logs de rastreamento do aplicativo aparecem nos arquivos de log de aplicativo da web hello, as tabelas do Azure, ou blobs do Azure dependendo de como você configura seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c06d-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="3c06d-291">Assim como de toda a saída de Console, logs de aplicativo 100 mais recentes Olá também aparecem na página painel Olá Olá WebJob, não a página Olá para uma invocação de função.</span><span class="sxs-lookup"><span data-stu-id="3c06d-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="3c06d-292">Saída do console é exibida em Olá painel somente se o programa hello está sendo executado em um trabalho de Web do Azure, não se programa hello está sendo executado localmente ou em algum outro ambiente.</span><span class="sxs-lookup"><span data-stu-id="3c06d-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="3c06d-293">Você pode desabilitar o registro em log definindo Olá toonull de cadeia de caracteres de conexão de painel.</span><span class="sxs-lookup"><span data-stu-id="3c06d-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="3c06d-294">Para obter mais informações, consulte [como tooset opções de configuração](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="3c06d-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="3c06d-295">Olá, exemplo a seguir mostra várias maneiras toowrite logs:</span><span class="sxs-lookup"><span data-stu-id="3c06d-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="3c06d-296">Em Olá painel do SDK do WebJobs, Olá saída de hello **TextWriter** mostra backup quando você entrar toohello página para uma determinada chamada de função e selecione objeto **alternar saída**:</span><span class="sxs-lookup"><span data-stu-id="3c06d-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Link de invocação](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Logs na página de invocação de função](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="3c06d-299">Em Olá painel do SDK do WebJobs, linhas Olá 100 mais recente do Console de saída mostrar backup quando você vá para a página toohello para Olá WebJob (não para invocação de função hello) e selecione **alternar saída**.</span><span class="sxs-lookup"><span data-stu-id="3c06d-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Ativar/Desativar Saída](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="3c06d-301">Em um trabalho Web contínuo, logs de aplicativo exibido no/dados/trabalhos/contínua/*{webjobname}*/job_log.txt no sistema de arquivos de aplicativo de web hello.</span><span class="sxs-lookup"><span data-stu-id="3c06d-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="3c06d-302">Em um aplicativo hello de BLOBs do Azure logs ter esta aparência: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Olá, mundo!, 2014-09-26T21:01:13, erro, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Olá, mundo!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Olá, mundo!,</span><span class="sxs-lookup"><span data-stu-id="3c06d-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="3c06d-303">Em uma saudação de tabela do Azure **Console.Out** e **Console.Error** logs ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="3c06d-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Log de informações na tabela](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Log de erros na tabela](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="3c06d-306">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c06d-306">Next steps</span></span>
<span data-ttu-id="3c06d-307">Este artigo fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c06d-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="3c06d-308">Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="3c06d-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

