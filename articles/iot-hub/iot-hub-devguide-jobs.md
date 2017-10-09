---
title: trabalhos de Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - agendar trabalhos toorun em vários dispositivos conectados tooyour IoT hub. Os trabalhos podem atualizar marcações e propriedades desejadas e invocar métodos diretos em vários dispositivos."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="61581-104">Agendar trabalhos em vários dispositivos</span><span class="sxs-lookup"><span data-stu-id="61581-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="61581-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="61581-105">Overview</span></span>
<span data-ttu-id="61581-106">Conforme descrito em artigos anteriores, o Hub IoT do Azure permite diversos blocos de construção ([marcas e propriedades do dispositivo gêmeo][lnk-twin-devguide] e [métodos diretos][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="61581-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="61581-107">Normalmente, os aplicativos de back-end habilitar tooupdate de operadores e administradores do dispositivo e interagem com dispositivos IoT em massa e em um horário agendado.</span><span class="sxs-lookup"><span data-stu-id="61581-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="61581-108">Trabalhos encapsulam a execução de saudação do dispositivo duas atualizações e métodos diretos de um conjunto de dispositivos em um tempo de agendamento.</span><span class="sxs-lookup"><span data-stu-id="61581-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="61581-109">Por exemplo, um operador seria usar um aplicativo de back-end que iniciar e acompanhar um trabalho tooreboot um conjunto de dispositivos na criação de cada vez que não seriam toohello interrupções operações de criação de saudação 43 e andar 3.</span><span class="sxs-lookup"><span data-stu-id="61581-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="61581-110">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="61581-110">When toouse</span></span>
<span data-ttu-id="61581-111">Considere usar trabalhos quando: uma solução tooschedule de necessidades de back-end e acompanhar andamento qualquer Olá atividades a seguir em um conjunto de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="61581-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="61581-112">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="61581-112">Update desired properties</span></span>
* <span data-ttu-id="61581-113">Marcas de atualização</span><span class="sxs-lookup"><span data-stu-id="61581-113">Update tags</span></span>
* <span data-ttu-id="61581-114">Chamar métodos diretos</span><span class="sxs-lookup"><span data-stu-id="61581-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="61581-115">Ciclo de vida do trabalho</span><span class="sxs-lookup"><span data-stu-id="61581-115">Job lifecycle</span></span>
<span data-ttu-id="61581-116">Trabalhos são iniciados pelo back-end de solução hello e mantidos pelo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61581-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="61581-117">Você pode iniciar um trabalho por meio de um URI voltado para o serviço (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) e consultar o andamento de um trabalho em execução por meio de um URI voltado para o serviço (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="61581-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="61581-118">Depois que um trabalho é iniciado, consultando trabalhos habilita o status de saudação de toorefresh do hello aplicativo de back-end de trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="61581-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="61581-119">Quando você inicia um trabalho, valores e nomes de propriedade só podem conter US-ASCII imprimível alfanumérico, exceto qualquer em Olá conjunto a seguir: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="61581-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="61581-120">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="61581-120">Reference topics:</span></span>
<span data-ttu-id="61581-121">Olá tópicos de referência a seguir fornece mais informações sobre como usar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="61581-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="61581-122">Métodos diretos de tooexecute trabalhos</span><span class="sxs-lookup"><span data-stu-id="61581-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="61581-123">Olá, seguinte é Olá HTTP 1.1 detalhes de solicitação para executar um [método direto] [ lnk-dev-methods] em um conjunto de dispositivos usando um trabalho:</span><span class="sxs-lookup"><span data-stu-id="61581-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="61581-124">condição de consulta Olá também pode ser em um único dispositivo Id ou em uma lista de Ids de dispositivo conforme mostrado abaixo</span><span class="sxs-lookup"><span data-stu-id="61581-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="61581-125">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="61581-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="61581-126">A [Linguagem de consulta de Hub IoT][lnk-query] aborda a linguagem de consulta de Hub IoT em detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="61581-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="61581-127">Trabalhos tooupdate duas propriedades</span><span class="sxs-lookup"><span data-stu-id="61581-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="61581-128">a seguir Olá é detalhes da solicitação de saudação do HTTP 1.1 para atualizar as propriedades do dispositivo duas usando um trabalho:</span><span class="sxs-lookup"><span data-stu-id="61581-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="61581-129">Consultar o andamento dos trabalhos</span><span class="sxs-lookup"><span data-stu-id="61581-129">Querying for progress on jobs</span></span>
<span data-ttu-id="61581-130">Olá seguinte é hello detalhes da solicitação HTTP 1.1 para [consultar trabalhos][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="61581-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="61581-131">Olá continuationToken é fornecido pela resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="61581-132">Propriedades dos trabalhos</span><span class="sxs-lookup"><span data-stu-id="61581-132">Jobs Properties</span></span>
<span data-ttu-id="61581-133">a seguir Olá é uma lista de propriedades e descrições correspondentes, que podem ser usadas durante a consulta para trabalhos ou os resultados do trabalho.</span><span class="sxs-lookup"><span data-stu-id="61581-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="61581-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="61581-134">Property</span></span> | <span data-ttu-id="61581-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="61581-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61581-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="61581-136">**jobId**</span></span> |<span data-ttu-id="61581-137">Aplicativo fornecido ID de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="61581-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="61581-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="61581-138">**startTime**</span></span> |<span data-ttu-id="61581-139">Hora de início do aplicativo fornecido (ISO 8601) para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="61581-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="61581-140">**endTime**</span></span> |<span data-ttu-id="61581-141">IoT Hub fornecido Data (ISO 8601) para quando Olá trabalho concluído.</span><span class="sxs-lookup"><span data-stu-id="61581-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="61581-142">Válido somente depois que o trabalho Olá atinge o estado de saudação 'concluído'.</span><span class="sxs-lookup"><span data-stu-id="61581-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="61581-143">**tipo**</span><span class="sxs-lookup"><span data-stu-id="61581-143">**type**</span></span> |<span data-ttu-id="61581-144">Tipos de trabalhos:</span><span class="sxs-lookup"><span data-stu-id="61581-144">Types of jobs:</span></span> |
| <span data-ttu-id="61581-145">**scheduledUpdateTwin**: tooupdate um trabalho usado um conjunto de propriedades desejadas ou marcas.</span><span class="sxs-lookup"><span data-stu-id="61581-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="61581-146">**scheduledDeviceMethod**: tooinvoke um trabalho usado um método de dispositivo em um conjunto de twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61581-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="61581-147">**status**</span><span class="sxs-lookup"><span data-stu-id="61581-147">**status**</span></span> |<span data-ttu-id="61581-148">Estado atual do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-148">Current state of hello job.</span></span> <span data-ttu-id="61581-149">Valores possíveis para o status:</span><span class="sxs-lookup"><span data-stu-id="61581-149">Possible values for status:</span></span> |
| <span data-ttu-id="61581-150">**pendente** : agendado e aguardando toobe captados pelo serviço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="61581-151">**agendado** : agendado para uma hora no futuro de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="61581-152">**executando**: trabalho ativo no momento.</span><span class="sxs-lookup"><span data-stu-id="61581-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="61581-153">**cancelado**: o trabalho foi cancelado.</span><span class="sxs-lookup"><span data-stu-id="61581-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="61581-154">**falha**: o trabalho falhou.</span><span class="sxs-lookup"><span data-stu-id="61581-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="61581-155">**concluído**: o trabalho foi concluído.</span><span class="sxs-lookup"><span data-stu-id="61581-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="61581-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="61581-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="61581-157">Estatísticas sobre a execução do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="61581-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="61581-158">Propriedades **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="61581-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="61581-159">Propriedade</span><span class="sxs-lookup"><span data-stu-id="61581-159">Property</span></span> | <span data-ttu-id="61581-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="61581-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61581-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="61581-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="61581-162">Número de dispositivos no trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="61581-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="61581-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="61581-164">Número de dispositivos em que o trabalho de saudação falhou.</span><span class="sxs-lookup"><span data-stu-id="61581-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="61581-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="61581-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="61581-166">Número de dispositivos em que o trabalho de saudação teve êxito.</span><span class="sxs-lookup"><span data-stu-id="61581-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="61581-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="61581-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="61581-168">Número de dispositivos que estão executando o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="61581-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="61581-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="61581-170">Número de dispositivos que estão aguardando o trabalho de saudação toorun.</span><span class="sxs-lookup"><span data-stu-id="61581-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="61581-171">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="61581-171">Additional reference material</span></span>
<span data-ttu-id="61581-172">Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:</span><span class="sxs-lookup"><span data-stu-id="61581-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="61581-173">[Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="61581-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="61581-174">[Limitação e cotas] [ lnk-quotas] descreve cotas Olá que se aplicam a toohello serviço de IoT Hub e Olá limitação tooexpect de comportamento quando você usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="61581-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="61581-175">[SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs de vários idiomas você pode usar ao desenvolver aplicativos de dispositivo e o serviço que interagem com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61581-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="61581-176">[Linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens] [ lnk-query] descreve Olá linguagem de consulta de IoT Hub, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61581-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="61581-177">[Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="61581-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61581-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61581-178">Next steps</span></span>
<span data-ttu-id="61581-179">Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá seguindo o tutorial de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="61581-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="61581-180">[Agendar e transmitir trabalhos][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="61581-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
