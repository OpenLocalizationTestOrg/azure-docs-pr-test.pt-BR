---
title: "Monitoramento de operações de Hub IoT do Azure | Microsoft Docs"
description: "Como usar o monitoramento das operações do Hub IoT do Azure para monitorar o status das operações no seu Hub IoT em tempo real."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="a8af7-103">Monitoramento de operações do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="a8af7-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="a8af7-104">O monitoramento das operações do Hub IoT permite monitorar o status das operações no seu Hub IoT em tempo real.</span><span class="sxs-lookup"><span data-stu-id="a8af7-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="a8af7-105">O Hub IoT controla eventos em várias categorias de operações.</span><span class="sxs-lookup"><span data-stu-id="a8af7-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="a8af7-106">Você pode aceitar o envio de eventos de uma ou mais categorias para um ponto de extremidade do seu Hub IoT para processamento.</span><span class="sxs-lookup"><span data-stu-id="a8af7-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="a8af7-107">É possível monitorar os dados em busca de erros ou configurar processamento mais complexo com base nos padrões de dados.</span><span class="sxs-lookup"><span data-stu-id="a8af7-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="a8af7-108">O Hub IoT monitora seis categorias de eventos:</span><span class="sxs-lookup"><span data-stu-id="a8af7-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="a8af7-109">Operações de identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8af7-109">Device identity operations</span></span>
* <span data-ttu-id="a8af7-110">Telemetria de dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8af7-110">Device telemetry</span></span>
* <span data-ttu-id="a8af7-111">Mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8af7-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="a8af7-112">Conexões</span><span class="sxs-lookup"><span data-stu-id="a8af7-112">Connections</span></span>
* <span data-ttu-id="a8af7-113">Carregamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="a8af7-113">File uploads</span></span>
* <span data-ttu-id="a8af7-114">Roteamento de mensagem</span><span class="sxs-lookup"><span data-stu-id="a8af7-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="a8af7-115">Como habilitar o monitoramento de operações</span><span class="sxs-lookup"><span data-stu-id="a8af7-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="a8af7-116">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8af7-116">Create an IoT hub.</span></span> <span data-ttu-id="a8af7-117">Você pode encontrar instruções sobre como criar um Hub IoT no guia de [Introdução][lnk-get-started].</span><span class="sxs-lookup"><span data-stu-id="a8af7-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="a8af7-118">Abra a folha do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8af7-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="a8af7-119">Nela, clique em **Monitoramento de operações**.</span><span class="sxs-lookup"><span data-stu-id="a8af7-119">From there, click **Operations monitoring**.</span></span>

    ![Acessar a configuração do monitoramento de operações no portal][1]

1. <span data-ttu-id="a8af7-121">Selecione as categorias de monitoramento que deseja monitorar e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a8af7-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="a8af7-122">Os eventos estão disponíveis para leitura no ponto de extremidade compatível com o Hub de Eventos listado em **Configurações de monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="a8af7-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="a8af7-123">O ponto de extremidade do Hub IoT chama-se `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="a8af7-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configurar o monitoramento de operações no Hub IoT][2]

> [!NOTE]
> <span data-ttu-id="a8af7-125">A seleção do monitoramento **Detalhado** para a categoria **Conexões** faz com que o Hub IoT gere mensagens de diagnóstico adicionais.</span><span class="sxs-lookup"><span data-stu-id="a8af7-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="a8af7-126">Para todas as outras categorias, a configuração **Detalhada** muda a quantidade de informações incluídas pelo Hub IoT em cada mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="a8af7-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="a8af7-127">Categorias de evento e como usá-las</span><span class="sxs-lookup"><span data-stu-id="a8af7-127">Event categories and how to use them</span></span>

<span data-ttu-id="a8af7-128">Cada categoria de monitoramento de operações rastreia um tipo diferente de interação com o Hub IoT e cada categoria de monitoramento tem um esquema que define como os eventos nessa categoria são estruturados.</span><span class="sxs-lookup"><span data-stu-id="a8af7-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="a8af7-129">Operações de identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8af7-129">Device identity operations</span></span>

