---
title: Entender os trabalhos de Hub IoT do Azure | Microsoft Docs
description: "Guia do desenvolvedor – agendar trabalhos para execução em vários dispositivos conectados ao seu Hub IoT. Os trabalhos podem atualizar marcações e propriedades desejadas e invocar métodos diretos em vários dispositivos."
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
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="7272b-104">Agendar trabalhos em vários dispositivos</span><span class="sxs-lookup"><span data-stu-id="7272b-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="7272b-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7272b-105">Overview</span></span>
<span data-ttu-id="7272b-106">Conforme descrito em artigos anteriores, o Hub IoT do Azure permite diversos blocos de construção ([marcas e propriedades do dispositivo gêmeo][lnk-twin-devguide] e [métodos diretos][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="7272b-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="7272b-107">Normalmente, os aplicativos back-end permitem que administradores e operadores do dispositivo atualizem e interajam com dispositivos IoT em massa e em um horário agendado.</span><span class="sxs-lookup"><span data-stu-id="7272b-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="7272b-108">Os trabalhos encapsulam a execução de atualizações do dispositivo gêmeo e de métodos diretos em um conjunto de dispositivos e em um horário agendado.</span><span class="sxs-lookup"><span data-stu-id="7272b-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="7272b-109">Por exemplo, um operador poderia usar um aplicativo back-end que iniciaria e controlaria um trabalho a fim de reinicializar um conjunto de dispositivos no edifício 43, no terceiro andar, em um horário que não interromperia as operações do edifício.</span><span class="sxs-lookup"><span data-stu-id="7272b-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="7272b-110">Quando usar</span><span class="sxs-lookup"><span data-stu-id="7272b-110">When to use</span></span>
<span data-ttu-id="7272b-111">Considere o uso de trabalhos quando: uma solução back-end precisar agendar e acompanhar o andamento de qualquer uma das seguintes atividades a seguir em um conjunto de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="7272b-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="7272b-112">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="7272b-112">Update desired properties</span></span>
* <span data-ttu-id="7272b-113">Marcas de atualização</span><span class="sxs-lookup"><span data-stu-id="7272b-113">Update tags</span></span>
* <span data-ttu-id="7272b-114">Chamar métodos diretos</span><span class="sxs-lookup"><span data-stu-id="7272b-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="7272b-115">Ciclo de vida do trabalho</span><span class="sxs-lookup"><span data-stu-id="7272b-115">Job lifecycle</span></span>
<span data-ttu-id="7272b-116">Os trabalhos são iniciados pelo back-end da solução e mantidos pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7272b-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="7272b-117">Você pode iniciar um trabalho por meio de um URI voltado para o serviço (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) e consultar o andamento de um trabalho em execução por meio de um URI voltado para o serviço (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="7272b-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="7272b-118">Após o início de um trabalho, a consulta aos trabalhos permite que o aplicativo back-end atualize o status dos trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="7272b-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="7272b-119">Quando você inicia um trabalho, os valores e nomes de propriedade só podem conter caracteres alfanuméricos imprimíveis US-ASCII, exceto pelo seguinte conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="7272b-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="7272b-120">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="7272b-120">Reference topics:</span></span>
<span data-ttu-id="7272b-121">Os tópicos de referência a seguir fornecem a você mais informações sobre como usar os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="7272b-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="7272b-122">Trabalhos para execução de métodos diretos</span><span class="sxs-lookup"><span data-stu-id="7272b-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="7272b-123">Veja a seguir os detalhes da solicitação HTTP 1.1 para execução de um [método direto][lnk-dev-methods] em um conjunto de dispositivos usando um trabalho:</span><span class="sxs-lookup"><span data-stu-id="7272b-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="7272b-124">A condição de consulta também pode ser em uma única ID de dispositivo ou em uma lista de IDs de dispositivos, conforme mostrado abaixo</span><span class="sxs-lookup"><span data-stu-id="7272b-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="7272b-125">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="7272b-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="7272b-126">A [Linguagem de consulta de Hub IoT][lnk-query] aborda a linguagem de consulta de Hub IoT em detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="7272b-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="7272b-127">Trabalhos para atualização das propriedades do dispositivo gêmeo</span><span class="sxs-lookup"><span data-stu-id="7272b-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="7272b-128">Veja a seguir os detalhes da solicitação HTTP 1.1 de atualização das propriedades do dispositivo gêmeo usando um trabalho:</span><span class="sxs-lookup"><span data-stu-id="7272b-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="7272b-129">Consultar o andamento dos trabalhos</span><span class="sxs-lookup"><span data-stu-id="7272b-129">Querying for progress on jobs</span></span>
<span data-ttu-id="7272b-130">Veja a seguir os detalhes da solicitação HTTP 1.1 para [consultar trabalhos][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="7272b-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="7272b-131">O continuationToken é fornecido pela resposta.</span><span class="sxs-lookup"><span data-stu-id="7272b-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="7272b-132">Propriedades dos trabalhos</span><span class="sxs-lookup"><span data-stu-id="7272b-132">Jobs Properties</span></span>
<span data-ttu-id="7272b-133">Veja a seguir uma lista de propriedades e descrições correspondentes que podem ser usadas durante a consulta por trabalhos ou por resultados do trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="7272b-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7272b-134">Property</span></span> | <span data-ttu-id="7272b-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="7272b-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7272b-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="7272b-136">**jobId**</span></span> |<span data-ttu-id="7272b-137">ID fornecida pelo aplicativo para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="7272b-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="7272b-138">**startTime**</span></span> |<span data-ttu-id="7272b-139">Hora de início fornecida pelo aplicativo (ISO 8601) para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="7272b-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="7272b-140">**endTime**</span></span> |<span data-ttu-id="7272b-141">Data fornecida pelo Hub IoT (ISO-8601) para a conclusão do trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="7272b-142">Válida somente após o trabalho atingir o estado 'concluído'.</span><span class="sxs-lookup"><span data-stu-id="7272b-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="7272b-143">**tipo**</span><span class="sxs-lookup"><span data-stu-id="7272b-143">**type**</span></span> |<span data-ttu-id="7272b-144">Tipos de trabalhos:</span><span class="sxs-lookup"><span data-stu-id="7272b-144">Types of jobs:</span></span> |
| <span data-ttu-id="7272b-145">**scheduledUpdateTwin**: Um trabalho usado para atualizar um conjunto de propriedades ou marcas desejadas.</span><span class="sxs-lookup"><span data-stu-id="7272b-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="7272b-146">**scheduledDeviceMethod**: um trabalho usado para invocar um método de dispositivo em um conjunto de dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="7272b-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="7272b-147">**status**</span><span class="sxs-lookup"><span data-stu-id="7272b-147">**status**</span></span> |<span data-ttu-id="7272b-148">Estado atual do trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-148">Current state of the job.</span></span> <span data-ttu-id="7272b-149">Valores possíveis para o status:</span><span class="sxs-lookup"><span data-stu-id="7272b-149">Possible values for status:</span></span> |
| <span data-ttu-id="7272b-150">**pendente**: agendado e aguardando ser selecionado pelo serviço do trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="7272b-151">**agendado**: agendado para um horário no futuro.</span><span class="sxs-lookup"><span data-stu-id="7272b-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="7272b-152">**executando**: trabalho ativo no momento.</span><span class="sxs-lookup"><span data-stu-id="7272b-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="7272b-153">**cancelado**: o trabalho foi cancelado.</span><span class="sxs-lookup"><span data-stu-id="7272b-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="7272b-154">**falha**: o trabalho falhou.</span><span class="sxs-lookup"><span data-stu-id="7272b-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="7272b-155">**concluído**: o trabalho foi concluído.</span><span class="sxs-lookup"><span data-stu-id="7272b-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="7272b-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="7272b-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="7272b-157">Estatísticas sobre a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="7272b-158">Propriedades **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="7272b-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="7272b-159">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7272b-159">Property</span></span> | <span data-ttu-id="7272b-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="7272b-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7272b-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="7272b-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="7272b-162">Número de dispositivos no trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="7272b-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="7272b-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="7272b-164">Número de dispositivos nos quais o trabalho falhou.</span><span class="sxs-lookup"><span data-stu-id="7272b-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="7272b-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="7272b-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="7272b-166">Número de dispositivos nos quais o trabalho teve êxito.</span><span class="sxs-lookup"><span data-stu-id="7272b-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="7272b-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="7272b-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="7272b-168">Número de dispositivos que estão executando o trabalho no momento.</span><span class="sxs-lookup"><span data-stu-id="7272b-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="7272b-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="7272b-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="7272b-170">Número de dispositivos com execução pendente do trabalho.</span><span class="sxs-lookup"><span data-stu-id="7272b-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="7272b-171">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="7272b-171">Additional reference material</span></span>
<span data-ttu-id="7272b-172">Outros tópicos de referência no Guia do desenvolvedor do Hub IoT incluem:</span><span class="sxs-lookup"><span data-stu-id="7272b-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="7272b-173">[Pontos de extremidade do Hub IoT][lnk-endpoints] descreve os vários pontos de extremidade que cada Hub IoT expõe para operações de tempo de execução e de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="7272b-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="7272b-174">[Limitação e cotas][lnk-quotas] descreve as cotas que se aplicam ao serviço Hub IoT e o comportamento de limitação esperado ao usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="7272b-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="7272b-175">[SDKs de dispositivo e serviço do Azure IoT][lnk-sdks] lista os vários SDKs de linguagem que você pode usar no desenvolvimento de aplicativos de dispositivo e de serviço que interagem com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7272b-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="7272b-176">[Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens][lnk-query] descreve a linguagem de consulta do Hub IoT que você pode usar para recuperar informações do Hub IoT sobre dispositivos gêmeos e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="7272b-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="7272b-177">[Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt] fornece mais informações sobre o suporte do Hub IoT para o protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="7272b-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7272b-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7272b-178">Next steps</span></span>
<span data-ttu-id="7272b-179">Se você quiser experimentar alguns dos conceitos descritos neste artigo, talvez se interesse pelo seguinte tutorial de Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="7272b-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="7272b-180">[Agendar e transmitir trabalhos][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="7272b-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
