---
title: "monitoramento de operações de Hub IoT aaaAzure | Microsoft Docs"
description: "Como as operações de Azure IoT Hub toouse monitoramento toomonitor Olá status das operações em seu hub IoT em tempo real."
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
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="46d20-103">Monitoramento de operações do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="46d20-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="46d20-104">Monitoramento de operações de IoT Hub permite toomonitor status de saudação de operações em seu hub IoT em tempo real.</span><span class="sxs-lookup"><span data-stu-id="46d20-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="46d20-105">O Hub IoT controla eventos em várias categorias de operações.</span><span class="sxs-lookup"><span data-stu-id="46d20-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="46d20-106">Você pode optar por enviar eventos de um ou mais categorias tooan ponto de extremidade do seu hub IoT para processamento.</span><span class="sxs-lookup"><span data-stu-id="46d20-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="46d20-107">Você pode monitorar dados Olá erros ou configurar o processamento mais complexo com base nos padrões de dados.</span><span class="sxs-lookup"><span data-stu-id="46d20-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="46d20-108">O Hub IoT monitora seis categorias de eventos:</span><span class="sxs-lookup"><span data-stu-id="46d20-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="46d20-109">Operações de identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="46d20-109">Device identity operations</span></span>
* <span data-ttu-id="46d20-110">Telemetria de dispositivo</span><span class="sxs-lookup"><span data-stu-id="46d20-110">Device telemetry</span></span>
* <span data-ttu-id="46d20-111">Mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="46d20-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="46d20-112">Conexões</span><span class="sxs-lookup"><span data-stu-id="46d20-112">Connections</span></span>
* <span data-ttu-id="46d20-113">Carregamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="46d20-113">File uploads</span></span>
* <span data-ttu-id="46d20-114">Roteamento de mensagem</span><span class="sxs-lookup"><span data-stu-id="46d20-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="46d20-115">Como tooenable operações de monitoramento</span><span class="sxs-lookup"><span data-stu-id="46d20-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="46d20-116">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46d20-116">Create an IoT hub.</span></span> <span data-ttu-id="46d20-117">Você pode encontrar instruções sobre como toocreate um hub IoT Olá [começar] [ lnk-get-started] guia.</span><span class="sxs-lookup"><span data-stu-id="46d20-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="46d20-118">Abra a folha de saudação do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46d20-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="46d20-119">Nela, clique em **Monitoramento de operações**.</span><span class="sxs-lookup"><span data-stu-id="46d20-119">From there, click **Operations monitoring**.</span></span>

    ![Operações de acesso de monitoramento de configuração no portal de saudação][1]

