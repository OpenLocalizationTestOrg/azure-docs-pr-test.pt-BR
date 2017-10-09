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
# <a name="iot-hub-operations-monitoring"></a>Monitoramento de operações do Hub IoT

Monitoramento de operações de IoT Hub permite toomonitor status de saudação de operações em seu hub IoT em tempo real. O Hub IoT controla eventos em várias categorias de operações. Você pode optar por enviar eventos de um ou mais categorias tooan ponto de extremidade do seu hub IoT para processamento. Você pode monitorar dados Olá erros ou configurar o processamento mais complexo com base nos padrões de dados.

O Hub IoT monitora seis categorias de eventos:

* Operações de identidade do dispositivo
* Telemetria de dispositivo
* Mensagens da nuvem para o dispositivo
* Conexões
* Carregamentos de arquivos
* Roteamento de mensagem

## <a name="how-tooenable-operations-monitoring"></a>Como tooenable operações de monitoramento

1. Crie um Hub IoT. Você pode encontrar instruções sobre como toocreate um hub IoT Olá [começar] [ lnk-get-started] guia.

1. Abra a folha de saudação do seu hub IoT. Nela, clique em **Monitoramento de operações**.

    ![Operações de acesso de monitoramento de configuração no portal de saudação][1]

1. Selecione Olá monitoramento categorias que você deseja toomonitor e, em seguida, clique em **salvar**. Olá eventos estão disponíveis para leitura do ponto de extremidade de saudação compatível com o Hub de evento listada na **configurações de monitoramento**. Olá ponto de extremidade de IoT Hub é chamado `messages/operationsmonitoringevents`.

    ![Configurar o monitoramento de operações no Hub IoT][2]

> [!NOTE]
> Selecionando **detalhado** monitoramento para Olá **conexões** categoria faz com que o IoT Hub toogenerate mensagens de diagnósticos adicionais. Para todas as outras categorias, Olá **detalhado** quantidade de saudação do IoT Hub de informações de alterações de configuração incluem em cada mensagem de erro.

## <a name="event-categories-and-how-toouse-them"></a>Categorias de evento e como toouse-los

Cada categoria de monitoramento de operações rastreia um tipo diferente de interação com o Hub IoT e cada categoria de monitoramento tem um esquema que define como os eventos nessa categoria são estruturados.

### <a name="device-identity-operations"></a>Operações de identidade do dispositivo

categoria de operações de identidade de dispositivo Olá rastreia erros que ocorrem durante a tentativa de toocreate, atualizar ou excluir uma entrada no registro de identidade do seu hub IoT. O rastreamento dessa categoria é útil em cenários de provisionamento.

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

### <a name="device-telemetry"></a>Telemetria de dispositivo

categoria de telemetria do dispositivo Olá rastreia erros que ocorrem no hub IoT de saudação e pipeline de telemetria toohello relacionados. Essa categoria inclui erros que ocorrem no envio de eventos de telemetria (como limitação) e no recebimento de eventos de telemetria (como leitor não autorizado). Esta categoria não pode capturar erros causados pelo código em execução no dispositivo de saudação em si.

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

### <a name="cloud-to-device-commands"></a>Comandos da nuvem para o dispositivo

categoria de comandos de nuvem para dispositivo Olá rastreia erros que ocorrem no hub IoT de saudação e pipeline de mensagem de nuvem para dispositivo toohello relacionados. Essa categoria inclui erros que ocorrem no envio (tal como remetente não autorizado) e recebimento (como contagem de entrega excedida) de mensagens da nuvem para o dispositivo e no recebimento de comentários de mensagens da nuvem para o dispositivo (como comentário expirado). Esta categoria não capturar erros de um dispositivo que manipula incorretamente uma mensagem de nuvem para dispositivo se a mensagem de saudação do nuvem para dispositivo foi entregue com êxito.

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

### <a name="connections"></a>Conexões

categoria de conexões Olá rastreia erros que ocorrem quando os dispositivos se conectar ou desconectar um hub IoT. Rastrear essa categoria é útil para identificar tentativas de conexão não autorizada e para saber quando dispositivos em áreas de conectividade ruim perdem conexão.

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

### <a name="file-uploads"></a>Carregamentos de arquivos

