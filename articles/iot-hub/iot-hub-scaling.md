---
title: dimensionamento do Hub IoT de aaaAzure | Microsoft Docs
description: "Como tooscale o toosupport de hub IoT a taxa de transferência de mensagem esperado. Inclui um resumo das opções de fragmentação e taxa de transferência de saudação com suporte para cada camada."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="d2ad0-104">Escalar sua solução do hub IoT</span><span class="sxs-lookup"><span data-stu-id="d2ad0-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="d2ad0-105">IoT Hub do Azure pode dar suporte a dispositivos conectados simultaneamente milhões de tooa.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="d2ad0-106">Para saber mais, confira [Preço do Hub IoT][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="d2ad0-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="d2ad0-107">Cada unidade do Hub IoT permite uma determinada quantidade de mensagens diárias.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="d2ad0-108">tooproperly dimensionar sua solução, considere o uso do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="d2ad0-109">Em particular, considere a possibilidade de taxa de transferência de pico de saudação necessária para Olá categorias de operações a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="d2ad0-110">Mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="d2ad0-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="d2ad0-111">Mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="d2ad0-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="d2ad0-112">Operações de registro de identidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-112">Identity registry operations</span></span>

<span data-ttu-id="d2ad0-113">Informações de taxa de transferência de toothis adição, consulte [cotas de IoT Hub e limitadores] [ IoT Hub quotas and throttles] e projetar sua solução adequadamente.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="d2ad0-114">Taxa de transferência de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="d2ad0-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="d2ad0-115">saudação de melhor forma toosize uma solução de IoT Hub é o tráfego de saudação tooevaluate em uma base por unidade.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="d2ad0-116">As mensagens do dispositivo para a nuvem seguem estas diretrizes de taxa de transferência sustentada.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="d2ad0-117">Camada</span><span class="sxs-lookup"><span data-stu-id="d2ad0-117">Tier</span></span> | <span data-ttu-id="d2ad0-118">Taxa de transferência sustentada</span><span class="sxs-lookup"><span data-stu-id="d2ad0-118">Sustained throughput</span></span> | <span data-ttu-id="d2ad0-119">Taxa de envio sustentada</span><span class="sxs-lookup"><span data-stu-id="d2ad0-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d2ad0-120">S1</span><span class="sxs-lookup"><span data-stu-id="d2ad0-120">S1</span></span> |<span data-ttu-id="d2ad0-121">Backup too1111 KB por minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="d2ad0-122">(1,5 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="d2ad0-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="d2ad0-123">Média de 278 mensagens/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="d2ad0-124">(400.000 mensagens/dia por unidade)</span><span class="sxs-lookup"><span data-stu-id="d2ad0-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="d2ad0-125">S2</span><span class="sxs-lookup"><span data-stu-id="d2ad0-125">S2</span></span> |<span data-ttu-id="d2ad0-126">Backup too16 MB por minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="d2ad0-127">(22,8 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="d2ad0-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="d2ad0-128">Média de 4.167 mensagens/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="d2ad0-129">(6 milhões de mensagens/dia por unidade)</span><span class="sxs-lookup"><span data-stu-id="d2ad0-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="d2ad0-130">S3</span><span class="sxs-lookup"><span data-stu-id="d2ad0-130">S3</span></span> |<span data-ttu-id="d2ad0-131">Backup too814 MB por minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="d2ad0-132">(1144,4 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="d2ad0-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="d2ad0-133">Média de 208,333 mensagens/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="d2ad0-134">(300 milhões de mensagens/dia por unidade)</span><span class="sxs-lookup"><span data-stu-id="d2ad0-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="d2ad0-135">Taxa de transferência de operações de registro de identidade</span><span class="sxs-lookup"><span data-stu-id="d2ad0-135">Identity registry operation throughput</span></span>
<span data-ttu-id="d2ad0-136">Operações de registro de identidade de IoT Hub não devem toobe operações de tempo de execução, como eles são principalmente provisionamento toodevice relacionado.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="d2ad0-137">Para ver número de pico de desempenho específicos, consulte [Cotas e limites do Hub IoT][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="d2ad0-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="d2ad0-138">Fragmentação</span><span class="sxs-lookup"><span data-stu-id="d2ad0-138">Sharding</span></span>
<span data-ttu-id="d2ad0-139">Enquanto um único hub IoT pode dimensionar toomillions de dispositivos, às vezes, sua solução requer características específicas de desempenho que um único hub IoT não pode garantir.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="d2ad0-140">Nesse caso, é recomendável que você particione seus dispositivos em vários Hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="d2ad0-141">Vários hubs IoT smooth picos de tráfego e obter a taxa de transferência necessária hello ou taxas de operação são necessárias.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2ad0-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2ad0-142">Next steps</span></span>
<span data-ttu-id="d2ad0-143">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d2ad0-144">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d2ad0-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d2ad0-145">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d2ad0-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
