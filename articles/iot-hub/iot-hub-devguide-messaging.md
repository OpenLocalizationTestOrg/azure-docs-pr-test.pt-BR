---
title: mensagens de Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor – Mensagens do dispositivo para a nuvem e da nuvem para o dispositivo com o Hub IoT. Inclui informações sobre formatos de mensagem e protocolos de comunicação com suporte."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="21fb7-104">Mensagens de dispositivo para nuvem e nuvem para dispositivo com o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="21fb7-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="21fb7-105">Use IoT Hub mensagens toocommunicate com seus dispositivos por:</span><span class="sxs-lookup"><span data-stu-id="21fb7-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="21fb7-106">Enviar [dispositivo para nuvem] [ lnk-d2c] mensagens de sua solução de tooyour dispositivos back-end.</span><span class="sxs-lookup"><span data-stu-id="21fb7-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="21fb7-107">Enviar [nuvem para dispositivo] [ lnk-c2d] mensagens de volta a solução Olá terminar tooyour dispositivos.</span><span class="sxs-lookup"><span data-stu-id="21fb7-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="21fb7-108">Propriedades de núcleo da funcionalidade de mensagens de IoT Hub são confiabilidade hello e durabilidade de mensagens.</span><span class="sxs-lookup"><span data-stu-id="21fb7-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="21fb7-109">Essas propriedades permitem conectividade de toointermittent resiliência no lado do dispositivo de saudação e tooload picos em processamento no lado da nuvem de saudação de eventos.</span><span class="sxs-lookup"><span data-stu-id="21fb7-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="21fb7-110">O Hub IoT implementa *pelo menos uma vez* as garantias de entrega de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21fb7-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="21fb7-111">Para recursos de toohello uma introdução de IoT Hub, consulte os artigos de saudação [Azure e Internet das coisas] [ lnk-azure-iot] e [visão geral da saudação serviço Azure IoT Hub] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="21fb7-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="21fb7-112">Quando mensagens de Hub IoT toouse</span><span class="sxs-lookup"><span data-stu-id="21fb7-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="21fb7-113">Use mensagens de dispositivo para nuvem para enviar telemetria de série de tempo e alertas do seu aplicativo de dispositivo e de nuvem para dispositivo para o aplicativo de dispositivo tooyour notificações unidirecional.</span><span class="sxs-lookup"><span data-stu-id="21fb7-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="21fb7-114">Consulte também[orientação de comunicação do dispositivo para nuvem] [ lnk-d2c-guidance] se em dúvida entre usar mensagens de dispositivo para nuvem, propriedades relatadas ou carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="21fb7-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="21fb7-115">Consulte também[orientação de comunicação de nuvem para dispositivo] [ lnk-c2d-guidance] se em dúvida entre o uso diretos métodos, propriedades desejadas ou mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21fb7-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21fb7-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21fb7-116">Next steps</span></span>

* <span data-ttu-id="21fb7-117">Saiba mais sobre [mensagens de dispositivo para a nuvem][lnk-d2c] do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="21fb7-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="21fb7-118">Saiba mais sobre [mensagens da nuvem para dispositivos][lnk-c2d] do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="21fb7-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md