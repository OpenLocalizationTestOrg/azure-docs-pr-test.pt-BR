---
title: "Olá aaaUnderstand linguagem de consulta do Azure IoT Hub | Microsoft Docs"
description: "Guia do desenvolvedor - descrição da linguagem de consulta do tipo SQL IoT Hub Olá usado tooretrieve informações sobre trabalhos do seu hub IoT e twins do dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="f8809-103">Referência – linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens</span><span class="sxs-lookup"><span data-stu-id="f8809-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="f8809-104">IoT Hub informa uma poderosa linguagem SQL tooretrieve sobre [twins dispositivo] [ lnk-twins] e [trabalhos][lnk-jobs]e [roteamento de mensagens][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="f8809-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="f8809-105">Este artigo apresenta:</span><span class="sxs-lookup"><span data-stu-id="f8809-105">This article presents:</span></span>

* <span data-ttu-id="f8809-106">Uma introdução toohello principais recursos de linguagem de consulta de IoT Hub de hello e</span><span class="sxs-lookup"><span data-stu-id="f8809-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="f8809-107">Olá descrição detalhada do idioma de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="f8809-108">Introdução às consultas com dispositivos gêmeos</span><span class="sxs-lookup"><span data-stu-id="f8809-108">Get started with device twin queries</span></span>
<span data-ttu-id="f8809-109">Os [dispositivos gêmeos][lnk-twins] podem conter objetos JSON arbitrários como tags e propriedades.</span><span class="sxs-lookup"><span data-stu-id="f8809-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="f8809-110">IoT Hub permite tooquery twins de dispositivo como um único documento JSON que contém todas as informações do dispositivo duas.</span><span class="sxs-lookup"><span data-stu-id="f8809-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="f8809-111">Por exemplo, suponha que seu twins de dispositivo do hub IoT Olá estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8809-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="f8809-112">IoT Hub expõe twins de dispositivo hello como uma coleção de documento chamada **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="f8809-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="f8809-113">Portanto Olá consulta a seguir recupera todo o conjunto de saudação do twins do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="f8809-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="f8809-114">Os [SDKs do Hub IoT][lnk-hub-sdks] dão suporte à paginação de resultados grandes.</span><span class="sxs-lookup"><span data-stu-id="f8809-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="f8809-115">IoT Hub permite twins de dispositivo tooretrieve filtragem com condições arbitrárias.</span><span class="sxs-lookup"><span data-stu-id="f8809-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="f8809-116">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f8809-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="f8809-117">recupera Olá twins de dispositivo com hello **location.region** marca definido muito**EUA**.</span><span class="sxs-lookup"><span data-stu-id="f8809-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="f8809-118">Os operadores boolianos e as comparações aritméticas também têm suporte, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f8809-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="f8809-119">recupera todos os twins dispositivos localizados em Olá nos configurado toosend telemetria menor geralmente a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="f8809-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="f8809-120">Como uma conveniência, também é possível toouse constantes de matriz com hello **na** e **login** operadores (não em).</span><span class="sxs-lookup"><span data-stu-id="f8809-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="f8809-121">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f8809-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="f8809-122">recupera todos os dispositivos gêmeos que relataram conectividade WiFi ou com fio.</span><span class="sxs-lookup"><span data-stu-id="f8809-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="f8809-123">Ele é geralmente necessário tooidentify todos os twins de dispositivo que contém uma propriedade específica.</span><span class="sxs-lookup"><span data-stu-id="f8809-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="f8809-124">IoT Hub dá suporte a função hello `is_defined()` para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="f8809-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="f8809-125">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f8809-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="f8809-126">recuperar todos os twins de dispositivo que definem Olá `connectivity` relatados de propriedade.</span><span class="sxs-lookup"><span data-stu-id="f8809-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="f8809-127">Consulte toohello [cláusula WHERE] [ lnk-query-where] seção para referência completa Olá Olá recursos de filtragem.</span><span class="sxs-lookup"><span data-stu-id="f8809-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="f8809-128">Também há suporte para agrupamento e agregações.</span><span class="sxs-lookup"><span data-stu-id="f8809-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="f8809-129">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f8809-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="f8809-130">Retorna a contagem de saudação de dispositivos de saudação em cada status de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="f8809-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="f8809-131">Olá, exemplo acima ilustra uma situação onde três dispositivos relatado configuração bem-sucedida, dois ainda estiver aplicando a configuração hello e um relatou um erro.</span><span class="sxs-lookup"><span data-stu-id="f8809-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="f8809-132">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="f8809-132">C# example</span></span>
<span data-ttu-id="f8809-133">funcionalidade de consulta Olá é exposta pelo Olá [c# SDK do serviço] [ lnk-hub-sdks] em Olá **RegistryManager** classe.</span><span class="sxs-lookup"><span data-stu-id="f8809-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="f8809-134">Aqui está um exemplo de uma consulta simples:</span><span class="sxs-lookup"><span data-stu-id="f8809-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="f8809-135">Observe como Olá **consulta** objeto é instanciado com um tamanho de página (até too1000) e, em seguida, várias páginas podem ser recuperadas pela chamada hello **GetNextAsTwinAsync** métodos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="f8809-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="f8809-136">Observe que esse objeto de consulta Olá expõe várias **próximo\***, dependendo de opção de desserialização Olá exigida por consulta hello, como objetos de duas ou trabalho do dispositivo, ou simples toobe JSON usado ao usar projeções.</span><span class="sxs-lookup"><span data-stu-id="f8809-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="f8809-137">Exemplo do Node.js</span><span class="sxs-lookup"><span data-stu-id="f8809-137">Node.js example</span></span>
<span data-ttu-id="f8809-138">funcionalidade de consulta Olá é exposta pelo Olá [serviço IoT do Azure SDK para Node.js] [ lnk-hub-sdks] em Olá **registro** objeto.</span><span class="sxs-lookup"><span data-stu-id="f8809-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="f8809-139">Aqui está um exemplo de uma consulta simples:</span><span class="sxs-lookup"><span data-stu-id="f8809-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="f8809-140">Observe como Olá **consulta** objeto é instanciado com um tamanho de página (até too1000) e, em seguida, várias páginas podem ser recuperadas pela chamada hello **nextAsTwin** métodos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="f8809-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="f8809-141">Observe que esse objeto de consulta Olá expõe várias **próximo\***, dependendo de opção de desserialização Olá exigida por consulta hello, como objetos de duas ou trabalho do dispositivo, ou simples toobe JSON usado ao usar projeções.</span><span class="sxs-lookup"><span data-stu-id="f8809-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="f8809-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="f8809-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f8809-143">Resultados da consulta podem ter alguns minutos de atraso com respeito toohello mais recentes valores no twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f8809-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="f8809-144">Se consultar twins dispositivo individual por id, sempre é preferível toouse Olá recuperar duas API do dispositivo, que sempre contém valores mais recentes hello e tem limites de limitação superior.</span><span class="sxs-lookup"><span data-stu-id="f8809-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="f8809-145">Atualmente, há suporte para as comparações apenas entre tipos primitivos (sem objetos), por exemplo `... WHERE properties.desired.config = properties.reported.config` tem suporte apenas se essas propriedades tiverem valores primitivos.</span><span class="sxs-lookup"><span data-stu-id="f8809-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="f8809-146">Introdução às consultas de trabalhos</span><span class="sxs-lookup"><span data-stu-id="f8809-146">Get started with jobs queries</span></span>
<span data-ttu-id="f8809-147">[Trabalhos] [ lnk-jobs] fornecem uma maneira tooexecute operações em conjuntos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f8809-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="f8809-148">Duas cada dispositivo contém informações de saudação de trabalhos de saudação do qual faz parte de uma coleção chamada **trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="f8809-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="f8809-149">Logicamente,</span><span class="sxs-lookup"><span data-stu-id="f8809-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="f8809-150">Atualmente, essa coleção é passível de consulta como **devices.jobs** em Olá linguagem de consulta de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f8809-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8809-151">No momento, a propriedade de trabalhos Olá nunca é retornada ao consultar twins de dispositivo (ou seja, consultas que contém 'de dispositivos').</span><span class="sxs-lookup"><span data-stu-id="f8809-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="f8809-152">Ela só pode ser acessada diretamente com consultas usando `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="f8809-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="f8809-153">Por exemplo, tooget todos os trabalhos (últimos e agendados) que afetam um único dispositivo, você pode usar o hello consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8809-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="f8809-154">Observe como esta consulta fornece o status de dispositivo específico hello (e possivelmente Olá método direto resposta) de cada trabalho retornado.</span><span class="sxs-lookup"><span data-stu-id="f8809-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="f8809-155">Também é possível toofilter com condições Boolianas arbitrárias em todas as propriedades do objeto no hello **devices.jobs** coleção.</span><span class="sxs-lookup"><span data-stu-id="f8809-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="f8809-156">Olá, por exemplo, a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="f8809-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="f8809-157">recupera todos os trabalhos de atualização do dispositivo gêmeo concluídos para o dispositivo **myDeviceId** que foram criados depois de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="f8809-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="f8809-158">Também é possível tooretrieve Olá por dispositivo resultados um único trabalho.</span><span class="sxs-lookup"><span data-stu-id="f8809-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="f8809-159">Limitações</span><span class="sxs-lookup"><span data-stu-id="f8809-159">Limitations</span></span>
<span data-ttu-id="f8809-160">No momento, as consultas em **devices.jobs** não dão suporte a:</span><span class="sxs-lookup"><span data-stu-id="f8809-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="f8809-161">Projeções, portanto, apenas `SELECT *` é possível.</span><span class="sxs-lookup"><span data-stu-id="f8809-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="f8809-162">Condições que fazem referência a duas de dispositivo toohello nas propriedades de toojob de adição (consulte Olá anterior seção).</span><span class="sxs-lookup"><span data-stu-id="f8809-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="f8809-163">Realização de agregações, tal como count, avg e group by.</span><span class="sxs-lookup"><span data-stu-id="f8809-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="f8809-164">Começar a usar expressões de consulta de rotas de mensagem do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="f8809-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="f8809-165">Usando [rotas de dispositivo para nuvem][lnk-devguide-messaging-routes], você pode configurar o IoT Hub mensagens de dispositivo para nuvem toodispatch toodifferent pontos de extremidade com base em expressões avaliadas em relação a mensagens individuais.</span><span class="sxs-lookup"><span data-stu-id="f8809-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="f8809-166">rota de saudação [condição] [ lnk-query-expressions] usa Olá a mesma linguagem de consulta de IoT Hub como condições em duas consultas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f8809-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="f8809-167">Condições de rota são avaliadas no corpo e cabeçalhos de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="f8809-168">A expressão de consulta de roteamento pode envolver somente cabeçalhos das mensagens, apenas Olá corpo da mensagem, ou em cabeçalhos de mensagem e corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="f8809-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="f8809-169">IoT Hub pressupõe um esquema específico para cabeçalhos de saudação e corpo de mensagem em mensagens de ordem de tooroute e Olá seções a seguir descreve o que é necessário para a rota do IoT Hub tooproperly:</span><span class="sxs-lookup"><span data-stu-id="f8809-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="f8809-170">Encaminhamento em cabeçalhos de mensagens</span><span class="sxs-lookup"><span data-stu-id="f8809-170">Routing on message headers</span></span>

<span data-ttu-id="f8809-171">IoT Hub assume Olá representação JSON de cabeçalhos de mensagem para roteamento de mensagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8809-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="f8809-172">Propriedades do sistema de mensagens são prefixadas com hello `'$'` símbolo.</span><span class="sxs-lookup"><span data-stu-id="f8809-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="f8809-173">As propriedades do usuário sempre serão acessadas com seu nome.</span><span class="sxs-lookup"><span data-stu-id="f8809-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="f8809-174">Se um nome de propriedade do usuário acontece toocoincide com uma propriedade do sistema (como `$to`), propriedade de saudação do usuário será recuperada com hello `$to` expressão.</span><span class="sxs-lookup"><span data-stu-id="f8809-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="f8809-175">Você sempre pode acessar a propriedade do sistema hello usando colchetes `{}`: por exemplo, você pode usar a expressão de saudação `{$to}` tooaccess Olá propriedade sistema `to`.</span><span class="sxs-lookup"><span data-stu-id="f8809-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="f8809-176">Nomes de propriedade entre colchetes sempre recuperam a propriedade de sistema correspondentes hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="f8809-177">Lembre-se que os nomes de propriedade não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f8809-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="f8809-178">Todas as propriedades de mensagem são cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f8809-178">All message properties are strings.</span></span> <span data-ttu-id="f8809-179">Propriedades do sistema, conforme descrito em Olá [guia desenvolvedor][lnk-devguide-messaging-format], não estão atualmente disponível toouse em consultas.</span><span class="sxs-lookup"><span data-stu-id="f8809-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="f8809-180">Por exemplo, se você usar um `messageType` propriedade, talvez você queira tooroute todos os ponto de extremidade de tooone de telemetria e o ponto de extremidade do todos os alertas tooanother.</span><span class="sxs-lookup"><span data-stu-id="f8809-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="f8809-181">Você pode escrever Olá telemetria de saudação tooroute expressão a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8809-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="f8809-182">E Olá mensagens de alerta tooroute Olá expressão a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8809-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="f8809-183">Também há suporte para expressões e funções boolianas.</span><span class="sxs-lookup"><span data-stu-id="f8809-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="f8809-184">Esse recurso permite que você toodistinguish entre o nível de gravidade, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f8809-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="f8809-185">Consulte toohello [expressão e condições] [ lnk-query-expressions] seção para a lista completa de saudação de funções e operadores com suporte.</span><span class="sxs-lookup"><span data-stu-id="f8809-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="f8809-186">Encaminhamento em corpos de mensagem</span><span class="sxs-lookup"><span data-stu-id="f8809-186">Routing on message bodies</span></span>

<span data-ttu-id="f8809-187">IoT Hub só pode rotear com base no corpo da mensagem conteúdo se o corpo da mensagem de saudação está corretamente formado JSON codificado em UTF-8, UTF-16 e UTF-32.</span><span class="sxs-lookup"><span data-stu-id="f8809-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="f8809-188">Você deve definir o tipo de conteúdo de saudação da mensagem de saudação muito`application/json` e Olá tooone de codificação de conteúdo de saudação suporte UTF codificações em tooallow de cabeçalhos de mensagem de saudação mensagem de saudação do IoT Hub tooroute com base no conteúdo do corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="f8809-189">Se qualquer um dos cabeçalhos de saudação não for especificado, IoT Hub não tentará tooevaluate qualquer expressão de consulta que envolvem o corpo de saudação em relação a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="f8809-190">Se a mensagem não é uma mensagem JSON, ou se a mensagem de saudação não especificar o tipo de conteúdo hello e codificação de conteúdo, você ainda pode usar mensagem de saudação tooroute com base em cabeçalhos de mensagem de saudação de roteamento de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f8809-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="f8809-191">Você pode usar `$body` na mensagem de saudação do hello consulta expressão tooroute.</span><span class="sxs-lookup"><span data-stu-id="f8809-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="f8809-192">Você pode usar uma referência de corpo simples, referência de matriz de corpo ou várias referências de corpo na expressão de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="f8809-193">A expressão de consulta também pode combinar uma referência de corpo a uma referência de cabeçalho de mensagem.</span><span class="sxs-lookup"><span data-stu-id="f8809-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="f8809-194">Por exemplo, Olá seguem todas as expressões de consulta válida:</span><span class="sxs-lookup"><span data-stu-id="f8809-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="f8809-195">Noções básicas de uma consulta de Hub IoT</span><span class="sxs-lookup"><span data-stu-id="f8809-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="f8809-196">Todas as consultas de Hub IoT são compostas por cláusulas SELECT e FROM cláusulas WHERE e GROUP BY opcionais.</span><span class="sxs-lookup"><span data-stu-id="f8809-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="f8809-197">Cada consulta é executada em uma coleção de documentos JSON, por exemplo, dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="f8809-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="f8809-198">cláusula FROM de saudação indica Olá documento coleção toobe iterada em (**dispositivos** ou **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="f8809-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="f8809-199">Em seguida, Olá filtro no hello onde cláusula é aplicada.</span><span class="sxs-lookup"><span data-stu-id="f8809-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="f8809-200">Com agregações, resultados de saudação desta etapa serão agrupados como Olá especificado na cláusula GROUP BY e, para cada grupo, uma linha é gerada como especificado na cláusula SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="f8809-201">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="f8809-201">FROM clause</span></span>
<span data-ttu-id="f8809-202">Olá **de < from_specification >** cláusula pode assumir somente dois valores: **de dispositivos**, tooquery twins do dispositivo, ou **de devices.jobs**, trabalho de tooquery por dispositivo detalhes.</span><span class="sxs-lookup"><span data-stu-id="f8809-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="f8809-203">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="f8809-203">WHERE clause</span></span>
<span data-ttu-id="f8809-204">Olá **onde < filter_condition >** cláusula é opcional.</span><span class="sxs-lookup"><span data-stu-id="f8809-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="f8809-205">Especifica uma ou mais condições que os documentos JSON Olá na coleção de FROM Olá devem atender toobe incluído como parte do resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="f8809-206">Qualquer documento JSON deve ser avaliada Olá especificado condições muito "true" toobe incluído no resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="f8809-207">Olá permitido condições são descritas na seção [expressões e condições][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="f8809-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="f8809-208">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="f8809-208">SELECT clause</span></span>
<span data-ttu-id="f8809-209">cláusula SELECT Hello (**selecione < select_list >**) é obrigatório e especifica quais valores são recuperados da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="f8809-210">Ele especifica Olá JSON valores toobe usado toogenerate novos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="f8809-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="f8809-211">Para cada elemento de Olá subconjunto filtrado (e, opcionalmente, agrupado) da coleção de FROM hello, a fase de projeção hello gera um novo objeto JSON, construído com valores hello especificados na cláusula SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="f8809-212">Gramática de saudação da cláusula SELECT Olá é do seguinte:</span><span class="sxs-lookup"><span data-stu-id="f8809-212">Following is hello grammar of hello SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="f8809-213">onde **attribute_name** refere-se a propriedade tooany de documento JSON Olá na coleção de FROM hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="f8809-214">Alguns exemplos de cláusulas SELECT podem ser encontrados no hello [guia de Introdução com consultas de duas dispositivo] [ lnk-query-getstarted] seção.</span><span class="sxs-lookup"><span data-stu-id="f8809-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="f8809-215">No momento, as cláusulas de seleção diferentes de **SELECT \*** têm suporte apenas em consultas de agregação em dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="f8809-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="f8809-216">Cláusula GROUP BY</span><span class="sxs-lookup"><span data-stu-id="f8809-216">GROUP BY clause</span></span>
<span data-ttu-id="f8809-217">Olá **GROUP BY < group_specification >** cláusula é uma etapa opcional que pode ser executada depois de filtro de saudação especificado em Olá cláusula WHERE e antes de projeção de saudação especificada no hello selecionar.</span><span class="sxs-lookup"><span data-stu-id="f8809-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="f8809-218">Ela agrupa documentos com base no valor de saudação de um atributo.</span><span class="sxs-lookup"><span data-stu-id="f8809-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="f8809-219">Esses grupos são usados toogenerate agregado valores conforme especificado na cláusula SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="f8809-220">Um exemplo de uma consulta usando GROUP BY é:</span><span class="sxs-lookup"><span data-stu-id="f8809-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="f8809-221">a sintaxe formal Olá para GROUP BY é:</span><span class="sxs-lookup"><span data-stu-id="f8809-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="f8809-222">onde **attribute_name** refere-se a propriedade tooany de documento JSON Olá na coleção de FROM hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="f8809-223">Atualmente, a cláusula GROUP BY da saudação só tem suporte ao consultar twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f8809-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="f8809-224">Expressões e condições</span><span class="sxs-lookup"><span data-stu-id="f8809-224">Expressions and conditions</span></span>
<span data-ttu-id="f8809-225">Em um alto nível, uma *expressão*:</span><span class="sxs-lookup"><span data-stu-id="f8809-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="f8809-226">Avalia tooan instância de um tipo JSON (como booleano, número, cadeia de caracteres, matriz ou objeto), e</span><span class="sxs-lookup"><span data-stu-id="f8809-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="f8809-227">É definido pela manipulação de dados provenientes do documento JSON de dispositivo hello e constantes usando funções e operadores internos.</span><span class="sxs-lookup"><span data-stu-id="f8809-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="f8809-228">*Condições* são expressões que avaliam tooa booliano.</span><span class="sxs-lookup"><span data-stu-id="f8809-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="f8809-229">Qualquer constante diferente de booliano **true** é considerado como **false** (incluindo **nulo**, **indefinido**, qualquer instância de objeto ou matriz qualquer cadeia de caracteres e claramente saudação booliano **false**).</span><span class="sxs-lookup"><span data-stu-id="f8809-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="f8809-230">saudação de sintaxe para expressões é:</span><span class="sxs-lookup"><span data-stu-id="f8809-230">hello syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="f8809-231">onde:</span><span class="sxs-lookup"><span data-stu-id="f8809-231">where:</span></span>

| <span data-ttu-id="f8809-232">Símbolo</span><span class="sxs-lookup"><span data-stu-id="f8809-232">Symbol</span></span> | <span data-ttu-id="f8809-233">Definição</span><span class="sxs-lookup"><span data-stu-id="f8809-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="f8809-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="f8809-234">attribute_name</span></span> | <span data-ttu-id="f8809-235">Qualquer propriedade de documento JSON Olá Olá **FROM** coleção.</span><span class="sxs-lookup"><span data-stu-id="f8809-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="f8809-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="f8809-236">binary_operator</span></span> | <span data-ttu-id="f8809-237">Qualquer operador binário listados no hello [operadores](#operators) seção.</span><span class="sxs-lookup"><span data-stu-id="f8809-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="f8809-238">function_name</span><span class="sxs-lookup"><span data-stu-id="f8809-238">function_name</span></span>| <span data-ttu-id="f8809-239">Todas as funções listadas na Olá [funções](#functions) seção.</span><span class="sxs-lookup"><span data-stu-id="f8809-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="f8809-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="f8809-240">decimal_literal</span></span> |<span data-ttu-id="f8809-241">Um float expresso em notação decimal.</span><span class="sxs-lookup"><span data-stu-id="f8809-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="f8809-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="f8809-242">hexadecimal_literal</span></span> |<span data-ttu-id="f8809-243">Um número expresso pela cadeia de caracteres de saudação '0x' seguido por uma cadeia de caracteres de dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="f8809-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="f8809-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="f8809-244">string_literal</span></span> |<span data-ttu-id="f8809-245">Literais de cadeia de caracteres são cadeias de caracteres Unicode representadas por uma sequência de zero ou mais caracteres Unicode ou sequências de escape.</span><span class="sxs-lookup"><span data-stu-id="f8809-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="f8809-246">As literais de cadeia de caracteres são colocadas entre aspas simples (apóstrofe: ') ou aspas duplas (aspas: ").</span><span class="sxs-lookup"><span data-stu-id="f8809-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="f8809-247">Escapes permitidos: `\'`, `\"`, `\\`, `\uXXXX` para caracteres Unicode definidos por quatro dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="f8809-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="f8809-248">Operadores</span><span class="sxs-lookup"><span data-stu-id="f8809-248">Operators</span></span>
<span data-ttu-id="f8809-249">Olá operadores a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="f8809-249">hello following operators are supported:</span></span>

| <span data-ttu-id="f8809-250">Família</span><span class="sxs-lookup"><span data-stu-id="f8809-250">Family</span></span> | <span data-ttu-id="f8809-251">Operadores</span><span class="sxs-lookup"><span data-stu-id="f8809-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="f8809-252">Aritmético</span><span class="sxs-lookup"><span data-stu-id="f8809-252">Arithmetic</span></span> |<span data-ttu-id="f8809-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="f8809-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="f8809-254">Lógico</span><span class="sxs-lookup"><span data-stu-id="f8809-254">Logical</span></span> |<span data-ttu-id="f8809-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="f8809-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="f8809-256">Comparação</span><span class="sxs-lookup"><span data-stu-id="f8809-256">Comparison</span></span> |<span data-ttu-id="f8809-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="f8809-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="f8809-258">Funções</span><span class="sxs-lookup"><span data-stu-id="f8809-258">Functions</span></span>
<span data-ttu-id="f8809-259">Ao consultar Olá twins e trabalhos só tem suportada a função é:</span><span class="sxs-lookup"><span data-stu-id="f8809-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="f8809-260">Função</span><span class="sxs-lookup"><span data-stu-id="f8809-260">Function</span></span> | <span data-ttu-id="f8809-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8809-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f8809-262">IS_DEFINED(propriedade)</span><span class="sxs-lookup"><span data-stu-id="f8809-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="f8809-263">Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor (incluindo `null`).</span><span class="sxs-lookup"><span data-stu-id="f8809-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="f8809-264">Em condições de rotas, Olá funções matemáticas a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="f8809-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="f8809-265">Função</span><span class="sxs-lookup"><span data-stu-id="f8809-265">Function</span></span> | <span data-ttu-id="f8809-266">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8809-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f8809-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-267">ABS(x)</span></span> | <span data-ttu-id="f8809-268">Retorna Olá valor absoluto (positivo) da saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="f8809-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="f8809-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-269">EXP(x)</span></span> | <span data-ttu-id="f8809-270">Retorna um valor Olá exponencial de saudação especificado expressão numérica (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="f8809-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="f8809-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="f8809-271">POWER(x,y)</span></span> | <span data-ttu-id="f8809-272">Retorna Olá Olá especificado valor toohello da expressão especificada power (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="f8809-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="f8809-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-273">SQUARE(x)</span></span> | <span data-ttu-id="f8809-274">Saudação de retorna quadrada de saudação especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="f8809-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="f8809-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-275">CEILING(x)</span></span> | <span data-ttu-id="f8809-276">Retorna Olá menor valor de número inteiro maior ou igual ao Olá expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="f8809-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="f8809-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-277">FLOOR(x)</span></span> | <span data-ttu-id="f8809-278">Retorna Olá maior inteiro menor ou igual a toohello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="f8809-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="f8809-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-279">SIGN(x)</span></span> | <span data-ttu-id="f8809-280">Retorna Olá positivo (+ 1), zero (0), ou sinal de negativo (-1) de saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="f8809-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="f8809-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-281">SQRT(x)</span></span> | <span data-ttu-id="f8809-282">Saudação de retorna quadrada de saudação especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="f8809-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="f8809-283">Em condições de rotas, Olá Verificando e funções de conversão de tipo a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="f8809-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="f8809-284">Função</span><span class="sxs-lookup"><span data-stu-id="f8809-284">Function</span></span> | <span data-ttu-id="f8809-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8809-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f8809-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f8809-286">AS_NUMBER</span></span> | <span data-ttu-id="f8809-287">Converte o número de tooa de cadeia de caracteres de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="f8809-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="f8809-288">`noop` se a entrada for um número; `Undefined` se a cadeia de caracteres não representar um número.</span><span class="sxs-lookup"><span data-stu-id="f8809-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="f8809-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="f8809-289">IS_ARRAY</span></span> | <span data-ttu-id="f8809-290">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="f8809-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="f8809-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="f8809-291">IS_BOOL</span></span> | <span data-ttu-id="f8809-292">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="f8809-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="f8809-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="f8809-293">IS_DEFINED</span></span> | <span data-ttu-id="f8809-294">Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor.</span><span class="sxs-lookup"><span data-stu-id="f8809-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="f8809-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="f8809-295">IS_NULL</span></span> | <span data-ttu-id="f8809-296">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é nulo.</span><span class="sxs-lookup"><span data-stu-id="f8809-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="f8809-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f8809-297">IS_NUMBER</span></span> | <span data-ttu-id="f8809-298">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um número.</span><span class="sxs-lookup"><span data-stu-id="f8809-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="f8809-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="f8809-299">IS_OBJECT</span></span> | <span data-ttu-id="f8809-300">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="f8809-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="f8809-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="f8809-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="f8809-302">Retorna um valor booliano que indica se o tipo de saudação do hello especificado de expressão é um primitivo (cadeia de caracteres, booleano, numérico ou `null`).</span><span class="sxs-lookup"><span data-stu-id="f8809-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="f8809-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="f8809-303">IS_STRING</span></span> | <span data-ttu-id="f8809-304">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f8809-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="f8809-305">Em condições de rotas, Olá funções de cadeia de caracteres a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="f8809-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="f8809-306">Função</span><span class="sxs-lookup"><span data-stu-id="f8809-306">Function</span></span> | <span data-ttu-id="f8809-307">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8809-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f8809-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="f8809-308">CONCAT(x, …)</span></span> | <span data-ttu-id="f8809-309">Retorna uma cadeia de caracteres que é o resultado de saudação da concatenação de dois ou mais valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f8809-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="f8809-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-310">LENGTH(x)</span></span> | <span data-ttu-id="f8809-311">Retorna o número de saudação de caracteres da saudação especificado expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f8809-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="f8809-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-312">LOWER(x)</span></span> | <span data-ttu-id="f8809-313">Retorna uma expressão de cadeia de caracteres após converter caracteres maiusculos toolowercase de dados.</span><span class="sxs-lookup"><span data-stu-id="f8809-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="f8809-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="f8809-314">UPPER(x)</span></span> | <span data-ttu-id="f8809-315">Retorna uma expressão de cadeia de caracteres após converter caracteres minúsculos toouppercase de dados.</span><span class="sxs-lookup"><span data-stu-id="f8809-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="f8809-316">SUBSTRING(cadeia de caracteres, início [, tamanho])</span><span class="sxs-lookup"><span data-stu-id="f8809-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="f8809-317">Retorna parte de uma expressão de cadeia de caracteres começando em Olá especificado a posição do caractere com base em zero e continua toohello especificado comprimento ou toohello final da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8809-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="f8809-318">INDEX_OF (cadeia de caracteres, fragmento)</span><span class="sxs-lookup"><span data-stu-id="f8809-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="f8809-319">Retorna a saudação iniciando a posição da primeira ocorrência de saudação da segunda expressão de cadeia de caracteres hello na primeira expressão de cadeia de caracteres especificada hello, ou -1 se a cadeia de caracteres de saudação não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="f8809-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="f8809-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="f8809-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="f8809-321">Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello começa com hello segundo.</span><span class="sxs-lookup"><span data-stu-id="f8809-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="f8809-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="f8809-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="f8809-323">Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo.</span><span class="sxs-lookup"><span data-stu-id="f8809-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="f8809-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="f8809-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="f8809-325">Retorna um valor booleano que indica se a primeira expressão de cadeia de caracteres hello contém Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="f8809-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f8809-326">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8809-326">Next steps</span></span>
<span data-ttu-id="f8809-327">Saiba como as consultas em seus aplicativos usando tooexecute [SDKs do Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="f8809-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
