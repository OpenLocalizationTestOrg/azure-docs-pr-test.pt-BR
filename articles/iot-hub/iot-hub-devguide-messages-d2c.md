---
title: mensagens de dispositivo para a nuvem de Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - como toouse dispositivo para a nuvem com o IoT Hub de mensagens. Inclui informações sobre o envio de dados de telemetria e não telemtry e usando o roteamento de mensagens toodeliver."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="878c1-104">Enviar mensagens de dispositivo para nuvem tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="878c1-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="878c1-105">Telemetria de série temporal toosend e alertas de seu dispositivos tooyour solução back-end, enviar mensagens de dispositivo para a nuvem de hub IoT de tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="878c1-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="878c1-106">Para ver uma discussão sobre outras opções de dispositivo para a nuvem com suporte no Hub IoT, confira [Orientação sobre comunicações de dispositivo para a nuvem][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="878c1-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="878c1-107">Você envia mensagens do dispositivo para a nuvem por meio de um ponto de extremidade voltado para o dispositivo (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="878c1-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="878c1-108">Regras de roteamento e rotear o tooone mensagens de pontos de extremidade de serviço voltados Olá em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="878c1-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="878c1-109">Regras de roteamento usam cabeçalhos de saudação e corpo de mensagens de saudação do dispositivo para a nuvem que passam por seu hub toodetermine onde tooroute-los.</span><span class="sxs-lookup"><span data-stu-id="878c1-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="878c1-110">Por padrão, as mensagens são roteadas toohello internos voltados para o serviço endpoint (**mensagens de eventos**), que é compatível com [Hubs de eventos][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="878c1-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="878c1-111">Portanto, você pode usar o padrão [integração com Hubs de evento e SDKs] [ lnk-compatible-endpoint] tooreceive mensagens de dispositivo para nuvem em sua solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="878c1-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="878c1-112">O Hub IoT implementa mensagens de dispositivo para nuvem usando um padrão de sistema de mensagens de streaming.</span><span class="sxs-lookup"><span data-stu-id="878c1-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="878c1-113">Mensagens de dispositivo para a nuvem do IoT Hub são mais [Hubs de eventos] [ lnk-event-hubs] *eventos* que [Service Bus] [ lnk-servicebus] *mensagens* que há um grande volume de eventos que passam pelo serviço de saudação que pode ser lido por vários leitores.</span><span class="sxs-lookup"><span data-stu-id="878c1-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="878c1-114">Mensagens com o IoT Hub dispositivo para nuvem tem Olá características a seguir:</span><span class="sxs-lookup"><span data-stu-id="878c1-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="878c1-115">Mensagens de dispositivo para nuvem são duráveis e mantidas no padrão de um hub IoT **mensagens de eventos** ponto de extremidade para o tooseven dias.</span><span class="sxs-lookup"><span data-stu-id="878c1-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="878c1-116">Mensagens de dispositivo para nuvem podem ter no máximo 256 KB e podem ser agrupadas em lotes toooptimize envia.</span><span class="sxs-lookup"><span data-stu-id="878c1-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="878c1-117">Os lotes podem ter no máximo 256 KB.</span><span class="sxs-lookup"><span data-stu-id="878c1-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="878c1-118">Conforme explicado em Olá [tooIoT de acesso de controle Hub] [ lnk-devguide-security] seção, o IoT Hub habilita o controle de acesso e autenticação por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="878c1-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="878c1-119">IoT Hub permite toocreate too10 pontos de extremidade personalizado.</span><span class="sxs-lookup"><span data-stu-id="878c1-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="878c1-120">As mensagens são entregues toohello pontos de extremidade com base nas rotas configuradas em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="878c1-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="878c1-121">Para saber mais, confira [Regras de direcionamento](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="878c1-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="878c1-122">O Hub IoT habilita milhões de dispositivos conectados simultaneamente (confira [Cotas e limitação][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="878c1-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="878c1-123">O Hub IoT não permite o particionamento arbitrário.</span><span class="sxs-lookup"><span data-stu-id="878c1-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="878c1-124">As mensagens do dispositivo para a nuvem são particionadas com base em sua **deviceId**de origem.</span><span class="sxs-lookup"><span data-stu-id="878c1-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="878c1-125">Para obter mais informações sobre as diferenças de saudação entre Olá IoT Hub e os serviços de Hubs de eventos, consulte [comparação de IoT Hub do Azure e Hubs de eventos do Azure][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="878c1-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="878c1-126">Enviar tráfego sem telemetria</span><span class="sxs-lookup"><span data-stu-id="878c1-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="878c1-127">Geralmente, os dispositivos além de pontos de dados de tootelemetry, enviam mensagens e solicitações que exigem tratamento no back-end de solução hello e execução separado.</span><span class="sxs-lookup"><span data-stu-id="878c1-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="878c1-128">Por exemplo, alertas críticos que devem disparar uma ação específica em Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="878c1-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="878c1-129">Você pode escrever facilmente um [regra de roteamento] [ lnk-devguide-custom] toosend esses tipos de ponto de extremidade de mensagens tooan dedicado tootheir processamento com base em qualquer um cabeçalho de mensagem de saudação ou um valor no corpo da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="878c1-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="878c1-130">Para obter mais informações sobre Olá melhor maneira tooprocess nesse tipo de mensagem, consulte Olá [Tutorial: como tooprocess mensagens de dispositivo para a nuvem de IoT Hub] [ lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="878c1-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="878c1-131">Encaminhar mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="878c1-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="878c1-132">Você tem duas opções para aplicativos de back-end do roteamento mensagens de dispositivo para nuvem tooyour:</span><span class="sxs-lookup"><span data-stu-id="878c1-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="878c1-133">Usar Olá interno [ponto de extremidade compatível com o evento Hub] [ lnk-compatible-endpoint] tooenable aplicativos de back-end tooread Olá dispositivo para nuvem as mensagens recebidas pelo hub hello.</span><span class="sxs-lookup"><span data-stu-id="878c1-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="878c1-134">toolearn sobre ponto de extremidade Olá de interno compatível Hub de eventos, consulte [ler mensagens de dispositivo para a nuvem de ponto de extremidade internos Olá][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="878c1-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="878c1-135">Use o roteamento regras toosend mensagens toocustom pontos de extremidade em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="878c1-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="878c1-136">Pontos de extremidade personalizados permitem que as mensagens de dispositivo para nuvem tooread aplicativos de back-end usando Hubs de eventos, filas de barramento de serviço ou tópicos do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="878c1-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="878c1-137">toolearn sobre pontos de extremidade personalizados e roteamentos, consulte [usar pontos de extremidade personalizados e regras de roteamento para mensagens de dispositivo para nuvem][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="878c1-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="878c1-138">Propriedades antifalsificação</span><span class="sxs-lookup"><span data-stu-id="878c1-138">Anti-spoofing properties</span></span>

<span data-ttu-id="878c1-139">dispositivo tooavoid falsificação em mensagens de dispositivo para nuvem, o IoT Hub carimbos todas as mensagens com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="878c1-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="878c1-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="878c1-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="878c1-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="878c1-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="878c1-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="878c1-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="878c1-143">Olá primeiro dois contêm Olá **deviceId** e **generationId** de saudação provenientes do dispositivo, como por [propriedades de identidade de dispositivo][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="878c1-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="878c1-144">Olá **ConnectionAuthMethod** propriedade contém um objeto JSON serializado, com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="878c1-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="878c1-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="878c1-145">Next steps</span></span>

<span data-ttu-id="878c1-146">Para obter informações sobre SDKs de saudação, você pode usar mensagens de dispositivo para nuvem toosend, consulte [SDKs do Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="878c1-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="878c1-147">Olá [começar] [ lnk-get-started] tutoriais mostram como dispositivo para nuvem toosend mensagens de dispositivos simulados e físicos.</span><span class="sxs-lookup"><span data-stu-id="878c1-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="878c1-148">Para obter mais detalhes, consulte Olá [mensagens de dispositivo para nuvem processo IoT Hub usando rotas] [ lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="878c1-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
