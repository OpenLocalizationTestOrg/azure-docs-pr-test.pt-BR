---
title: "Como usar o Barramento de Serviço do Azure com o SDK de Trabalhos Web"
description: "Saiba como usar tópicos e filas do barramento de serviço do Azure com o SDK de Trabalhos Web."
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
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="9b50b-103">Como usar o Barramento de Serviço do Azure com o SDK de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="9b50b-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="9b50b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9b50b-104">Overview</span></span>
<span data-ttu-id="9b50b-105">Este guia fornece exemplos de código c# que mostram como disparar um processo quando uma mensagem do Barramento de Serviço é recebida.</span><span class="sxs-lookup"><span data-stu-id="9b50b-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="9b50b-106">Os exemplos de código que usam o [SDK WebJobs](websites-dotnet-webjobs-sdk.md) versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="9b50b-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="9b50b-107">O guia pressupõe que você saiba [como criar um projeto de Trabalho Web no Visual Studio com cadeias de conexão que apontam para sua conta de armazenamento](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9b50b-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="9b50b-108">Os trechos de código mostram apenas funções, não o código que cria o objeto `JobHost` , como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b50b-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="9b50b-109">Um [exemplo de código completo do Barramento de Serviço](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) está no repositório de exemplos azure-webjobs-sdk no GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="9b50b-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="9b50b-110"><a id="prerequisites"></a> Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9b50b-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="9b50b-111">Para trabalhar com o Barramento de Serviço, você precisa instalar o pacote do NuGet [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) , além dos pacotes do SDK de Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="9b50b-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="9b50b-112">Você também deve definir a cadeia de conexão AzureWebJobsServiceBus além de cadeias de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9b50b-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="9b50b-113">Você pode fazer isso na seção `connectionStrings` do arquivo  App.config, conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b50b-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="9b50b-114">Para um projeto de exemplo que inclui a configuração de cadeia de conexão do Barramento de Serviço no arquivo App.config, consulte [exemplo de Barramento de Serviço](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="9b50b-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="9b50b-115">As cadeias de conexão também podem ser definidas no ambiente de tempo de execução do Azure, que, em seguida, substitui as configurações do App.config quando o Trabalho Web é executado no Azure. Para obter mais informações, consulte [Introdução ao SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9b50b-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="9b50b-116"><a id="trigger"></a> Como disparar uma função quando uma mensagem da fila de Barramento de Serviço é recebida</span><span class="sxs-lookup"><span data-stu-id="9b50b-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="9b50b-117">Para gravar uma função que o SDK de Trabalhos Web chama quando uma mensagem da fila é recebida, use o atributo `ServiceBusTrigger` .</span><span class="sxs-lookup"><span data-stu-id="9b50b-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="9b50b-118">O construtor de atributo tem um parâmetro que especifica o nome da fila para sondagem.</span><span class="sxs-lookup"><span data-stu-id="9b50b-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="9b50b-119">Como funciona o ServicebusTrigger</span><span class="sxs-lookup"><span data-stu-id="9b50b-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="9b50b-120">O SDK recebe uma mensagem em modo `PeekLock` e chamadas `Complete` na mensagem se a função for concluída com êxito, ou chamadas `Abandon` se a função falhar.</span><span class="sxs-lookup"><span data-stu-id="9b50b-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="9b50b-121">Se a função for executada por mais tempo que o limite `PeekLock` , o bloqueio é renovado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9b50b-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="9b50b-122">O barramento de serviço faz seu próprio tratamento de fila de mensagens suspeitas que não podem ser controladas ou configuradas pelo SDK do WebJobs.</span><span class="sxs-lookup"><span data-stu-id="9b50b-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="9b50b-123">Mensagem da fila da cadeia</span><span class="sxs-lookup"><span data-stu-id="9b50b-123">String queue message</span></span>
<span data-ttu-id="9b50b-124">O exemplo de código a seguir lê uma mensagem da fila que contém uma cadeia de caracteres e grava a cadeia de caracteres no painel do SDK de Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="9b50b-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="9b50b-125">**Observação:** se você estiver criando as mensagens de fila em um aplicativo que não usa o SDK de Trabalhos Web, certifique-se de definir [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) para "text/plain".</span><span class="sxs-lookup"><span data-stu-id="9b50b-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="9b50b-126">Mensagem da fila POCO</span><span class="sxs-lookup"><span data-stu-id="9b50b-126">POCO queue message</span></span>
<span data-ttu-id="9b50b-127">O SDK desserializará automaticamente uma mensagem da fila que contém o JSON para um tipo POCO [(objeto Plain Old CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)).</span><span class="sxs-lookup"><span data-stu-id="9b50b-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="9b50b-128">O exemplo de código a seguir lê uma mensagem da fila que contém um objeto `BlobInformation` que tem uma propriedade `BlobName`:</span><span class="sxs-lookup"><span data-stu-id="9b50b-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="9b50b-129">Para obter exemplos de código mostrando como usar propriedades do POCO para trabalhar com blobs e tabelas na mesma função, consulte a [versão de filas de armazenamento deste artigo](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span><span class="sxs-lookup"><span data-stu-id="9b50b-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="9b50b-130">Se seu código que cria a mensagem da fila não usa o SDK WebJobs, use um código semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b50b-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="9b50b-131">O tipo ServiceBusTrigger funciona com</span><span class="sxs-lookup"><span data-stu-id="9b50b-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="9b50b-132">Além dos tipos `string` e POCO, você pode usar o atributo `ServiceBusTrigger` com uma matriz de bytes ou um objeto `BrokeredMessage`.</span><span class="sxs-lookup"><span data-stu-id="9b50b-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="9b50b-133"><a id="create"></a> Como criar mensagens de fila do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="9b50b-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="9b50b-134">Para escrever uma função que cria um uma nova mensagem de fila, use o atributo `ServiceBus` e passe o nome da fila para o construtor de atributo.</span><span class="sxs-lookup"><span data-stu-id="9b50b-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="9b50b-135">Criar uma mensagem de fila única em uma função não sincronizada</span><span class="sxs-lookup"><span data-stu-id="9b50b-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="9b50b-136">O exemplo de código a seguir usa um parâmetro de saída para criar uma nova mensagem na fila denominada "outputqueue" com o mesmo conteúdo que a mensagem recebida na fila denominada "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="9b50b-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="9b50b-137">O parâmetro de saída para a criação de uma mensagem de fila única pode ser qualquer um dos seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="9b50b-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="9b50b-138">Um tipo POCO serializável que você define.</span><span class="sxs-lookup"><span data-stu-id="9b50b-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="9b50b-139">Automaticamente serializado como JSON.</span><span class="sxs-lookup"><span data-stu-id="9b50b-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="9b50b-140">Para parâmetros de tipo POCO, uma mensagem de fila sempre é criada quando a função termina. Se o parâmetro for null, o SDK cria uma mensagem de fila que retorna nula quando a mensagem é recebida e desserializada.</span><span class="sxs-lookup"><span data-stu-id="9b50b-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="9b50b-141">Para outros tipos, se o parâmetro for nulo nenhuma mensagem da fila é criada.</span><span class="sxs-lookup"><span data-stu-id="9b50b-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="9b50b-142">Criar várias mensagens de fila ou nas funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="9b50b-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="9b50b-143">Para criar várias mensagens, use o atributo `ServiceBus` com `ICollector<T>` ou `IAsyncCollector<T>`, conforme mostrado no exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b50b-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="9b50b-144">Cada mensagem da fila é criada imediatamente quando o método `Add` é chamado.</span><span class="sxs-lookup"><span data-stu-id="9b50b-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="9b50b-145"><a id="topics"></a>Como trabalhar com tópicos do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="9b50b-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="9b50b-146">Para gravar uma função que o SDK chama quando uma mensagem é recebida em um tópico do barramento de serviço, use o atributo `ServiceBusTrigger` com o construtor que usa o nome do tópico e assinatura, conforme mostrado no exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b50b-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="9b50b-147">Para criar uma mensagem em um tópico, use o atributo `ServiceBus` com um nome de tópico da mesma forma que você pode usá-lo com um nome de fila.</span><span class="sxs-lookup"><span data-stu-id="9b50b-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="9b50b-148">Recursos adicionados na versão 1.1</span><span class="sxs-lookup"><span data-stu-id="9b50b-148">Features added in release 1.1</span></span>
<span data-ttu-id="9b50b-149">Os seguintes recursos foram adicionados na versão 1.1:</span><span class="sxs-lookup"><span data-stu-id="9b50b-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="9b50b-150">Permitir personalização profunda de processamento de mensagens via `ServiceBusConfiguration.MessagingProvider`.</span><span class="sxs-lookup"><span data-stu-id="9b50b-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="9b50b-151">`MessagingProvider` dá suporte à personalização do Barramento de Serviço `MessagingFactory` e `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="9b50b-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="9b50b-152">Um padrão de estratégia `MessageProcessor` permite que você especifique um processador por fila/tópico.</span><span class="sxs-lookup"><span data-stu-id="9b50b-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="9b50b-153">A simultaneidade de processamento de mensagem tem suporte por padrão.</span><span class="sxs-lookup"><span data-stu-id="9b50b-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="9b50b-154">Personalização fácil de `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span><span class="sxs-lookup"><span data-stu-id="9b50b-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="9b50b-155">Permita que [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) seja especificado em `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (para cenários em que você talvez não precise gerenciar direitos).</span><span class="sxs-lookup"><span data-stu-id="9b50b-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="9b50b-156">Observe que o Azure WebJobs não pode provisionar automaticamente filas e tópicos inexistentes sem AccessRights Gerenciar.</span><span class="sxs-lookup"><span data-stu-id="9b50b-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="9b50b-157"><a id="queues"></a>Tópicos relacionados abordados no artigo de instruções de filas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9b50b-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="9b50b-158">Para obter informações sobre cenários do SDK de Trabalhos Web não específicos para o barramento de serviço, consulte [Como usar armazenamento de fila do Azure com o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="9b50b-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="9b50b-159">Os tópicos abordados nesse artigo incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9b50b-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="9b50b-160">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="9b50b-160">Async functions</span></span>
* <span data-ttu-id="9b50b-161">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="9b50b-161">Multiple instances</span></span>
* <span data-ttu-id="9b50b-162">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="9b50b-162">Graceful shutdown</span></span>
* <span data-ttu-id="9b50b-163">Usar atributos do SDK de Trabalhos Web no corpo de uma função</span><span class="sxs-lookup"><span data-stu-id="9b50b-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="9b50b-164">Definir as cadeias de conexão do SDK no código</span><span class="sxs-lookup"><span data-stu-id="9b50b-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="9b50b-165">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="9b50b-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="9b50b-166">Disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="9b50b-166">Trigger a function manually</span></span>
* <span data-ttu-id="9b50b-167">Gravar logs</span><span class="sxs-lookup"><span data-stu-id="9b50b-167">Write logs</span></span>

## <span data-ttu-id="9b50b-168"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b50b-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="9b50b-169">Este guia forneceu exemplos de amostras que mostram como lidar com cenários comuns para trabalhar com o Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b50b-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="9b50b-170">Para obter mais informações sobre como usar os Trabalhos Web do Azure e o SDK de Trabalhos Web, consulte [Trabalhos Web do Azure – Recursos recomendados](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="9b50b-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

