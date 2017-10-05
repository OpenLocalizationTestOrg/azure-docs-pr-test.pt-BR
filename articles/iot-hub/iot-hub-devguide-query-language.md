---
title: Entender a linguagem de consulta do Hub IoT do Azure | Microsoft Azure
description: "Guia do desenvolvedor – descrição da linguagem de consulta do Hub IoT semelhante a SQL, usada para recuperar informações sobre dispositivos gêmeos e trabalhos do seu Hub IoT."
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
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="9c2c9-103">Referência – linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens</span><span class="sxs-lookup"><span data-stu-id="9c2c9-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="9c2c9-104">O Hub IoT fornece uma linguagem avançada semelhante à SQL para recuperação de informações sobre [dispositivos gêmeos][lnk-twins] e [trabalhos][lnk-jobs] e [encaminhamento de mensagens][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="9c2c9-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="9c2c9-105">Este artigo apresenta:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-105">This article presents:</span></span>

* <span data-ttu-id="9c2c9-106">Uma introdução aos principais recursos da linguagem de consulta do Hub IoT e</span><span class="sxs-lookup"><span data-stu-id="9c2c9-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="9c2c9-107">Uma descrição mais detalhada da linguagem.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="9c2c9-108">Introdução às consultas com dispositivos gêmeos</span><span class="sxs-lookup"><span data-stu-id="9c2c9-108">Get started with device twin queries</span></span>
<span data-ttu-id="9c2c9-109">Os [dispositivos gêmeos][lnk-twins] podem conter objetos JSON arbitrários como tags e propriedades.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="9c2c9-110">O Hub IoT permite consultar dispositivos gêmeos como um único documento JSON que contém todas as informações do dispositivo gêmeo.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="9c2c9-111">Por exemplo, suponha que seus dispositivos gêmeos do Hub IoT tenham a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

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