categoria de carregamento de arquivo Hello rastreia erros que ocorrem no hub IoT de saudação e funcionalidade de carregamento de toofile relacionados. Essa categoria inclui:

* Erros que ocorrem com hello SAS URI, como quando ele expirar antes que um dispositivo notifica o hub de saudação de um carregamento concluído.
* Falha carregamentos relatados pelo dispositivo hello.
* Erros que ocorrem quando um arquivo não for encontrado no armazenamento durante a criação de mensagem de notificação do Hub IoT.

Esta categoria não pode capturar erros que ocorrem diretamente ao dispositivo hello está carregando um arquivo toostorage.

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

### <a name="message-routing"></a>Roteamento de mensagem

categoria de roteamento de mensagem de saudação rastreia erros que ocorrem durante a avaliação de rota de mensagem e a integridade do ponto de extremidade conforme percebido pelo IoT Hub. Essa categoria inclui eventos, como quando uma regra é avaliada muito "indefinidos", ao IoT Hub marca um ponto de extremidade como inativo e todos os outros erros recebidos de um ponto de extremidade. Esta categoria não inclui erros específicos sobre mensagens de saudação si (como dispositivo erros de limitação), que são relatados na categoria de "telemetria do dispositivo" hello.

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

## <a name="view-events"></a>Exibir eventos

Você pode usar o hello *Gerenciador de Hub IOT* tooquickly da ferramenta de teste que o hub IoT está gerando eventos de monitoramento. Olá tooinstall ferramenta, consulte as instruções de Olá Olá [Gerenciador de Hub IOT] [ lnk-iothub-explorer] repositório GitHub.

1. Verifique se Olá **conexões** monitoramento categoria está definido muito**detalhado** no portal de saudação.

1. No prompt de comando, execute Olá após o comando tooread Olá monitoramento de ponto de extremidade:

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. No prompt de comando outra, execute Olá toosimulate de comando a seguir um dispositivo de envio de mensagens de dispositivo para nuvem:

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. prompt de comando da primeira Olá mostra eventos de monitoramento de saudação como dispositivo simulado Olá conecta tooyour hub IoT.

## <a name="connect-toohello-monitoring-endpoint"></a>Conecte-se toohello monitoramento de ponto de extremidade

Olá, monitoramento de ponto de extremidade em seu hub IoT é um ponto de extremidade compatível com o evento Hub. Você pode usar qualquer mecanismo que funciona com Hubs de eventos tooread monitoramentos mensagens esse ponto de extremidade. Olá, exemplo a seguir cria um leitor básico que não é adequado para uma implantação de alta taxa de transferência. Para obter mais informações sobre como tooprocess mensagens de Hubs de eventos, consulte Olá [Introdução aos Hubs de eventos] [ lnk-eventhubs-tutorial] tutorial.

tooconnect toohello ponto de extremidade monitoramento, é necessário um nome de ponto de extremidade de saudação e de cadeia de caracteres de conexão. Olá, as etapas a seguir mostra como toofind Olá valores necessários no portal de saudação:

1. No portal de hello, navegue até tooyour folha de recursos de IoT Hub.

1. Escolha **monitoramento das operações**e anote Olá **nome compatível com o evento Hub** e **ponto de extremidade compatível com o evento Hub** valores:

    ![Valores de ponto de extremidade compatível com o Hub de Eventos][img-endpoints]

1. Escolha **Políticas de acesso compartilhado** e, em seguida, escolha **serviço**. Anote Olá **chave primária** valor:

    ![Chave primária de política de acesso compartilhado de serviço][img-service-key]

Olá seguinte exemplo de código c# é obtido de um Visual Studio **área de trabalho clássica do Windows** o aplicativo de console c#. projeto de saudação tem Olá **windowsazure. ServiceBus** pacote do NuGet instalada.

* Substitua o espaço reservado de cadeia de caracteres de conexão Olá com uma cadeia de caracteres de conexão que usa Olá **ponto de extremidade compatível com o evento Hub** e serviço **chave primária** valores anotados anteriormente, conforme mostrado na seguinte Olá exemplo:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Substituir saudação monitoramento de espaço reservado para nome de ponto de extremidade com hello **nome compatível com o evento Hub** valor que você anotou anteriormente.

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

## <a name="next-steps"></a>Próximas etapas
toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

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