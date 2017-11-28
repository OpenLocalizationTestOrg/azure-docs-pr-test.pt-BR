---
title: aaaAzure modelo de dados do Application Insights | Microsoft Docs
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
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="8139e-103">Modelo de dados de exportação do Application Insights</span><span class="sxs-lookup"><span data-stu-id="8139e-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="8139e-104">Esta tabela lista as propriedades de saudação de telemetria enviada do hello [Application Insights](app-insights-overview.md) SDKs toohello portal.</span><span class="sxs-lookup"><span data-stu-id="8139e-104">This table lists hello properties of telemetry sent from hello [Application Insights](app-insights-overview.md) SDKs toohello portal.</span></span>
<span data-ttu-id="8139e-105">Você verá essas propriedades na saída de dados de [Exportação Contínua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="8139e-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="8139e-106">Elas também aparecerão nos filtros da propriedade no [Explorador de Métrica](app-insights-metrics-explorer.md) e na [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="8139e-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="8139e-107">Toonote pontos:</span><span class="sxs-lookup"><span data-stu-id="8139e-107">Points toonote:</span></span>

* <span data-ttu-id="8139e-108">`[0]`nessas tabelas denota um ponto no caminho de saudação onde você tenha tooinsert um índice. mas nem sempre é 0.</span><span class="sxs-lookup"><span data-stu-id="8139e-108">`[0]` in these tables denotes a point in hello path where you have tooinsert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="8139e-109">A duração é em décimos de microssegundo, portanto, 10000000 = = 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="8139e-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="8139e-110">Datas e horas são UTC e são fornecidas no formato ISO de saudação`yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="8139e-110">Dates and times are UTC, and are given in hello ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="8139e-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8139e-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
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
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
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
  <span data-ttu-id="8139e-112">}</span><span class="sxs-lookup"><span data-stu-id="8139e-112">}</span></span>

