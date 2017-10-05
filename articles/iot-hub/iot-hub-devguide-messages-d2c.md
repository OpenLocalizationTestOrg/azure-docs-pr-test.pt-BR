---
title: Compreender mensagens de dispositivo para a nuvem do Hub IoT do Azure | Microsoft Docs
description: "Guia do desenvolvedor – como usar mensagens de dispositivo para a nuvem com o Hub IoT. Inclui informações sobre o envio de dados de telemetria e não telemetria e o uso do direcionamento para entregar mensagens."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="11d66-104">Enviar mensagens de dispositivo para a nuvem para o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="11d66-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="11d66-105">Para enviar telemetria de série temporal e alertas de dispositivos ao back-end da solução, envie mensagens de dispositivo para a nuvem do dispositivo para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11d66-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="11d66-106">Para ver uma discussão sobre outras opções de dispositivo para a nuvem com suporte no Hub IoT, confira [Orientação sobre comunicações de dispositivo para a nuvem][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="11d66-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="11d66-107">Você envia mensagens do dispositivo para a nuvem por meio de um ponto de extremidade voltado para o dispositivo (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="11d66-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="11d66-108">As regras de roteamento roteiam as mensagens para um dos pontos de extremidade voltados para o serviço em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11d66-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="11d66-109">As regras de roteamento usam os cabeçalhos e o corpo das mensagens de dispositivo para a nuvem que fluem através de seu hub para determinar para onde roteá-las.</span><span class="sxs-lookup"><span data-stu-id="11d66-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="11d66-110">Por padrão, as mensagens são roteadas para o ponto de extremidade voltado para o serviço interno (**mensagens/eventos**) compatíveis com [Hubs de Eventos][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="11d66-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="11d66-111">Portanto, você pode usar os [SDKs e integração com Hubs de Evento][lnk-compatible-endpoint] Standard para receber mensagens de dispositivo para a nuvem no back-end da solução.</span><span class="sxs-lookup"><span data-stu-id="11d66-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="11d66-112">O Hub IoT implementa mensagens de dispositivo para nuvem usando um padrão de sistema de mensagens de streaming.</span><span class="sxs-lookup"><span data-stu-id="11d66-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="11d66-113">As mensagens do dispositivo para nuvem do Hub IoT são mais semelhantes a *eventos* de [Hubs de Eventos][lnk-event-hubs] do que a *mensagens* do [Barramento de Serviço][lnk-servicebus] na medida em que há um alto volume de eventos passando pelo serviço que pode ser lido por vários leitores.</span><span class="sxs-lookup"><span data-stu-id="11d66-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="11d66-114">As mensagens de dispositivo para a nuvem com o Hub IoT têm as seguintes características:</span><span class="sxs-lookup"><span data-stu-id="11d66-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="11d66-115">As mensagens do dispositivo para a nuvem são duráveis e mantidas em um ponto de extremidade de **mensagens/eventos** padrão do Hub IoT por até sete dias.</span><span class="sxs-lookup"><span data-stu-id="11d66-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="11d66-116">As mensagens de dispositivo para a nuvem podem ter no máximo 256 KB e podem ser agrupadas em lotes para otimizar os envios.</span><span class="sxs-lookup"><span data-stu-id="11d66-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="11d66-117">Os lotes podem ter no máximo 256 KB.</span><span class="sxs-lookup"><span data-stu-id="11d66-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="11d66-118">Como explicado na seção [Controlar o acesso ao Hub IoT][lnk-devguide-security], o Hub IoT habilita a autenticação e o controle de acesso por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11d66-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="11d66-119">O Hub IoT permite que você crie até 10 pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="11d66-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="11d66-120">As mensagens são entregues aos pontos de extremidade com base nas rotas configuradas em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11d66-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="11d66-121">Para saber mais, confira [Regras de direcionamento](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="11d66-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="11d66-122">O Hub IoT habilita milhões de dispositivos conectados simultaneamente (confira [Cotas e limitação][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="11d66-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="11d66-123">O Hub IoT não permite o particionamento arbitrário.</span><span class="sxs-lookup"><span data-stu-id="11d66-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="11d66-124">As mensagens do dispositivo para a nuvem são particionadas com base em sua **deviceId**de origem.</span><span class="sxs-lookup"><span data-stu-id="11d66-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="11d66-125">Para saber mais sobre as diferenças entre os serviços de Hubs de Eventos e o Hub IoT, confira [Comparação do Hub IoT do Azure e Hubs de Eventos do Azure][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="11d66-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="11d66-126">Enviar tráfego sem telemetria</span><span class="sxs-lookup"><span data-stu-id="11d66-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="11d66-127">Muitas vezes, além dos pontos de dados de telemetria, os dispositivos enviam mensagens e solicitações que exigem execução separada e manipulação no back-end de solução.</span><span class="sxs-lookup"><span data-stu-id="11d66-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="11d66-128">Por exemplo, alertas críticos que devem disparar uma ação específica no back-end.</span><span class="sxs-lookup"><span data-stu-id="11d66-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="11d66-129">Você pode escrever facilmente uma [regra de direcionamento][lnk-devguide-custom] para enviar esses tipos de mensagens a um ponto de extremidade dedicado ao respectivo processamento, com base em um cabeçalho da mensagem ou um valor no corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="11d66-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="11d66-130">Para obter mais informações sobre a melhor maneira de processar esse tipo de mensagem, consulte o [Tutorial: como processar mensagens do dispositivo para a nuvem do Hub IoT][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="11d66-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="11d66-131">Encaminhar mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="11d66-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="11d66-132">Você tem duas opções para direcionamento de mensagens de dispositivo para a nuvem para os aplicativos de back-end:</span><span class="sxs-lookup"><span data-stu-id="11d66-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="11d66-133">Use o [ponto de extremidade compatível com o Hub de Eventos][lnk-compatible-endpoint] interno para habilitar os aplicativos de back-end para ler as mensagens de dispositivo para a nuvem recebidas pelo hub.</span><span class="sxs-lookup"><span data-stu-id="11d66-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="11d66-134">Para saber mais sobre o ponto de extremidade compatível com o Hub de Eventos interno, confira [Ler mensagens de dispositivo para a nuvem do ponto de extremidade interno][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="11d66-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="11d66-135">Use regras de direcionamento para enviar mensagens a pontos de extremidade personalizados no hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11d66-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="11d66-136">Os pontos de extremidade personalizados permitem que os aplicativos de back-end a ler mensagens de dispositivo para a nuvem usando Hubs de Eventos, filas do Barramento de Serviço ou tópicos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="11d66-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="11d66-137">Para saber mais sobre pontos de extremidade personalizados e direcionamentos, confira [Usar pontos de extremidade personalizados e regras de direcionamento de mensagens de dispositivo para a nuvem][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="11d66-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="11d66-138">Propriedades antifalsificação</span><span class="sxs-lookup"><span data-stu-id="11d66-138">Anti-spoofing properties</span></span>

<span data-ttu-id="11d66-139">Para evitar a falsificação em mensagens do dispositivo para a nuvem, o Hub IoT carimba todas as mensagens com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="11d66-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="11d66-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="11d66-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="11d66-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="11d66-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="11d66-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="11d66-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="11d66-143">As duas primeiras contêm a **deviceId** e a **generationId** do dispositivo de origem, conforme as [Propriedades de identidade do dispositivo][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="11d66-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="11d66-144">A propriedade **ConnectionAuthMethod** contém um objeto JSON serializado com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="11d66-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="11d66-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11d66-145">Next steps</span></span>

<span data-ttu-id="11d66-146">Para saber mais sobre os SDKs que você pode usar para enviar mensagens de dispositivo para a nuvem, confira [SDKs do Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="11d66-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="11d66-147">Os tutoriais de [Introdução][lnk-get-started] mostram como enviar mensagens de dispositivo para a nuvem de dispositivos simulados e físicos.</span><span class="sxs-lookup"><span data-stu-id="11d66-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="11d66-148">Para saber mais, confira o tutorial [Como processar as mensagens entre o dispositivo e a nuvem do Hub IoT usando rotas][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="11d66-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
