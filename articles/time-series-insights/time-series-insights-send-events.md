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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="1957e-103">Enviar o ambiente de informações da série de tempo de tooa eventos usando o hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1957e-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="1957e-104">Este tutorial explica como toocreate configurar hub de eventos e executar um toopush do aplicativo de exemplo de eventos.</span><span class="sxs-lookup"><span data-stu-id="1957e-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="1957e-105">Se você tiver um hub de eventos existente com eventos no formato JSON, ignore este tutorial e exibir seu ambiente na [análise de séries temporais](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1957e-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="1957e-106">Configurar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1957e-106">Configure an event hub</span></span>
1. <span data-ttu-id="1957e-107">toocreate um hub de eventos, siga as instruções do Hub de eventos de saudação [documentação](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="1957e-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="1957e-108">Certifique-se de criar um grupo de consumidores que é usado exclusivamente pela sua origem de evento de Análise de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="1957e-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1957e-109">Verifique se esse grupo de consumidores não é usado por qualquer outro serviço (como um trabalho do Stream Analytics ou outro ambiente de Análise de Séries Temporais).</span><span class="sxs-lookup"><span data-stu-id="1957e-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="1957e-110">Se o grupo de consumidores é usado por outros serviços, leia a operação é afetada negativamente para esse ambiente e Olá outros serviços.</span><span class="sxs-lookup"><span data-stu-id="1957e-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="1957e-111">Se você estiver usando "$Default" como o grupo de consumidores hello, isso pode levar a reutilização de toopotential por outros leitores.</span><span class="sxs-lookup"><span data-stu-id="1957e-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Selecione o grupo de consumidores do hub de eventos](media/send-events/consumer-group.png)

