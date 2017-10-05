---
title: "Introdução ao armazenamento de filas e aos serviços conectados do Visual Studio (projetos de Trabalho Web) | Microsoft Docs"
description: "Como começar a usar o armazenamento de fila do Azure em um projeto WebJob depois de se conectar a uma conta de armazenamento usando os serviços conectados do Visual Studio."
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
ms.openlocfilehash: abd4814c099620345e04833e14dafd38432064e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="464ce-103">Introdução ao Armazenamento de Fila do Azure e aos Serviços Conectados do Visual Studio (Projetos WebJob)</span><span class="sxs-lookup"><span data-stu-id="464ce-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="464ce-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="464ce-104">Overview</span></span>
<span data-ttu-id="464ce-105">Este artigo descreve como começar a usar o armazenamento de filas do Azure em um projeto de Trabalho Web do Azure Visual Studio depois de ter criado ou referenciado uma conta de armazenamento do Azure usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="464ce-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="464ce-106">Quando você adiciona uma conta de armazenamento a um projeto de WebJob usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio, os pacotes NuGet do Armazenamento do Azure apropriados são instalados, as referências apropriadas .NET são adicionadas ao projeto e cadeias de conexão para a conta de armazenamento são atualizadas no arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="464ce-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="464ce-107">Este artigo fornece exemplos de código em C# que mostram como usar o SDK do Azure WebJobs versão 1.x com o serviço de armazenamento de Fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="464ce-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="464ce-108">O armazenamento de filas do Azure é um serviço para armazenamento de um grande número de mensagens que podem ser acessadas de qualquer lugar do mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="464ce-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="464ce-109">Uma única mensagem de fila pode ter até 64 KB de tamanho e uma fila pode conter milhões de mensagens, até o limite de capacidade total de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="464ce-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="464ce-110">Consulte a [Introdução ao Armazenamento de Filas do Azure usando o .NET](storage-dotnet-how-to-use-queues.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="464ce-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="464ce-111">Para saber mais sobre ASP.NET, confira [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="464ce-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="464ce-112">Como disparar uma função quando é recebida uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="464ce-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="464ce-113">Para gravar uma função que o SDK de Trabalhos Web chama quando uma mensagem da fila é recebida, use o atributo **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="464ce-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="464ce-114">O construtor de atributo tem um parâmetro de cadeia que especifica o nome da fila para sondagem.</span><span class="sxs-lookup"><span data-stu-id="464ce-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="464ce-115">Para saber como definir o nome da fila dinamicamente, confira [Como definir as Opções de Configuração](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="464ce-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="464ce-116">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="464ce-116">String queue messages</span></span>
<span data-ttu-id="464ce-117">No exemplo a seguir, a fila contém uma mensagem de cadeia de caracteres, portanto **QueueTrigger** é aplicado a um parâmetro de cadeia de caracteres chamado **logMessage**, que inclui o conteúdo da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="464ce-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="464ce-118">A função [grava uma mensagem de log no painel](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="464ce-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="464ce-119">Além da **cadeia de caracteres**, o parâmetro pode ser uma matriz de bytes, um objeto **CloudQueueMessage** ou um POCO definido por você.</span><span class="sxs-lookup"><span data-stu-id="464ce-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="464ce-120">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="464ce-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="464ce-121">No exemplo a seguir, a mensagem da fila contém o JSON para um objeto **BlobInformation**, que inclui uma propriedade **BlobName**.</span><span class="sxs-lookup"><span data-stu-id="464ce-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="464ce-122">O SDK automaticamente desserializa o objeto.</span><span class="sxs-lookup"><span data-stu-id="464ce-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="464ce-123">O SDK usa o [pacote NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) para serializar e desserializar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="464ce-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="464ce-124">Se criar mensagens de fila em um programa que não usa o SDK de Trabalhos Web, você poderá escrever código como o exemplo a seguir para criar uma mensagem de fila POCO que o SDK possa analisar.</span><span class="sxs-lookup"><span data-stu-id="464ce-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="464ce-125">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="464ce-125">Async functions</span></span>
<span data-ttu-id="464ce-126">A seguinte função assíncrona [grava um log no painel](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="464ce-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="464ce-127">As funções assíncronas podem levar um [token de cancelamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), conforme mostrado no exemplo a seguir, que copia um blob.</span><span class="sxs-lookup"><span data-stu-id="464ce-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="464ce-128">(Para obter uma explicação do espaço reservado **queueTrigger** , consulte a seção [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) ).</span><span class="sxs-lookup"><span data-stu-id="464ce-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="464ce-129">Tipos com os quais o atributo QueueTrigger funciona</span><span class="sxs-lookup"><span data-stu-id="464ce-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="464ce-130">Você pode usar **QueueTrigger** com os seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="464ce-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="464ce-131">**string**</span><span class="sxs-lookup"><span data-stu-id="464ce-131">**string**</span></span>
* <span data-ttu-id="464ce-132">Um tipo POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="464ce-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="464ce-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="464ce-133">**byte[]**</span></span>
* <span data-ttu-id="464ce-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="464ce-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="464ce-135">Algoritmo de sondagem</span><span class="sxs-lookup"><span data-stu-id="464ce-135">Polling algorithm</span></span>
<span data-ttu-id="464ce-136">O SDK implementa um algoritmo exponencial aleatório de retirada para reduzir o efeito de sondagem de fila ociosa nos custos das transações de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="464ce-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="464ce-137">Quando uma mensagem for encontrada, o SDK aguarda dois segundos e, em seguida, verifica outra mensagem; quando nenhuma mensagem for encontrada, ele aguarda cerca de quatro segundos antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="464ce-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="464ce-138">Após subsequentes tentativas falhas para obter uma mensagem da fila, o tempo de espera continua a aumentar até atingir o tempo de espera máximo, cujo padrão é um minuto.</span><span class="sxs-lookup"><span data-stu-id="464ce-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="464ce-139">[O tempo de espera máximo é configurável](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="464ce-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="464ce-140">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="464ce-140">Multiple instances</span></span>
<span data-ttu-id="464ce-141">Se o seu aplicativo Web for executado em várias instâncias, um Trabalho Web contínuo será executado em todos os computadores, e cada computador aguardará os gatilhos e tentará executar as funções.</span><span class="sxs-lookup"><span data-stu-id="464ce-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="464ce-142">Em alguns cenários, isso pode fazer com que algumas funções processem os mesmos dados duas vezes. Assim, as funções devem ser idempotentes (escritas de forma que chamá-las repetidamente com os mesmos dados de entrada não produza resultados duplicados).</span><span class="sxs-lookup"><span data-stu-id="464ce-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="464ce-143">Execução paralela</span><span class="sxs-lookup"><span data-stu-id="464ce-143">Parallel execution</span></span>
<span data-ttu-id="464ce-144">Se você tiver várias funções escutando em filas diferentes, o SDK as chamará em paralelo quando as mensagens forem recebidas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="464ce-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="464ce-145">O mesmo é verdadeiro quando várias mensagens são recebidas para uma única fila.</span><span class="sxs-lookup"><span data-stu-id="464ce-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="464ce-146">Por padrão, o SDK obtém um lote de 16 mensagens de fila por vez e executa a função que as processa em paralelo.</span><span class="sxs-lookup"><span data-stu-id="464ce-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="464ce-147">[O tamanho do lote é configurável](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="464ce-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="464ce-148">Quando o número que está sendo processado chega até a metade do tamanho do lote, o SDK obtém outro lote e começa a processar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="464ce-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="464ce-149">Portanto, o número máximo de mensagens simultâneas que estão sendo processadas por função é uma vez e meia o tamanho do lote.</span><span class="sxs-lookup"><span data-stu-id="464ce-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="464ce-150">Esse limite se aplica separadamente a cada função que tem um atributo **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="464ce-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="464ce-151">Se você não quiser uma execução paralela para mensagens recebidas em uma fila, defina o tamanho do lote como 1.</span><span class="sxs-lookup"><span data-stu-id="464ce-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="464ce-152">Obter fila ou metadados de mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="464ce-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="464ce-153">Você pode obter as propriedades da mensagem a seguir adicionando parâmetros à assinatura do método:</span><span class="sxs-lookup"><span data-stu-id="464ce-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="464ce-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="464ce-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="464ce-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="464ce-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="464ce-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="464ce-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="464ce-157">**string** queueTrigger (contém o texto da mensagem)</span><span class="sxs-lookup"><span data-stu-id="464ce-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="464ce-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="464ce-158">**string** id</span></span>
* <span data-ttu-id="464ce-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="464ce-159">**string** popReceipt</span></span>
* <span data-ttu-id="464ce-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="464ce-160">**int** dequeueCount</span></span>

<span data-ttu-id="464ce-161">Se você quiser trabalhar diretamente com a API de armazenamento do Azure, também é possível adicionar um parâmetro **CloudStorageAccount** .</span><span class="sxs-lookup"><span data-stu-id="464ce-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="464ce-162">O exemplo a seguir grava todos os metadados em um log de aplicativo de informações.</span><span class="sxs-lookup"><span data-stu-id="464ce-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="464ce-163">No exemplo, tanto logMessage quanto queueTrigger contém o conteúdo da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="464ce-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="464ce-164">Este é um log de exemplo gravado pelo código de exemplo:</span><span class="sxs-lookup"><span data-stu-id="464ce-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="464ce-165">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="464ce-165">Graceful shutdown</span></span>
<span data-ttu-id="464ce-166">Uma função que é executada em um Trabalho Web contínuo pode aceitar um parâmetro **CancellationToken** que permite ao sistema operacional notificar a função quando o Trabalho Web está prestes a ser encerrado.</span><span class="sxs-lookup"><span data-stu-id="464ce-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="464ce-167">Você pode usar essa notificação para certificar-se de que a função não finalize inesperadamente de uma maneira que os dados fiquem em um estado inconsistente.</span><span class="sxs-lookup"><span data-stu-id="464ce-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="464ce-168">O exemplo a seguir mostra como verificar se há eminência de encerramento do trabalho Web em uma função.</span><span class="sxs-lookup"><span data-stu-id="464ce-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="464ce-169">**Observação:** o painel pode não mostrar corretamente o status e a saída das funções que foram desligadas.</span><span class="sxs-lookup"><span data-stu-id="464ce-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="464ce-170">Para obter mais informações, consulte [Desligamento normal dos trabalhos Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="464ce-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="464ce-171">Como criar uma mensagem da fila durante o processamento de uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="464ce-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="464ce-172">Para gravar uma função que cria uma nova mensagem da fila, use o atributo **Queue** .</span><span class="sxs-lookup"><span data-stu-id="464ce-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="464ce-173">Como **QueueTrigger**, você passa o nome da fila como uma cadeia de caracteres ou pode [definir o nome da fila dinamicamente](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="464ce-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="464ce-174">Mensagens da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="464ce-174">String queue messages</span></span>
<span data-ttu-id="464ce-175">O exemplo de código não síncrono a seguir cria uma nova mensagem de fila na fila denominada "outputqueue" com o mesmo conteúdo que a mensagem da fila recebida na fila denominada "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="464ce-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="464ce-176">(Para funções assíncronas, use **IAsyncCollector<T>** , conforme mostrado posteriormente nesta seção.)</span><span class="sxs-lookup"><span data-stu-id="464ce-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="464ce-177">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="464ce-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="464ce-178">Para criar uma mensagem da fila que contenha um POCO em vez de uma cadeia de caracteres, passe o tipo POCO como um parâmetro de saída para o construtor de atributo **Queue** .</span><span class="sxs-lookup"><span data-stu-id="464ce-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="464ce-179">O SDK serializa automaticamente o objeto em JSON.</span><span class="sxs-lookup"><span data-stu-id="464ce-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="464ce-180">Uma mensagem da fila sempre é criada, mesmo que o objeto seja nulo.</span><span class="sxs-lookup"><span data-stu-id="464ce-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="464ce-181">Criar várias mensagens ou em funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="464ce-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="464ce-182">Para criar várias mensagens, crie o tipo de parâmetro para a fila de saída **ICollector<T>** ou **IAsyncCollector<T>**, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="464ce-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="464ce-183">Cada mensagem da fila é criada imediatamente quando o método **Add** é chamado.</span><span class="sxs-lookup"><span data-stu-id="464ce-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="464ce-184">Tipos com os quais o atributo Queue funciona</span><span class="sxs-lookup"><span data-stu-id="464ce-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="464ce-185">Você pode usar o atributo **Queue** nos seguintes tipos de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="464ce-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="464ce-186">**out string** (criará a mensagem da fila se o valor do parâmetro não for nulo quando a função terminar)</span><span class="sxs-lookup"><span data-stu-id="464ce-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="464ce-187">**out byte[]** (funciona como **string**)</span><span class="sxs-lookup"><span data-stu-id="464ce-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="464ce-188">**out CloudQueueMessage** (funciona como **string**)</span><span class="sxs-lookup"><span data-stu-id="464ce-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="464ce-189">**out POCO** (um tipo serializável; criará uma mensagem com um objeto nulo se o parâmetro for nulo quando a função terminar)</span><span class="sxs-lookup"><span data-stu-id="464ce-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="464ce-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="464ce-190">**ICollector**</span></span>
* <span data-ttu-id="464ce-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="464ce-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="464ce-192">**CloudQueue** (para a criação de mensagens manualmente usando a API de Armazenamento do Azure diretamente)</span><span class="sxs-lookup"><span data-stu-id="464ce-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="464ce-193">Usar atributos do SDK de Trabalhos Web no corpo de uma função</span><span class="sxs-lookup"><span data-stu-id="464ce-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="464ce-194">Se precisar realizar algum trabalho em sua função antes de usar um atributo do SDK de Trabalhos Web como **Queue** , **Blob** ou **Table** , você poderá usar a interface **IBinder** .</span><span class="sxs-lookup"><span data-stu-id="464ce-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="464ce-195">O exemplo a seguir usa uma mensagem da fila de entrada e cria uma nova mensagem com o mesmo conteúdo em uma fila de saída.</span><span class="sxs-lookup"><span data-stu-id="464ce-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="464ce-196">O nome da fila de saída é definido pelo código no corpo da função.</span><span class="sxs-lookup"><span data-stu-id="464ce-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="464ce-197">A interface **IBinder** também pode ser usada com os atributos **Table** e **Blob**.</span><span class="sxs-lookup"><span data-stu-id="464ce-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="464ce-198">Como ler e gravar blobs e tabelas ao processar uma mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="464ce-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="464ce-199">Os atributos **Blob** e **Table** permitem que você leia e grave os blobs e as tabelas.</span><span class="sxs-lookup"><span data-stu-id="464ce-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="464ce-200">Os exemplos nesta seção se aplicam a blobs.</span><span class="sxs-lookup"><span data-stu-id="464ce-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="464ce-201">Para obter exemplos de código que mostram como disparar processos quando blobs são criados ou atualizados, consulte [Como usar o armazenamento de blobs do Azure com o SDK de Trabalhos Web](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) e para obter exemplos de código que leem e gravam as tabelas, consulte [Como usar o armazenamento de tabelas do Azure com o SDK de Trabalhos Web](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="464ce-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="464ce-202">Mensagens da fila de cadeia de caracteres que disparam operações de blob</span><span class="sxs-lookup"><span data-stu-id="464ce-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="464ce-203">Para uma mensagem da fila que contém uma cadeia de caracteres, **queueTrigger** é um espaço reservado que você pode utilizar no parâmetro **blobPath** do atributo **Blob** que inclui o conteúdo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="464ce-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="464ce-204">O exemplo a seguir utiliza objetos **Stream** para ler e gravar os blobs.</span><span class="sxs-lookup"><span data-stu-id="464ce-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="464ce-205">A mensagem da fila é o nome de um blob localizado no contêiner de textblobs.</span><span class="sxs-lookup"><span data-stu-id="464ce-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="464ce-206">Uma cópia de blob com "-new" acrescentado ao nome é criada no mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="464ce-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="464ce-207">O construtor do atributo **Blob** aceita um parâmetro **blobPath** que especifica o nome do blob e o contêiner.</span><span class="sxs-lookup"><span data-stu-id="464ce-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="464ce-208">Para obter mais informações sobre esse espaço reservado, consulte [Como usar o Armazenamento de Blobs do Azure com o SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="464ce-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="464ce-209">Quando o atributo decora um objeto **Stream**, outro parâmetro de construtor especifica o modo **FileAccess** como leitura, gravação ou leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="464ce-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="464ce-210">O exemplo a seguir utiliza um objeto **CloudBlockBlob** para excluir um blob.</span><span class="sxs-lookup"><span data-stu-id="464ce-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="464ce-211">A mensagem da fila é o nome do blob.</span><span class="sxs-lookup"><span data-stu-id="464ce-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="464ce-212">Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="464ce-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="464ce-213">Para um POCO armazenado como JSON na mensagem da fila, é possível utilizar espaços reservados que nomeiam propriedades do objeto no parâmetro **blobPath** do atributo **Queue**.</span><span class="sxs-lookup"><span data-stu-id="464ce-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="464ce-214">Também é possível utilizar os nomes de propriedade de metadados de fila como espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="464ce-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="464ce-215">Consulte [Obter a fila ou os metadados de mensagem da fila](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="464ce-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="464ce-216">O exemplo a seguir copia um blob para um novo blob com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="464ce-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="464ce-217">A mensagem da fila é um objeto **BlobInformation** que inclui as propriedades **BlobName** e **BlobNameWithoutExtension**.</span><span class="sxs-lookup"><span data-stu-id="464ce-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="464ce-218">Os nomes de propriedade são usados como espaços reservados no caminho de blob para os atributos **Blob** .</span><span class="sxs-lookup"><span data-stu-id="464ce-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="464ce-219">O SDK usa o [pacote NuGet Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) para serializar e desserializar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="464ce-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="464ce-220">Se criar mensagens de fila em um programa que não usa o SDK de Trabalhos Web, você poderá escrever código como o exemplo a seguir para criar uma mensagem de fila POCO que o SDK possa analisar.</span><span class="sxs-lookup"><span data-stu-id="464ce-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="464ce-221">Se você precisar fazer algum trabalho em sua função antes de associar um blob a um objeto, você poderá usar o atributo no corpo da função, conforme mostrado em [Usar o SDK do WebJobs no corpo de uma função](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="464ce-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="464ce-222">Tipos com os quais você pode usar o atributo Blob</span><span class="sxs-lookup"><span data-stu-id="464ce-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="464ce-223">O atributo **Blob** pode ser usado com os seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="464ce-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="464ce-224">**Stream** (leitura ou gravação, especificadas usando o parâmetro de construtor FileAccess)</span><span class="sxs-lookup"><span data-stu-id="464ce-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="464ce-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="464ce-225">**TextReader**</span></span>
* <span data-ttu-id="464ce-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="464ce-226">**TextWriter**</span></span>
* <span data-ttu-id="464ce-227">**string** (leitura)</span><span class="sxs-lookup"><span data-stu-id="464ce-227">**string** (read)</span></span>
* <span data-ttu-id="464ce-228">**out string** (gravação; criará um blob somente se o parâmetro de cadeia de caracteres não for nulo quando a função retornar)</span><span class="sxs-lookup"><span data-stu-id="464ce-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="464ce-229">POCO (leitura)</span><span class="sxs-lookup"><span data-stu-id="464ce-229">POCO (read)</span></span>
* <span data-ttu-id="464ce-230">out POCO (gravação; sempre cria um blob; criará como objeto nulo se o parâmetro POCO for nulo quando a função retornar)</span><span class="sxs-lookup"><span data-stu-id="464ce-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="464ce-231">**CloudBlobStream** (gravação)</span><span class="sxs-lookup"><span data-stu-id="464ce-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="464ce-232">**ICloudBlob** (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="464ce-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="464ce-233">**CloudBlockBlob** (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="464ce-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="464ce-234">**CloudPageBlob** (leitura ou gravação)</span><span class="sxs-lookup"><span data-stu-id="464ce-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="464ce-235">Como tratar mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="464ce-235">How to handle poison messages</span></span>
<span data-ttu-id="464ce-236">As mensagens cujo conteúdo faz com que uma função falhe são chamadas de *mensagens suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="464ce-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="464ce-237">Quando a função falhar, a mensagem da fila não é excluída e eventualmente é captada novamente, fazendo com que o ciclo seja repetido.</span><span class="sxs-lookup"><span data-stu-id="464ce-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="464ce-238">O SDK pode interromper automaticamente o ciclo após algumas iterações, ou você fazê-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="464ce-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="464ce-239">Manipulação automática de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="464ce-239">Automatic poison message handling</span></span>
<span data-ttu-id="464ce-240">O SDK chamará uma função até 5 vezes para processar uma mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="464ce-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="464ce-241">Se a quinta tentativa falhar, a mensagem é movida para uma fila de mensagens suspeitas.</span><span class="sxs-lookup"><span data-stu-id="464ce-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="464ce-242">Veja como configurar o número máximo de tentativas em [Como definir opções de configuração](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="464ce-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="464ce-243">A fila de mensagens suspeita é denominada *{originalqueuename}*-suspeita.</span><span class="sxs-lookup"><span data-stu-id="464ce-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="464ce-244">Você pode gravar uma função para processar as mensagens da fila de mensagens suspeitas registrando-as ou enviando uma notificação de que a atenção manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="464ce-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="464ce-245">No exemplo a seguir a função **CopyBlob** falhará quando uma mensagem da fila tiver o nome de um blob que não existe.</span><span class="sxs-lookup"><span data-stu-id="464ce-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="464ce-246">Quando isso acontece, a mensagem será movida da fila copyblobqueue para a fila copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="464ce-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="464ce-247">O **ProcessPoisonMessage** , em seguida, registra a mensagem suspeita.</span><span class="sxs-lookup"><span data-stu-id="464ce-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

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

<span data-ttu-id="464ce-248">A ilustração a seguir mostra a saída do console dessas funções quando uma mensagem suspeita é processada.</span><span class="sxs-lookup"><span data-stu-id="464ce-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Saída do console para tratamento de mensagens suspeitas](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="464ce-250">Manipulação manual de mensagens suspeitas</span><span class="sxs-lookup"><span data-stu-id="464ce-250">Manual poison message handling</span></span>
<span data-ttu-id="464ce-251">É possível obter o número de vezes que uma mensagem foi selecionada para processamento, bastando adicionar um parâmetro **int** chamado **dequeueCount** à sua função.</span><span class="sxs-lookup"><span data-stu-id="464ce-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="464ce-252">Você pode, então, verificar a contagem de remoção da fila no código de função e realizar seu próprio tratamento de mensagem suspeita quando o número exceder um limite, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="464ce-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="464ce-253">Como definir as Opções de Configuração</span><span class="sxs-lookup"><span data-stu-id="464ce-253">How to set configuration options</span></span>
<span data-ttu-id="464ce-254">É possível utilizar o tipo **JobHostConfiguration** para definir as seguintes opções de configuração:</span><span class="sxs-lookup"><span data-stu-id="464ce-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="464ce-255">Definir as cadeias de conexão do SDK no código.</span><span class="sxs-lookup"><span data-stu-id="464ce-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="464ce-256">Definir as configurações de **QueueTrigger** como contagem máxima de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="464ce-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="464ce-257">Obtenha nomes de fila por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="464ce-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="464ce-258">Defina as cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="464ce-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="464ce-259">A definição das cadeias de conexão do SDK no código lhe permite usar seus próprios nomes de cadeia de conexão em arquivos de configuração ou variáveis de ambiente, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="464ce-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="464ce-260">Definir configurações de QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="464ce-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="464ce-261">Você pode definir as seguintes configurações que se aplicam ao processamento de mensagem de fila:</span><span class="sxs-lookup"><span data-stu-id="464ce-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="464ce-262">O número máximo de mensagens da fila que são recebidas simultaneamente a serem executadas em paralelo (o padrão é 16).</span><span class="sxs-lookup"><span data-stu-id="464ce-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="464ce-263">O número máximo de tentativas antes de uma mensagem da fila ser enviada para uma fila de suspeita (o padrão é 5).</span><span class="sxs-lookup"><span data-stu-id="464ce-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="464ce-264">O tempo máximo de espera antes de sondar novamente quando uma fila está vazia (o padrão é 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="464ce-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="464ce-265">O exemplo a seguir mostra como definir essas configurações:</span><span class="sxs-lookup"><span data-stu-id="464ce-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="464ce-266">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="464ce-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="464ce-267">Às vezes você deseja especificar um nome de fila, um nome de blob ou contêiner ou um nome de tabela no código em vez de embuti-lo no código.</span><span class="sxs-lookup"><span data-stu-id="464ce-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="464ce-268">Por exemplo, você talvez queira especificar o nome da fila para **QueueTrigger** em um arquivo de configuração ou variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="464ce-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="464ce-269">Você pode fazer isso passando um objeto **NameResolver** para o tipo **JobHostConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="464ce-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="464ce-270">Você inclui espaços reservados especiais entre sinais de percentual (%) em parâmetros do construtor de atributos do SDK de Trabalhos Web e o código **NameResolver** especifica os valores reais a serem usados no lugar desses espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="464ce-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="464ce-271">Por exemplo, suponha que você deseje usar uma fila denominada logqueuetest no ambiente de teste e uma denominada logqueueprod na produção.</span><span class="sxs-lookup"><span data-stu-id="464ce-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="464ce-272">Ao invés de um nome de fila embutido em código, você deseja especificar o nome de uma entrada na coleção **appSettings** que tem o nome da fila real.</span><span class="sxs-lookup"><span data-stu-id="464ce-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="464ce-273">Se a chave **appSettings** for logqueue, sua função pode parecer com o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="464ce-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="464ce-274">A classe **NameResolver** pode, em seguida, obter o nome da fila de **appSettings**, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="464ce-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="464ce-275">Você passa a classe **NameResolver** para o objeto **JobHost**, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="464ce-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="464ce-276">**Observação:** os nomes de fila, tabela e blob são resolvidos sempre que uma função é chamada, mas os nomes de contêineres de blob são resolvidos somente quando o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="464ce-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="464ce-277">Você não pode alterar o nome do contêiner de blob enquanto o trabalho está em execução.</span><span class="sxs-lookup"><span data-stu-id="464ce-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="464ce-278">Como disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="464ce-278">How to trigger a function manually</span></span>
<span data-ttu-id="464ce-279">Para disparar uma função manualmente, use o método **Call** ou **CallAsync** no objeto **JobHost** e no atributo **NoAutomaticTrigger** na função, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="464ce-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

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

## <a name="how-to-write-logs"></a><span data-ttu-id="464ce-280">Como gravar logs</span><span class="sxs-lookup"><span data-stu-id="464ce-280">How to write logs</span></span>
<span data-ttu-id="464ce-281">O painel mostra logs em dois lugares: na página do Trabalho Web e na página de determinada invocação do Trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="464ce-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Logs na página do Trabalho Web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Logs na página de invocação de função](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="464ce-284">A saída de métodos de console que você chama em uma função ou no método **Main()** aparece na página Painel para o trabalho Web, não na página de uma invocação de método específica.</span><span class="sxs-lookup"><span data-stu-id="464ce-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="464ce-285">A saída do objeto TextWriter obtido de um parâmetro na assinatura do método é exibida na página Painel para uma invocação de método.</span><span class="sxs-lookup"><span data-stu-id="464ce-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="464ce-286">A saída do console não pode ser vinculada a uma invocação de método específica porque o console é single-threaded, embora muitas funções de trabalho possam estar sendo executadas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="464ce-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="464ce-287">É por isso que o SDK fornece a cada invocação de função seu próprio objeto de gravador de log exclusivo.</span><span class="sxs-lookup"><span data-stu-id="464ce-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="464ce-288">Para gravar [logs de rastreamento do aplicativo](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (cria logs marcados como INFO) e **Console.Error** (cria logs marcados como ERROR).</span><span class="sxs-lookup"><span data-stu-id="464ce-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="464ce-289">Uma alternativa é usar [Rastreamento ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que fornece os níveis Detalhado, de Aviso e Crítico, além de Informações e Erro.</span><span class="sxs-lookup"><span data-stu-id="464ce-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="464ce-290">Os logs de rastreamento de aplicativo aparecem nos arquivos de log de aplicativo Web, nas tabelas do Azure ou nos blobs do Azure, dependendo de como você configura seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="464ce-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="464ce-291">Assim como ocorre com toda a saída do console, os 100 logs de aplicativos mais recentes também são exibidos na página Painel do Trabalho Web, não na página de uma invocação de função.</span><span class="sxs-lookup"><span data-stu-id="464ce-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="464ce-292">A saída do console aparecerá no painel somente se o programa estiver em execução em um Trabalho Web do Azure, não se o programa estiver em execução localmente ou em outro ambiente.</span><span class="sxs-lookup"><span data-stu-id="464ce-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="464ce-293">É possível desabilitar o log definindo a cadeia de conexão do painel de controle como null.</span><span class="sxs-lookup"><span data-stu-id="464ce-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="464ce-294">Para obter mais informações, consulte [Como definir as Opções de Configuração](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="464ce-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="464ce-295">O exemplo a seguir mostra várias maneiras de gravar logs:</span><span class="sxs-lookup"><span data-stu-id="464ce-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="464ce-296">No painel do SDK de Trabalhos Web, a saída do objeto **TextWriter** aparece quando você acessa a página de invocação de uma função específica e seleciona **Ativar/Desativar Saída**:</span><span class="sxs-lookup"><span data-stu-id="464ce-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Link de invocação](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Logs na página de invocação de função](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="464ce-299">No painel do SDK do Web Jobs, as 100 linhas da saída do Console mais recentes são mostradas quando você vai até a página do Web Jobs (não da invocação de função) e selecione **Alternar Saída**.</span><span class="sxs-lookup"><span data-stu-id="464ce-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Ativar/Desativar Saída](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="464ce-301">Em um Trabalho Web contínuo, os logs de aplicativo são mostrados em /data/jobs/continuous/*{nomedotrabalhoweb}*/job_log.txt no sistema de arquivos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="464ce-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="464ce-302">Em um blob do Azure, os logs de aplicativo se parecem com este: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Olá, mundo!,</span><span class="sxs-lookup"><span data-stu-id="464ce-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="464ce-303">Em uma tabela do Azure, os logs de **Console.Out** e **Console.Error** têm esta aparência:</span><span class="sxs-lookup"><span data-stu-id="464ce-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Log de informações na tabela](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Log de erros na tabela](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="464ce-306">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="464ce-306">Next steps</span></span>
<span data-ttu-id="464ce-307">Este guia forneceu exemplos de código que mostram como lidar com cenários comuns para trabalhar com filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="464ce-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="464ce-308">Para obter mais informações sobre como usar o Azure WebJobs e o SDK do WebJobs, consulte [Recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="464ce-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