<span data-ttu-id="9c2c9-112">O Hub IoT expõe os dispositivos gêmeos como uma coleção de documentos chamada **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="9c2c9-113">Então, a consulta a seguir recupera o conjunto completo de dispositivos gêmeos:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="9c2c9-114">Os [SDKs do Hub IoT][lnk-hub-sdks] dão suporte à paginação de resultados grandes.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="9c2c9-115">O Hub IoT permite a você recuperar a filtragem de dispositivos gêmeos com condições arbitrárias.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="9c2c9-116">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="9c2c9-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="9c2c9-117">recupera os dispositivos gêmeos com a tag **location.region** definida como **US**.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="9c2c9-118">Os operadores boolianos e as comparações aritméticas também têm suporte, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="9c2c9-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="9c2c9-119">recupera todos os dispositivos gêmeos localizados nos Estados Unidos configurados para enviar telemetria com menos frequência do que a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="9c2c9-120">Como uma conveniência, também é possível usar constantes de matriz com os operadores **IN** e **NIN** (não in).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="9c2c9-121">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="9c2c9-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="9c2c9-122">recupera todos os dispositivos gêmeos que relataram conectividade WiFi ou com fio.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="9c2c9-123">Normalmente, é necessário identificar todos os dispositivos gêmeos que contêm uma propriedade específica.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="9c2c9-124">O Hub IoT oferece suporte à função `is_defined()` para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="9c2c9-125">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="9c2c9-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="9c2c9-126">recuperou todos os dispositivos gêmeos que definem a propriedade reportada `connectivity`.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="9c2c9-127">Consulte a seção [Cláusula WHERE][lnk-query-where] para encontrar a referência completa dos recursos de filtragem.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="9c2c9-128">Também há suporte para agrupamento e agregações.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="9c2c9-129">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="9c2c9-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="9c2c9-130">retorna a contagem dos dispositivos em cada status de configuração de telemetria.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-130">returns the count of the devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="9c2c9-131">O exemplo anterior ilustra uma situação em que três dispositivos relataram a configuração bem-sucedida, dois ainda estão aplicando a configuração e um relatou um erro.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="9c2c9-132">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="9c2c9-132">C# example</span></span>
<span data-ttu-id="9c2c9-133">A funcionalidade de consulta é exposta pelo [SDK de serviço de C#][lnk-hub-sdks] na classe **RegistryManager**.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="9c2c9-134">Aqui está um exemplo de uma consulta simples:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="9c2c9-135">Observe como o objeto **query** é instanciado com um tamanho de página (até 1000) e, em seguida, várias páginas podem ser recuperadas chamando os métodos **GetNextAsTwinAsync** várias vezes.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="9c2c9-136">Observe que o objeto de consulta expõe vários **Avançar\***, dependendo da opção de desserialização necessária para a consulta, como dispositivos gêmeos ou objetos de trabalho ou JSON simples usado ao utilizar projeções.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="9c2c9-137">Exemplo do Node.js</span><span class="sxs-lookup"><span data-stu-id="9c2c9-137">Node.js example</span></span>
<span data-ttu-id="9c2c9-138">A funcionalidade de consulta é exposta pelo [SDK de serviço IoT do Azure para Node.js][lnk-hub-sdks] no objeto **Registry**.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="9c2c9-139">Aqui está um exemplo de uma consulta simples:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
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

<span data-ttu-id="9c2c9-140">Observe como o objeto **query** é instanciado com um tamanho de página (até 1000) e, em seguida, várias páginas podem ser recuperadas chamando os métodos **nextAsTwin** várias vezes.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="9c2c9-141">Observe que o objeto de consulta expõe vários **avançar\***, dependendo da opção de desserialização necessária para a consulta, como dispositivos gêmeos ou objetos de trabalho ou JSON simples usado ao utilizar projeções.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="9c2c9-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="9c2c9-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9c2c9-143">Os resultados da consulta podem ter alguns minutos de atraso em relação aos valores mais recentes em dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="9c2c9-144">Ao consultar dispositivos gêmeos individuais por ID, é sempre preferível usar a API de recuperação de dispositivo gêmeo, a qual sempre contém os valores mais recentes e tem limites maiores.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="9c2c9-145">Atualmente, há suporte para as comparações apenas entre tipos primitivos (sem objetos), por exemplo `... WHERE properties.desired.config = properties.reported.config` tem suporte apenas se essas propriedades tiverem valores primitivos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="9c2c9-146">Introdução às consultas de trabalhos</span><span class="sxs-lookup"><span data-stu-id="9c2c9-146">Get started with jobs queries</span></span>
<span data-ttu-id="9c2c9-147">Os [Trabalhos][lnk-jobs] fornecem uma maneira de executar operações em conjuntos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="9c2c9-148">Cada dispositivo gêmeo contém as informações dos trabalhos dos quais ele faz parte em uma coleção chamada **jobs**.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="9c2c9-149">Logicamente,</span><span class="sxs-lookup"><span data-stu-id="9c2c9-149">Logically,</span></span>

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

<span data-ttu-id="9c2c9-150">Atualmente, essa coleção pode ser consultada como **devices.jobs** na linguagem de consulta do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c2c9-151">Atualmente, a propriedade jobs nunca é retornada ao consultar dispositivos gêmeos (ou seja, consultas que contém “FROM devices”).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="9c2c9-152">Ela só pode ser acessada diretamente com consultas usando `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="9c2c9-153">Por exemplo, para obter todos os trabalhos (agendados e anteriores) que afetam um único dispositivo, você pode usar a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="9c2c9-154">Observe como essa consulta fornece o status específico do dispositivo (e possivelmente a resposta do método direto) de cada trabalho retornado.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="9c2c9-155">Também é possível filtrar com condições boolianas arbitrárias em todas as propriedades dos objetos na coleção **devices.jobs**.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="9c2c9-156">Por exemplo, a consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="9c2c9-157">recupera todos os trabalhos de atualização do dispositivo gêmeo concluídos para o dispositivo **myDeviceId** que foram criados depois de setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="9c2c9-158">Também é possível recuperar os resultados por dispositivo de um único trabalho.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="9c2c9-159">Limitações</span><span class="sxs-lookup"><span data-stu-id="9c2c9-159">Limitations</span></span>
<span data-ttu-id="9c2c9-160">No momento, as consultas em **devices.jobs** não dão suporte a:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="9c2c9-161">Projeções, portanto, apenas `SELECT *` é possível.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="9c2c9-162">Condições que se referem ao dispositivo gêmeo além das propriedades de trabalho (consulte a seção anterior).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="9c2c9-163">Realização de agregações, tal como count, avg e group by.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="9c2c9-164">Começar a usar expressões de consulta de rotas de mensagem do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="9c2c9-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="9c2c9-165">Usando as [rotas do dispositivo para nuvem][lnk-devguide-messaging-routes], você pode configurar o Hub IoT para distribuir mensagens de dispositivo para a nuvem para diferentes pontos de extremidade com base em expressões avaliadas em relação a mensagens individuais.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="9c2c9-166">A [condição][lnk-query-expressions] da rota usa a mesma linguagem de consulta que o Hub IoT como condições em consultas gêmeas e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="9c2c9-167">Condições de rota são avaliadas no corpo e nos cabeçalhos de mensagem.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="9c2c9-168">A expressão de consulta de direcionamento pode envolver somente cabeçalhos de mensagens, apenas o corpo da mensagem ou os cabeçalhos e o corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="9c2c9-169">O Hub IoT pressupõe que haja um esquema específico para os cabeçalhos e o corpo da mensagem para direcionar mensagens. As seções a seguir descrevem o que é necessário para que o Hub IoT encaminhe corretamente:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="9c2c9-170">Encaminhamento em cabeçalhos de mensagens</span><span class="sxs-lookup"><span data-stu-id="9c2c9-170">Routing on message headers</span></span>

<span data-ttu-id="9c2c9-171">O Hub IoT pressupõe que haja a seguinte representação JSON dos cabeçalhos de mensagem para direcionamento de mensagens:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="9c2c9-172">As propriedades do sistema de mensagens são fixadas previamente com o símbolo `'$'`.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="9c2c9-173">As propriedades do usuário sempre serão acessadas com seu nome.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="9c2c9-174">Se um nome de propriedade de usuário coincidir com uma propriedade do sistema (como `$to`), a propriedade de usuário será recuperada com a expressão `$to`.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="9c2c9-175">Você sempre pode acessar a propriedade do sistema usando colchetes `{}`: por exemplo, é possível usar a expressão `{$to}` para acessar a propriedade de sistema `to`.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="9c2c9-176">Nomes de propriedade entre colchetes sempre recuperam a propriedade do sistema correspondente.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="9c2c9-177">Lembre-se que os nomes de propriedade não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="9c2c9-178">Todas as propriedades de mensagem são cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-178">All message properties are strings.</span></span> <span data-ttu-id="9c2c9-179">As propriedades do sistema, conforme descrito no [guia do desenvolvedor][lnk-devguide-messaging-format], não estão disponíveis para serem usadas em consultas no momento.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="9c2c9-180">Por exemplo, se você usar uma propriedade `messageType`, poderá querer rotear toda a telemetria para um ponto de extremidade e todos os alertas para outro.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="9c2c9-181">Você pode escrever a expressão a seguir para rotear a telemetria:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="9c2c9-182">E a expressão a seguir para rotear as mensagens de alerta:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="9c2c9-183">Também há suporte para expressões e funções boolianas.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="9c2c9-184">Esse recurso permite distinguir entre o nível de severidade, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="9c2c9-185">Consulte a seção [Expressão e condições][lnk-query-expressions] para ver a lista completa de funções e operadores com suporte.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="9c2c9-186">Encaminhamento em corpos de mensagem</span><span class="sxs-lookup"><span data-stu-id="9c2c9-186">Routing on message bodies</span></span>

<span data-ttu-id="9c2c9-187">O Hub IoT só poderá direcionar com base no conteúdo do corpo da mensagem se o corpo da mensagem estiver corretamente formado em JSON, codificado em UTF-8, UTF-16 ou UTF-32.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="9c2c9-188">Você deve definir o tipo de conteúdo da mensagem como `application/json` e a codificação do conteúdo como uma das codificações UTF com suporte nos cabeçalhos da mensagem para permitir que o Hub IoT direcione a mensagem com base no conteúdo do corpo.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="9c2c9-189">Se qualquer um dos cabeçalhos não for especificado, o Hub IoT não tentará avaliar qualquer expressão de consulta que envolva o corpo em relação à mensagem.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="9c2c9-190">Se a mensagem não for uma mensagem JSON ou se não especificar o tipo de conteúdo e a codificação de conteúdo, você ainda poderá usar o direcionamento de mensagens para direcionar a mensagem com base em cabeçalhos de mensagens.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="9c2c9-191">Você pode usar `$body` na expressão de consulta para direcionar a mensagem.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="9c2c9-192">Você pode usar uma referência de corpo simples, referência de matriz de corpo ou várias referências de corpo na expressão de consulta.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="9c2c9-193">A expressão de consulta também pode combinar uma referência de corpo a uma referência de cabeçalho de mensagem.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="9c2c9-194">Por exemplo, a seguir estão todas as expressões de consulta válidas:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="9c2c9-195">Noções básicas de uma consulta de Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9c2c9-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="9c2c9-196">Todas as consultas de Hub IoT são compostas por cláusulas SELECT e FROM cláusulas WHERE e GROUP BY opcionais.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="9c2c9-197">Cada consulta é executada em uma coleção de documentos JSON, por exemplo, dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="9c2c9-198">A cláusula FROM indica a coleção de documentos a ser iterada em (**devices** ou **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="9c2c9-199">Em seguida, o filtro na cláusula WHERE é aplicado.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="9c2c9-200">Nas agregações, os resultados desta etapa são agrupados como especificado na cláusula GROUP BY e, para cada grupo, uma linha é gerada conforme especificado na cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="9c2c9-201">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="9c2c9-201">FROM clause</span></span>
<span data-ttu-id="9c2c9-202">A cláusula **FROM <from_specification>** pode assumir somente dois valores: **FROM devices**, para consultar dispositivos gêmeos, ou **FROM devices.jobs**, para consultar os detalhes de trabalho por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="9c2c9-203">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="9c2c9-203">WHERE clause</span></span>
<span data-ttu-id="9c2c9-204">A cláusula **WHERE <filter_condition>** é opcional.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="9c2c9-205">Ela especifica uma ou mais condições que os documentos JSON na coleção FROM devem satisfazer para serem incluídos como parte dos resultados.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="9c2c9-206">Todos os documentos JSON devem avaliar as condições especificadas como “true” para ser incluídos no resultado.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="9c2c9-207">As condições permitidas são descritas na seção [Expressões e condições][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="9c2c9-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="9c2c9-208">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="9c2c9-208">SELECT clause</span></span>
<span data-ttu-id="9c2c9-209">A cláusula SELECT (**SELECT <select_list>**) é obrigatória e especifica quais valores são recuperados pela consulta.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="9c2c9-210">Ela especifica os valores JSON a serem usado para gerar novos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="9c2c9-211">Para cada elemento do subconjunto filtrado (e opcionalmente agrupado) da coleção FROM, a fase de projeção gera um novo objeto JSON, construído com os valores especificados na cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="9c2c9-212">Veja a seguir a gramática da cláusula SELECT:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-212">Following is the grammar of the SELECT clause:</span></span>

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

<span data-ttu-id="9c2c9-213">em que **attribute_name** refere-se a qualquer propriedade do documento JSON na coleção FROM.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="9c2c9-214">Alguns exemplos de cláusulas SELECT podem ser encontrados na seção [Introdução às consultas de dispositivo gêmeo][lnk-query-getstarted].</span><span class="sxs-lookup"><span data-stu-id="9c2c9-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="9c2c9-215">No momento, as cláusulas de seleção diferentes de **SELECT \*** têm suporte apenas em consultas de agregação em dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="9c2c9-216">Cláusula GROUP BY</span><span class="sxs-lookup"><span data-stu-id="9c2c9-216">GROUP BY clause</span></span>
<span data-ttu-id="9c2c9-217">A cláusula **GROUP BY <group_specification>** é uma etapa opcional que pode ser executada após o filtro especificado na cláusula WHERE e antes da projeção especificada em SELECT.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="9c2c9-218">Ela agrupa documentos com base no valor de um atributo.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="9c2c9-219">Esses grupos são usados para gerar valores agregados conforme especificado na cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="9c2c9-220">Um exemplo de uma consulta usando GROUP BY é:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="9c2c9-221">A sintaxe formal para GROUP BY é:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="9c2c9-222">em que **attribute_name** refere-se a qualquer propriedade do documento JSON na coleção FROM.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="9c2c9-223">No momento, a cláusula GROUP BY tem suporte apenas ao consultar dispositivos gêmeos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="9c2c9-224">Expressões e condições</span><span class="sxs-lookup"><span data-stu-id="9c2c9-224">Expressions and conditions</span></span>
<span data-ttu-id="9c2c9-225">Em um alto nível, uma *expressão*:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="9c2c9-226">Avalia para uma instância de um tipo JSON (por exemplo, booliano, número, cadeia de caracteres, matriz ou objeto) e</span><span class="sxs-lookup"><span data-stu-id="9c2c9-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="9c2c9-227">É definida pela manipulação de dados provenientes do documento JSON de dispositivo e constantes usando as funções e operadores internos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="9c2c9-228">*Condições* são expressões que retornam um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="9c2c9-229">Qualquer constante diferente de booliana **true** é considerada como **false** (incluindo **null**, **undefined**, qualquer instância de matriz ou objeto, qualquer cadeia de caracteres e claramente o booliano **false**).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="9c2c9-230">A sintaxe de expressões é:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-230">The syntax for expressions is:</span></span>

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

<span data-ttu-id="9c2c9-231">onde:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-231">where:</span></span>

| <span data-ttu-id="9c2c9-232">Símbolo</span><span class="sxs-lookup"><span data-stu-id="9c2c9-232">Symbol</span></span> | <span data-ttu-id="9c2c9-233">Definição</span><span class="sxs-lookup"><span data-stu-id="9c2c9-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="9c2c9-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="9c2c9-234">attribute_name</span></span> | <span data-ttu-id="9c2c9-235">Qualquer propriedade do documento JSON na coleção **FROM**.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="9c2c9-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="9c2c9-236">binary_operator</span></span> | <span data-ttu-id="9c2c9-237">Qualquer operador binário listado na seção [Operadores](#operators).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="9c2c9-238">function_name</span><span class="sxs-lookup"><span data-stu-id="9c2c9-238">function_name</span></span>| <span data-ttu-id="9c2c9-239">Qualquer função listada na seção [Funções](#functions).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="9c2c9-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="9c2c9-240">decimal_literal</span></span> |<span data-ttu-id="9c2c9-241">Um float expresso em notação decimal.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="9c2c9-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="9c2c9-242">hexadecimal_literal</span></span> |<span data-ttu-id="9c2c9-243">Um número expresso pela cadeia de caracteres '0x' seguida por uma cadeia de caracteres de dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="9c2c9-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="9c2c9-244">string_literal</span></span> |<span data-ttu-id="9c2c9-245">Literais de cadeia de caracteres são cadeias de caracteres Unicode representadas por uma sequência de zero ou mais caracteres Unicode ou sequências de escape.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="9c2c9-246">As literais de cadeia de caracteres são colocadas entre aspas simples (apóstrofe: ') ou aspas duplas (aspas: ").</span><span class="sxs-lookup"><span data-stu-id="9c2c9-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="9c2c9-247">Escapes permitidos: `\'`, `\"`, `\\`, `\uXXXX` para caracteres Unicode definidos por quatro dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="9c2c9-248">Operadores</span><span class="sxs-lookup"><span data-stu-id="9c2c9-248">Operators</span></span>
<span data-ttu-id="9c2c9-249">Há suporte para os seguintes operadores:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-249">The following operators are supported:</span></span>

| <span data-ttu-id="9c2c9-250">Família</span><span class="sxs-lookup"><span data-stu-id="9c2c9-250">Family</span></span> | <span data-ttu-id="9c2c9-251">Operadores</span><span class="sxs-lookup"><span data-stu-id="9c2c9-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="9c2c9-252">Aritmético</span><span class="sxs-lookup"><span data-stu-id="9c2c9-252">Arithmetic</span></span> |<span data-ttu-id="9c2c9-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="9c2c9-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="9c2c9-254">Lógico</span><span class="sxs-lookup"><span data-stu-id="9c2c9-254">Logical</span></span> |<span data-ttu-id="9c2c9-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="9c2c9-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="9c2c9-256">Comparação</span><span class="sxs-lookup"><span data-stu-id="9c2c9-256">Comparison</span></span> |<span data-ttu-id="9c2c9-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="9c2c9-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="9c2c9-258">Funções</span><span class="sxs-lookup"><span data-stu-id="9c2c9-258">Functions</span></span>
<span data-ttu-id="9c2c9-259">Ao consultar gêmeos e trabalhos, a única função com suporte é:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="9c2c9-260">Função</span><span class="sxs-lookup"><span data-stu-id="9c2c9-260">Function</span></span> | <span data-ttu-id="9c2c9-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="9c2c9-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c2c9-262">IS_DEFINED(propriedade)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="9c2c9-263">Retorna um valor booliano que indica se um valor foi atribuído à propriedade (incluindo `null`).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="9c2c9-264">Em condições de rotas, há suporte para as seguintes funções matemáticas:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="9c2c9-265">Função</span><span class="sxs-lookup"><span data-stu-id="9c2c9-265">Function</span></span> | <span data-ttu-id="9c2c9-266">Descrição</span><span class="sxs-lookup"><span data-stu-id="9c2c9-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c2c9-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-267">ABS(x)</span></span> | <span data-ttu-id="9c2c9-268">Retorna o valor absoluto (positivo) da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="9c2c9-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-269">EXP(x)</span></span> | <span data-ttu-id="9c2c9-270">Retorna o valor exponencial da expressão numérica especificada (e^x).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="9c2c9-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-271">POWER(x,y)</span></span> | <span data-ttu-id="9c2c9-272">Retorna o valor da expressão especificada para a potência indicada (x^y).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="9c2c9-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-273">SQUARE(x)</span></span> | <span data-ttu-id="9c2c9-274">Retorna o quadrado do valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="9c2c9-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-275">CEILING(x)</span></span> | <span data-ttu-id="9c2c9-276">Retorna o menor valor de número inteiro maior ou igual à expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="9c2c9-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-277">FLOOR(x)</span></span> | <span data-ttu-id="9c2c9-278">Retorna o maior inteiro menor ou igual à expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="9c2c9-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-279">SIGN(x)</span></span> | <span data-ttu-id="9c2c9-280">Retorna o sinal positivo (+1), zero (0) ou negativo (-1) da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="9c2c9-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-281">SQRT(x)</span></span> | <span data-ttu-id="9c2c9-282">Retorna o quadrado do valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="9c2c9-283">Em condições de rotas, há suporte para as seguintes funções de verificação de tipo e conversão de tipo:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="9c2c9-284">Função</span><span class="sxs-lookup"><span data-stu-id="9c2c9-284">Function</span></span> | <span data-ttu-id="9c2c9-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="9c2c9-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c2c9-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="9c2c9-286">AS_NUMBER</span></span> | <span data-ttu-id="9c2c9-287">Converte a cadeia de caracteres de entrada em um número.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-287">Converts the input string to a number.</span></span> <span data-ttu-id="9c2c9-288">`noop` se a entrada for um número; `Undefined` se a cadeia de caracteres não representar um número.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="9c2c9-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="9c2c9-289">IS_ARRAY</span></span> | <span data-ttu-id="9c2c9-290">Retorna um valor booliano que indica se o tipo da expressão especificada é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="9c2c9-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="9c2c9-291">IS_BOOL</span></span> | <span data-ttu-id="9c2c9-292">Retorna um valor booliano que indica se o tipo da expressão especificada é um booliano.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="9c2c9-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="9c2c9-293">IS_DEFINED</span></span> | <span data-ttu-id="9c2c9-294">Retorna um valor booliano que indica se um valor foi atribuído à propriedade.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="9c2c9-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="9c2c9-295">IS_NULL</span></span> | <span data-ttu-id="9c2c9-296">Retorna um valor booliano que indica se o tipo da expressão especificada é nulo.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="9c2c9-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="9c2c9-297">IS_NUMBER</span></span> | <span data-ttu-id="9c2c9-298">Retorna um valor booliano que indica se o tipo da expressão especificada é um número.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="9c2c9-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="9c2c9-299">IS_OBJECT</span></span> | <span data-ttu-id="9c2c9-300">Retorna um valor booliano que indica se o tipo da expressão especificada é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="9c2c9-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="9c2c9-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="9c2c9-302">Retorna um valor booliano que indica se o tipo da expressão especificada é um primitivo (cadeia de caracteres, booliano, numérico ou `null`).</span><span class="sxs-lookup"><span data-stu-id="9c2c9-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="9c2c9-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="9c2c9-303">IS_STRING</span></span> | <span data-ttu-id="9c2c9-304">Retorna um valor booliano que indica se o tipo da expressão especificada é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="9c2c9-305">Em condições de rotas, há suporte para as seguintes funções de cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="9c2c9-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="9c2c9-306">Função</span><span class="sxs-lookup"><span data-stu-id="9c2c9-306">Function</span></span> | <span data-ttu-id="9c2c9-307">Descrição</span><span class="sxs-lookup"><span data-stu-id="9c2c9-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9c2c9-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-308">CONCAT(x, …)</span></span> | <span data-ttu-id="9c2c9-309">Retorna uma cadeia de caracteres que é o resultado da concatenação de dois ou mais valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="9c2c9-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-310">LENGTH(x)</span></span> | <span data-ttu-id="9c2c9-311">Retorna o número de caracteres da expressão de cadeia de caracteres especificada.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="9c2c9-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-312">LOWER(x)</span></span> | <span data-ttu-id="9c2c9-313">Retorna uma expressão de cadeia de caracteres depois de converter dados de caracteres maiúsculos em minúsculos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="9c2c9-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-314">UPPER(x)</span></span> | <span data-ttu-id="9c2c9-315">Retorna uma expressão de cadeia de caracteres depois de converter dados de caracteres minúsculos em maiúsculos.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="9c2c9-316">SUBSTRING(cadeia de caracteres, início [, tamanho])</span><span class="sxs-lookup"><span data-stu-id="9c2c9-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="9c2c9-317">Retorna parte de uma expressão de cadeia de caracteres começando na posição baseada em zero do caractere especificado e continua até o comprimento especificado ou até o final da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="9c2c9-318">INDEX_OF (cadeia de caracteres, fragmento)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="9c2c9-319">Retorna a posição inicial da primeira ocorrência da segunda expressão de cadeia de caracteres dentro da primeira expressão de cadeia de caracteres especificada, ou -1 se a cadeia de caracteres não for encontrada.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="9c2c9-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="9c2c9-321">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres começa com a segunda.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="9c2c9-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="9c2c9-323">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres termina com a segunda.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="9c2c9-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="9c2c9-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="9c2c9-325">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres contém a segunda.</span><span class="sxs-lookup"><span data-stu-id="9c2c9-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c2c9-326">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c2c9-326">Next steps</span></span>
<span data-ttu-id="9c2c9-327">Saiba como executar consultas em seus aplicativos usando [SDKs do IoT do Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="9c2c9-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