3. <span data-ttu-id="1957e-113">No hub de eventos hello, crie "MySendPolicy" que é usado toosend eventos no exemplo do hello csharp.</span><span class="sxs-lookup"><span data-stu-id="1957e-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Selecione Políticas de acesso compartilhado e clique no botão Adicionar](media/send-events/shared-access-policy.png)  

  ![Adicione uma política de acesso compartilhado](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="1957e-116">Criar origem de evento de Análise de Séries Temporais</span><span class="sxs-lookup"><span data-stu-id="1957e-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="1957e-117">Se você não criou uma fonte de evento, execute [estas instruções](time-series-insights-add-event-source.md) toocreate uma fonte de evento.</span><span class="sxs-lookup"><span data-stu-id="1957e-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="1957e-118">Especifique "deviceTimestamp" como nome de propriedade de carimbo de hora hello – essa propriedade é usada como Olá carimbo de hora real no exemplo de csharp hello.</span><span class="sxs-lookup"><span data-stu-id="1957e-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="1957e-119">nome da propriedade timestamp Olá diferencia maiusculas de minúsculas e os valores devem seguir o formato de saudação __AAAA-MM-ddTHH. FFFFFFFK__ quando enviado como o hub de tooevent JSON.</span><span class="sxs-lookup"><span data-stu-id="1957e-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="1957e-120">Se a propriedade Olá não existe no evento Olá, em seguida, hello tempo de enfileiramento do hub de eventos é usado.</span><span class="sxs-lookup"><span data-stu-id="1957e-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Criar uma origem de eventos](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="1957e-122">Eventos de toopush de código de exemplo</span><span class="sxs-lookup"><span data-stu-id="1957e-122">Sample code toopush events</span></span>
1. <span data-ttu-id="1957e-123">Vá toohello política de hub de eventos "MySendPolicy" e copie a cadeia de caracteres de conexão de saudação com a chave de política hello.</span><span class="sxs-lookup"><span data-stu-id="1957e-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![Copie a cadeia de conexão MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="1957e-125">Execute Olá código a seguir que os eventos toosend 600 por cada um dos dispositivos Olá três.</span><span class="sxs-lookup"><span data-stu-id="1957e-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="1957e-126">Atualize `eventHubConnectionString` com a sua cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="1957e-126">Update `eventHubConnectionString` with your connection string.</span></span>

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
## <a name="supported-json-shapes"></a><span data-ttu-id="1957e-127">Formas de JSON com suporte</span><span class="sxs-lookup"><span data-stu-id="1957e-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="1957e-128">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="1957e-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="1957e-129">Entrada</span><span class="sxs-lookup"><span data-stu-id="1957e-129">Input</span></span>

<span data-ttu-id="1957e-130">Um objeto JSON simples.</span><span class="sxs-lookup"><span data-stu-id="1957e-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="1957e-131">Saída - 1 evento</span><span class="sxs-lookup"><span data-stu-id="1957e-131">Output - 1 event</span></span>

|<span data-ttu-id="1957e-132">ID</span><span class="sxs-lookup"><span data-stu-id="1957e-132">id</span></span>|<span data-ttu-id="1957e-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="1957e-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="1957e-134">device1</span><span class="sxs-lookup"><span data-stu-id="1957e-134">device1</span></span>|<span data-ttu-id="1957e-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="1957e-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="1957e-136">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="1957e-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="1957e-137">Entrada</span><span class="sxs-lookup"><span data-stu-id="1957e-137">Input</span></span>
<span data-ttu-id="1957e-138">Uma matriz JSON com dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="1957e-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="1957e-139">Cada objeto JSON será convertido tooan eventos.</span><span class="sxs-lookup"><span data-stu-id="1957e-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="1957e-140">Saída - 2 eventos</span><span class="sxs-lookup"><span data-stu-id="1957e-140">Output - 2 Events</span></span>

|<span data-ttu-id="1957e-141">ID</span><span class="sxs-lookup"><span data-stu-id="1957e-141">id</span></span>|<span data-ttu-id="1957e-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="1957e-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="1957e-143">device1</span><span class="sxs-lookup"><span data-stu-id="1957e-143">device1</span></span>|<span data-ttu-id="1957e-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="1957e-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="1957e-145">device2</span><span class="sxs-lookup"><span data-stu-id="1957e-145">device2</span></span>|<span data-ttu-id="1957e-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="1957e-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="1957e-147">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="1957e-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="1957e-148">Entrada</span><span class="sxs-lookup"><span data-stu-id="1957e-148">Input</span></span>

<span data-ttu-id="1957e-149">Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="1957e-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="1957e-150">Saída - 2 eventos</span><span class="sxs-lookup"><span data-stu-id="1957e-150">Output - 2 Events</span></span>
<span data-ttu-id="1957e-151">Observe que a propriedade hello "local" é copiada por tooeach de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="1957e-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="1957e-152">location</span><span class="sxs-lookup"><span data-stu-id="1957e-152">location</span></span>|<span data-ttu-id="1957e-153">events.id</span><span class="sxs-lookup"><span data-stu-id="1957e-153">events.id</span></span>|<span data-ttu-id="1957e-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="1957e-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="1957e-155">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="1957e-155">WestUs</span></span>|<span data-ttu-id="1957e-156">device1</span><span class="sxs-lookup"><span data-stu-id="1957e-156">device1</span></span>|<span data-ttu-id="1957e-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="1957e-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="1957e-158">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="1957e-158">WestUs</span></span>|<span data-ttu-id="1957e-159">device2</span><span class="sxs-lookup"><span data-stu-id="1957e-159">device2</span></span>|<span data-ttu-id="1957e-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="1957e-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="1957e-161">Exemplo 4</span><span class="sxs-lookup"><span data-stu-id="1957e-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="1957e-162">Entrada</span><span class="sxs-lookup"><span data-stu-id="1957e-162">Input</span></span>

<span data-ttu-id="1957e-163">Um objeto JSON com uma matriz JSON aninhada que contém dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="1957e-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="1957e-164">Essa entrada demonstra que propriedades globais Olá podem ser representadas pelo objeto JSON complexo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1957e-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="1957e-165">Saída - 2 eventos</span><span class="sxs-lookup"><span data-stu-id="1957e-165">Output - 2 Events</span></span>

|<span data-ttu-id="1957e-166">location</span><span class="sxs-lookup"><span data-stu-id="1957e-166">location</span></span>|<span data-ttu-id="1957e-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="1957e-167">manufacturer.name</span></span>|<span data-ttu-id="1957e-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="1957e-168">manufacturer.location</span></span>|<span data-ttu-id="1957e-169">events.id</span><span class="sxs-lookup"><span data-stu-id="1957e-169">events.id</span></span>|<span data-ttu-id="1957e-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="1957e-170">events.timestamp</span></span>|<span data-ttu-id="1957e-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="1957e-171">events.data.type</span></span>|<span data-ttu-id="1957e-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="1957e-172">events.data.units</span></span>|<span data-ttu-id="1957e-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="1957e-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="1957e-174">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="1957e-174">WestUs</span></span>|<span data-ttu-id="1957e-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="1957e-175">manufacturer1</span></span>|<span data-ttu-id="1957e-176">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="1957e-176">EastUs</span></span>|<span data-ttu-id="1957e-177">device1</span><span class="sxs-lookup"><span data-stu-id="1957e-177">device1</span></span>|<span data-ttu-id="1957e-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="1957e-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="1957e-179">pressure</span><span class="sxs-lookup"><span data-stu-id="1957e-179">pressure</span></span>|<span data-ttu-id="1957e-180">psi</span><span class="sxs-lookup"><span data-stu-id="1957e-180">psi</span></span>|<span data-ttu-id="1957e-181">108.09</span><span class="sxs-lookup"><span data-stu-id="1957e-181">108.09</span></span>|
|<span data-ttu-id="1957e-182">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="1957e-182">WestUs</span></span>|<span data-ttu-id="1957e-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="1957e-183">manufacturer1</span></span>|<span data-ttu-id="1957e-184">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="1957e-184">EastUs</span></span>|<span data-ttu-id="1957e-185">device2</span><span class="sxs-lookup"><span data-stu-id="1957e-185">device2</span></span>|<span data-ttu-id="1957e-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="1957e-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="1957e-187">vibration</span><span class="sxs-lookup"><span data-stu-id="1957e-187">vibration</span></span>|<span data-ttu-id="1957e-188">abs G</span><span class="sxs-lookup"><span data-stu-id="1957e-188">abs G</span></span>|<span data-ttu-id="1957e-189">217.09</span><span class="sxs-lookup"><span data-stu-id="1957e-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="1957e-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1957e-190">Next steps</span></span>

* <span data-ttu-id="1957e-191">Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1957e-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
