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
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>Como os dados de toostore do Azure Stream Analytics em um Cache Redis do Azure usando funções do Azure
Análise de fluxo do Azure permite desenvolver e implantar as informações em tempo real do toogain soluções de baixo custo de dispositivos, sensores, infraestrutura e aplicativos ou qualquer fluxo de dados rapidamente. Ele habilita vários casos de uso, como o gerenciamento e monitoramento em tempo real, o comando e controle, a detecção de fraudes, carros conectados e muito mais. Em muitos cenários, convém toostore dados gerados pelo Azure Stream Analytics em um repositório de dados distribuído como um cache Redis do Azure.

Suponha que você faça parte de uma empresa de telecomunicações. Você está tentando fraude SIM toodetect onde provenientes de várias chamadas Olá mesma identidade, no hello mesmo tempo, mas em diferentes geograficamente locais. Você fica encarregado de armazenar todos os Olá potencial fraudulentas chamadas telefônicas em um cache Redis do Azure. Neste blog, fornecemos diretrizes sobre como você pode concluir sua tarefa facilmente. 

## <a name="prerequisites"></a>Pré-requisitos
Olá completa [detecção de fraudes em tempo real] [ fraud-detection] passo a passo para ASA

## <a name="architecture-overview"></a>Visão geral da arquitetura
![Captura de tela da arquitetura](./media/stream-analytics-functions-redis/architecture-overview.png)

Conforme mostrado na saudação anterior figura, análise de fluxo permite toobe de dados de entrada de streaming consultado e enviados tooan saída. Com base na saída de hello, funções do Azure pode disparar algum tipo de evento. 

Neste blog se concentrar na parte de funções do Azure de saudação desse pipeline ou hello mais especificamente o disparo de um evento que armazena dados fraudulentos no cache de saudação.
Depois de concluir a saudação [detecção de fraudes em tempo real] [ fraud-detection] tutorial, você tem uma entrada (um hub de eventos), uma consulta e uma saída (armazenamento de blob) já configurado e em execução. Este blog, alteramos Olá saída toouse uma fila do barramento de serviço em vez disso. Depois disso, se conectar a uma fila de toothis de função do Azure. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Criar e conectar-se a uma saída de Fila do Barramento de Serviço
toocreate uma fila do barramento de serviço, siga as etapas 1 e 2 da seção .NET Olá [começar com filas do barramento de serviço][servicebus-getstarted].
Agora vamos conectar Olá toohello Stream Analytics trabalho em fila que foi criado no hello anterior detalhado de detecção de fraudes.