<span data-ttu-id="a8af7-130">A categoria de operações de identidade do dispositivo rastreia erros que ocorrem quando você tenta criar, atualizar ou excluir uma entrada no registro de identidade do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8af7-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="a8af7-131">O rastreamento dessa categoria é útil em cenários de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="a8af7-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="a8af7-132">Telemetria de dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8af7-132">Device telemetry</span></span>

<span data-ttu-id="a8af7-133">A categoria de telemetria de dispositivo rastreia erros que ocorrem no Hub IoT e estão relacionados ao pipeline de telemetria.</span><span class="sxs-lookup"><span data-stu-id="a8af7-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="a8af7-134">Essa categoria inclui erros que ocorrem no envio de eventos de telemetria (como limitação) e no recebimento de eventos de telemetria (como leitor não autorizado).</span><span class="sxs-lookup"><span data-stu-id="a8af7-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="a8af7-135">Essa categoria não pode capturar erros causados pelo código em execução no próprio dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8af7-135">This category cannot catch errors caused by code running on the device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="a8af7-136">Comandos da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8af7-136">Cloud-to-device commands</span></span>

<span data-ttu-id="a8af7-137">A categoria de comandos da nuvem para o dispositivo rastreia erros que ocorrem no Hub IoT e são relacionados ao pipeline de mensagem da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8af7-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="a8af7-138">Essa categoria inclui erros que ocorrem no envio (tal como remetente não autorizado) e recebimento (como contagem de entrega excedida) de mensagens da nuvem para o dispositivo e no recebimento de comentários de mensagens da nuvem para o dispositivo (como comentário expirado).</span><span class="sxs-lookup"><span data-stu-id="a8af7-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="a8af7-139">Essa categoria não capturará erros de um dispositivo que manipula incorretamente uma mensagem da nuvem para o dispositivo se tal mensagem tiver sido entregue com êxito.</span><span class="sxs-lookup"><span data-stu-id="a8af7-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="a8af7-140">Conexões</span><span class="sxs-lookup"><span data-stu-id="a8af7-140">Connections</span></span>

<span data-ttu-id="a8af7-141">A categoria de conexões rastreia erros que ocorrem quando os dispositivos se conectam a um Hub IoT ou se desconectam dele.</span><span class="sxs-lookup"><span data-stu-id="a8af7-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="a8af7-142">Rastrear essa categoria é útil para identificar tentativas de conexão não autorizada e para saber quando dispositivos em áreas de conectividade ruim perdem conexão.</span><span class="sxs-lookup"><span data-stu-id="a8af7-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="a8af7-143">Carregamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="a8af7-143">File uploads</span></span>

<span data-ttu-id="a8af7-144">A categoria de carregamento de arquivo rastreia erros que ocorrem no Hub IoT e estão relacionados à funcionalidade de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="a8af7-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="a8af7-145">Essa categoria inclui:</span><span class="sxs-lookup"><span data-stu-id="a8af7-145">This category includes:</span></span>

* <span data-ttu-id="a8af7-146">Erros que ocorrem com o URI de SAS, como quando ele expirar antes que um dispositivo notifique o hub de um carregamento concluído.</span><span class="sxs-lookup"><span data-stu-id="a8af7-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="a8af7-147">Carregamentos com falha relatados pelo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8af7-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="a8af7-148">Erros que ocorrem quando um arquivo não for encontrado no armazenamento durante a criação de mensagem de notificação do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8af7-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="a8af7-149">Essa categoria não pode capturar erros que ocorrem diretamente enquanto o dispositivo está carregando um arquivo no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a8af7-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="a8af7-150">Roteamento de mensagem</span><span class="sxs-lookup"><span data-stu-id="a8af7-150">Message routing</span></span>

<span data-ttu-id="a8af7-151">A categoria de roteamento de mensagem acompanha os erros que ocorrem durante a avaliação da rota da mensagem e da integridade do ponto de extremidade, conforme visto pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8af7-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="a8af7-152">Essa categoria inclui eventos, por exemplo, quando uma regra é avaliada como "não definida", quando o Hub IoT marca um ponto de extremidade como inativo e todos os outros erros são recebidos de um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="a8af7-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="a8af7-153">Essa categoria não inclui erros específicos sobre as próprias mensagens (como erros de limitação de dispositivo), que são relatados na categoria "telemetria de dispositivo".</span><span class="sxs-lookup"><span data-stu-id="a8af7-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="a8af7-154">Exibir eventos</span><span class="sxs-lookup"><span data-stu-id="a8af7-154">View events</span></span>

