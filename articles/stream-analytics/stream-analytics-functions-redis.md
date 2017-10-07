---
title: "processamento em tempo real de análise de aaaStream para funções do Azure | Microsoft Docs"
description: "Saiba como toouse uma função do Azure conectadas a uma fila de barramento de serviço, toopopulate um Cache Redis do Azure da saída de saudação de um trabalho do Stream Analytics."
keywords: "transmissão de dados, cache redis, fila do barramento de serviço"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="60814-104">Como os dados de toostore do Azure Stream Analytics em um Cache Redis do Azure usando funções do Azure</span><span class="sxs-lookup"><span data-stu-id="60814-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="60814-105">Análise de fluxo do Azure permite desenvolver e implantar as informações em tempo real do toogain soluções de baixo custo de dispositivos, sensores, infraestrutura e aplicativos ou qualquer fluxo de dados rapidamente.</span><span class="sxs-lookup"><span data-stu-id="60814-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="60814-106">Ele habilita vários casos de uso, como o gerenciamento e monitoramento em tempo real, o comando e controle, a detecção de fraudes, carros conectados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="60814-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="60814-107">Em muitos cenários, convém toostore dados gerados pelo Azure Stream Analytics em um repositório de dados distribuído como um cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="60814-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="60814-108">Suponha que você faça parte de uma empresa de telecomunicações.</span><span class="sxs-lookup"><span data-stu-id="60814-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="60814-109">Você está tentando fraude SIM toodetect onde provenientes de várias chamadas Olá mesma identidade, no hello mesmo tempo, mas em diferentes geograficamente locais.</span><span class="sxs-lookup"><span data-stu-id="60814-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="60814-110">Você fica encarregado de armazenar todos os Olá potencial fraudulentas chamadas telefônicas em um cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="60814-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="60814-111">Neste blog, fornecemos diretrizes sobre como você pode concluir sua tarefa facilmente.</span><span class="sxs-lookup"><span data-stu-id="60814-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="60814-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="60814-112">Prerequisites</span></span>
<span data-ttu-id="60814-113">Olá completa [detecção de fraudes em tempo real] [ fraud-detection] passo a passo para ASA</span><span class="sxs-lookup"><span data-stu-id="60814-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="60814-114">Visão geral da arquitetura</span><span class="sxs-lookup"><span data-stu-id="60814-114">Architecture Overview</span></span>
![Captura de tela da arquitetura](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="60814-116">Conforme mostrado na saudação anterior figura, análise de fluxo permite toobe de dados de entrada de streaming consultado e enviados tooan saída.</span><span class="sxs-lookup"><span data-stu-id="60814-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="60814-117">Com base na saída de hello, funções do Azure pode disparar algum tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="60814-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="60814-118">Neste blog se concentrar na parte de funções do Azure de saudação desse pipeline ou hello mais especificamente o disparo de um evento que armazena dados fraudulentos no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="60814-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="60814-119">Depois de concluir a saudação [detecção de fraudes em tempo real] [ fraud-detection] tutorial, você tem uma entrada (um hub de eventos), uma consulta e uma saída (armazenamento de blob) já configurado e em execução.</span><span class="sxs-lookup"><span data-stu-id="60814-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="60814-120">Este blog, alteramos Olá saída toouse uma fila do barramento de serviço em vez disso.</span><span class="sxs-lookup"><span data-stu-id="60814-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="60814-121">Depois disso, se conectar a uma fila de toothis de função do Azure.</span><span class="sxs-lookup"><span data-stu-id="60814-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="60814-122">Criar e conectar-se a uma saída de Fila do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="60814-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="60814-123">toocreate uma fila do barramento de serviço, siga as etapas 1 e 2 da seção .NET Olá [começar com filas do barramento de serviço][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="60814-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="60814-124">Agora vamos conectar Olá toohello Stream Analytics trabalho em fila que foi criado no hello anterior detalhado de detecção de fraudes.</span><span class="sxs-lookup"><span data-stu-id="60814-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="60814-125">No portal do Azure de Olá, vá toohello **saídas** folha do seu trabalho e selecione **adicionar** na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="60814-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![Adição de saídas](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="60814-127">Escolha **fila do barramento de serviço** como Olá **coletor** e siga as instruções de saudação na tela hello.</span><span class="sxs-lookup"><span data-stu-id="60814-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="60814-128">Namespace de saudação toochoose-se de saudação fila do barramento de serviço que você criou na [começar com filas do barramento de serviço][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="60814-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="60814-129">Quando tiver terminado, clique botão "direita" hello.</span><span class="sxs-lookup"><span data-stu-id="60814-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="60814-130">Especifique Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="60814-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="60814-131">**Formato do Serializador de Evento**: JSON</span><span class="sxs-lookup"><span data-stu-id="60814-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="60814-132">**Codificação**: UTF8</span><span class="sxs-lookup"><span data-stu-id="60814-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="60814-133">**FORMATO**: linha separada</span><span class="sxs-lookup"><span data-stu-id="60814-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="60814-134">Clique em Olá **criar** botão tooadd essa fonte e tooverify que Stream Analytics pode se conectar com êxito toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="60814-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="60814-135">Em Olá **consulta** guia, substitua a consulta atual Olá pela seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="60814-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="60814-136">Substituir * [seu nome de barramento de serviço] * com o nome de saída de hello criado na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="60814-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="60814-137">Criar um Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="60814-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="60814-138">Criar um cache Redis do Azure seguindo seção .NET Olá [como tooUse Cache Redis do Azure] [ use-rediscache] até Olá seção chamada ***configurar clientes de cache Olá***.</span><span class="sxs-lookup"><span data-stu-id="60814-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="60814-139">Uma vez concluído, você terá um novo Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="60814-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="60814-140">Em **todas as configurações**, selecione **chaves de acesso** e anote Olá ***cadeia de caracteres de conexão primária***.</span><span class="sxs-lookup"><span data-stu-id="60814-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![Captura de tela da arquitetura](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="60814-142">Criar uma Função do Azure</span><span class="sxs-lookup"><span data-stu-id="60814-142">Create an Azure Function</span></span>
<span data-ttu-id="60814-143">Execute [criar sua primeira função Azure] [ functions-getstarted] tooget tutorial de Introdução com funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="60814-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="60814-144">Se você já tiver uma função do Azure seria como toouse e pular muito[tooRedis Cache de gravação](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="60814-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="60814-145">No portal de hello, selecione Serviços de aplicativos de navegação do lado esquerdo Olá, clique em site do aplicativo de sua função do Azure aplicativo nome tooget toohello da função.</span><span class="sxs-lookup"><span data-stu-id="60814-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="60814-146">![Captura de tela da lista de função dos Serviços de Aplicativos](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="60814-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="60814-147">Clique em **Nova função > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="60814-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="60814-148">Para Olá campos a seguir, siga estas instruções:</span><span class="sxs-lookup"><span data-stu-id="60814-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="60814-149">**Nome da fila**: Olá mesmo nome como nome hello inserida ao criar fila de saudação em [começar com filas do barramento de serviço] [ servicebus-getstarted] (não o nome Olá Olá do barramento do serviço).</span><span class="sxs-lookup"><span data-stu-id="60814-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="60814-150">Verifique se que você usar a fila de saudação toohello conectado, análise de fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="60814-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="60814-151">**Conexão do Barramento de Serviço**: selecione **Adicionar uma cadeia de conexão**.</span><span class="sxs-lookup"><span data-stu-id="60814-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="60814-152">cadeia de conexão toofind hello, portal clássico do vá toohello, selecione **Service Bus**, Olá barramento de serviço que você criou, e **informações de conexão** na parte inferior da saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="60814-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="60814-153">Verifique se que você estiver na tela principal hello nesta página.</span><span class="sxs-lookup"><span data-stu-id="60814-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="60814-154">Copie e cole a cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="60814-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="60814-155">Se sentir livre tooenter qualquer nome de conexão.</span><span class="sxs-lookup"><span data-stu-id="60814-155">Feel free tooenter any connection name.</span></span>
     
       ![Captura de tela da conexão do Barramento de Serviço](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="60814-157">**AccessRights**: escolha **Gerenciar**</span><span class="sxs-lookup"><span data-stu-id="60814-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="60814-158">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="60814-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="60814-159">Gravação tooRedis Cache</span><span class="sxs-lookup"><span data-stu-id="60814-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="60814-160">Agora, criamos uma função do Azure que lê de uma Fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="60814-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="60814-161">Resta toodo é usar nossa função toowrite este toohello de dados Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="60814-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="60814-162">Selecione o recém-criado **ServiceBusQueueTrigger**e clique em **configurações do aplicativo de função** em Olá canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="60814-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="60814-163">Selecione **ir tooApp serviço Configurações > Configurações > configurações do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="60814-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="60814-164">Na seção de cadeias de caracteres de Conexão do hello, crie um nome em Olá **nome** seção.</span><span class="sxs-lookup"><span data-stu-id="60814-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="60814-165">Cole a cadeia de caracteres de conexão primária Olá encontrado no hello **criar um Cache Redis** intervir Olá **valor** seção.</span><span class="sxs-lookup"><span data-stu-id="60814-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="60814-166">Selecione **Personalizado**, no lugar indicado como **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="60814-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="60814-167">Clique em **salvar** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="60814-167">Click **Save** at hello top.</span></span>
   
    ![Captura de tela da conexão do Barramento de Serviço](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="60814-169">Agora volte toohello configurações de serviço de aplicativo e selecione **Ferramentas > Editor de aplicativo de serviço (visualização) > em > vá**.</span><span class="sxs-lookup"><span data-stu-id="60814-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Captura de tela da conexão do Barramento de Serviço](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="60814-171">Em um editor de sua escolha, crie um arquivo JSON chamado **Project** com hello a seguir e salve-o disco local tooyour.</span><span class="sxs-lookup"><span data-stu-id="60814-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="60814-172">Carregar esse arquivo no diretório raiz de saudação de sua função (não WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="60814-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="60814-173">Você deve ver um arquivo chamado **Project** aparecem automaticamente, confirmando que o Nuget Olá pacotes "Stackexchange" e "Newtonsoft. JSON" foram importados.</span><span class="sxs-lookup"><span data-stu-id="60814-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="60814-174">Em Olá **run.csx** arquivo, substitua código pré-gerado Olá Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="60814-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="60814-175">Na função de lazyConnection hello, substitua "CONN NAME" pelo nome de saudação criado na etapa 2 do **armazenar dados em cache do Redis Olá**.</span><span class="sxs-lookup"><span data-stu-id="60814-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="60814-176">Iniciar o trabalho de análise de fluxo de saudação</span><span class="sxs-lookup"><span data-stu-id="60814-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="60814-177">Inicie o aplicativo de telcodatagen.exe hello.</span><span class="sxs-lookup"><span data-stu-id="60814-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="60814-178">uso de saudação é o seguinte:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="60814-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="60814-179">Na folha de trabalho do Stream Analytics Olá no portal de saudação, clique em **iniciar** na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="60814-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![Captura de tela de início do trabalho](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="60814-181">Em Olá **Iniciar trabalho** folha que aparece, selecione **agora** e, em seguida, clique em Olá **iniciar** botão Olá final da tela hello.</span><span class="sxs-lookup"><span data-stu-id="60814-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="60814-182">status do trabalho Olá altera tooStarting e depois de algum tempo tooRunning de alterações.</span><span class="sxs-lookup"><span data-stu-id="60814-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![Captura de tela de seleção de início do horário de trabalho](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="60814-184">Executar a solução e os resultados da verificação</span><span class="sxs-lookup"><span data-stu-id="60814-184">Run solution and check results</span></span>
<span data-ttu-id="60814-185">Voltando tooyour **ServiceBusQueueTrigger** página, agora você deve ver instruções de log.</span><span class="sxs-lookup"><span data-stu-id="60814-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="60814-186">Esses logs mostram que você obteve algo Olá fila do barramento de serviço, coloque-o em um banco de dados Olá e buscadas ele usando o tempo de saudação como chave Olá!</span><span class="sxs-lookup"><span data-stu-id="60814-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="60814-187">tooverify que os dados estiverem em seu cache Redis, vá tooyour página do cache Redis no novo portal de saudação (conforme mostrado na saudação anterior [criar um Cache Redis do Azure](#Create-an-Azure-Redis-Cache) etapa) e selecione o Console.</span><span class="sxs-lookup"><span data-stu-id="60814-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="60814-188">Agora você pode escrever Redis comandos tooconfirm que os dados estarem de fato no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="60814-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Captura de tela do Console Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="60814-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60814-190">Next steps</span></span>
<span data-ttu-id="60814-191">Estamos felizes coisas Olá novas funções do Azure Stream analytics pode fazer juntos e esperamos que isso lhe oferece novas possibilidades.</span><span class="sxs-lookup"><span data-stu-id="60814-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="60814-192">Se você tiver qualquer comentário sobre o que você deseja, sinta-se livre toouse Olá [site UserVoice do Azure](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="60814-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="60814-193">Se você for novo Microsoft Azure, você está convidado tootry fora pelo inscrever-se para uma [conta de avaliação do Azure gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60814-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="60814-194">Se tiver tooStream de nova análise, você está convidado muito[criar seu primeiro emprego de análise de fluxo](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="60814-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="60814-195">Caso precise de ajuda ou se tiver dúvidas, poste-as nos fóruns do [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) ou do [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="60814-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="60814-196">Você também pode ver Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="60814-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="60814-197">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60814-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="60814-198">Referência do desenvolvedor de C# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60814-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="60814-199">Referência do desenvolvedor em F# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60814-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="60814-200">Referência do desenvolvedor de NodeJS do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60814-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="60814-201">Gatilhos e de associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60814-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="60814-202">Como toomonitor Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="60814-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="60814-203">toostay atualizado em todas as notícias mais recentes hello e recursos, siga [ @AzureStreaming ](https://twitter.com/AzureStreaming) no Twitter.</span><span class="sxs-lookup"><span data-stu-id="60814-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
