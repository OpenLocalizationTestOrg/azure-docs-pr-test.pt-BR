---
title: Entender as mensagens do Hub IoT do Azure| Microsoft Docs
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
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="e076e-104">Mensagens de dispositivo para nuvem e nuvem para dispositivo com o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="e076e-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="e076e-105">Use mensagens do Hub IoT para se comunicar com os dispositivos da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e076e-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="e076e-106">Enviando mensagens de [dispositivo para nuvem][lnk-d2c] de dispositivos para a solução de back-end.</span><span class="sxs-lookup"><span data-stu-id="e076e-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="e076e-107">Enviando mensagens de [nuvem para dispositivo][lnk-c2d] da solução de back-end para os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e076e-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="e076e-108">As propriedades básicas da funcionalidade de mensagens do Hub IoT são a confiabilidade e a durabilidade das mensagens.</span><span class="sxs-lookup"><span data-stu-id="e076e-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="e076e-109">Essas propriedades habilitam a adaptação à conectividade intermitente no lado do dispositivo e a picos de carga no processamento de eventos no lado da nuvem.</span><span class="sxs-lookup"><span data-stu-id="e076e-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="e076e-110">O Hub IoT implementa *pelo menos uma vez* as garantias de entrega de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e076e-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="e076e-111">Para obter uma introdução aos recursos de Hub IoT, confira os artigos [Azure e Internet das Coisas][lnk-azure-iot] e [Visão geral do serviço do Hub IoT do Azure][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="e076e-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="e076e-112">Quando usar mensagens do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="e076e-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="e076e-113">Use mensagens de dispositivo para nuvem a fim de enviar alertas e telemetria de série temporal de seu aplicativo de dispositivo e de nuvem para dispositivo no caso de notificações unidirecionais para o aplicativo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e076e-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="e076e-114">Veja as[diretrizes de comunicação do dispositivo para a nuvem][lnk-d2c-guidance] se está em dúvida entre o uso de mensagens do dispositivo para a nuvem, propriedades reportadas ou carregamento do arquivo.</span><span class="sxs-lookup"><span data-stu-id="e076e-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="e076e-115">Veja as [diretrizes de comunicação da nuvem para o dispositivo][lnk-c2d-guidance] se está em dúvida entre o uso de mensagens da nuvem para o dispositivo, propriedades desejadas ou métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="e076e-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e076e-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e076e-116">Next steps</span></span>

* <span data-ttu-id="e076e-117">Saiba mais sobre [mensagens de dispositivo para a nuvem][lnk-d2c] do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e076e-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="e076e-118">Saiba mais sobre [mensagens da nuvem para dispositivos][lnk-c2d] do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e076e-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md