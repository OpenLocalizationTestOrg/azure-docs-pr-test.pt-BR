---
title: Modelo de Dados do Azure Application Insights | Microsoft Docs
description: "Descreve as propriedades exportadas de exportação contínua em JSON e usados como filtros."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: a485ddd555f65473d81896effc4a3562bda71410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="e346f-103">Modelo de dados de exportação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="e346f-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="e346f-104">Esta tabela lista as propriedades de telemetria enviadas dos SDKs do [Application Insights](app-insights-overview.md) para o portal.</span><span class="sxs-lookup"><span data-stu-id="e346f-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span></span>
<span data-ttu-id="e346f-105">Você verá essas propriedades na saída de dados de [Exportação Contínua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="e346f-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="e346f-106">Elas também aparecerão nos filtros da propriedade no [Explorador de Métrica](app-insights-metrics-explorer.md) e na [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="e346f-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="e346f-107">Pontos a serem observados:</span><span class="sxs-lookup"><span data-stu-id="e346f-107">Points to note:</span></span>

* <span data-ttu-id="e346f-108">`[0]` nessas tabelas indica um ponto no caminho no qual você precisa inserir um índice; mas nem sempre é 0.</span><span class="sxs-lookup"><span data-stu-id="e346f-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="e346f-109">A duração é em décimos de microssegundo, portanto, 10000000 = = 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="e346f-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="e346f-110">Datas e horas estão em UTC e são fornecidas no formato ISO `yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="e346f-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="e346f-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e346f-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent to client
        "success": true, // Default == responseCode<400
        // Request id becomes the operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently the following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized to 0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent to portal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  <span data-ttu-id="e346f-112">}</span><span class="sxs-lookup"><span data-stu-id="e346f-112">}</span></span>

## <a name="context"></a><span data-ttu-id="e346f-113">Contexto</span><span class="sxs-lookup"><span data-stu-id="e346f-113">Context</span></span>
<span data-ttu-id="e346f-114">Todos os tipos de telemetria são acompanhados por uma seção de contexto.</span><span class="sxs-lookup"><span data-stu-id="e346f-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="e346f-115">Nem todos esses campos são transmitidos com cada ponto de dados.</span><span class="sxs-lookup"><span data-stu-id="e346f-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="e346f-116">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-116">Path</span></span> | <span data-ttu-id="e346f-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-117">Type</span></span> | <span data-ttu-id="e346f-118">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="e346f-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="e346f-120">object [ ]</span><span class="sxs-lookup"><span data-stu-id="e346f-120">object [ ]</span></span> |<span data-ttu-id="e346f-121">Pares de cadeira de caractere chave-valor definidos pelo parâmetro das propriedades personalizadas.</span><span class="sxs-lookup"><span data-stu-id="e346f-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="e346f-122">Comprimento máximo da chave 100, comprimento máximo dos valores 1024.</span><span class="sxs-lookup"><span data-stu-id="e346f-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="e346f-123">Mais de 100 valores exclusivos, é possível pesquisar na propriedade, mas não usá-la para segmentação.</span><span class="sxs-lookup"><span data-stu-id="e346f-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="e346f-124">Máximo de 200 chaves por ikey.</span><span class="sxs-lookup"><span data-stu-id="e346f-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="e346f-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="e346f-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="e346f-126">object [ ]</span><span class="sxs-lookup"><span data-stu-id="e346f-126">object [ ]</span></span> |<span data-ttu-id="e346f-127">Pares de chave-valor definidos pelo parâmetro de medidas personalizadas e por TrackMetrics.</span><span class="sxs-lookup"><span data-stu-id="e346f-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="e346f-128">Comprimento máximo da chave 100, os valores podem ser numéricos.</span><span class="sxs-lookup"><span data-stu-id="e346f-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="e346f-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="e346f-129">context.data.eventTime</span></span> |<span data-ttu-id="e346f-130">string</span><span class="sxs-lookup"><span data-stu-id="e346f-130">string</span></span> |<span data-ttu-id="e346f-131">UTC</span><span class="sxs-lookup"><span data-stu-id="e346f-131">UTC</span></span> |
| <span data-ttu-id="e346f-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="e346f-132">context.data.isSynthetic</span></span> |<span data-ttu-id="e346f-133">booleano</span><span class="sxs-lookup"><span data-stu-id="e346f-133">boolean</span></span> |<span data-ttu-id="e346f-134">A solicitação parece ser proveniente de um teste na Web ou de um bot.</span><span class="sxs-lookup"><span data-stu-id="e346f-134">Request appears to come from a bot or web test.</span></span> |
| <span data-ttu-id="e346f-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="e346f-135">context.data.samplingRate</span></span> |<span data-ttu-id="e346f-136">número</span><span class="sxs-lookup"><span data-stu-id="e346f-136">number</span></span> |<span data-ttu-id="e346f-137">Porcentagem de telemetria gerada pelo SDK enviado ao portal.</span><span class="sxs-lookup"><span data-stu-id="e346f-137">Percentage of telemetry generated by the SDK that is sent to portal.</span></span> <span data-ttu-id="e346f-138">Intervalo 0.0-100.0.</span><span class="sxs-lookup"><span data-stu-id="e346f-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="e346f-139">context.device</span><span class="sxs-lookup"><span data-stu-id="e346f-139">context.device</span></span> |<span data-ttu-id="e346f-140">objeto</span><span class="sxs-lookup"><span data-stu-id="e346f-140">object</span></span> |<span data-ttu-id="e346f-141">Dispositivo de cliente</span><span class="sxs-lookup"><span data-stu-id="e346f-141">Client device</span></span> |
| <span data-ttu-id="e346f-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="e346f-142">context.device.browser</span></span> |<span data-ttu-id="e346f-143">string</span><span class="sxs-lookup"><span data-stu-id="e346f-143">string</span></span> |<span data-ttu-id="e346f-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="e346f-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="e346f-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="e346f-145">context.device.browserVersion</span></span> |<span data-ttu-id="e346f-146">string</span><span class="sxs-lookup"><span data-stu-id="e346f-146">string</span></span> |<span data-ttu-id="e346f-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="e346f-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="e346f-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="e346f-148">context.device.deviceModel</span></span> |<span data-ttu-id="e346f-149">string</span><span class="sxs-lookup"><span data-stu-id="e346f-149">string</span></span> | |
| <span data-ttu-id="e346f-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="e346f-150">context.device.deviceName</span></span> |<span data-ttu-id="e346f-151">string</span><span class="sxs-lookup"><span data-stu-id="e346f-151">string</span></span> | |
| <span data-ttu-id="e346f-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="e346f-152">context.device.id</span></span> |<span data-ttu-id="e346f-153">string</span><span class="sxs-lookup"><span data-stu-id="e346f-153">string</span></span> | |
| <span data-ttu-id="e346f-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="e346f-154">context.device.locale</span></span> |<span data-ttu-id="e346f-155">string</span><span class="sxs-lookup"><span data-stu-id="e346f-155">string</span></span> |<span data-ttu-id="e346f-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="e346f-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="e346f-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="e346f-157">context.device.network</span></span> |<span data-ttu-id="e346f-158">string</span><span class="sxs-lookup"><span data-stu-id="e346f-158">string</span></span> | |
| <span data-ttu-id="e346f-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="e346f-159">context.device.oemName</span></span> |<span data-ttu-id="e346f-160">string</span><span class="sxs-lookup"><span data-stu-id="e346f-160">string</span></span> | |
| <span data-ttu-id="e346f-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="e346f-161">context.device.osVersion</span></span> |<span data-ttu-id="e346f-162">string</span><span class="sxs-lookup"><span data-stu-id="e346f-162">string</span></span> |<span data-ttu-id="e346f-163">SO host</span><span class="sxs-lookup"><span data-stu-id="e346f-163">Host OS</span></span> |
| <span data-ttu-id="e346f-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="e346f-164">context.device.roleInstance</span></span> |<span data-ttu-id="e346f-165">string</span><span class="sxs-lookup"><span data-stu-id="e346f-165">string</span></span> |<span data-ttu-id="e346f-166">ID do host do servidor</span><span class="sxs-lookup"><span data-stu-id="e346f-166">ID of server host</span></span> |
| <span data-ttu-id="e346f-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="e346f-167">context.device.roleName</span></span> |<span data-ttu-id="e346f-168">string</span><span class="sxs-lookup"><span data-stu-id="e346f-168">string</span></span> | |
| <span data-ttu-id="e346f-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="e346f-169">context.device.type</span></span> |<span data-ttu-id="e346f-170">string</span><span class="sxs-lookup"><span data-stu-id="e346f-170">string</span></span> |<span data-ttu-id="e346f-171">PC, navegador,...</span><span class="sxs-lookup"><span data-stu-id="e346f-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="e346f-172">context.location</span><span class="sxs-lookup"><span data-stu-id="e346f-172">context.location</span></span> |<span data-ttu-id="e346f-173">objeto</span><span class="sxs-lookup"><span data-stu-id="e346f-173">object</span></span> |<span data-ttu-id="e346f-174">Derivado de clientip.</span><span class="sxs-lookup"><span data-stu-id="e346f-174">Derived from clientip.</span></span> |
| <span data-ttu-id="e346f-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="e346f-175">context.location.city</span></span> |<span data-ttu-id="e346f-176">string</span><span class="sxs-lookup"><span data-stu-id="e346f-176">string</span></span> |<span data-ttu-id="e346f-177">Derivado de clientip, se conhecido</span><span class="sxs-lookup"><span data-stu-id="e346f-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="e346f-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="e346f-178">context.location.clientip</span></span> |<span data-ttu-id="e346f-179">string</span><span class="sxs-lookup"><span data-stu-id="e346f-179">string</span></span> |<span data-ttu-id="e346f-180">Último octógono tornado anônimo pelo valor 0.</span><span class="sxs-lookup"><span data-stu-id="e346f-180">Last octagon is anonymized to 0.</span></span> |
| <span data-ttu-id="e346f-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="e346f-181">context.location.continent</span></span> |<span data-ttu-id="e346f-182">string</span><span class="sxs-lookup"><span data-stu-id="e346f-182">string</span></span> | |
| <span data-ttu-id="e346f-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="e346f-183">context.location.country</span></span> |<span data-ttu-id="e346f-184">string</span><span class="sxs-lookup"><span data-stu-id="e346f-184">string</span></span> | |
| <span data-ttu-id="e346f-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="e346f-185">context.location.province</span></span> |<span data-ttu-id="e346f-186">string</span><span class="sxs-lookup"><span data-stu-id="e346f-186">string</span></span> |<span data-ttu-id="e346f-187">Estado ou província</span><span class="sxs-lookup"><span data-stu-id="e346f-187">State or province</span></span> |
| <span data-ttu-id="e346f-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="e346f-188">context.operation.id</span></span> |<span data-ttu-id="e346f-189">string</span><span class="sxs-lookup"><span data-stu-id="e346f-189">string</span></span> |<span data-ttu-id="e346f-190">Itens que têm a mesma ID de operação são mostrados como Itens Relacionados no portal.</span><span class="sxs-lookup"><span data-stu-id="e346f-190">Items that have the same operation id are shown as Related Items in the portal.</span></span> <span data-ttu-id="e346f-191">Normalmente a ID da solicitação.</span><span class="sxs-lookup"><span data-stu-id="e346f-191">Usually the request id.</span></span> |
| <span data-ttu-id="e346f-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="e346f-192">context.operation.name</span></span> |<span data-ttu-id="e346f-193">string</span><span class="sxs-lookup"><span data-stu-id="e346f-193">string</span></span> |<span data-ttu-id="e346f-194">nome solicitação ou url</span><span class="sxs-lookup"><span data-stu-id="e346f-194">url or request name</span></span> |
| <span data-ttu-id="e346f-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="e346f-195">context.operation.parentId</span></span> |<span data-ttu-id="e346f-196">string</span><span class="sxs-lookup"><span data-stu-id="e346f-196">string</span></span> |<span data-ttu-id="e346f-197">Permite itens relacionados aninhados.</span><span class="sxs-lookup"><span data-stu-id="e346f-197">Allows nested related items.</span></span> |
| <span data-ttu-id="e346f-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="e346f-198">context.session.id</span></span> |<span data-ttu-id="e346f-199">string</span><span class="sxs-lookup"><span data-stu-id="e346f-199">string</span></span> |<span data-ttu-id="e346f-200">ID de um grupo de operações da mesma fonte.</span><span class="sxs-lookup"><span data-stu-id="e346f-200">Id of a group of operations from the same source.</span></span> <span data-ttu-id="e346f-201">Um período de 30 minutos sem uma operação sinaliza o término de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="e346f-201">A period of 30 minutes without an operation signals the end of a session.</span></span> |
| <span data-ttu-id="e346f-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="e346f-202">context.session.isFirst</span></span> |<span data-ttu-id="e346f-203">booleano</span><span class="sxs-lookup"><span data-stu-id="e346f-203">boolean</span></span> | |
| <span data-ttu-id="e346f-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="e346f-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="e346f-205">string</span><span class="sxs-lookup"><span data-stu-id="e346f-205">string</span></span> | |
| <span data-ttu-id="e346f-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="e346f-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="e346f-207">string</span><span class="sxs-lookup"><span data-stu-id="e346f-207">string</span></span> | |
| <span data-ttu-id="e346f-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="e346f-208">context.user.anonId</span></span> |<span data-ttu-id="e346f-209">string</span><span class="sxs-lookup"><span data-stu-id="e346f-209">string</span></span> | |
| <span data-ttu-id="e346f-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="e346f-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="e346f-211">string</span><span class="sxs-lookup"><span data-stu-id="e346f-211">string</span></span> |[<span data-ttu-id="e346f-212">Usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="e346f-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="e346f-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="e346f-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="e346f-214">booleano</span><span class="sxs-lookup"><span data-stu-id="e346f-214">boolean</span></span> | |
| <span data-ttu-id="e346f-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="e346f-215">internal.data.documentVersion</span></span> |<span data-ttu-id="e346f-216">string</span><span class="sxs-lookup"><span data-stu-id="e346f-216">string</span></span> | |
| <span data-ttu-id="e346f-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="e346f-217">internal.data.id</span></span> |<span data-ttu-id="e346f-218">string</span><span class="sxs-lookup"><span data-stu-id="e346f-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="e346f-219">Eventos</span><span class="sxs-lookup"><span data-stu-id="e346f-219">Events</span></span>
<span data-ttu-id="e346f-220">Eventos personalizados gerados por [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="e346f-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="e346f-221">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-221">Path</span></span> | <span data-ttu-id="e346f-222">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-222">Type</span></span> | <span data-ttu-id="e346f-223">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="e346f-224">event [0] count</span></span> |<span data-ttu-id="e346f-225">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-225">integer</span></span> |<span data-ttu-id="e346f-226">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e346f-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e346f-227">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="e346f-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e346f-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="e346f-228">event [0] name</span></span> |<span data-ttu-id="e346f-229">string</span><span class="sxs-lookup"><span data-stu-id="e346f-229">string</span></span> |<span data-ttu-id="e346f-230">Nome do evento.</span><span class="sxs-lookup"><span data-stu-id="e346f-230">Event name.</span></span>  <span data-ttu-id="e346f-231">Comprimento máximo 250.</span><span class="sxs-lookup"><span data-stu-id="e346f-231">Max length 250.</span></span> |
| <span data-ttu-id="e346f-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="e346f-232">event [0] url</span></span> |<span data-ttu-id="e346f-233">string</span><span class="sxs-lookup"><span data-stu-id="e346f-233">string</span></span> | |
| <span data-ttu-id="e346f-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e346f-234">event [0] urlData.base</span></span> |<span data-ttu-id="e346f-235">string</span><span class="sxs-lookup"><span data-stu-id="e346f-235">string</span></span> | |
| <span data-ttu-id="e346f-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e346f-236">event [0] urlData.host</span></span> |<span data-ttu-id="e346f-237">string</span><span class="sxs-lookup"><span data-stu-id="e346f-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="e346f-238">Exceções</span><span class="sxs-lookup"><span data-stu-id="e346f-238">Exceptions</span></span>
<span data-ttu-id="e346f-239">[Exceções](app-insights-asp-net-exceptions.md) do relatório no servidor e no navegador.</span><span class="sxs-lookup"><span data-stu-id="e346f-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span></span>

| <span data-ttu-id="e346f-240">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-240">Path</span></span> | <span data-ttu-id="e346f-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-241">Type</span></span> | <span data-ttu-id="e346f-242">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="e346f-243">basicException [0] assembly</span></span> |<span data-ttu-id="e346f-244">string</span><span class="sxs-lookup"><span data-stu-id="e346f-244">string</span></span> | |
| <span data-ttu-id="e346f-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="e346f-245">basicException [0] count</span></span> |<span data-ttu-id="e346f-246">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-246">integer</span></span> |<span data-ttu-id="e346f-247">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e346f-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e346f-248">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="e346f-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e346f-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="e346f-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="e346f-250">string</span><span class="sxs-lookup"><span data-stu-id="e346f-250">string</span></span> | |
| <span data-ttu-id="e346f-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="e346f-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="e346f-252">string</span><span class="sxs-lookup"><span data-stu-id="e346f-252">string</span></span> | |
| <span data-ttu-id="e346f-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="e346f-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="e346f-254">string</span><span class="sxs-lookup"><span data-stu-id="e346f-254">string</span></span> | |
| <span data-ttu-id="e346f-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="e346f-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="e346f-256">string</span><span class="sxs-lookup"><span data-stu-id="e346f-256">string</span></span> | |
| <span data-ttu-id="e346f-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="e346f-257">basicException [0] handledAt</span></span> |<span data-ttu-id="e346f-258">string</span><span class="sxs-lookup"><span data-stu-id="e346f-258">string</span></span> | |
| <span data-ttu-id="e346f-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="e346f-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="e346f-260">booleano</span><span class="sxs-lookup"><span data-stu-id="e346f-260">boolean</span></span> | |
| <span data-ttu-id="e346f-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="e346f-261">basicException [0] id</span></span> |<span data-ttu-id="e346f-262">string</span><span class="sxs-lookup"><span data-stu-id="e346f-262">string</span></span> | |
| <span data-ttu-id="e346f-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="e346f-263">basicException [0] method</span></span> |<span data-ttu-id="e346f-264">string</span><span class="sxs-lookup"><span data-stu-id="e346f-264">string</span></span> | |
| <span data-ttu-id="e346f-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="e346f-265">basicException [0] message</span></span> |<span data-ttu-id="e346f-266">string</span><span class="sxs-lookup"><span data-stu-id="e346f-266">string</span></span> |<span data-ttu-id="e346f-267">Mensagem de exceção.</span><span class="sxs-lookup"><span data-stu-id="e346f-267">Exception message.</span></span> <span data-ttu-id="e346f-268">Comprimento máximo 10k.</span><span class="sxs-lookup"><span data-stu-id="e346f-268">Max length 10k.</span></span> |
| <span data-ttu-id="e346f-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="e346f-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="e346f-270">string</span><span class="sxs-lookup"><span data-stu-id="e346f-270">string</span></span> | |
| <span data-ttu-id="e346f-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="e346f-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="e346f-272">string</span><span class="sxs-lookup"><span data-stu-id="e346f-272">string</span></span> | |
| <span data-ttu-id="e346f-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="e346f-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="e346f-274">string</span><span class="sxs-lookup"><span data-stu-id="e346f-274">string</span></span> | |
| <span data-ttu-id="e346f-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="e346f-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="e346f-276">string</span><span class="sxs-lookup"><span data-stu-id="e346f-276">string</span></span> | |
| <span data-ttu-id="e346f-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="e346f-277">basicException [0] outerId</span></span> |<span data-ttu-id="e346f-278">string</span><span class="sxs-lookup"><span data-stu-id="e346f-278">string</span></span> | |
| <span data-ttu-id="e346f-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="e346f-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="e346f-280">string</span><span class="sxs-lookup"><span data-stu-id="e346f-280">string</span></span> | |
| <span data-ttu-id="e346f-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="e346f-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="e346f-282">string</span><span class="sxs-lookup"><span data-stu-id="e346f-282">string</span></span> | |
| <span data-ttu-id="e346f-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="e346f-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="e346f-284">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-284">integer</span></span> | |
| <span data-ttu-id="e346f-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="e346f-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="e346f-286">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-286">integer</span></span> | |
| <span data-ttu-id="e346f-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="e346f-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="e346f-288">string</span><span class="sxs-lookup"><span data-stu-id="e346f-288">string</span></span> | |
| <span data-ttu-id="e346f-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="e346f-289">basicException [0] stack</span></span> |<span data-ttu-id="e346f-290">string</span><span class="sxs-lookup"><span data-stu-id="e346f-290">string</span></span> |<span data-ttu-id="e346f-291">Comprimento máximo 10k</span><span class="sxs-lookup"><span data-stu-id="e346f-291">Max length 10k</span></span> |
| <span data-ttu-id="e346f-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="e346f-292">basicException [0] typeName</span></span> |<span data-ttu-id="e346f-293">string</span><span class="sxs-lookup"><span data-stu-id="e346f-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="e346f-294">Mensagens de rastreamento</span><span class="sxs-lookup"><span data-stu-id="e346f-294">Trace Messages</span></span>
<span data-ttu-id="e346f-295">Enviado por [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace) e pelos [adaptadores de log](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e346f-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="e346f-296">path</span><span class="sxs-lookup"><span data-stu-id="e346f-296">Path</span></span> | <span data-ttu-id="e346f-297">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-297">Type</span></span> | <span data-ttu-id="e346f-298">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="e346f-299">message [0] loggerName</span></span> |<span data-ttu-id="e346f-300">string</span><span class="sxs-lookup"><span data-stu-id="e346f-300">string</span></span> | |
| <span data-ttu-id="e346f-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="e346f-301">message [0] parameters</span></span> |<span data-ttu-id="e346f-302">string</span><span class="sxs-lookup"><span data-stu-id="e346f-302">string</span></span> | |
| <span data-ttu-id="e346f-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="e346f-303">message [0] raw</span></span> |<span data-ttu-id="e346f-304">string</span><span class="sxs-lookup"><span data-stu-id="e346f-304">string</span></span> |<span data-ttu-id="e346f-305">A mensagem de log, comprimento máximo de 10 mil.</span><span class="sxs-lookup"><span data-stu-id="e346f-305">The log message, max length 10k.</span></span> |
| <span data-ttu-id="e346f-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="e346f-306">message [0] severityLevel</span></span> |<span data-ttu-id="e346f-307">string</span><span class="sxs-lookup"><span data-stu-id="e346f-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="e346f-308">Dependência remota</span><span class="sxs-lookup"><span data-stu-id="e346f-308">Remote dependency</span></span>
<span data-ttu-id="e346f-309">Enviado por TrackDependency.</span><span class="sxs-lookup"><span data-stu-id="e346f-309">Sent by TrackDependency.</span></span> <span data-ttu-id="e346f-310">Usado para indicar o desempenho e o uso das [chamadas para dependências](app-insights-asp-net-dependencies.md) no servidor, e chamadas do AJAX no navegador.</span><span class="sxs-lookup"><span data-stu-id="e346f-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span></span>

| <span data-ttu-id="e346f-311">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-311">Path</span></span> | <span data-ttu-id="e346f-312">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-312">Type</span></span> | <span data-ttu-id="e346f-313">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="e346f-314">remoteDependency [0] async</span></span> |<span data-ttu-id="e346f-315">booleano</span><span class="sxs-lookup"><span data-stu-id="e346f-315">boolean</span></span> | |
| <span data-ttu-id="e346f-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="e346f-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="e346f-317">string</span><span class="sxs-lookup"><span data-stu-id="e346f-317">string</span></span> | |
| <span data-ttu-id="e346f-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="e346f-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="e346f-319">string</span><span class="sxs-lookup"><span data-stu-id="e346f-319">string</span></span> |<span data-ttu-id="e346f-320">Por exemplo, "home/index"</span><span class="sxs-lookup"><span data-stu-id="e346f-320">For example "home/index"</span></span> |
| <span data-ttu-id="e346f-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="e346f-321">remoteDependency [0] count</span></span> |<span data-ttu-id="e346f-322">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-322">integer</span></span> |<span data-ttu-id="e346f-323">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e346f-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e346f-324">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="e346f-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e346f-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="e346f-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="e346f-326">string</span><span class="sxs-lookup"><span data-stu-id="e346f-326">string</span></span> |<span data-ttu-id="e346f-327">HTTP, SQL, ...</span><span class="sxs-lookup"><span data-stu-id="e346f-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="e346f-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e346f-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="e346f-329">número</span><span class="sxs-lookup"><span data-stu-id="e346f-329">number</span></span> |<span data-ttu-id="e346f-330">Tempo desde a chamada até a conclusão da resposta por dependência</span><span class="sxs-lookup"><span data-stu-id="e346f-330">Time from call to completion of response by dependency</span></span> |
| <span data-ttu-id="e346f-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="e346f-331">remoteDependency [0] id</span></span> |<span data-ttu-id="e346f-332">string</span><span class="sxs-lookup"><span data-stu-id="e346f-332">string</span></span> | |
| <span data-ttu-id="e346f-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="e346f-333">remoteDependency [0] name</span></span> |<span data-ttu-id="e346f-334">string</span><span class="sxs-lookup"><span data-stu-id="e346f-334">string</span></span> |<span data-ttu-id="e346f-335">Url.</span><span class="sxs-lookup"><span data-stu-id="e346f-335">Url.</span></span> <span data-ttu-id="e346f-336">Comprimento máximo 250.</span><span class="sxs-lookup"><span data-stu-id="e346f-336">Max length 250.</span></span> |
| <span data-ttu-id="e346f-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="e346f-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="e346f-338">string</span><span class="sxs-lookup"><span data-stu-id="e346f-338">string</span></span> |<span data-ttu-id="e346f-339">da dependência de HTTP</span><span class="sxs-lookup"><span data-stu-id="e346f-339">from HTTP dependency</span></span> |
| <span data-ttu-id="e346f-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="e346f-340">remoteDependency [0] success</span></span> |<span data-ttu-id="e346f-341">booleano</span><span class="sxs-lookup"><span data-stu-id="e346f-341">boolean</span></span> | |
| <span data-ttu-id="e346f-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="e346f-342">remoteDependency [0] type</span></span> |<span data-ttu-id="e346f-343">string</span><span class="sxs-lookup"><span data-stu-id="e346f-343">string</span></span> |<span data-ttu-id="e346f-344">Http, Sql,...</span><span class="sxs-lookup"><span data-stu-id="e346f-344">Http, Sql,...</span></span> |
| <span data-ttu-id="e346f-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="e346f-345">remoteDependency [0] url</span></span> |<span data-ttu-id="e346f-346">string</span><span class="sxs-lookup"><span data-stu-id="e346f-346">string</span></span> |<span data-ttu-id="e346f-347">Comprimento máximo 2000</span><span class="sxs-lookup"><span data-stu-id="e346f-347">Max length 2000</span></span> |
| <span data-ttu-id="e346f-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e346f-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="e346f-349">string</span><span class="sxs-lookup"><span data-stu-id="e346f-349">string</span></span> |<span data-ttu-id="e346f-350">Comprimento máximo 2000</span><span class="sxs-lookup"><span data-stu-id="e346f-350">Max length 2000</span></span> |
| <span data-ttu-id="e346f-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e346f-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="e346f-352">string</span><span class="sxs-lookup"><span data-stu-id="e346f-352">string</span></span> | |
| <span data-ttu-id="e346f-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e346f-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="e346f-354">string</span><span class="sxs-lookup"><span data-stu-id="e346f-354">string</span></span> |<span data-ttu-id="e346f-355">Comprimento máximo 200</span><span class="sxs-lookup"><span data-stu-id="e346f-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="e346f-356">Solicitações</span><span class="sxs-lookup"><span data-stu-id="e346f-356">Requests</span></span>
<span data-ttu-id="e346f-357">Enviado por [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="e346f-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="e346f-358">Os módulos padrão usam isso para indicar o tempo de resposta do servidor, medido no servidor.</span><span class="sxs-lookup"><span data-stu-id="e346f-358">The standard modules use this to reports server response time, measured at the server.</span></span>

| <span data-ttu-id="e346f-359">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-359">Path</span></span> | <span data-ttu-id="e346f-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-360">Type</span></span> | <span data-ttu-id="e346f-361">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="e346f-362">request [0] count</span></span> |<span data-ttu-id="e346f-363">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-363">integer</span></span> |<span data-ttu-id="e346f-364">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e346f-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e346f-365">Por exemplo: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="e346f-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e346f-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e346f-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="e346f-367">número</span><span class="sxs-lookup"><span data-stu-id="e346f-367">number</span></span> |<span data-ttu-id="e346f-368">Tempo de chegada da solicitação até a resposta.</span><span class="sxs-lookup"><span data-stu-id="e346f-368">Time from request arriving to response.</span></span> <span data-ttu-id="e346f-369">1e7 == 1s</span><span class="sxs-lookup"><span data-stu-id="e346f-369">1e7 == 1s</span></span> |
| <span data-ttu-id="e346f-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="e346f-370">request [0] id</span></span> |<span data-ttu-id="e346f-371">string</span><span class="sxs-lookup"><span data-stu-id="e346f-371">string</span></span> |<span data-ttu-id="e346f-372">ID da operação</span><span class="sxs-lookup"><span data-stu-id="e346f-372">Operation id</span></span> |
| <span data-ttu-id="e346f-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="e346f-373">request [0] name</span></span> |<span data-ttu-id="e346f-374">string</span><span class="sxs-lookup"><span data-stu-id="e346f-374">string</span></span> |<span data-ttu-id="e346f-375">GET/POST + url base.</span><span class="sxs-lookup"><span data-stu-id="e346f-375">GET/POST + url base.</span></span>  <span data-ttu-id="e346f-376">Comprimento máximo 250</span><span class="sxs-lookup"><span data-stu-id="e346f-376">Max length 250</span></span> |
| <span data-ttu-id="e346f-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="e346f-377">request [0] responseCode</span></span> |<span data-ttu-id="e346f-378">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-378">integer</span></span> |<span data-ttu-id="e346f-379">Resposta HTTP enviada ao cliente</span><span class="sxs-lookup"><span data-stu-id="e346f-379">HTTP response sent to client</span></span> |
| <span data-ttu-id="e346f-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="e346f-380">request [0] success</span></span> |<span data-ttu-id="e346f-381">booleano</span><span class="sxs-lookup"><span data-stu-id="e346f-381">boolean</span></span> |<span data-ttu-id="e346f-382">Padrão == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="e346f-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="e346f-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="e346f-383">request [0] url</span></span> |<span data-ttu-id="e346f-384">string</span><span class="sxs-lookup"><span data-stu-id="e346f-384">string</span></span> |<span data-ttu-id="e346f-385">Não incluindo o host</span><span class="sxs-lookup"><span data-stu-id="e346f-385">Not including host</span></span> |
| <span data-ttu-id="e346f-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e346f-386">request [0] urlData.base</span></span> |<span data-ttu-id="e346f-387">string</span><span class="sxs-lookup"><span data-stu-id="e346f-387">string</span></span> | |
| <span data-ttu-id="e346f-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e346f-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="e346f-389">string</span><span class="sxs-lookup"><span data-stu-id="e346f-389">string</span></span> | |
| <span data-ttu-id="e346f-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e346f-390">request [0] urlData.host</span></span> |<span data-ttu-id="e346f-391">string</span><span class="sxs-lookup"><span data-stu-id="e346f-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="e346f-392">Desempenho de exibição da página</span><span class="sxs-lookup"><span data-stu-id="e346f-392">Page View Performance</span></span>
<span data-ttu-id="e346f-393">Enviado pelo navegador.</span><span class="sxs-lookup"><span data-stu-id="e346f-393">Sent by the browser.</span></span> <span data-ttu-id="e346f-394">Mede o tempo de processamento de uma página, desde o início da solicitação do usuário até a exibição completa (excluindo as chamadas do AJAX assíncronas).</span><span class="sxs-lookup"><span data-stu-id="e346f-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="e346f-395">Os valores de contexto mostram a versão do navegador e do sistema operacional cliente.</span><span class="sxs-lookup"><span data-stu-id="e346f-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="e346f-396">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-396">Path</span></span> | <span data-ttu-id="e346f-397">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-397">Type</span></span> | <span data-ttu-id="e346f-398">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="e346f-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="e346f-400">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-400">integer</span></span> |<span data-ttu-id="e346f-401">Tempo desde o término do recebimento do HTML até a exibição da página.</span><span class="sxs-lookup"><span data-stu-id="e346f-401">Time from end of receiving the HTML to displaying the page.</span></span> |
| <span data-ttu-id="e346f-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="e346f-402">clientPerformance [0] name</span></span> |<span data-ttu-id="e346f-403">string</span><span class="sxs-lookup"><span data-stu-id="e346f-403">string</span></span> | |
| <span data-ttu-id="e346f-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="e346f-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="e346f-405">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-405">integer</span></span> |<span data-ttu-id="e346f-406">Tempo necessário para estabelecer uma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="e346f-406">Time taken to establish a network connection.</span></span> |
| <span data-ttu-id="e346f-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="e346f-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="e346f-408">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-408">integer</span></span> |<span data-ttu-id="e346f-409">Tempo desde o término do envio da solicitação até o recebimento do HTML na resposta.</span><span class="sxs-lookup"><span data-stu-id="e346f-409">Time from end of sending the request to receiving the HTML in reply.</span></span> |
| <span data-ttu-id="e346f-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="e346f-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="e346f-411">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-411">integer</span></span> |<span data-ttu-id="e346f-412">Tempo necessário para enviar a solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="e346f-412">Time from taken to send the HTTP request.</span></span> |
| <span data-ttu-id="e346f-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="e346f-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="e346f-414">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-414">integer</span></span> |<span data-ttu-id="e346f-415">Tempo desde o início até o envio da solicitação para exibição da página.</span><span class="sxs-lookup"><span data-stu-id="e346f-415">Time from starting to send the request to displaying the page.</span></span> |
| <span data-ttu-id="e346f-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="e346f-416">clientPerformance [0] url</span></span> |<span data-ttu-id="e346f-417">string</span><span class="sxs-lookup"><span data-stu-id="e346f-417">string</span></span> |<span data-ttu-id="e346f-418">URL dessa solicitação</span><span class="sxs-lookup"><span data-stu-id="e346f-418">URL of this request</span></span> |
| <span data-ttu-id="e346f-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e346f-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="e346f-420">string</span><span class="sxs-lookup"><span data-stu-id="e346f-420">string</span></span> | |
| <span data-ttu-id="e346f-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e346f-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="e346f-422">string</span><span class="sxs-lookup"><span data-stu-id="e346f-422">string</span></span> | |
| <span data-ttu-id="e346f-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e346f-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="e346f-424">string</span><span class="sxs-lookup"><span data-stu-id="e346f-424">string</span></span> | |
| <span data-ttu-id="e346f-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="e346f-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="e346f-426">string</span><span class="sxs-lookup"><span data-stu-id="e346f-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="e346f-427">Visualizações de página</span><span class="sxs-lookup"><span data-stu-id="e346f-427">Page Views</span></span>
<span data-ttu-id="e346f-428">Enviado por trackPageView() ou [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="e346f-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="e346f-429">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-429">Path</span></span> | <span data-ttu-id="e346f-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-430">Type</span></span> | <span data-ttu-id="e346f-431">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="e346f-432">view [0] count</span></span> |<span data-ttu-id="e346f-433">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-433">integer</span></span> |<span data-ttu-id="e346f-434">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e346f-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e346f-435">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="e346f-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e346f-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e346f-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="e346f-437">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-437">integer</span></span> |<span data-ttu-id="e346f-438">Valor definido opcionalmente em trackPageView() ou por startTrackPage() - stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="e346f-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="e346f-439">Não é igual aos valores de clientPerformance.</span><span class="sxs-lookup"><span data-stu-id="e346f-439">Not the same as clientPerformance values.</span></span> |
| <span data-ttu-id="e346f-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="e346f-440">view [0] name</span></span> |<span data-ttu-id="e346f-441">string</span><span class="sxs-lookup"><span data-stu-id="e346f-441">string</span></span> |<span data-ttu-id="e346f-442">Título da página.</span><span class="sxs-lookup"><span data-stu-id="e346f-442">Page title.</span></span>  <span data-ttu-id="e346f-443">Comprimento máximo 250</span><span class="sxs-lookup"><span data-stu-id="e346f-443">Max length 250</span></span> |
| <span data-ttu-id="e346f-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="e346f-444">view [0] url</span></span> |<span data-ttu-id="e346f-445">string</span><span class="sxs-lookup"><span data-stu-id="e346f-445">string</span></span> | |
| <span data-ttu-id="e346f-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="e346f-446">view [0] urlData.base</span></span> |<span data-ttu-id="e346f-447">string</span><span class="sxs-lookup"><span data-stu-id="e346f-447">string</span></span> | |
| <span data-ttu-id="e346f-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="e346f-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="e346f-449">string</span><span class="sxs-lookup"><span data-stu-id="e346f-449">string</span></span> | |
| <span data-ttu-id="e346f-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="e346f-450">view [0] urlData.host</span></span> |<span data-ttu-id="e346f-451">string</span><span class="sxs-lookup"><span data-stu-id="e346f-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="e346f-452">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="e346f-452">Availability</span></span>
<span data-ttu-id="e346f-453">Relata os [testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="e346f-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="e346f-454">Caminho</span><span class="sxs-lookup"><span data-stu-id="e346f-454">Path</span></span> | <span data-ttu-id="e346f-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="e346f-455">Type</span></span> | <span data-ttu-id="e346f-456">Observações</span><span class="sxs-lookup"><span data-stu-id="e346f-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e346f-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="e346f-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="e346f-458">string</span><span class="sxs-lookup"><span data-stu-id="e346f-458">string</span></span> |<span data-ttu-id="e346f-459">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="e346f-459">availability</span></span> |
| <span data-ttu-id="e346f-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="e346f-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="e346f-461">número</span><span class="sxs-lookup"><span data-stu-id="e346f-461">number</span></span> |<span data-ttu-id="e346f-462">1.0 ou 0.0</span><span class="sxs-lookup"><span data-stu-id="e346f-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="e346f-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="e346f-463">availability [0] count</span></span> |<span data-ttu-id="e346f-464">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-464">integer</span></span> |<span data-ttu-id="e346f-465">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="e346f-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="e346f-466">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="e346f-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="e346f-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="e346f-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="e346f-468">string</span><span class="sxs-lookup"><span data-stu-id="e346f-468">string</span></span> | |
| <span data-ttu-id="e346f-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="e346f-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="e346f-470">inteiro</span><span class="sxs-lookup"><span data-stu-id="e346f-470">integer</span></span> | |
| <span data-ttu-id="e346f-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="e346f-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="e346f-472">string</span><span class="sxs-lookup"><span data-stu-id="e346f-472">string</span></span> | |
| <span data-ttu-id="e346f-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="e346f-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="e346f-474">número</span><span class="sxs-lookup"><span data-stu-id="e346f-474">number</span></span> |<span data-ttu-id="e346f-475">Duração do teste.</span><span class="sxs-lookup"><span data-stu-id="e346f-475">Duration of test.</span></span> <span data-ttu-id="e346f-476">1e7==1s</span><span class="sxs-lookup"><span data-stu-id="e346f-476">1e7==1s</span></span> |
| <span data-ttu-id="e346f-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="e346f-477">availability [0] message</span></span> |<span data-ttu-id="e346f-478">string</span><span class="sxs-lookup"><span data-stu-id="e346f-478">string</span></span> |<span data-ttu-id="e346f-479">Diagnóstico de falha</span><span class="sxs-lookup"><span data-stu-id="e346f-479">Failure diagnostic</span></span> |
| <span data-ttu-id="e346f-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="e346f-480">availability [0] result</span></span> |<span data-ttu-id="e346f-481">string</span><span class="sxs-lookup"><span data-stu-id="e346f-481">string</span></span> |<span data-ttu-id="e346f-482">Aprovado/Reprovado</span><span class="sxs-lookup"><span data-stu-id="e346f-482">Pass/Fail</span></span> |
| <span data-ttu-id="e346f-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="e346f-483">availability [0] runLocation</span></span> |<span data-ttu-id="e346f-484">string</span><span class="sxs-lookup"><span data-stu-id="e346f-484">string</span></span> |<span data-ttu-id="e346f-485">Fonte geográfica de solicitações http</span><span class="sxs-lookup"><span data-stu-id="e346f-485">Geo source of http req</span></span> |
| <span data-ttu-id="e346f-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="e346f-486">availability [0] testName</span></span> |<span data-ttu-id="e346f-487">string</span><span class="sxs-lookup"><span data-stu-id="e346f-487">string</span></span> | |
| <span data-ttu-id="e346f-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="e346f-488">availability [0] testRunId</span></span> |<span data-ttu-id="e346f-489">string</span><span class="sxs-lookup"><span data-stu-id="e346f-489">string</span></span> | |
| <span data-ttu-id="e346f-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="e346f-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="e346f-491">string</span><span class="sxs-lookup"><span data-stu-id="e346f-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="e346f-492">Métricas</span><span class="sxs-lookup"><span data-stu-id="e346f-492">Metrics</span></span>
<span data-ttu-id="e346f-493">Gerado por TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="e346f-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="e346f-494">O valor da métrica é encontrado em context.custom.metrics[0]</span><span class="sxs-lookup"><span data-stu-id="e346f-494">The metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="e346f-495">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e346f-495">For example:</span></span>

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a><span data-ttu-id="e346f-496">Sobre valores de métricas</span><span class="sxs-lookup"><span data-stu-id="e346f-496">About metric values</span></span>
<span data-ttu-id="e346f-497">Valores de métricas, tanto em relatórios de métrica quanto em outros locais, são relatados com uma estrutura de objeto padrão.</span><span class="sxs-lookup"><span data-stu-id="e346f-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="e346f-498">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e346f-498">For example:</span></span>

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

<span data-ttu-id="e346f-499">Atualmente, embora isso possa mudar no futuro, em todos os valores relatados pelos módulos padrão do SDK, `count==1` e apenas os campos `name` e `value` são úteis.</span><span class="sxs-lookup"><span data-stu-id="e346f-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span></span> <span data-ttu-id="e346f-500">O único caso em que eles poderiam ser diferentes seria se você escrevesse suas próprias chamadas TrackMetric, nas quais definiria os outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e346f-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span></span>

<span data-ttu-id="e346f-501">A finalidade dos outros campos é permitir que as métricas sejam agregadas ao SDK, a fim de reduzir o tráfego no portal.</span><span class="sxs-lookup"><span data-stu-id="e346f-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span></span> <span data-ttu-id="e346f-502">Por exemplo, você pode realizar várias leituras sucessivas antes de enviar cada relatório de métricas.</span><span class="sxs-lookup"><span data-stu-id="e346f-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="e346f-503">Depois, você deve calcular o desvio mín., máx. e padrão e o valor agregado (soma ou média), e definir a contagem como o número de leituras representado pelo relatório.</span><span class="sxs-lookup"><span data-stu-id="e346f-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span></span>

<span data-ttu-id="e346f-504">Nas tabelas acima, omitimos os campos min, max, stdDev e sampledValue, que são usados raramente.</span><span class="sxs-lookup"><span data-stu-id="e346f-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="e346f-505">Em vez de agregar previamente as métricas, você pode usar a [amostragem](app-insights-sampling.md) se precisar reduzir o volume de telemetria.</span><span class="sxs-lookup"><span data-stu-id="e346f-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="e346f-506">Durações</span><span class="sxs-lookup"><span data-stu-id="e346f-506">Durations</span></span>
<span data-ttu-id="e346f-507">Exceto quando indicado o contrário, as durações são representadas em décimos de microssegundo, de modo que 10000000.0 significa 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="e346f-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="e346f-508">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e346f-508">See also</span></span>
* [<span data-ttu-id="e346f-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="e346f-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="e346f-510">Exportação Contínua</span><span class="sxs-lookup"><span data-stu-id="e346f-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="e346f-511">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="e346f-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
