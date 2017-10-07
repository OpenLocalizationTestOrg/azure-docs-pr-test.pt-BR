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
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Introdução ao Armazenamento de Fila do Azure e aos Serviços Conectados do Visual Studio (Projetos WebJob)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral
Este artigo descreve como obter iniciado usando a fila do Azure Olá de armazenamento em um projeto de trabalho de Web do Visual Studio Azure depois que você criou ou referenciados de uma conta de armazenamento do Azure usando o Visual Studio **adicionar serviços conectados** caixa de diálogo. Quando você adiciona um projeto WebJob de tooa de conta de armazenamento usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo, pacotes do NuGet do armazenamento do Azure apropriados Olá estiverem instalados, referências de .NET apropriadas Olá são toohello adicionado projeto e cadeias de caracteres de conexão para a conta de armazenamento Olá são atualizadas no arquivo App. config de saudação.  

Este artigo fornece c# exemplos de código que mostram como toouse Olá versão do SDK do Azure WebJobs 1. x com hello serviço de armazenamento de fila do Azure.

Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS. Uma mensagem da fila única pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento. Consulte a [Introdução ao Armazenamento de Filas do Azure usando o .NET](storage-dotnet-how-to-use-queues.md) para obter mais informações. Para saber mais sobre ASP.NET, confira [ASP.NET](http://www.asp.net).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>Como tootrigger uma função quando é recebida uma mensagem da fila
toowrite uma função que Olá SDK do WebJobs chama quando é recebida uma mensagem da fila, use Olá **QueueTrigger** atributo. o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome de saudação do hello toopoll de fila. toosee como tooset Olá nome da fila dinamicamente, check-out [como tooset opções de configuração](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Mensagens da fila da cadeia
Olá exemplo a seguir, fila Olá contém uma mensagem de cadeia de caracteres, portanto **QueueTrigger** parâmetro de cadeia de caracteres tooa aplicada denominado **logMessage** que contém o conteúdo de saudação de mensagem da fila de saudação. Olá função [grava uma mensagem de log toohello painel](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Além disso **cadeia de caracteres**, parâmetro hello pode ser uma matriz de bytes, um **CloudQueueMessage** objeto ou um POCO que você definir.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Olá exemplo a seguir, mensagem de saudação do fila contém JSON para um **BlobInformation** objeto que inclui um **BlobName** propriedade. Olá SDK automaticamente desserializa o objeto de saudação.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Olá SDK usa Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e desserializar de mensagens. Se você criar a fila de mensagens em um programa que não usa o SDK do WebJobs do hello, você pode escrever código como Olá seguindo o exemplo toocreate uma mensagem da fila POCO que Olá que SDK pode ser analisado.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Funções assíncronas
Olá seguinte função assíncrona [grava um log toohello painel](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Funções assíncronas podem levar uma [token de cancelamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), conforme mostrado no hello exemplo que copia um blob a seguir. (Para obter uma explicação da saudação **queueTrigger** espaço reservado, consulte Olá [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) seção.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Atributo de QueueTrigger Olá tipos funciona com
Você pode usar **QueueTrigger** com hello tipos a seguir:

* **string**
* Um tipo POCO serializado como JSON
* **byte[]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Algoritmo de sondagem
Olá SDK implementa um efeito de saudação tooreduce aleatória exponencial algoritmo de retirada da fila ociosa em custos de transações de armazenamento de sondagem.  Quando uma mensagem é encontrada, Olá SDK espera 2 segundos e, em seguida, verifica a outra mensagem; Quando nenhuma mensagem for encontrada, ele aguarda cerca de quatro segundos antes de tentar novamente. Depois de tentativas subsequentes tooget uma mensagem da fila, o tempo de espera Olá continua tooincrease até atingir o tempo de espera máximo Olá, quais minuto de tooone padrões. [Olá tempo de espera máximo é configurável](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Várias instâncias
Se seu aplicativo web é executado em várias instâncias, um trabalhos Web contínuos é executado em cada computador, e cada computador aguardará para gatilhos e tentar toorun funções. Em alguns cenários, que isso pode levar funções toosome processamento Olá mesmo dados duas vezes, para que funções devem ser idempotentes (gravado de forma que chamando repetidamente com hello mesmos dados de entrada não produzem duplicar os resultados).  

## <a name="parallel-execution"></a>Execução paralela
Se você tiver várias funções diferentes filas escutando, Olá SDK ligá-los em paralelo quando as mensagens são recebidas simultaneamente.

Olá mesmo é verdadeiro quando várias mensagens são recebidas para uma única fila. Por padrão, hello SDK obtém um lote de mensagens de fila de 16 por vez e executa a função hello processa-los em paralelo. [tamanho do lote Olá é configurável](#how-to-set-configuration-options). Quando o número Olá processado chega toohalf de tamanho de lote hello, Olá SDK obtém outro lote e começa a processar essas mensagens. Portanto o número de máximo de saudação simultâneas mensagens processadas por função é tamanho de lote de saudação de uma vez e meia. Esse limite se aplica separadamente função tooeach que tem um **QueueTrigger** atributo. Se não quiser que a execução paralela para mensagens recebidas em uma fila, defina Olá too1 de tamanho de lote.

## <a name="get-queue-or-queue-message-metadata"></a>Obter fila ou metadados de mensagem da fila
Você pode obter Olá propriedades de mensagem a seguir, adicionando a assinatura do método toohello parâmetros:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **string** queueTrigger (contém o texto da mensagem)
* **string** id
* **string** popReceipt
* **int** dequeueCount

Se você desejar toowork diretamente com hello API de armazenamento do Azure, você também pode adicionar uma **CloudStorageAccount** parâmetro.

Olá exemplo a seguir grava todos os este metadados tooan informações do log de aplicativo. No exemplo hello, logMessage e queueTrigger contêm conteúdo Olá de mensagem da fila de saudação.

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

Aqui está um exemplo de log gravado pelo código de exemplo hello:

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a>Desligamento normal
Uma função que é executado em um trabalho Web contínuo pode aceitar um **CancellationToken** parâmetro que permite Olá toonotify Olá função do sistema operacional quando hello WebJob é sobre toobe encerrada. Você pode usar este toomake notificação se a função hello não finalização inesperada de forma que deixa os dados em um estado inconsistente.

Olá mostrado no exemplo a seguir como toocheck iminente encerramento do trabalho Web em uma função.

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

**Observação:** Olá painel não pode mostrar corretamente o status de saudação e a saída de funções que ter sido desligado.

Para obter mais informações, consulte [Desligamento normal dos trabalhos Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Como toocreate uma fila de mensagens ao processar uma mensagem da fila
toowrite uma função que cria uma nova mensagem da fila, use Olá **fila** atributo. Como **QueueTrigger**, passar no nome da fila hello como uma cadeia de caracteres, ou você pode [definir dinamicamente o nome da fila Olá](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Mensagens da fila da cadeia
Olá async não exemplo de código a seguir cria uma nova mensagem de fila na fila de saudação denominada "outputqueue" com hello mesmo conteúdo como mensagem de saudação do fila recebidos na fila de saudação denominada "inputqueue". (Para funções assíncronas, use **IAsyncCollector<T>** , conforme mostrado posteriormente nesta seção.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
tipo de uma mensagem da fila que contém um POCO em vez de uma cadeia de caracteres, passagem Olá POCO toocreate como um toohello de parâmetro de saída **fila** construtor de atributo.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Olá SDK automaticamente serializa Olá tooJSON de objeto. Uma mensagem da fila é sempre criada, mesmo se o objeto de saudação é nulo.

### <a name="create-multiple-messages-or-in-async-functions"></a>Criar várias mensagens ou em funções assíncronas
toocreate várias mensagens, verifique o tipo de parâmetro de saudação para fila de saída de hello **ICollector<T>**  ou **IAsyncCollector<T>**, conforme mostrado no exemplo a seguir de saudação.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Cada mensagem de fila é criada imediatamente quando hello **adicionar** método é chamado.

### <a name="types-that-hello-queue-attribute-works-with"></a>Tipos de atributo fila Olá funciona com
Você pode usar o hello **fila** atributo Olá tipos de parâmetro a seguir:

* **saída de cadeia de caracteres** (cria a mensagem da fila se o valor do parâmetro é não nulo quando a função hello termina)
* **out byte[]** (funciona como **string**)
* **out CloudQueueMessage** (funciona como **string**)
* **limite POCO** (um tipo serializável, cria uma mensagem com um objeto nulo se o parâmetro hello é nulo quando termina de função hello)
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (para a criação de mensagens manualmente usando Olá API de armazenamento do Azure diretamente)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Usar atributos de SDK do WebJobs no corpo de saudação de uma função
Se você precisar toodo alguns funcionar na sua função antes de usar um atributo do SDK do WebJobs como **fila**, **Blob**, ou **tabela**, você pode usar o hello **IBinder** interface.

saudação de exemplo a seguir usa uma mensagem da fila de entrada e cria uma nova mensagem com hello mesmo conteúdo em uma fila de saída. nome de fila de saída de saudação é definido pelo código no corpo de saudação do função hello.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Olá **IBinder** interface também pode ser usada com hello **tabela** e **Blob** atributos.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Como tooread e gravar os blobs e tabelas durante o processamento de uma mensagem da fila
Olá **Blob** e **tabela** atributos permitem que você tooread e gravar os blobs e tabelas. exemplos de saudação nesta seção se aplicam a tooblobs. Para obter exemplos de código que mostram como tootrigger processa quando blobs são criados ou atualizados, consulte [como toouse Azure blob storage com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e para obter exemplos de código que leem e gravam tabelas, consulte [como toouse tabela do Azure armazenamento com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Mensagens da fila de cadeia de caracteres que disparam operações de blob
Para uma mensagem da fila que contém uma cadeia de caracteres, **queueTrigger** é um espaço reservado que você pode usar em Olá **Blob** do atributo **blobPath** parâmetro que contém o conteúdo de saudação do mensagem de saudação.

Olá exemplo a seguir usa **fluxo** objetos blobs tooread e gravação. mensagem de saudação do fila é o nome de saudação de um blob localizado no contêiner de textblobs hello. Uma cópia de blob Olá com "-novo" acrescentada toohello nome é criado no hello mesmo contêiner.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Olá **Blob** atributo construtor usa um **blobPath** parâmetro que especifica o contêiner de saudação e nome do blob. Para obter mais informações sobre esse espaço reservado, consulte [como toouse Azure blob storage com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Quando o atributo Olá decora uma **fluxo** do objeto, outro parâmetro de construtor Especifica Olá **FileAccess** modo como leitura, gravação ou leitura/gravação.

Olá exemplo a seguir usa uma **CloudBlockBlob** toodelete um blob do objeto. mensagem da fila de saudação é o nome de saudação do blob hello.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Mensagens de fila POCO [(Objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Para um POCO armazenada como JSON na mensagem de saudação do fila, você pode usar espaços reservados que propriedades de objeto Olá Olá nomes **fila** do atributo **blobPath** parâmetro. Também é possível utilizar os nomes de propriedade de metadados de fila como espaços reservados. Consulte [Obter a fila ou os metadados de mensagem da fila](#get-queue-or-queue-message-metadata).

Olá, exemplo a seguir copia um blob tooa novo blob com uma extensão diferente. mensagem de saudação do fila é um **BlobInformation** objeto inclui **BlobName** e **BlobNameWithoutExtension** propriedades. nomes de propriedade Olá são usados como espaços reservados no caminho de blob Olá Olá **Blob** atributos.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Olá SDK usa Olá [pacote NuGet newtonsoft](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e desserializar de mensagens. Se você criar a fila de mensagens em um programa que não usa o SDK do WebJobs do hello, você pode escrever código como Olá seguindo o exemplo toocreate uma mensagem da fila POCO que Olá que SDK pode ser analisado.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Se você precisar toodo alguns funcionar na sua função antes de associar um objeto de tooan de blob, você pode usar o atributo de saudação no corpo de saudação do função hello, conforme mostrado no [atributos de usar o SDK do WebJobs no corpo de saudação de uma função](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Tipos que você pode usar o hello Blob de atributo com
Olá **Blob** atributo pode ser usado com hello tipos a seguir:

* **Fluxo** (leitura ou gravação, especificadas usando o parâmetro de construtor FileAccess Olá)
* **TextReader**
* **TextWriter**
* **string** (leitura)
* **saída de cadeia de caracteres** (gravação; cria um blob somente se o parâmetro de cadeia de caracteres de saudação for não nulo quando a função hello retorna)
* POCO (leitura)
* limite POCO (gravação; sempre cria um blob, cria como objeto nulo se o parâmetro POCO é nulo quando a função hello retorna)
* **CloudBlobStream** (gravação)
* **ICloudBlob** (leitura ou gravação)
* **CloudBlockBlob** (leitura ou gravação)
* **CloudPageBlob** (leitura ou gravação)

## <a name="how-toohandle-poison-messages"></a>Como o toohandle mensagens suspeitas
São chamadas de mensagens cujo conteúdo faz com que uma função toofail *mensagens suspeitas*. Quando a função hello falha, mensagem de saudação do fila não é excluída e eventualmente é obtida novamente, causando toobe de ciclo de saudação repetido. Olá SDK automaticamente pode interromper o ciclo de saudação após um número limitado de iterações ou você pode fazer isso manualmente.

### <a name="automatic-poison-message-handling"></a>Manipulação automática de mensagens suspeitas
Olá SDK chamará uma função de backup too5 vezes tooprocess uma mensagem da fila. Se tentar quinto Olá falhar, mensagem de saudação é fila inviabilização movida tooa. Você pode ver como tooconfigure Olá número máximo de repetições em [como opções de configuração de tooset](#how-to-set-configuration-options).

fila suspeitas Olá é denominada *{originalqueuename}*-suspeitas. Você pode escrever uma função tooprocess mensagens da fila de suspeitas Olá registrá-los ou enviar uma notificação que atenção manual é necessária.

Em Olá Olá de exemplo a seguir **CopyBlob** função falhará quando uma mensagem da fila contém nome de saudação de um blob que não existe. Quando isso acontece, a mensagem de saudação é movida da fila de suspeitas copyblobqueue Olá copyblobqueue fila toohello. Olá **ProcessPoisonMessage** e logs Olá mensagens suspeitas.

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

Olá ilustração a seguir mostra a saída de console dessas funções quando uma mensagem suspeita é processada.

![Saída do console para tratamento de mensagens suspeitas](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>Manipulação manual de mensagens suspeitas
Você pode obter o número de saudação de vezes que uma mensagem tem foram coletada para processamento, adicionando um **int** parâmetro denominado **dequeueCount** tooyour função. Você pode então seleção Olá contagem no código da função de remoção da fila e executar seu próprio tratamento de mensagens suspeitas quando o número de saudação excede um limite, conforme mostrado no exemplo a seguir de saudação.

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

## <a name="how-tooset-configuration-options"></a>Como as opções de configuração de tooset
Você pode usar o hello **JobHostConfiguration** saudação do tipo tooset as opções de configuração a seguir:

* Defina cadeias de caracteres de conexão do hello SDK no código.
* Definir as configurações de **QueueTrigger** como contagem máxima de remoção da fila.
* Obtenha nomes de fila por meio da configuração.

### <a name="set-sdk-connection-strings-in-code"></a>Defina as cadeias de conexão do SDK no código
Definindo cadeias de caracteres de conexão do hello SDK no código permite que você toouse seus próprios nomes de cadeia de caracteres de conexão em arquivos de configuração ou variáveis de ambiente, conforme mostrado no exemplo a seguir de saudação.

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

### <a name="configure-queuetrigger--settings"></a>Definir configurações de QueueTrigger
Você pode configurar Olá configurações que se aplicam a toohello processamento de mensagens de fila a seguir:

* Olá número máximo de fila de mensagens que são aplicadas simultaneamente toobe executado em paralelo (o padrão é 16).
* Olá número máximo de tentativas antes de uma mensagem da fila é enviada a fila de suspeitas tooa (o padrão é 5).
* tempo de espera máximo Olá antes de sondar novamente quando uma fila está vazia (o padrão é 1 minuto).

Olá mostrado no exemplo a seguir como tooconfigure essas configurações:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Definir valores para parâmetros do construtor do SDK WebJobs no código
Às vezes, você deseja toospecify um nome de fila, um nome de blob ou contêiner ou nome de uma tabela no código em vez de embuti-lo. Por exemplo, convém toospecify Olá nome **QueueTrigger** em uma variável de ambiente ou arquivo de configuração.

Você pode fazer isso, passando um **NameResolver** objeto toohello **JobHostConfiguration** tipo. Incluir espaços reservados especiais entre sinais de porcentagem (%)) nos parâmetros de construtor de atributo do SDK do WebJobs e sua **NameResolver** código especifica Olá toobe de valores reais usado no lugar desses espaços reservados.

Por exemplo, suponha que você queira toouse uma fila denominada logqueuetest no ambiente de teste hello e um logqueueprod nomeado na produção. Em vez de um nome de fila embutidos, você deseja que o nome de saudação toospecify da entrada hello **appSettings** coleção que tem nome de fila real hello. Se hello **appSettings** chave é logqueue, sua função pode parecer com o exemplo a seguir de saudação.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

O **NameResolver** classe, em seguida, foi possível obter o nome da fila de saudação do **appSettings** conforme mostrado no exemplo a seguir de saudação:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Você passa Olá **NameResolver** classe toohello **JobHost** conforme mostrado no exemplo a seguir de saudação do objeto.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Observação:** nomes de blob, tabela e fila são resolvidos sempre que uma função é chamada, mas os nomes de contêiner de blob são resolvidos somente quando o aplicativo hello inicia. Você não pode alterar o nome do contêiner de blob enquanto Olá trabalho está em execução.

## <a name="how-tootrigger-a-function-manually"></a>Como uma função de tootrigger manualmente
tootrigger uma função manualmente, use Olá **chamar** ou **CallAsync** método hello **JobHost** objeto e hello **NoAutomaticTrigger** atributo na função hello, conforme mostrado no exemplo a seguir de saudação.

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

## <a name="how-toowrite-logs"></a>Como os logs de toowrite
Olá painel mostra logs em dois lugares: página Olá Olá trabalho Web e página Olá para determinada invocação WebJob.

![Logs na página do Trabalho Web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Logs na página de invocação de função](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Saída de métodos de Console que você chama uma função ou de saudação **Main** método aparece na página painel Olá Olá WebJob, não na página de saudação para uma invocação de método específico. Saída do objeto de TextWriter Olá que você obteve de um parâmetro na sua assinatura do método aparece na página do painel de saudação de uma invocação de método.

Saída do console não pode ser vinculado tooa da invocação do método particular porque Olá Console é de thread único, enquanto muitas funções de trabalho podem ser executadas ao Olá simultaneamente. É por isso que Olá SDK fornece cada invocação de função com seu próprio objeto do gravador de log exclusivo.

toowrite [logs de rastreamento de aplicativo](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (cria marcados como informações de logs) e **Console.Error** (cria logs marcados como erro). Uma alternativa é toouse [rastreamento ou TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que fornece detalhado, aviso e crítico níveis em adição tooInfo e erro. Logs de rastreamento do aplicativo aparecem nos arquivos de log de aplicativo da web hello, as tabelas do Azure, ou blobs do Azure dependendo de como você configura seu aplicativo web do Azure. Assim como de toda a saída de Console, logs de aplicativo 100 mais recentes Olá também aparecem na página painel Olá Olá WebJob, não a página Olá para uma invocação de função.

Saída do console é exibida em Olá painel somente se o programa hello está sendo executado em um trabalho de Web do Azure, não se programa hello está sendo executado localmente ou em algum outro ambiente.

Você pode desabilitar o registro em log definindo Olá toonull de cadeia de caracteres de conexão de painel. Para obter mais informações, consulte [como tooset opções de configuração](#how-to-set-configuration-options).

Olá, exemplo a seguir mostra várias maneiras toowrite logs:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

Em Olá painel do SDK do WebJobs, Olá saída de hello **TextWriter** mostra backup quando você entrar toohello página para uma determinada chamada de função e selecione objeto **alternar saída**:

![Link de invocação](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Logs na página de invocação de função](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Em Olá painel do SDK do WebJobs, linhas Olá 100 mais recente do Console de saída mostrar backup quando você vá para a página toohello para Olá WebJob (não para invocação de função hello) e selecione **alternar saída**.

![Ativar/Desativar Saída](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

Em um trabalho Web contínuo, logs de aplicativo exibido no/dados/trabalhos/contínua/*{webjobname}*/job_log.txt no sistema de arquivos de aplicativo de web hello.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

Em um aplicativo hello de BLOBs do Azure logs ter esta aparência: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Olá, mundo!, 2014-09-26T21:01:13, erro, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Olá, mundo!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Olá, mundo!,

Em uma saudação de tabela do Azure **Console.Out** e **Console.Error** logs ter esta aparência:

![Log de informações na tabela](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Log de erros na tabela](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Próximas etapas
Este artigo fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com filas do Azure. Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