<span data-ttu-id="a8af7-155">Você pode usar a ferramenta *iothub explorer* para testar rapidamente se o Hub IoT está gerando eventos de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="a8af7-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="a8af7-156">Para instalar a ferramenta, consulte as instruções no repositório do GitHub [iothub-explorer][lnk-iothub-explorer].</span><span class="sxs-lookup"><span data-stu-id="a8af7-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="a8af7-157">Certifique-se de que a categoria de monitoramento **Conexões** esteja definida como **Detalhadas** no portal.</span><span class="sxs-lookup"><span data-stu-id="a8af7-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="a8af7-158">No prompt de comando, execute o seguinte comando para ler do ponto de extremidade de monitoramento:</span><span class="sxs-lookup"><span data-stu-id="a8af7-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="a8af7-159">Em outro prompt de comando, execute o seguinte comando para simular um dispositivo enviando mensagens do dispositivo para a nuvem:</span><span class="sxs-lookup"><span data-stu-id="a8af7-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="a8af7-160">O primeiro prompt de comando mostra os eventos de monitoramento conforme o dispositivo simulado se conecta ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8af7-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="a8af7-161">Conectar-se ao ponto de extremidade de monitoramento</span><span class="sxs-lookup"><span data-stu-id="a8af7-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="a8af7-162">O ponto de extremidade de monitoramento em seu Hub IoT é um ponto de extremidade compatível com o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="a8af7-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="a8af7-163">Você pode usar qualquer mecanismo que funciona com os Hubs de Eventos para ler mensagens de monitoramento desse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="a8af7-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="a8af7-164">A amostra a seguir cria um leitor básico que não é adequado para uma implantação com alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="a8af7-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="a8af7-165">Para obter mais informações sobre como processar as mensagens dos Hubs de Eventos, confira o tutorial [Introdução aos Hubs de Eventos][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="a8af7-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="a8af7-166">Para se conectar ao ponto de extremidade de monitoramento, você precisa de uma cadeia de conexão e do nome do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="a8af7-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="a8af7-167">As etapas a seguir mostram como localizar os valores necessários no portal:</span><span class="sxs-lookup"><span data-stu-id="a8af7-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="a8af7-168">No portal, navegue até a folha de recursos do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8af7-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="a8af7-169">Escolha **Monitoramento de operações** e anote os valores do **Nome compatível com o Hub de Eventos** e do **Ponto de extremidade compatível com o Hub de Eventos**:</span><span class="sxs-lookup"><span data-stu-id="a8af7-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Valores de ponto de extremidade compatível com o Hub de Eventos][img-endpoints]

1. <span data-ttu-id="a8af7-171">Escolha **Políticas de acesso compartilhado** e, em seguida, escolha **serviço**.</span><span class="sxs-lookup"><span data-stu-id="a8af7-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="a8af7-172">Anote o valor da **Chave primária**:</span><span class="sxs-lookup"><span data-stu-id="a8af7-172">Make a note of the **Primary key** value:</span></span>

    ![Chave primária de política de acesso compartilhado de serviço][img-service-key]

<span data-ttu-id="a8af7-174">O exemplo de código C# a seguir provém de um aplicativo de console C# da **Área de Trabalho Clássica do Windows** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8af7-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="a8af7-175">O projeto tem o pacote do NuGet **WindowsAzure.ServiceBus** instalado.</span><span class="sxs-lookup"><span data-stu-id="a8af7-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="a8af7-176">Substitua o espaço reservado da cadeia de conexão por uma cadeia de conexão que usa os valores de **ponto de extremidade compatível com o Hub de Eventos** e **Chave primária** do serviço anotados anteriormente, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8af7-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="a8af7-177">Substitua o espaço reservado nome de ponto de extremidade de monitoramento pelo valor de **Nome compatível com o Hub de Eventos** que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a8af7-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a8af7-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8af7-178">Next steps</span></span>
<span data-ttu-id="a8af7-179">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="a8af7-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a8af7-180">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a8af7-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="a8af7-181">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a8af7-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md