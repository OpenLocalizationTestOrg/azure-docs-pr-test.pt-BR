---
title: "Enviar eventos para um ambiente de Análise de Séries Temporais do Azure | Microsoft Docs"
description: "Este tutorial aborda as etapas enviar eventos para seu ambiente de Análise de Séries Temporais por push"
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
ms.openlocfilehash: b4ef96a045393f28b3cd750068fe82a5a8411afa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="2d17c-103">Envie eventos para um ambiente de Análise de Séries Temporais usando o hub de eventos</span><span class="sxs-lookup"><span data-stu-id="2d17c-103">Send events to a Time Series Insights environment using event hub</span></span>

<span data-ttu-id="2d17c-104">Este tutorial explica como criar e configurar o hub de eventos e executa um aplicativo de exemplo para enviar eventos.</span><span class="sxs-lookup"><span data-stu-id="2d17c-104">This tutorial explains how to create and configure event hub and run a sample application to push events.</span></span> <span data-ttu-id="2d17c-105">Se você tiver um hub de eventos existente com eventos no formato JSON, ignore este tutorial e exibir seu ambiente na [análise de séries temporais](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d17c-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="2d17c-106">Configurar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="2d17c-106">Configure an event hub</span></span>
1. <span data-ttu-id="2d17c-107">Para criar um hub de eventos, siga as instruções na [documentação](https://docs.microsoft.com/azure/event-hubs/event-hubs-create) sobre Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="2d17c-107">To create an event hub, follow instructions from the Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="2d17c-108">Certifique-se de criar um grupo de consumidores que é usado exclusivamente pela sua origem de evento de Análise de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="2d17c-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2d17c-109">Verifique se esse grupo de consumidores não é usado por qualquer outro serviço (como um trabalho do Stream Analytics ou outro ambiente de Análise de Séries Temporais).</span><span class="sxs-lookup"><span data-stu-id="2d17c-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="2d17c-110">Se o grupo de consumidores é usado por outros serviços, a operação de leitura é prejudicada para esse ambiente e outros serviços.</span><span class="sxs-lookup"><span data-stu-id="2d17c-110">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="2d17c-111">Se você estiver usando "$Default" como o grupo de consumidores, isso pode levar à potencial reutilização por outros leitores.</span><span class="sxs-lookup"><span data-stu-id="2d17c-111">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

  ![Selecione o grupo de consumidores do hub de eventos](media/send-events/consumer-group.png)

3. <span data-ttu-id="2d17c-113">No hub de eventos, crie "MySendPolicy" que é usado para enviar eventos no exemplo csharp.</span><span class="sxs-lookup"><span data-stu-id="2d17c-113">On the event hub, create “MySendPolicy” that is used to send events in the csharp sample.</span></span>

  ![Selecione Políticas de acesso compartilhado e clique no botão Adicionar](media/send-events/shared-access-policy.png)  

  ![Adicione uma política de acesso compartilhado](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="2d17c-116">Criar origem de evento de Análise de Séries Temporais</span><span class="sxs-lookup"><span data-stu-id="2d17c-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="2d17c-117">Se você ainda não criou a origem do evento, siga [estas instruções](time-series-insights-add-event-source.md) para criar uma origem de evento.</span><span class="sxs-lookup"><span data-stu-id="2d17c-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) to create an event source.</span></span>

2. <span data-ttu-id="2d17c-118">Especifique "deviceTimestamp" como o nome da propriedade de carimbo de data/hora – esta propriedade é usada como o carimbo de data/hora real no exemplo csharp.</span><span class="sxs-lookup"><span data-stu-id="2d17c-118">Specify “deviceTimestamp” as the timestamp property name – this property is used as the actual timestamp in the csharp sample.</span></span> <span data-ttu-id="2d17c-119">O nome da propriedade de carimbo de data/hora diferencia maiúsculas de minúsculas e os valores precisam seguir o formato __aaaa-MM-ddTHH:mm:ss.FFFFFFFK__ quando enviado como JSON ao hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2d17c-119">The timestamp property name is case-sensitive and values must follow the format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON to event hub.</span></span> <span data-ttu-id="2d17c-120">Se a propriedade não existir no evento, o tempo de enfileiramento do hub de eventos será usado.</span><span class="sxs-lookup"><span data-stu-id="2d17c-120">If the property does not exist in the event, then the event hub enqueued time is used.</span></span>

  ![Criar uma origem de eventos](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a><span data-ttu-id="2d17c-122">Código de exemplo para enviar eventos por push</span><span class="sxs-lookup"><span data-stu-id="2d17c-122">Sample code to push events</span></span>
1. <span data-ttu-id="2d17c-123">Vá para a política de hub de eventos "MySendPolicy" e copie a cadeia de conexão com a chave da política.</span><span class="sxs-lookup"><span data-stu-id="2d17c-123">Go to the event hub policy “MySendPolicy” and copy the connection string with the policy key.</span></span>

  ![Copie a cadeia de conexão MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="2d17c-125">Execute o seguinte código para enviar 600 eventos a cada um dos três dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2d17c-125">Run the following code that to send 600 events per each of the three devices.</span></span> <span data-ttu-id="2d17c-126">Atualize `eventHubConnectionString` com a sua cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="2d17c-126">Update `eventHubConnectionString` with your connection string.</span></span>

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

                // Send JSON to event hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="2d17c-127">Formas de JSON com suporte</span><span class="sxs-lookup"><span data-stu-id="2d17c-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="2d17c-128">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="2d17c-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="2d17c-129">Entrada</span><span class="sxs-lookup"><span data-stu-id="2d17c-129">Input</span></span>

<span data-ttu-id="2d17c-130">Um objeto JSON simples.</span><span class="sxs-lookup"><span data-stu-id="2d17c-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="2d17c-131">Saída - 1 evento</span><span class="sxs-lookup"><span data-stu-id="2d17c-131">Output - 1 event</span></span>

|<span data-ttu-id="2d17c-132">ID</span><span class="sxs-lookup"><span data-stu-id="2d17c-132">id</span></span>|<span data-ttu-id="2d17c-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="2d17c-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="2d17c-134">device1</span><span class="sxs-lookup"><span data-stu-id="2d17c-134">device1</span></span>|<span data-ttu-id="2d17c-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="2d17c-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="2d17c-136">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="2d17c-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="2d17c-137">Entrada</span><span class="sxs-lookup"><span data-stu-id="2d17c-137">Input</span></span>
<span data-ttu-id="2d17c-138">Uma matriz JSON com dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="2d17c-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="2d17c-139">Cada objeto JSON será convertido em um evento.</span><span class="sxs-lookup"><span data-stu-id="2d17c-139">Each JSON object will be converted to an event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="2d17c-140">Saída - 2 eventos</span><span class="sxs-lookup"><span data-stu-id="2d17c-140">Output - 2 Events</span></span>

|<span data-ttu-id="2d17c-141">ID</span><span class="sxs-lookup"><span data-stu-id="2d17c-141">id</span></span>|<span data-ttu-id="2d17c-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="2d17c-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="2d17c-143">device1</span><span class="sxs-lookup"><span data-stu-id="2d17c-143">device1</span></span>|<span data-ttu-id="2d17c-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="2d17c-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="2d17c-145">device2</span><span class="sxs-lookup"><span data-stu-id="2d17c-145">device2</span></span>|<span data-ttu-id="2d17c-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="2d17c-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="2d17c-147">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="2d17c-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="2d17c-148">Entrada</span><span class="sxs-lookup"><span data-stu-id="2d17c-148">Input</span></span>

<span data-ttu-id="2d17c-149">Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="2d17c-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="2d17c-150">Saída - 2 eventos</span><span class="sxs-lookup"><span data-stu-id="2d17c-150">Output - 2 Events</span></span>
<span data-ttu-id="2d17c-151">Observe que a propriedade "location" é copiada para cada evento.</span><span class="sxs-lookup"><span data-stu-id="2d17c-151">Note that the property "location" is copied over to each of the event.</span></span>

|<span data-ttu-id="2d17c-152">location</span><span class="sxs-lookup"><span data-stu-id="2d17c-152">location</span></span>|<span data-ttu-id="2d17c-153">events.id</span><span class="sxs-lookup"><span data-stu-id="2d17c-153">events.id</span></span>|<span data-ttu-id="2d17c-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="2d17c-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="2d17c-155">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="2d17c-155">WestUs</span></span>|<span data-ttu-id="2d17c-156">device1</span><span class="sxs-lookup"><span data-stu-id="2d17c-156">device1</span></span>|<span data-ttu-id="2d17c-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="2d17c-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="2d17c-158">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="2d17c-158">WestUs</span></span>|<span data-ttu-id="2d17c-159">device2</span><span class="sxs-lookup"><span data-stu-id="2d17c-159">device2</span></span>|<span data-ttu-id="2d17c-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="2d17c-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="2d17c-161">Exemplo 4</span><span class="sxs-lookup"><span data-stu-id="2d17c-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="2d17c-162">Entrada</span><span class="sxs-lookup"><span data-stu-id="2d17c-162">Input</span></span>

<span data-ttu-id="2d17c-163">Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="2d17c-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="2d17c-164">Essa entrada demonstra que as propriedades globais podem ser representadas pelo objeto JSON complexo.</span><span class="sxs-lookup"><span data-stu-id="2d17c-164">This input demonstrates that the global properties may be represented by the complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="2d17c-165">Saída - 2 eventos</span><span class="sxs-lookup"><span data-stu-id="2d17c-165">Output - 2 Events</span></span>

|<span data-ttu-id="2d17c-166">location</span><span class="sxs-lookup"><span data-stu-id="2d17c-166">location</span></span>|<span data-ttu-id="2d17c-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="2d17c-167">manufacturer.name</span></span>|<span data-ttu-id="2d17c-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="2d17c-168">manufacturer.location</span></span>|<span data-ttu-id="2d17c-169">events.id</span><span class="sxs-lookup"><span data-stu-id="2d17c-169">events.id</span></span>|<span data-ttu-id="2d17c-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="2d17c-170">events.timestamp</span></span>|<span data-ttu-id="2d17c-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="2d17c-171">events.data.type</span></span>|<span data-ttu-id="2d17c-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="2d17c-172">events.data.units</span></span>|<span data-ttu-id="2d17c-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="2d17c-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="2d17c-174">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="2d17c-174">WestUs</span></span>|<span data-ttu-id="2d17c-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="2d17c-175">manufacturer1</span></span>|<span data-ttu-id="2d17c-176">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="2d17c-176">EastUs</span></span>|<span data-ttu-id="2d17c-177">device1</span><span class="sxs-lookup"><span data-stu-id="2d17c-177">device1</span></span>|<span data-ttu-id="2d17c-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="2d17c-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="2d17c-179">pressure</span><span class="sxs-lookup"><span data-stu-id="2d17c-179">pressure</span></span>|<span data-ttu-id="2d17c-180">psi</span><span class="sxs-lookup"><span data-stu-id="2d17c-180">psi</span></span>|<span data-ttu-id="2d17c-181">108.09</span><span class="sxs-lookup"><span data-stu-id="2d17c-181">108.09</span></span>|
|<span data-ttu-id="2d17c-182">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="2d17c-182">WestUs</span></span>|<span data-ttu-id="2d17c-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="2d17c-183">manufacturer1</span></span>|<span data-ttu-id="2d17c-184">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="2d17c-184">EastUs</span></span>|<span data-ttu-id="2d17c-185">device2</span><span class="sxs-lookup"><span data-stu-id="2d17c-185">device2</span></span>|<span data-ttu-id="2d17c-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="2d17c-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="2d17c-187">vibration</span><span class="sxs-lookup"><span data-stu-id="2d17c-187">vibration</span></span>|<span data-ttu-id="2d17c-188">abs G</span><span class="sxs-lookup"><span data-stu-id="2d17c-188">abs G</span></span>|<span data-ttu-id="2d17c-189">217.09</span><span class="sxs-lookup"><span data-stu-id="2d17c-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="2d17c-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d17c-190">Next steps</span></span>

* <span data-ttu-id="2d17c-191">Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="2d17c-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