1. No portal do Azure de Olá, vá toohello **saídas** folha do seu trabalho e selecione **adicionar** na parte superior de saudação da página de saudação.
   
    ![Adição de saídas](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Escolha **fila do barramento de serviço** como Olá **coletor** e siga as instruções de saudação na tela hello. Namespace de saudação toochoose-se de saudação fila do barramento de serviço que você criou na [começar com filas do barramento de serviço][servicebus-getstarted]. Quando tiver terminado, clique botão "direita" hello.
3. Especifique Olá valores a seguir:
   
   * **Formato do Serializador de Evento**: JSON
   * **Codificação**: UTF8
   * **FORMATO**: linha separada
4. Clique em Olá **criar** botão tooadd essa fonte e tooverify que Stream Analytics pode se conectar com êxito toohello conta de armazenamento.
5. Em Olá **consulta** guia, substitua a consulta atual Olá pela seguinte hello. Substituir * [seu nome de barramento de serviço] * com o nome de saída de hello criado na etapa 3. 
   
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

## <a name="create-an-azure-redis-cache"></a>Criar um Cache Redis do Azure
Criar um cache Redis do Azure seguindo seção .NET Olá [como tooUse Cache Redis do Azure] [ use-rediscache] até Olá seção chamada ***configurar clientes de cache Olá***.
Uma vez concluído, você terá um novo Cache Redis. Em **todas as configurações**, selecione **chaves de acesso** e anote Olá ***cadeia de caracteres de conexão primária***.

![Captura de tela da arquitetura](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Criar uma Função do Azure
Execute [criar sua primeira função Azure] [ functions-getstarted] tooget tutorial de Introdução com funções do Azure. Se você já tiver uma função do Azure seria como toouse e pular muito[tooRedis Cache de gravação](#Writing-to-Redis-Cache)

1. No portal de hello, selecione Serviços de aplicativos de navegação do lado esquerdo Olá, clique em site do aplicativo de sua função do Azure aplicativo nome tooget toohello da função.
    ![Captura de tela da lista de função dos Serviços de Aplicativos](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Clique em **Nova função > ServiceBusQueueTrigger – C#**. Para Olá campos a seguir, siga estas instruções:
   
   * **Nome da fila**: Olá mesmo nome como nome hello inserida ao criar fila de saudação em [começar com filas do barramento de serviço] [ servicebus-getstarted] (não o nome Olá Olá do barramento do serviço). Verifique se que você usar a fila de saudação toohello conectado, análise de fluxo de saída.
   * **Conexão do Barramento de Serviço**: selecione **Adicionar uma cadeia de conexão**. cadeia de conexão toofind hello, portal clássico do vá toohello, selecione **Service Bus**, Olá barramento de serviço que você criou, e **informações de conexão** na parte inferior da saudação da tela hello. Verifique se que você estiver na tela principal hello nesta página. Copie e cole a cadeia de caracteres de conexão de saudação. Se sentir livre tooenter qualquer nome de conexão.
     
       ![Captura de tela da conexão do Barramento de Serviço](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights**: escolha **Gerenciar**
3. Clique em **Criar**

## <a name="writing-tooredis-cache"></a>Gravação tooRedis Cache
Agora, criamos uma função do Azure que lê de uma Fila do Barramento de Serviço. Resta toodo é usar nossa função toowrite este toohello de dados Redis Cache. 

1. Selecione o recém-criado **ServiceBusQueueTrigger**e clique em **configurações do aplicativo de função** em Olá canto superior direito. Selecione **ir tooApp serviço Configurações > Configurações > configurações do aplicativo**
2. Na seção de cadeias de caracteres de Conexão do hello, crie um nome em Olá **nome** seção. Cole a cadeia de caracteres de conexão primária Olá encontrado no hello **criar um Cache Redis** intervir Olá **valor** seção. Selecione **Personalizado**, no lugar indicado como **Banco de Dados SQL**.
3. Clique em **salvar** na parte superior da saudação.
   
    ![Captura de tela da conexão do Barramento de Serviço](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Agora volte toohello configurações de serviço de aplicativo e selecione **Ferramentas > Editor de aplicativo de serviço (visualização) > em > vá**.
   
    ![Captura de tela da conexão do Barramento de Serviço](./media/stream-analytics-functions-redis/app-service-editor.png)
5. Em um editor de sua escolha, crie um arquivo JSON chamado **Project** com hello a seguir e salve-o disco local tooyour.
   
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
6. Carregar esse arquivo no diretório raiz de saudação de sua função (não WWWROOT). Você deve ver um arquivo chamado **Project** aparecem automaticamente, confirmando que o Nuget Olá pacotes "Stackexchange" e "Newtonsoft. JSON" foram importados.
7. Em Olá **run.csx** arquivo, substitua código pré-gerado Olá Olá código a seguir. Na função de lazyConnection hello, substitua "CONN NAME" pelo nome de saudação criado na etapa 2 do **armazenar dados em cache do Redis Olá**.

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

## <a name="start-hello-stream-analytics-job"></a>Iniciar o trabalho de análise de fluxo de saudação
1. Inicie o aplicativo de telcodatagen.exe hello. uso de saudação é o seguinte:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. Na folha de trabalho do Stream Analytics Olá no portal de saudação, clique em **iniciar** na parte superior de saudação da página de saudação.
   
    ![Captura de tela de início do trabalho](./media/stream-analytics-functions-redis/starting-job.png)
3. Em Olá **Iniciar trabalho** folha que aparece, selecione **agora** e, em seguida, clique em Olá **iniciar** botão Olá final da tela hello. status do trabalho Olá altera tooStarting e depois de algum tempo tooRunning de alterações.
   
    ![Captura de tela de seleção de início do horário de trabalho](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Executar a solução e os resultados da verificação
Voltando tooyour **ServiceBusQueueTrigger** página, agora você deve ver instruções de log. Esses logs mostram que você obteve algo Olá fila do barramento de serviço, coloque-o em um banco de dados Olá e buscadas ele usando o tempo de saudação como chave Olá!

tooverify que os dados estiverem em seu cache Redis, vá tooyour página do cache Redis no novo portal de saudação (conforme mostrado na saudação anterior [criar um Cache Redis do Azure](#Create-an-Azure-Redis-Cache) etapa) e selecione o Console.

Agora você pode escrever Redis comandos tooconfirm que os dados estarem de fato no cache de saudação.

![Captura de tela do Console Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Próximas etapas
Estamos felizes coisas Olá novas funções do Azure Stream analytics pode fazer juntos e esperamos que isso lhe oferece novas possibilidades. Se você tiver qualquer comentário sobre o que você deseja, sinta-se livre toouse Olá [site UserVoice do Azure](https://feedback.azure.com/forums/270577-stream-analytics).

Se você for novo Microsoft Azure, você está convidado tootry fora pelo inscrever-se para uma [conta de avaliação do Azure gratuita](https://azure.microsoft.com/pricing/free-trial/). Se tiver tooStream de nova análise, você está convidado muito[criar seu primeiro emprego de análise de fluxo](stream-analytics-create-a-job.md).

Caso precise de ajuda ou se tiver dúvidas, poste-as nos fóruns do [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) ou do [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics). 

Você também pode ver Olá recursos a seguir:

* [Referência do desenvolvedor do Azure Functions](../azure-functions/functions-reference.md)
* [Referência do desenvolvedor de C# do Azure Functions](../azure-functions/functions-reference-csharp.md)
* [Referência do desenvolvedor em F# do Azure Functions](../azure-functions/functions-reference-fsharp.md)
* [Referência do desenvolvedor de NodeJS do Azure Functions](../azure-functions/functions-reference.md)
* [Gatilhos e de associações do Azure Functions](../azure-functions/functions-triggers-bindings.md)
* [Como toomonitor Cache Redis do Azure](../redis-cache/cache-how-to-monitor.md)

toostay atualizado em todas as notícias mais recentes hello e recursos, siga [ @AzureStreaming ](https://twitter.com/AzureStreaming) no Twitter.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
