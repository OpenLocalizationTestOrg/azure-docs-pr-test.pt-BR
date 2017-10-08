---
title: aaaHow toouse Azure Service Bus com hello SDK do WebJobs
description: "Saiba como toouse filas de barramento de serviço do Azure e os tópicos com hello SDK do WebJobs."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>Como toouse de barramento de serviço do Azure com hello SDK do WebJobs
## <a name="overview"></a>Visão geral
Este guia fornece c# exemplos de código que mostram como tootrigger um processo quando é recebida uma mensagem de barramento de serviço do Azure. uso de exemplos de código de saudação [SDK do WebJobs](websites-dotnet-webjobs-sdk.md) versão 1. x.

Guia de saudação pressupõe que você sabe [como toocreate um projeto do WebJob no Visual Studio com conexão cadeias de caracteres essa conta de armazenamento de ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md).

trechos de código Olá mostram apenas as funções, hello não código que cria Olá `JobHost` objeto como neste exemplo:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

Um [exemplo de código completo do barramento de serviço](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) no repositório do azure webjobs-sdk exemplos Olá em GitHub.com.

## <a id="prerequisites"></a> Pré-requisitos
toowork com o barramento de serviço tiver Olá tooinstall [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet pacote Além disso toohello outros pacotes do SDK do WebJobs. 

Você também tem uma cadeia de caracteres de conexão do tooset Olá AzureWebJobsServiceBus em cadeias de conexão de armazenamento de toohello de adição.  Você pode fazer isso no hello `connectionStrings` seção do arquivo App. config de hello, conforme mostrado no exemplo a seguir de saudação:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Para um projeto de exemplo que inclui a configuração de cadeia de caracteres de conexão de barramento de serviço Olá no arquivo App. config de saudação, consulte [exemplo de barramento de serviço](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

cadeias de caracteres de conexão Olá também podem ser definidas no ambiente de tempo de execução do Azure hello, que, em seguida, substitui as configurações de App. config hello quando Olá trabalho Web é executado no Azure. Para obter mais informações, consulte [Introdução ao SDK do WebJobs do hello](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Como tootrigger uma função quando um barramento de serviço de fila de mensagem é recebida
toowrite uma função que Olá SDK do WebJobs chama quando é recebida uma mensagem da fila, use Olá `ServiceBusTrigger` atributo. o construtor de atributo Olá leva um parâmetro que especifica o nome de saudação do hello toopoll de fila.

### <a name="how-servicebustrigger-works"></a>Como funciona o ServicebusTrigger
Olá, SDK recebe uma mensagem no `PeekLock` modo e chamadas de `Complete` na mensagem de saudação quando função hello concluído com êxito, ou chamadas `Abandon` se a função hello falhar. Se a função hello executada por mais de saudação `PeekLock` tempo limite de bloqueio de saudação é renovada automaticamente.

Barramento de serviço faz seu próprio tratamento de fila suspeita que não pode ser controlado ou configurado por Olá SDK do WebJobs. 

### <a name="string-queue-message"></a>Mensagem da fila da cadeia
Olá, exemplo de código a seguir lê uma mensagem da fila que contém uma cadeia de caracteres e grava a cadeia de caracteres de saudação toohello painel do SDK do WebJobs.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Observação:** se você estiver criando Olá mensagens da fila em um aplicativo que não usa o SDK do WebJobs do hello, verifique se tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) muito "texto/simples".

### <a name="poco-queue-message"></a>Mensagem da fila POCO
Olá SDK desserializará automaticamente uma mensagem da fila que contém JSON para um POCO [(objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) tipo. Olá, exemplo de código a seguir lê uma mensagem da fila que contém um `BlobInformation` objeto que tem um `BlobName` propriedade:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Para exemplos de código mostrando como propriedades de toouse de saudação POCO toowork com blobs e tabelas no mesmo Olá funcionam, consulte Olá [versão de filas de armazenamento deste artigo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Se seu código que cria a mensagem da fila de saudação não usar Olá SDK do WebJobs, use toohello semelhante de código exemplo a seguir:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>O tipo ServiceBusTrigger funciona com
Além disso `string` e POCO tipos, você pode usar o hello `ServiceBusTrigger` atributo com uma matriz de bytes ou um `BrokeredMessage` objeto.

## <a id="create"></a>Como toocreate barramento de serviço de fila de mensagens
toowrite uma função que cria uma nova mensagem de fila usar Olá `ServiceBus` atributo e passar no construtor de atributo toohello do nome de fila hello. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Criar uma mensagem de fila única em uma função não sincronizada
saudação de exemplo de código a seguir usa um toocreate de parâmetro de saída que uma nova mensagem na fila de saudação denominado "outputqueue" com o mesmo conteúdo como Olá na fila de saudação denominada "inputqueue" foi recebida uma mensagem de saudação.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

saudação de parâmetro de saída para a criação de uma mensagem da fila única pode ser qualquer um dos seguintes tipos de saudação:

* `string`
* `byte[]`
* `BrokeredMessage`
* Um tipo POCO serializável que você define. Automaticamente serializado como JSON.

Para parâmetros de tipo POCO, uma mensagem da fila sempre é criada quando a função hello termina; Se o parâmetro hello for nulo, Olá SDK cria uma mensagem da fila que retorna null quando a mensagem de saudação é recebida e desserializada. Para Olá outros tipos, se o parâmetro hello é nulo nenhuma mensagem de fila é criada.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Criar várias mensagens de fila ou nas funções assíncronas
toocreate várias mensagens, use Olá `ServiceBus` atributo com `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no hello exemplo de código a seguir:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Cada mensagem de fila é criada imediatamente quando hello `Add` método é chamado.

## <a id="topics"></a>Como toowork com tópicos do barramento de serviço
toowrite uma função que Olá SDK chama quando uma mensagem é recebida em um tópico do barramento de serviço, use Olá `ServiceBusTrigger` atributo com o construtor de saudação que obtém o nome do tópico e assinatura, conforme mostrado no hello exemplo de código a seguir:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate uma mensagem em um tópico, use Olá `ServiceBus` atributo com uma saudação de nome do tópico mesmo maneira que você pode usá-lo com um nome de fila.

## <a name="features-added-in-release-11"></a>Recursos adicionados na versão 1.1
Olá recursos a seguir foram adicionado na versão 1.1:

* Permitir personalização profunda de processamento de mensagens via `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`oferece suporte à personalização de saudação do Service Bus `MessagingFactory` e `NamespaceManager`.
* Um `MessageProcessor` padrão de estratégia permite que você toospecify um processador por fila/tópico.
* A simultaneidade de processamento de mensagem tem suporte por padrão. 
* Personalização fácil de `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.
* Permitir [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe especificado em `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (para cenários em que você pode não ter gerenciam direitos). Observe que o Azure WebJobs é tooautomatically não é possível provisionar inexistente as filas e tópicos sem gerenciar AccessRights.

## <a id="queues"></a>Tópicos relacionados cobertos por filas de armazenamento da saudação como-tooarticle
Para obter informações sobre cenários de SDK do WebJobs tooService não específica do Bus, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Os tópicos abordados nesse artigo incluem o seguinte hello:

* Funções assíncronas
* Várias instâncias
* Desligamento normal
* Usar atributos de SDK do WebJobs no corpo de saudação de uma função
* Cadeias de conexão do conjunto Olá SDK no código
* Definir valores para parâmetros do construtor do SDK WebJobs no código
* Disparar uma função manualmente
* Gravar logs

## <a id="nextsteps"></a> Próximas etapas
Este guia fornece código exemplos que mostram como os cenários comuns de toohandle para trabalhar com o barramento de serviço do Azure. Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos recomendada do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