1. <span data-ttu-id="46d20-121">Selecione Olá monitoramento categorias que você deseja toomonitor e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="46d20-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="46d20-122">Olá eventos estão disponíveis para leitura do ponto de extremidade de saudação compatível com o Hub de evento listada na **configurações de monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="46d20-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="46d20-123">Olá ponto de extremidade de IoT Hub é chamado `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="46d20-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configurar o monitoramento de operações no Hub IoT][2]

> [!NOTE]
> <span data-ttu-id="46d20-125">Selecionando **detalhado** monitoramento para Olá **conexões** categoria faz com que o IoT Hub toogenerate mensagens de diagnósticos adicionais.</span><span class="sxs-lookup"><span data-stu-id="46d20-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="46d20-126">Para todas as outras categorias, Olá **detalhado** quantidade de saudação do IoT Hub de informações de alterações de configuração incluem em cada mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="46d20-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="46d20-127">Categorias de evento e como toouse-los</span><span class="sxs-lookup"><span data-stu-id="46d20-127">Event categories and how toouse them</span></span>

<span data-ttu-id="46d20-128">Cada categoria de monitoramento de operações rastreia um tipo diferente de interação com o Hub IoT e cada categoria de monitoramento tem um esquema que define como os eventos nessa categoria são estruturados.</span><span class="sxs-lookup"><span data-stu-id="46d20-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="46d20-129">Operações de identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="46d20-129">Device identity operations</span></span>

<span data-ttu-id="46d20-130">categoria de operações de identidade de dispositivo Olá rastreia erros que ocorrem durante a tentativa de toocreate, atualizar ou excluir uma entrada no registro de identidade do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46d20-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="46d20-131">O rastreamento dessa categoria é útil em cenários de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="46d20-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="46d20-132">Telemetria de dispositivo</span><span class="sxs-lookup"><span data-stu-id="46d20-132">Device telemetry</span></span>

<span data-ttu-id="46d20-133">categoria de telemetria do dispositivo Olá rastreia erros que ocorrem no hub IoT de saudação e pipeline de telemetria toohello relacionados.</span><span class="sxs-lookup"><span data-stu-id="46d20-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="46d20-134">Essa categoria inclui erros que ocorrem no envio de eventos de telemetria (como limitação) e no recebimento de eventos de telemetria (como leitor não autorizado).</span><span class="sxs-lookup"><span data-stu-id="46d20-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="46d20-135">Esta categoria não pode capturar erros causados pelo código em execução no dispositivo de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="46d20-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="46d20-136">Comandos da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="46d20-136">Cloud-to-device commands</span></span>

<span data-ttu-id="46d20-137">categoria de comandos de nuvem para dispositivo Olá rastreia erros que ocorrem no hub IoT de saudação e pipeline de mensagem de nuvem para dispositivo toohello relacionados.</span><span class="sxs-lookup"><span data-stu-id="46d20-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="46d20-138">Essa categoria inclui erros que ocorrem no envio (tal como remetente não autorizado) e recebimento (como contagem de entrega excedida) de mensagens da nuvem para o dispositivo e no recebimento de comentários de mensagens da nuvem para o dispositivo (como comentário expirado).</span><span class="sxs-lookup"><span data-stu-id="46d20-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="46d20-139">Esta categoria não capturar erros de um dispositivo que manipula incorretamente uma mensagem de nuvem para dispositivo se a mensagem de saudação do nuvem para dispositivo foi entregue com êxito.</span><span class="sxs-lookup"><span data-stu-id="46d20-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="46d20-140">Conexões</span><span class="sxs-lookup"><span data-stu-id="46d20-140">Connections</span></span>

<span data-ttu-id="46d20-141">categoria de conexões Olá rastreia erros que ocorrem quando os dispositivos se conectar ou desconectar um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46d20-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="46d20-142">Rastrear essa categoria é útil para identificar tentativas de conexão não autorizada e para saber quando dispositivos em áreas de conectividade ruim perdem conexão.</span><span class="sxs-lookup"><span data-stu-id="46d20-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="46d20-143">Carregamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="46d20-143">File uploads</span></span>

<span data-ttu-id="46d20-144">categoria de carregamento de arquivo Hello rastreia erros que ocorrem no hub IoT de saudação e funcionalidade de carregamento de toofile relacionados.</span><span class="sxs-lookup"><span data-stu-id="46d20-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="46d20-145">Essa categoria inclui:</span><span class="sxs-lookup"><span data-stu-id="46d20-145">This category includes:</span></span>

* <span data-ttu-id="46d20-146">Erros que ocorrem com hello SAS URI, como quando ele expirar antes que um dispositivo notifica o hub de saudação de um carregamento concluído.</span><span class="sxs-lookup"><span data-stu-id="46d20-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="46d20-147">Falha carregamentos relatados pelo dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="46d20-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="46d20-148">Erros que ocorrem quando um arquivo não for encontrado no armazenamento durante a criação de mensagem de notificação do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46d20-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="46d20-149">Esta categoria não pode capturar erros que ocorrem diretamente ao dispositivo hello está carregando um arquivo toostorage.</span><span class="sxs-lookup"><span data-stu-id="46d20-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="46d20-150">Roteamento de mensagem</span><span class="sxs-lookup"><span data-stu-id="46d20-150">Message routing</span></span>

<span data-ttu-id="46d20-151">categoria de roteamento de mensagem de saudação rastreia erros que ocorrem durante a avaliação de rota de mensagem e a integridade do ponto de extremidade conforme percebido pelo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="46d20-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="46d20-152">Essa categoria inclui eventos, como quando uma regra é avaliada muito "indefinidos", ao IoT Hub marca um ponto de extremidade como inativo e todos os outros erros recebidos de um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="46d20-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="46d20-153">Esta categoria não inclui erros específicos sobre mensagens de saudação si (como dispositivo erros de limitação), que são relatados na categoria de "telemetria do dispositivo" hello.</span><span class="sxs-lookup"><span data-stu-id="46d20-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="46d20-154">Exibir eventos</span><span class="sxs-lookup"><span data-stu-id="46d20-154">View events</span></span>

<span data-ttu-id="46d20-155">Você pode usar o hello *Gerenciador de Hub IOT* tooquickly da ferramenta de teste que o hub IoT está gerando eventos de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="46d20-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="46d20-156">Olá tooinstall ferramenta, consulte as instruções de Olá Olá [Gerenciador de Hub IOT] [ lnk-iothub-explorer] repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="46d20-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="46d20-157">Verifique se Olá **conexões** monitoramento categoria está definido muito**detalhado** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="46d20-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="46d20-158">No prompt de comando, execute Olá após o comando tooread Olá monitoramento de ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="46d20-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="46d20-159">No prompt de comando outra, execute Olá toosimulate de comando a seguir um dispositivo de envio de mensagens de dispositivo para nuvem:</span><span class="sxs-lookup"><span data-stu-id="46d20-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="46d20-160">prompt de comando da primeira Olá mostra eventos de monitoramento de saudação como dispositivo simulado Olá conecta tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="46d20-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="46d20-161">Conecte-se toohello monitoramento de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="46d20-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="46d20-162">Olá, monitoramento de ponto de extremidade em seu hub IoT é um ponto de extremidade compatível com o evento Hub.</span><span class="sxs-lookup"><span data-stu-id="46d20-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="46d20-163">Você pode usar qualquer mecanismo que funciona com Hubs de eventos tooread monitoramentos mensagens esse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="46d20-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="46d20-164">Olá, exemplo a seguir cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="46d20-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="46d20-165">Para obter mais informações sobre como tooprocess mensagens de Hubs de eventos, consulte Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="46d20-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="46d20-166">tooconnect toohello ponto de extremidade monitoramento, é necessário um nome de ponto de extremidade de saudação e de cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="46d20-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="46d20-167">Olá, as etapas a seguir mostra como toofind Olá valores necessários no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="46d20-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="46d20-168">No portal de hello, navegue até tooyour folha de recursos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="46d20-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="46d20-169">Escolha **monitoramento das operações**e anote Olá **nome compatível com o evento Hub** e **ponto de extremidade compatível com o evento Hub** valores:</span><span class="sxs-lookup"><span data-stu-id="46d20-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Valores de ponto de extremidade compatível com o Hub de Eventos][img-endpoints]

1. <span data-ttu-id="46d20-171">Escolha **Políticas de acesso compartilhado** e, em seguida, escolha **serviço**.</span><span class="sxs-lookup"><span data-stu-id="46d20-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="46d20-172">Anote Olá **chave primária** valor:</span><span class="sxs-lookup"><span data-stu-id="46d20-172">Make a note of hello **Primary key** value:</span></span>

    ![Chave primária de política de acesso compartilhado de serviço][img-service-key]

<span data-ttu-id="46d20-174">Olá seguinte exemplo de código c# é obtido de um Visual Studio **área de trabalho clássica do Windows** o aplicativo de console c#.</span><span class="sxs-lookup"><span data-stu-id="46d20-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="46d20-175">projeto de saudação tem Olá **windowsazure. ServiceBus** pacote do NuGet instalada.</span><span class="sxs-lookup"><span data-stu-id="46d20-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="46d20-176">Substitua o espaço reservado de cadeia de caracteres de conexão Olá com uma cadeia de caracteres de conexão que usa Olá **ponto de extremidade compatível com o evento Hub** e serviço **chave primária** valores anotados anteriormente, conforme mostrado na seguinte Olá exemplo:</span><span class="sxs-lookup"><span data-stu-id="46d20-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="46d20-177">Substituir saudação monitoramento de espaço reservado para nome de ponto de extremidade com hello **nome compatível com o evento Hub** valor que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46d20-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="46d20-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46d20-178">Next steps</span></span>
<span data-ttu-id="46d20-179">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="46d20-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="46d20-180">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="46d20-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="46d20-181">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="46d20-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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