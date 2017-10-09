---
title: "ambiente de tempo série Insights aaaSend eventos tooAzure | Microsoft Docs"
description: "Este tutorial apresenta o ambiente de informações da série de tempo de tooyour Olá etapas toopush eventos"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Enviar o ambiente de informações da série de tempo de tooa eventos usando o hub de eventos

Este tutorial explica como toocreate configurar hub de eventos e executar um toopush do aplicativo de exemplo de eventos. Se você tiver um hub de eventos existente com eventos no formato JSON, ignore este tutorial e exibir seu ambiente na [análise de séries temporais](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Configurar um hub de eventos
1. toocreate um hub de eventos, siga as instruções do Hub de eventos de saudação [documentação](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Certifique-se de criar um grupo de consumidores que é usado exclusivamente pela sua origem de evento de Análise de Séries Temporais.

  > [!IMPORTANT]
  > Verifique se esse grupo de consumidores não é usado por qualquer outro serviço (como um trabalho do Stream Analytics ou outro ambiente de Análise de Séries Temporais). Se o grupo de consumidores é usado por outros serviços, leia a operação é afetada negativamente para esse ambiente e Olá outros serviços. Se você estiver usando "$Default" como o grupo de consumidores hello, isso pode levar a reutilização de toopotential por outros leitores.

  ![Selecione o grupo de consumidores do hub de eventos](media/send-events/consumer-group.png)

3. No hub de eventos hello, crie "MySendPolicy" que é usado toosend eventos no exemplo do hello csharp.

  ![Selecione Políticas de acesso compartilhado e clique no botão Adicionar](media/send-events/shared-access-policy.png)  

  ![Adicione uma política de acesso compartilhado](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Criar origem de evento de Análise de Séries Temporais
1. Se você não criou uma fonte de evento, execute [estas instruções](time-series-insights-add-event-source.md) toocreate uma fonte de evento.

2. Especifique "deviceTimestamp" como nome de propriedade de carimbo de hora hello – essa propriedade é usada como Olá carimbo de hora real no exemplo de csharp hello. nome da propriedade timestamp Olá diferencia maiusculas de minúsculas e os valores devem seguir o formato de saudação __AAAA-MM-ddTHH. FFFFFFFK__ quando enviado como o hub de tooevent JSON. Se a propriedade Olá não existe no evento Olá, em seguida, hello tempo de enfileiramento do hub de eventos é usado.

  ![Criar uma origem de eventos](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Eventos de toopush de código de exemplo
1. Vá toohello política de hub de eventos "MySendPolicy" e copie a cadeia de caracteres de conexão de saudação com a chave de política hello.

  ![Copie a cadeia de conexão MySendPolicy](media/send-events/sample-code-connection-string.png)

2. Execute Olá código a seguir que os eventos toosend 600 por cada um dos dispositivos Olá três. Atualize `eventHubConnectionString` com a sua cadeia de conexão.

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a>Formas de JSON com suporte
### <a name="sample-1"></a>Exemplo 1

#### <a name="input"></a>Entrada

Um objeto JSON simples.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Saída - 1 evento

|ID|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Exemplo 2

#### <a name="input"></a>Entrada
Uma matriz JSON com dois objetos JSON. Cada objeto JSON será convertido tooan eventos.
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a>Saída - 2 eventos

|ID|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>Exemplo 3

#### <a name="input"></a>Entrada

Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON.
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a>Saída - 2 eventos
Observe que a propriedade hello "local" é copiada por tooeach de evento de saudação.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|Oeste dos EUA|device1|2016-01-08T01:08:00Z|
|Oeste dos EUA|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Exemplo 4

#### <a name="input"></a>Entrada

Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON. Essa entrada demonstra que propriedades globais Olá podem ser representadas pelo objeto JSON complexo de saudação.

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a>Saída - 2 eventos

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|Oeste dos EUA|manufacturer1|Leste dos EUA|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|Oeste dos EUA|manufacturer1|Leste dos EUA|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>Próximas etapas

* Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)
