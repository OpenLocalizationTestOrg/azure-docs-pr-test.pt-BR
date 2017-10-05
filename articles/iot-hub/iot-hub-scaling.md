---
title: Dimensionamento do Hub IoT do Azure | Microsoft Docs
description: "Como dimensionar o Hub IoT para dar suporte à taxa de transferência de mensagens esperada. Inclui um resumo das taxas de transferência com suporte para cada camada e opções de fragmentação."
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
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="a976a-104">Escalar sua solução do hub IoT</span><span class="sxs-lookup"><span data-stu-id="a976a-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="a976a-105">O Hub do IoT do Azure pode oferecer suporte a até um milhão de dispositivos conectados ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a976a-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="a976a-106">Para saber mais, confira [Preço do Hub IoT][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="a976a-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="a976a-107">Cada unidade do Hub IoT permite uma determinada quantidade de mensagens diárias.</span><span class="sxs-lookup"><span data-stu-id="a976a-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="a976a-108">Para dimensionar corretamente sua solução, considere sua utilização específica do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a976a-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="a976a-109">Em particular, considere a taxa de transferência de pico necessária para as seguintes categorias de operações:</span><span class="sxs-lookup"><span data-stu-id="a976a-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="a976a-110">Mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="a976a-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="a976a-111">Mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="a976a-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="a976a-112">Operações de registro de identidade</span><span class="sxs-lookup"><span data-stu-id="a976a-112">Identity registry operations</span></span>

<span data-ttu-id="a976a-113">Além dessas informações sobre produtividade, confira as [Cotas e limites do Hub IoT][IoT Hub quotas and throttles] e crie sua solução segundo com tais informações.</span><span class="sxs-lookup"><span data-stu-id="a976a-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="a976a-114">Taxa de transferência de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="a976a-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="a976a-115">A melhor maneira de dimensionar uma solução do Hub IoT é avaliar o tráfego de acordo com a unidade.</span><span class="sxs-lookup"><span data-stu-id="a976a-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="a976a-116">As mensagens do dispositivo para a nuvem seguem estas diretrizes de taxa de transferência sustentada.</span><span class="sxs-lookup"><span data-stu-id="a976a-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="a976a-117">Camada</span><span class="sxs-lookup"><span data-stu-id="a976a-117">Tier</span></span> | <span data-ttu-id="a976a-118">Taxa de transferência sustentada</span><span class="sxs-lookup"><span data-stu-id="a976a-118">Sustained throughput</span></span> | <span data-ttu-id="a976a-119">Taxa de envio sustentada</span><span class="sxs-lookup"><span data-stu-id="a976a-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a976a-120">S1</span><span class="sxs-lookup"><span data-stu-id="a976a-120">S1</span></span> |<span data-ttu-id="a976a-121">Até 1111 KB/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="a976a-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="a976a-122">(1,5 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="a976a-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="a976a-123">Média de 278 mensagens/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="a976a-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="a976a-124">(400.000 mensagens/dia por unidade)</span><span class="sxs-lookup"><span data-stu-id="a976a-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="a976a-125">S2</span><span class="sxs-lookup"><span data-stu-id="a976a-125">S2</span></span> |<span data-ttu-id="a976a-126">Até 16 MB/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="a976a-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="a976a-127">(22,8 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="a976a-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="a976a-128">Média de 4.167 mensagens/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="a976a-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="a976a-129">(6 milhões de mensagens/dia por unidade)</span><span class="sxs-lookup"><span data-stu-id="a976a-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="a976a-130">S3</span><span class="sxs-lookup"><span data-stu-id="a976a-130">S3</span></span> |<span data-ttu-id="a976a-131">Até 814 MB/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="a976a-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="a976a-132">(1144,4 GB/dia/unidade)</span><span class="sxs-lookup"><span data-stu-id="a976a-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="a976a-133">Média de 208,333 mensagens/minuto por unidade</span><span class="sxs-lookup"><span data-stu-id="a976a-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="a976a-134">(300 milhões de mensagens/dia por unidade)</span><span class="sxs-lookup"><span data-stu-id="a976a-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="a976a-135">Taxa de transferência de operações de registro de identidade</span><span class="sxs-lookup"><span data-stu-id="a976a-135">Identity registry operation throughput</span></span>
<span data-ttu-id="a976a-136">As operações de Registro de identidade do Hub IoT não devem ser operações em tempo de execução, pois estão relacionadas principalmente com provisionamento do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a976a-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="a976a-137">Para ver número de pico de desempenho específicos, consulte [Cotas e limites do Hub IoT][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="a976a-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="a976a-138">Fragmentação</span><span class="sxs-lookup"><span data-stu-id="a976a-138">Sharding</span></span>
<span data-ttu-id="a976a-139">Enquanto um único Hub IoT pode ser dimensionado para milhões de dispositivos, às vezes sua solução exigirá características específicas de desempenho que um único Hub IoT não pode garantir.</span><span class="sxs-lookup"><span data-stu-id="a976a-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="a976a-140">Nesse caso, é recomendável que você particione seus dispositivos em vários Hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="a976a-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="a976a-141">Vários hubs IoT suavizam picos de tráfego e obtêm a taxa de transferência ou as taxas de operação necessárias.</span><span class="sxs-lookup"><span data-stu-id="a976a-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a976a-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a976a-142">Next steps</span></span>
<span data-ttu-id="a976a-143">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="a976a-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a976a-144">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a976a-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="a976a-145">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a976a-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