## <a name="context"></a><span data-ttu-id="8139e-113">Contexto</span><span class="sxs-lookup"><span data-stu-id="8139e-113">Context</span></span>
<span data-ttu-id="8139e-114">Todos os tipos de telemetria são acompanhados por uma seção de contexto.</span><span class="sxs-lookup"><span data-stu-id="8139e-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="8139e-115">Nem todos esses campos são transmitidos com cada ponto de dados.</span><span class="sxs-lookup"><span data-stu-id="8139e-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="8139e-116">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-116">Path</span></span> | <span data-ttu-id="8139e-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-117">Type</span></span> | <span data-ttu-id="8139e-118">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="8139e-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="8139e-120">object [ ]</span><span class="sxs-lookup"><span data-stu-id="8139e-120">object [ ]</span></span> |<span data-ttu-id="8139e-121">Pares de cadeira de caractere chave-valor definidos pelo parâmetro das propriedades personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8139e-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="8139e-122">Comprimento máximo da chave 100, comprimento máximo dos valores 1024.</span><span class="sxs-lookup"><span data-stu-id="8139e-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="8139e-123">Mais de 100 valores exclusivos, propriedade Olá pode ser pesquisada, mas não pode ser usada para a segmentação.</span><span class="sxs-lookup"><span data-stu-id="8139e-123">More than 100 unique values, hello property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="8139e-124">Máximo de 200 chaves por ikey.</span><span class="sxs-lookup"><span data-stu-id="8139e-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="8139e-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="8139e-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="8139e-126">object [ ]</span><span class="sxs-lookup"><span data-stu-id="8139e-126">object [ ]</span></span> |<span data-ttu-id="8139e-127">Pares de chave-valor definidos pelo parâmetro de medidas personalizadas e por TrackMetrics.</span><span class="sxs-lookup"><span data-stu-id="8139e-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="8139e-128">Comprimento máximo da chave 100, os valores podem ser numéricos.</span><span class="sxs-lookup"><span data-stu-id="8139e-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="8139e-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="8139e-129">context.data.eventTime</span></span> |<span data-ttu-id="8139e-130">string</span><span class="sxs-lookup"><span data-stu-id="8139e-130">string</span></span> |<span data-ttu-id="8139e-131">UTC</span><span class="sxs-lookup"><span data-stu-id="8139e-131">UTC</span></span> |
| <span data-ttu-id="8139e-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="8139e-132">context.data.isSynthetic</span></span> |<span data-ttu-id="8139e-133">Booliano</span><span class="sxs-lookup"><span data-stu-id="8139e-133">boolean</span></span> |<span data-ttu-id="8139e-134">Solicitação aparece toocome de um teste da web ou de bot.</span><span class="sxs-lookup"><span data-stu-id="8139e-134">Request appears toocome from a bot or web test.</span></span> |
| <span data-ttu-id="8139e-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="8139e-135">context.data.samplingRate</span></span> |<span data-ttu-id="8139e-136">número</span><span class="sxs-lookup"><span data-stu-id="8139e-136">number</span></span> |<span data-ttu-id="8139e-137">Porcentagem de telemetria gerada por Olá SDK enviada tooportal.</span><span class="sxs-lookup"><span data-stu-id="8139e-137">Percentage of telemetry generated by hello SDK that is sent tooportal.</span></span> <span data-ttu-id="8139e-138">Intervalo 0.0-100.0.</span><span class="sxs-lookup"><span data-stu-id="8139e-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="8139e-139">context.device</span><span class="sxs-lookup"><span data-stu-id="8139e-139">context.device</span></span> |<span data-ttu-id="8139e-140">objeto</span><span class="sxs-lookup"><span data-stu-id="8139e-140">object</span></span> |<span data-ttu-id="8139e-141">Dispositivo de cliente</span><span class="sxs-lookup"><span data-stu-id="8139e-141">Client device</span></span> |
| <span data-ttu-id="8139e-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="8139e-142">context.device.browser</span></span> |<span data-ttu-id="8139e-143">string</span><span class="sxs-lookup"><span data-stu-id="8139e-143">string</span></span> |<span data-ttu-id="8139e-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="8139e-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="8139e-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="8139e-145">context.device.browserVersion</span></span> |<span data-ttu-id="8139e-146">string</span><span class="sxs-lookup"><span data-stu-id="8139e-146">string</span></span> |<span data-ttu-id="8139e-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="8139e-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="8139e-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="8139e-148">context.device.deviceModel</span></span> |<span data-ttu-id="8139e-149">string</span><span class="sxs-lookup"><span data-stu-id="8139e-149">string</span></span> | |
| <span data-ttu-id="8139e-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="8139e-150">context.device.deviceName</span></span> |<span data-ttu-id="8139e-151">string</span><span class="sxs-lookup"><span data-stu-id="8139e-151">string</span></span> | |
| <span data-ttu-id="8139e-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="8139e-152">context.device.id</span></span> |<span data-ttu-id="8139e-153">string</span><span class="sxs-lookup"><span data-stu-id="8139e-153">string</span></span> | |
| <span data-ttu-id="8139e-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="8139e-154">context.device.locale</span></span> |<span data-ttu-id="8139e-155">string</span><span class="sxs-lookup"><span data-stu-id="8139e-155">string</span></span> |<span data-ttu-id="8139e-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="8139e-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="8139e-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="8139e-157">context.device.network</span></span> |<span data-ttu-id="8139e-158">string</span><span class="sxs-lookup"><span data-stu-id="8139e-158">string</span></span> | |
| <span data-ttu-id="8139e-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="8139e-159">context.device.oemName</span></span> |<span data-ttu-id="8139e-160">string</span><span class="sxs-lookup"><span data-stu-id="8139e-160">string</span></span> | |
| <span data-ttu-id="8139e-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="8139e-161">context.device.osVersion</span></span> |<span data-ttu-id="8139e-162">string</span><span class="sxs-lookup"><span data-stu-id="8139e-162">string</span></span> |<span data-ttu-id="8139e-163">SO host</span><span class="sxs-lookup"><span data-stu-id="8139e-163">Host OS</span></span> |
| <span data-ttu-id="8139e-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="8139e-164">context.device.roleInstance</span></span> |<span data-ttu-id="8139e-165">string</span><span class="sxs-lookup"><span data-stu-id="8139e-165">string</span></span> |<span data-ttu-id="8139e-166">ID do host do servidor</span><span class="sxs-lookup"><span data-stu-id="8139e-166">ID of server host</span></span> |
| <span data-ttu-id="8139e-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="8139e-167">context.device.roleName</span></span> |<span data-ttu-id="8139e-168">string</span><span class="sxs-lookup"><span data-stu-id="8139e-168">string</span></span> | |
| <span data-ttu-id="8139e-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="8139e-169">context.device.type</span></span> |<span data-ttu-id="8139e-170">string</span><span class="sxs-lookup"><span data-stu-id="8139e-170">string</span></span> |<span data-ttu-id="8139e-171">PC, navegador,...</span><span class="sxs-lookup"><span data-stu-id="8139e-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="8139e-172">context.location</span><span class="sxs-lookup"><span data-stu-id="8139e-172">context.location</span></span> |<span data-ttu-id="8139e-173">objeto</span><span class="sxs-lookup"><span data-stu-id="8139e-173">object</span></span> |<span data-ttu-id="8139e-174">Derivado de clientip.</span><span class="sxs-lookup"><span data-stu-id="8139e-174">Derived from clientip.</span></span> |
| <span data-ttu-id="8139e-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="8139e-175">context.location.city</span></span> |<span data-ttu-id="8139e-176">string</span><span class="sxs-lookup"><span data-stu-id="8139e-176">string</span></span> |<span data-ttu-id="8139e-177">Derivado de clientip, se conhecido</span><span class="sxs-lookup"><span data-stu-id="8139e-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="8139e-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="8139e-178">context.location.clientip</span></span> |<span data-ttu-id="8139e-179">string</span><span class="sxs-lookup"><span data-stu-id="8139e-179">string</span></span> |<span data-ttu-id="8139e-180">Última octógono é too0 anônimos.</span><span class="sxs-lookup"><span data-stu-id="8139e-180">Last octagon is anonymized too0.</span></span> |
| <span data-ttu-id="8139e-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="8139e-181">context.location.continent</span></span> |<span data-ttu-id="8139e-182">string</span><span class="sxs-lookup"><span data-stu-id="8139e-182">string</span></span> | |
| <span data-ttu-id="8139e-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="8139e-183">context.location.country</span></span> |<span data-ttu-id="8139e-184">string</span><span class="sxs-lookup"><span data-stu-id="8139e-184">string</span></span> | |
| <span data-ttu-id="8139e-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="8139e-185">context.location.province</span></span> |<span data-ttu-id="8139e-186">string</span><span class="sxs-lookup"><span data-stu-id="8139e-186">string</span></span> |<span data-ttu-id="8139e-187">Estado ou província</span><span class="sxs-lookup"><span data-stu-id="8139e-187">State or province</span></span> |
| <span data-ttu-id="8139e-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="8139e-188">context.operation.id</span></span> |<span data-ttu-id="8139e-189">string</span><span class="sxs-lookup"><span data-stu-id="8139e-189">string</span></span> |<span data-ttu-id="8139e-190">Itens que têm Olá a mesma id de operação são mostrados como itens relacionados no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="8139e-190">Items that have hello same operation id are shown as Related Items in hello portal.</span></span> <span data-ttu-id="8139e-191">Geralmente Olá id da solicitação.</span><span class="sxs-lookup"><span data-stu-id="8139e-191">Usually hello request id.</span></span> |
| <span data-ttu-id="8139e-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="8139e-192">context.operation.name</span></span> |<span data-ttu-id="8139e-193">string</span><span class="sxs-lookup"><span data-stu-id="8139e-193">string</span></span> |<span data-ttu-id="8139e-194">nome solicitação ou url</span><span class="sxs-lookup"><span data-stu-id="8139e-194">url or request name</span></span> |
| <span data-ttu-id="8139e-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="8139e-195">context.operation.parentId</span></span> |<span data-ttu-id="8139e-196">string</span><span class="sxs-lookup"><span data-stu-id="8139e-196">string</span></span> |<span data-ttu-id="8139e-197">Permite itens relacionados aninhados.</span><span class="sxs-lookup"><span data-stu-id="8139e-197">Allows nested related items.</span></span> |
| <span data-ttu-id="8139e-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="8139e-198">context.session.id</span></span> |<span data-ttu-id="8139e-199">string</span><span class="sxs-lookup"><span data-stu-id="8139e-199">string</span></span> |<span data-ttu-id="8139e-200">ID de um grupo de operações de saudação de mesma origem.</span><span class="sxs-lookup"><span data-stu-id="8139e-200">Id of a group of operations from hello same source.</span></span> <span data-ttu-id="8139e-201">Um período de 30 minutos sem uma operação sinaliza o término de saudação de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="8139e-201">A period of 30 minutes without an operation signals hello end of a session.</span></span> |
| <span data-ttu-id="8139e-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="8139e-202">context.session.isFirst</span></span> |<span data-ttu-id="8139e-203">booleano</span><span class="sxs-lookup"><span data-stu-id="8139e-203">boolean</span></span> | |
| <span data-ttu-id="8139e-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8139e-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="8139e-205">string</span><span class="sxs-lookup"><span data-stu-id="8139e-205">string</span></span> | |
| <span data-ttu-id="8139e-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8139e-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="8139e-207">string</span><span class="sxs-lookup"><span data-stu-id="8139e-207">string</span></span> | |
| <span data-ttu-id="8139e-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="8139e-208">context.user.anonId</span></span> |<span data-ttu-id="8139e-209">string</span><span class="sxs-lookup"><span data-stu-id="8139e-209">string</span></span> | |
| <span data-ttu-id="8139e-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8139e-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="8139e-211">string</span><span class="sxs-lookup"><span data-stu-id="8139e-211">string</span></span> |[<span data-ttu-id="8139e-212">Usuário autenticado</span><span class="sxs-lookup"><span data-stu-id="8139e-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="8139e-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="8139e-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="8139e-214">booleano</span><span class="sxs-lookup"><span data-stu-id="8139e-214">boolean</span></span> | |
| <span data-ttu-id="8139e-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="8139e-215">internal.data.documentVersion</span></span> |<span data-ttu-id="8139e-216">string</span><span class="sxs-lookup"><span data-stu-id="8139e-216">string</span></span> | |
| <span data-ttu-id="8139e-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="8139e-217">internal.data.id</span></span> |<span data-ttu-id="8139e-218">string</span><span class="sxs-lookup"><span data-stu-id="8139e-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="8139e-219">Eventos</span><span class="sxs-lookup"><span data-stu-id="8139e-219">Events</span></span>
<span data-ttu-id="8139e-220">Eventos personalizados gerados por [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="8139e-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="8139e-221">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-221">Path</span></span> | <span data-ttu-id="8139e-222">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-222">Type</span></span> | <span data-ttu-id="8139e-223">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="8139e-224">event [0] count</span></span> |<span data-ttu-id="8139e-225">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-225">integer</span></span> |<span data-ttu-id="8139e-226">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="8139e-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8139e-227">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8139e-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8139e-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="8139e-228">event [0] name</span></span> |<span data-ttu-id="8139e-229">string</span><span class="sxs-lookup"><span data-stu-id="8139e-229">string</span></span> |<span data-ttu-id="8139e-230">Nome do evento.</span><span class="sxs-lookup"><span data-stu-id="8139e-230">Event name.</span></span>  <span data-ttu-id="8139e-231">Comprimento máximo 250.</span><span class="sxs-lookup"><span data-stu-id="8139e-231">Max length 250.</span></span> |
| <span data-ttu-id="8139e-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="8139e-232">event [0] url</span></span> |<span data-ttu-id="8139e-233">string</span><span class="sxs-lookup"><span data-stu-id="8139e-233">string</span></span> | |
| <span data-ttu-id="8139e-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8139e-234">event [0] urlData.base</span></span> |<span data-ttu-id="8139e-235">string</span><span class="sxs-lookup"><span data-stu-id="8139e-235">string</span></span> | |
| <span data-ttu-id="8139e-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8139e-236">event [0] urlData.host</span></span> |<span data-ttu-id="8139e-237">string</span><span class="sxs-lookup"><span data-stu-id="8139e-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="8139e-238">Exceções</span><span class="sxs-lookup"><span data-stu-id="8139e-238">Exceptions</span></span>
<span data-ttu-id="8139e-239">Relatórios [exceções](app-insights-asp-net-exceptions.md) no servidor de saudação e no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="8139e-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in hello server and in hello browser.</span></span>

| <span data-ttu-id="8139e-240">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-240">Path</span></span> | <span data-ttu-id="8139e-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-241">Type</span></span> | <span data-ttu-id="8139e-242">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="8139e-243">basicException [0] assembly</span></span> |<span data-ttu-id="8139e-244">string</span><span class="sxs-lookup"><span data-stu-id="8139e-244">string</span></span> | |
| <span data-ttu-id="8139e-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="8139e-245">basicException [0] count</span></span> |<span data-ttu-id="8139e-246">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-246">integer</span></span> |<span data-ttu-id="8139e-247">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="8139e-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8139e-248">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8139e-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8139e-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="8139e-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="8139e-250">string</span><span class="sxs-lookup"><span data-stu-id="8139e-250">string</span></span> | |
| <span data-ttu-id="8139e-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="8139e-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="8139e-252">string</span><span class="sxs-lookup"><span data-stu-id="8139e-252">string</span></span> | |
| <span data-ttu-id="8139e-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="8139e-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="8139e-254">string</span><span class="sxs-lookup"><span data-stu-id="8139e-254">string</span></span> | |
| <span data-ttu-id="8139e-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="8139e-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="8139e-256">string</span><span class="sxs-lookup"><span data-stu-id="8139e-256">string</span></span> | |
| <span data-ttu-id="8139e-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="8139e-257">basicException [0] handledAt</span></span> |<span data-ttu-id="8139e-258">string</span><span class="sxs-lookup"><span data-stu-id="8139e-258">string</span></span> | |
| <span data-ttu-id="8139e-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="8139e-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="8139e-260">booleano</span><span class="sxs-lookup"><span data-stu-id="8139e-260">boolean</span></span> | |
| <span data-ttu-id="8139e-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="8139e-261">basicException [0] id</span></span> |<span data-ttu-id="8139e-262">string</span><span class="sxs-lookup"><span data-stu-id="8139e-262">string</span></span> | |
| <span data-ttu-id="8139e-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="8139e-263">basicException [0] method</span></span> |<span data-ttu-id="8139e-264">string</span><span class="sxs-lookup"><span data-stu-id="8139e-264">string</span></span> | |
| <span data-ttu-id="8139e-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="8139e-265">basicException [0] message</span></span> |<span data-ttu-id="8139e-266">string</span><span class="sxs-lookup"><span data-stu-id="8139e-266">string</span></span> |<span data-ttu-id="8139e-267">Mensagem de exceção.</span><span class="sxs-lookup"><span data-stu-id="8139e-267">Exception message.</span></span> <span data-ttu-id="8139e-268">Comprimento máximo 10k.</span><span class="sxs-lookup"><span data-stu-id="8139e-268">Max length 10k.</span></span> |
| <span data-ttu-id="8139e-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="8139e-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="8139e-270">string</span><span class="sxs-lookup"><span data-stu-id="8139e-270">string</span></span> | |
| <span data-ttu-id="8139e-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="8139e-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="8139e-272">string</span><span class="sxs-lookup"><span data-stu-id="8139e-272">string</span></span> | |
| <span data-ttu-id="8139e-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="8139e-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="8139e-274">string</span><span class="sxs-lookup"><span data-stu-id="8139e-274">string</span></span> | |
| <span data-ttu-id="8139e-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="8139e-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="8139e-276">string</span><span class="sxs-lookup"><span data-stu-id="8139e-276">string</span></span> | |
| <span data-ttu-id="8139e-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="8139e-277">basicException [0] outerId</span></span> |<span data-ttu-id="8139e-278">string</span><span class="sxs-lookup"><span data-stu-id="8139e-278">string</span></span> | |
| <span data-ttu-id="8139e-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="8139e-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="8139e-280">string</span><span class="sxs-lookup"><span data-stu-id="8139e-280">string</span></span> | |
| <span data-ttu-id="8139e-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="8139e-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="8139e-282">string</span><span class="sxs-lookup"><span data-stu-id="8139e-282">string</span></span> | |
| <span data-ttu-id="8139e-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="8139e-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="8139e-284">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-284">integer</span></span> | |
| <span data-ttu-id="8139e-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="8139e-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="8139e-286">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-286">integer</span></span> | |
| <span data-ttu-id="8139e-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="8139e-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="8139e-288">string</span><span class="sxs-lookup"><span data-stu-id="8139e-288">string</span></span> | |
| <span data-ttu-id="8139e-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="8139e-289">basicException [0] stack</span></span> |<span data-ttu-id="8139e-290">string</span><span class="sxs-lookup"><span data-stu-id="8139e-290">string</span></span> |<span data-ttu-id="8139e-291">Comprimento máximo 10k</span><span class="sxs-lookup"><span data-stu-id="8139e-291">Max length 10k</span></span> |
| <span data-ttu-id="8139e-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="8139e-292">basicException [0] typeName</span></span> |<span data-ttu-id="8139e-293">string</span><span class="sxs-lookup"><span data-stu-id="8139e-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="8139e-294">Mensagens de rastreamento</span><span class="sxs-lookup"><span data-stu-id="8139e-294">Trace Messages</span></span>
<span data-ttu-id="8139e-295">Enviado por [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)e por Olá [log adaptadores](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="8139e-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by hello [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="8139e-296">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-296">Path</span></span> | <span data-ttu-id="8139e-297">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-297">Type</span></span> | <span data-ttu-id="8139e-298">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="8139e-299">message [0] loggerName</span></span> |<span data-ttu-id="8139e-300">string</span><span class="sxs-lookup"><span data-stu-id="8139e-300">string</span></span> | |
| <span data-ttu-id="8139e-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="8139e-301">message [0] parameters</span></span> |<span data-ttu-id="8139e-302">string</span><span class="sxs-lookup"><span data-stu-id="8139e-302">string</span></span> | |
| <span data-ttu-id="8139e-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="8139e-303">message [0] raw</span></span> |<span data-ttu-id="8139e-304">string</span><span class="sxs-lookup"><span data-stu-id="8139e-304">string</span></span> |<span data-ttu-id="8139e-305">mensagem de log Hello, comprimento máximo 10k.</span><span class="sxs-lookup"><span data-stu-id="8139e-305">hello log message, max length 10k.</span></span> |
| <span data-ttu-id="8139e-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="8139e-306">message [0] severityLevel</span></span> |<span data-ttu-id="8139e-307">string</span><span class="sxs-lookup"><span data-stu-id="8139e-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="8139e-308">Dependência remota</span><span class="sxs-lookup"><span data-stu-id="8139e-308">Remote dependency</span></span>
<span data-ttu-id="8139e-309">Enviado por TrackDependency.</span><span class="sxs-lookup"><span data-stu-id="8139e-309">Sent by TrackDependency.</span></span> <span data-ttu-id="8139e-310">Usado tooreport desempenho e o uso de [chama toodependencies](app-insights-asp-net-dependencies.md) no servidor de saudação e chamadas AJAX no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="8139e-310">Used tooreport performance and usage of [calls toodependencies](app-insights-asp-net-dependencies.md) in hello server, and AJAX calls in hello browser.</span></span>

| <span data-ttu-id="8139e-311">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-311">Path</span></span> | <span data-ttu-id="8139e-312">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-312">Type</span></span> | <span data-ttu-id="8139e-313">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="8139e-314">remoteDependency [0] async</span></span> |<span data-ttu-id="8139e-315">booleano</span><span class="sxs-lookup"><span data-stu-id="8139e-315">boolean</span></span> | |
| <span data-ttu-id="8139e-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="8139e-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="8139e-317">string</span><span class="sxs-lookup"><span data-stu-id="8139e-317">string</span></span> | |
| <span data-ttu-id="8139e-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="8139e-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="8139e-319">string</span><span class="sxs-lookup"><span data-stu-id="8139e-319">string</span></span> |<span data-ttu-id="8139e-320">Por exemplo, "home/index"</span><span class="sxs-lookup"><span data-stu-id="8139e-320">For example "home/index"</span></span> |
| <span data-ttu-id="8139e-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="8139e-321">remoteDependency [0] count</span></span> |<span data-ttu-id="8139e-322">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-322">integer</span></span> |<span data-ttu-id="8139e-323">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="8139e-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8139e-324">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8139e-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8139e-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="8139e-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="8139e-326">string</span><span class="sxs-lookup"><span data-stu-id="8139e-326">string</span></span> |<span data-ttu-id="8139e-327">HTTP, SQL, ...</span><span class="sxs-lookup"><span data-stu-id="8139e-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="8139e-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8139e-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="8139e-329">número</span><span class="sxs-lookup"><span data-stu-id="8139e-329">number</span></span> |<span data-ttu-id="8139e-330">Hora da chamada toocompletion de resposta de dependência</span><span class="sxs-lookup"><span data-stu-id="8139e-330">Time from call toocompletion of response by dependency</span></span> |
| <span data-ttu-id="8139e-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="8139e-331">remoteDependency [0] id</span></span> |<span data-ttu-id="8139e-332">string</span><span class="sxs-lookup"><span data-stu-id="8139e-332">string</span></span> | |
| <span data-ttu-id="8139e-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="8139e-333">remoteDependency [0] name</span></span> |<span data-ttu-id="8139e-334">string</span><span class="sxs-lookup"><span data-stu-id="8139e-334">string</span></span> |<span data-ttu-id="8139e-335">Url.</span><span class="sxs-lookup"><span data-stu-id="8139e-335">Url.</span></span> <span data-ttu-id="8139e-336">Comprimento máximo 250.</span><span class="sxs-lookup"><span data-stu-id="8139e-336">Max length 250.</span></span> |
| <span data-ttu-id="8139e-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="8139e-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="8139e-338">string</span><span class="sxs-lookup"><span data-stu-id="8139e-338">string</span></span> |<span data-ttu-id="8139e-339">da dependência de HTTP</span><span class="sxs-lookup"><span data-stu-id="8139e-339">from HTTP dependency</span></span> |
| <span data-ttu-id="8139e-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="8139e-340">remoteDependency [0] success</span></span> |<span data-ttu-id="8139e-341">booleano</span><span class="sxs-lookup"><span data-stu-id="8139e-341">boolean</span></span> | |
| <span data-ttu-id="8139e-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="8139e-342">remoteDependency [0] type</span></span> |<span data-ttu-id="8139e-343">string</span><span class="sxs-lookup"><span data-stu-id="8139e-343">string</span></span> |<span data-ttu-id="8139e-344">Http, Sql,...</span><span class="sxs-lookup"><span data-stu-id="8139e-344">Http, Sql,...</span></span> |
| <span data-ttu-id="8139e-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="8139e-345">remoteDependency [0] url</span></span> |<span data-ttu-id="8139e-346">string</span><span class="sxs-lookup"><span data-stu-id="8139e-346">string</span></span> |<span data-ttu-id="8139e-347">Comprimento máximo 2000</span><span class="sxs-lookup"><span data-stu-id="8139e-347">Max length 2000</span></span> |
| <span data-ttu-id="8139e-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8139e-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="8139e-349">string</span><span class="sxs-lookup"><span data-stu-id="8139e-349">string</span></span> |<span data-ttu-id="8139e-350">Comprimento máximo 2000</span><span class="sxs-lookup"><span data-stu-id="8139e-350">Max length 2000</span></span> |
| <span data-ttu-id="8139e-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8139e-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="8139e-352">string</span><span class="sxs-lookup"><span data-stu-id="8139e-352">string</span></span> | |
| <span data-ttu-id="8139e-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8139e-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="8139e-354">string</span><span class="sxs-lookup"><span data-stu-id="8139e-354">string</span></span> |<span data-ttu-id="8139e-355">Comprimento máximo 200</span><span class="sxs-lookup"><span data-stu-id="8139e-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="8139e-356">Solicitações</span><span class="sxs-lookup"><span data-stu-id="8139e-356">Requests</span></span>
<span data-ttu-id="8139e-357">Enviado por [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="8139e-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="8139e-358">módulos padrão Olá usam esse tempo de resposta do servidor tooreports, medido no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8139e-358">hello standard modules use this tooreports server response time, measured at hello server.</span></span>

| <span data-ttu-id="8139e-359">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-359">Path</span></span> | <span data-ttu-id="8139e-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-360">Type</span></span> | <span data-ttu-id="8139e-361">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="8139e-362">request [0] count</span></span> |<span data-ttu-id="8139e-363">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-363">integer</span></span> |<span data-ttu-id="8139e-364">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="8139e-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8139e-365">Por exemplo: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8139e-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8139e-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8139e-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="8139e-367">número</span><span class="sxs-lookup"><span data-stu-id="8139e-367">number</span></span> |<span data-ttu-id="8139e-368">Tempo de tooresponse que chegam de solicitação.</span><span class="sxs-lookup"><span data-stu-id="8139e-368">Time from request arriving tooresponse.</span></span> <span data-ttu-id="8139e-369">1e7 == 1s</span><span class="sxs-lookup"><span data-stu-id="8139e-369">1e7 == 1s</span></span> |
| <span data-ttu-id="8139e-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="8139e-370">request [0] id</span></span> |<span data-ttu-id="8139e-371">string</span><span class="sxs-lookup"><span data-stu-id="8139e-371">string</span></span> |<span data-ttu-id="8139e-372">ID da operação</span><span class="sxs-lookup"><span data-stu-id="8139e-372">Operation id</span></span> |
| <span data-ttu-id="8139e-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="8139e-373">request [0] name</span></span> |<span data-ttu-id="8139e-374">string</span><span class="sxs-lookup"><span data-stu-id="8139e-374">string</span></span> |<span data-ttu-id="8139e-375">GET/POST + url base.</span><span class="sxs-lookup"><span data-stu-id="8139e-375">GET/POST + url base.</span></span>  <span data-ttu-id="8139e-376">Comprimento máximo 250</span><span class="sxs-lookup"><span data-stu-id="8139e-376">Max length 250</span></span> |
| <span data-ttu-id="8139e-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="8139e-377">request [0] responseCode</span></span> |<span data-ttu-id="8139e-378">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-378">integer</span></span> |<span data-ttu-id="8139e-379">Tooclient de resposta enviada de HTTP</span><span class="sxs-lookup"><span data-stu-id="8139e-379">HTTP response sent tooclient</span></span> |
| <span data-ttu-id="8139e-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="8139e-380">request [0] success</span></span> |<span data-ttu-id="8139e-381">booleano</span><span class="sxs-lookup"><span data-stu-id="8139e-381">boolean</span></span> |<span data-ttu-id="8139e-382">Padrão == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="8139e-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="8139e-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="8139e-383">request [0] url</span></span> |<span data-ttu-id="8139e-384">string</span><span class="sxs-lookup"><span data-stu-id="8139e-384">string</span></span> |<span data-ttu-id="8139e-385">Não incluindo o host</span><span class="sxs-lookup"><span data-stu-id="8139e-385">Not including host</span></span> |
| <span data-ttu-id="8139e-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8139e-386">request [0] urlData.base</span></span> |<span data-ttu-id="8139e-387">string</span><span class="sxs-lookup"><span data-stu-id="8139e-387">string</span></span> | |
| <span data-ttu-id="8139e-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8139e-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="8139e-389">string</span><span class="sxs-lookup"><span data-stu-id="8139e-389">string</span></span> | |
| <span data-ttu-id="8139e-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8139e-390">request [0] urlData.host</span></span> |<span data-ttu-id="8139e-391">string</span><span class="sxs-lookup"><span data-stu-id="8139e-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="8139e-392">Desempenho de exibição da página</span><span class="sxs-lookup"><span data-stu-id="8139e-392">Page View Performance</span></span>
<span data-ttu-id="8139e-393">Enviado pelo navegador hello.</span><span class="sxs-lookup"><span data-stu-id="8139e-393">Sent by hello browser.</span></span> <span data-ttu-id="8139e-394">Medidas Olá tempo tooprocess uma página, de usuário iniciante Olá solicitação toodisplay concluída (excluindo as chamadas de AJAX assíncronas).</span><span class="sxs-lookup"><span data-stu-id="8139e-394">Measures hello time tooprocess a page, from user initiating hello request toodisplay complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="8139e-395">Os valores de contexto mostram a versão do navegador e do sistema operacional cliente.</span><span class="sxs-lookup"><span data-stu-id="8139e-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="8139e-396">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-396">Path</span></span> | <span data-ttu-id="8139e-397">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-397">Type</span></span> | <span data-ttu-id="8139e-398">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="8139e-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="8139e-400">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-400">integer</span></span> |<span data-ttu-id="8139e-401">Hora de término da página de Olá Olá HTML toodisplaying de recebimento.</span><span class="sxs-lookup"><span data-stu-id="8139e-401">Time from end of receiving hello HTML toodisplaying hello page.</span></span> |
| <span data-ttu-id="8139e-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="8139e-402">clientPerformance [0] name</span></span> |<span data-ttu-id="8139e-403">string</span><span class="sxs-lookup"><span data-stu-id="8139e-403">string</span></span> | |
| <span data-ttu-id="8139e-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="8139e-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="8139e-405">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-405">integer</span></span> |<span data-ttu-id="8139e-406">Tempo gasto tooestablish uma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="8139e-406">Time taken tooestablish a network connection.</span></span> |
| <span data-ttu-id="8139e-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="8139e-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="8139e-408">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-408">integer</span></span> |<span data-ttu-id="8139e-409">Hora de término de envio Olá tooreceiving da solicitação Olá HTML na resposta.</span><span class="sxs-lookup"><span data-stu-id="8139e-409">Time from end of sending hello request tooreceiving hello HTML in reply.</span></span> |
| <span data-ttu-id="8139e-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="8139e-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="8139e-411">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-411">integer</span></span> |<span data-ttu-id="8139e-412">Hora da solicitação HTTP de saudação toosend obtido.</span><span class="sxs-lookup"><span data-stu-id="8139e-412">Time from taken toosend hello HTTP request.</span></span> |
| <span data-ttu-id="8139e-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="8139e-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="8139e-414">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-414">integer</span></span> |<span data-ttu-id="8139e-415">Tempo de toosend Olá solicitação toodisplaying Olá página inicial.</span><span class="sxs-lookup"><span data-stu-id="8139e-415">Time from starting toosend hello request toodisplaying hello page.</span></span> |
| <span data-ttu-id="8139e-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="8139e-416">clientPerformance [0] url</span></span> |<span data-ttu-id="8139e-417">string</span><span class="sxs-lookup"><span data-stu-id="8139e-417">string</span></span> |<span data-ttu-id="8139e-418">URL dessa solicitação</span><span class="sxs-lookup"><span data-stu-id="8139e-418">URL of this request</span></span> |
| <span data-ttu-id="8139e-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8139e-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="8139e-420">string</span><span class="sxs-lookup"><span data-stu-id="8139e-420">string</span></span> | |
| <span data-ttu-id="8139e-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8139e-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="8139e-422">string</span><span class="sxs-lookup"><span data-stu-id="8139e-422">string</span></span> | |
| <span data-ttu-id="8139e-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8139e-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="8139e-424">string</span><span class="sxs-lookup"><span data-stu-id="8139e-424">string</span></span> | |
| <span data-ttu-id="8139e-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="8139e-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="8139e-426">string</span><span class="sxs-lookup"><span data-stu-id="8139e-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="8139e-427">Visualizações de página</span><span class="sxs-lookup"><span data-stu-id="8139e-427">Page Views</span></span>
<span data-ttu-id="8139e-428">Enviado por trackPageView() ou [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="8139e-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="8139e-429">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-429">Path</span></span> | <span data-ttu-id="8139e-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-430">Type</span></span> | <span data-ttu-id="8139e-431">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="8139e-432">view [0] count</span></span> |<span data-ttu-id="8139e-433">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-433">integer</span></span> |<span data-ttu-id="8139e-434">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="8139e-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8139e-435">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8139e-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8139e-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8139e-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="8139e-437">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-437">integer</span></span> |<span data-ttu-id="8139e-438">Valor definido opcionalmente em trackPageView() ou por startTrackPage() - stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="8139e-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="8139e-439">Olá mesmo não como valores de nodesempenho do cliente.</span><span class="sxs-lookup"><span data-stu-id="8139e-439">Not hello same as clientPerformance values.</span></span> |
| <span data-ttu-id="8139e-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="8139e-440">view [0] name</span></span> |<span data-ttu-id="8139e-441">string</span><span class="sxs-lookup"><span data-stu-id="8139e-441">string</span></span> |<span data-ttu-id="8139e-442">Título da página.</span><span class="sxs-lookup"><span data-stu-id="8139e-442">Page title.</span></span>  <span data-ttu-id="8139e-443">Comprimento máximo 250</span><span class="sxs-lookup"><span data-stu-id="8139e-443">Max length 250</span></span> |
| <span data-ttu-id="8139e-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="8139e-444">view [0] url</span></span> |<span data-ttu-id="8139e-445">string</span><span class="sxs-lookup"><span data-stu-id="8139e-445">string</span></span> | |
| <span data-ttu-id="8139e-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8139e-446">view [0] urlData.base</span></span> |<span data-ttu-id="8139e-447">string</span><span class="sxs-lookup"><span data-stu-id="8139e-447">string</span></span> | |
| <span data-ttu-id="8139e-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8139e-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="8139e-449">string</span><span class="sxs-lookup"><span data-stu-id="8139e-449">string</span></span> | |
| <span data-ttu-id="8139e-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8139e-450">view [0] urlData.host</span></span> |<span data-ttu-id="8139e-451">string</span><span class="sxs-lookup"><span data-stu-id="8139e-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="8139e-452">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="8139e-452">Availability</span></span>
<span data-ttu-id="8139e-453">Relata os [testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="8139e-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="8139e-454">Caminho</span><span class="sxs-lookup"><span data-stu-id="8139e-454">Path</span></span> | <span data-ttu-id="8139e-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="8139e-455">Type</span></span> | <span data-ttu-id="8139e-456">Observações</span><span class="sxs-lookup"><span data-stu-id="8139e-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8139e-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="8139e-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="8139e-458">string</span><span class="sxs-lookup"><span data-stu-id="8139e-458">string</span></span> |<span data-ttu-id="8139e-459">Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="8139e-459">availability</span></span> |
| <span data-ttu-id="8139e-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="8139e-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="8139e-461">número</span><span class="sxs-lookup"><span data-stu-id="8139e-461">number</span></span> |<span data-ttu-id="8139e-462">1.0 ou 0.0</span><span class="sxs-lookup"><span data-stu-id="8139e-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="8139e-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="8139e-463">availability [0] count</span></span> |<span data-ttu-id="8139e-464">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-464">integer</span></span> |<span data-ttu-id="8139e-465">100/(taxa de[amostragem](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="8139e-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8139e-466">Por exemplo, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8139e-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8139e-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="8139e-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="8139e-468">string</span><span class="sxs-lookup"><span data-stu-id="8139e-468">string</span></span> | |
| <span data-ttu-id="8139e-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="8139e-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="8139e-470">inteiro</span><span class="sxs-lookup"><span data-stu-id="8139e-470">integer</span></span> | |
| <span data-ttu-id="8139e-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="8139e-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="8139e-472">string</span><span class="sxs-lookup"><span data-stu-id="8139e-472">string</span></span> | |
| <span data-ttu-id="8139e-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8139e-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="8139e-474">número</span><span class="sxs-lookup"><span data-stu-id="8139e-474">number</span></span> |<span data-ttu-id="8139e-475">Duração do teste.</span><span class="sxs-lookup"><span data-stu-id="8139e-475">Duration of test.</span></span> <span data-ttu-id="8139e-476">1e7==1s</span><span class="sxs-lookup"><span data-stu-id="8139e-476">1e7==1s</span></span> |
| <span data-ttu-id="8139e-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="8139e-477">availability [0] message</span></span> |<span data-ttu-id="8139e-478">string</span><span class="sxs-lookup"><span data-stu-id="8139e-478">string</span></span> |<span data-ttu-id="8139e-479">Diagnóstico de falha</span><span class="sxs-lookup"><span data-stu-id="8139e-479">Failure diagnostic</span></span> |
| <span data-ttu-id="8139e-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="8139e-480">availability [0] result</span></span> |<span data-ttu-id="8139e-481">string</span><span class="sxs-lookup"><span data-stu-id="8139e-481">string</span></span> |<span data-ttu-id="8139e-482">Aprovado/Reprovado</span><span class="sxs-lookup"><span data-stu-id="8139e-482">Pass/Fail</span></span> |
| <span data-ttu-id="8139e-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="8139e-483">availability [0] runLocation</span></span> |<span data-ttu-id="8139e-484">string</span><span class="sxs-lookup"><span data-stu-id="8139e-484">string</span></span> |<span data-ttu-id="8139e-485">Fonte geográfica de solicitações http</span><span class="sxs-lookup"><span data-stu-id="8139e-485">Geo source of http req</span></span> |
| <span data-ttu-id="8139e-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="8139e-486">availability [0] testName</span></span> |<span data-ttu-id="8139e-487">string</span><span class="sxs-lookup"><span data-stu-id="8139e-487">string</span></span> | |
| <span data-ttu-id="8139e-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="8139e-488">availability [0] testRunId</span></span> |<span data-ttu-id="8139e-489">string</span><span class="sxs-lookup"><span data-stu-id="8139e-489">string</span></span> | |
| <span data-ttu-id="8139e-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="8139e-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="8139e-491">string</span><span class="sxs-lookup"><span data-stu-id="8139e-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="8139e-492">Métricas</span><span class="sxs-lookup"><span data-stu-id="8139e-492">Metrics</span></span>
<span data-ttu-id="8139e-493">Gerado por TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="8139e-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="8139e-494">o valor de métrica Olá é encontrado no context.custom.metrics[0]</span><span class="sxs-lookup"><span data-stu-id="8139e-494">hello metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="8139e-495">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8139e-495">For example:</span></span>

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

## <a name="about-metric-values"></a><span data-ttu-id="8139e-496">Sobre valores de métricas</span><span class="sxs-lookup"><span data-stu-id="8139e-496">About metric values</span></span>
<span data-ttu-id="8139e-497">Valores de métricas, tanto em relatórios de métrica quanto em outros locais, são relatados com uma estrutura de objeto padrão.</span><span class="sxs-lookup"><span data-stu-id="8139e-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="8139e-498">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8139e-498">For example:</span></span>

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

<span data-ttu-id="8139e-499">No momento - Embora isso pode ser alterado em Olá futura - em todos os valores relatados de módulos SDK padrão hello, `count==1` e apenas Olá `name` e `value` os campos são úteis.</span><span class="sxs-lookup"><span data-stu-id="8139e-499">Currently - though this might change in hello future - in all values reported from hello standard SDK modules, `count==1` and only hello `name` and `value` fields are useful.</span></span> <span data-ttu-id="8139e-500">Olá único caso em que eles seriam diferentes seria se você escrever seus próprio chamadas TrackMetric na qual você define Olá outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8139e-500">hello only case where they would be different would be if you write your own TrackMetric calls in which you set hello other parameters.</span></span>

<span data-ttu-id="8139e-501">Olá finalidade da saudação outros campos é tooallow métricas toobe Olá SDK, portal de toohello tooreduce tráfego agregado.</span><span class="sxs-lookup"><span data-stu-id="8139e-501">hello purpose of hello other fields is tooallow metrics toobe aggregated in hello SDK, tooreduce traffic toohello portal.</span></span> <span data-ttu-id="8139e-502">Por exemplo, você pode realizar várias leituras sucessivas antes de enviar cada relatório de métricas.</span><span class="sxs-lookup"><span data-stu-id="8139e-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="8139e-503">Você deve calcular Olá min, max, desvio padrão e valor de agregação (soma ou média) e definir contagem toohello número de leituras representado pelo relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="8139e-503">Then you would calculate hello min, max, standard deviation and aggregate value (sum or average) and set count toohello number of readings represented by hello report.</span></span>

<span data-ttu-id="8139e-504">Nas tabelas de saudação acima, podemos ter omitido Olá campos usados raramente count, min, max, stdDev e sampledValue.</span><span class="sxs-lookup"><span data-stu-id="8139e-504">In hello tables above, we have omitted hello rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="8139e-505">Em vez de pré-agregar métricas, você pode usar [amostragem](app-insights-sampling.md) se precisar de volume de saudação tooreduce de telemetria.</span><span class="sxs-lookup"><span data-stu-id="8139e-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need tooreduce hello volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="8139e-506">Durações</span><span class="sxs-lookup"><span data-stu-id="8139e-506">Durations</span></span>
<span data-ttu-id="8139e-507">Exceto quando indicado o contrário, as durações são representadas em décimos de microssegundo, de modo que 10000000.0 significa 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="8139e-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="8139e-508">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8139e-508">See also</span></span>
* [<span data-ttu-id="8139e-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8139e-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="8139e-510">Exportação Contínua</span><span class="sxs-lookup"><span data-stu-id="8139e-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="8139e-511">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="8139e-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
