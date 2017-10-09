---
title: pontos de extremidade personalizados do Azure IoT Hub aaaUnderstand | Microsoft Docs
description: Guia do desenvolvedor - usando roteamento regras tooroute pontos de extremidade de toocustom de mensagens de dispositivo para a nuvem.
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="04a8a-103">Usar rotas de mensagens e pontos de extremidade personalizados para mensagens de dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="04a8a-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="04a8a-104">IoT Hub permite tooroute [mensagens de dispositivo para nuvem] [ lnk-device-to-cloud] tooIoT Hub voltados para o serviço de pontos de extremidade com base nas propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="04a8a-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="04a8a-105">Mensagens de onde eles precisarem toogo sem Olá roteamento dê regras Olá toosend flexibilidade necessário para mensagens de tooprocess serviços adicionais ou código adicional toowrite.</span><span class="sxs-lookup"><span data-stu-id="04a8a-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="04a8a-106">Cada regra de roteamento que você configurou tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="04a8a-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="04a8a-107">Propriedade</span><span class="sxs-lookup"><span data-stu-id="04a8a-107">Property</span></span>      | <span data-ttu-id="04a8a-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="04a8a-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="04a8a-109">**Nome**</span><span class="sxs-lookup"><span data-stu-id="04a8a-109">**Name**</span></span>      | <span data-ttu-id="04a8a-110">Olá nome exclusivo que identifica a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="04a8a-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="04a8a-111">**Fonte**</span><span class="sxs-lookup"><span data-stu-id="04a8a-111">**Source**</span></span>    | <span data-ttu-id="04a8a-112">origem de saudação do dados saudação fluxo toobe tratado.</span><span class="sxs-lookup"><span data-stu-id="04a8a-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="04a8a-113">Por exemplo, telemetria do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="04a8a-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="04a8a-114">**Condição**</span><span class="sxs-lookup"><span data-stu-id="04a8a-114">**Condition**</span></span> | <span data-ttu-id="04a8a-115">expressão de consulta Olá para regra de roteamento de saudação que é executada em cabeçalhos e corpo de mensagem de saudação e usados toodetermine seja uma correspondência para o ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="04a8a-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="04a8a-116">Para obter mais informações sobre como construir uma condição de rota, consulte Olá [referência - linguagem de consulta para trabalhos e twins dispositivo][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="04a8a-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="04a8a-117">**Ponto de extremidade**</span><span class="sxs-lookup"><span data-stu-id="04a8a-117">**Endpoint**</span></span>  | <span data-ttu-id="04a8a-118">nome de saudação do ponto de extremidade Olá onde o IoT Hub envia mensagens que correspondem à condição de saudação.</span><span class="sxs-lookup"><span data-stu-id="04a8a-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="04a8a-119">Pontos de extremidade devem estar no hello mesma região que o hub IoT de hello, caso contrário, você pode ser cobrado para grava entre regiões.</span><span class="sxs-lookup"><span data-stu-id="04a8a-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="04a8a-120">Uma única mensagem pode coincidir com a condição de saudação em várias regras de roteamento, caso o IoT Hub oferece Olá mensagem toohello ponto de extremidade associado a cada regra correspondente.</span><span class="sxs-lookup"><span data-stu-id="04a8a-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="04a8a-121">IoT Hub automaticamente também elimina a duplicação de entrega de mensagens, para se corresponder a uma mensagem de várias regras que tenham Olá mesmo destino, ela é apenas gravada toothat destino uma vez.</span><span class="sxs-lookup"><span data-stu-id="04a8a-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="04a8a-122">Um hub IoT tem um [ponto de extremidade interno][lnk-built-in] padrão.</span><span class="sxs-lookup"><span data-stu-id="04a8a-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="04a8a-123">Você pode criar pontos de extremidade personalizados tooroute mensagens tooby vinculação outros serviços em seu hub de toohello de assinatura.</span><span class="sxs-lookup"><span data-stu-id="04a8a-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="04a8a-124">O Hub IoT atualmente dá suporte aos Hubs de Eventos, filas do Barramento de Serviço e tópicos do Barramento de Serviço como pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="04a8a-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="04a8a-125">As filas e os tópicos do Barramento de Serviço com **Sessões** ou **Detecção de Duplicidades** habilitadas não têm suporte como pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="04a8a-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="04a8a-126">Para obter mais informações sobre a criação de pontos de extremidade personalizados no Hub IoT, consulte [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="04a8a-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="04a8a-127">Para saber mais sobre a leitura de pontos de extremidade personalizados, confira:</span><span class="sxs-lookup"><span data-stu-id="04a8a-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="04a8a-128">Leitura de [Hubs de Eventos][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="04a8a-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="04a8a-129">Leitura de [filas do Barramento de Serviço][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="04a8a-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="04a8a-130">Leitura de [tópicos do Barramento de Serviço][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="04a8a-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="04a8a-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04a8a-131">Next steps</span></span>

<span data-ttu-id="04a8a-132">Para saber mais sobre pontos de extremidade do Hub IoT, confira [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="04a8a-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="04a8a-133">Para obter mais informações sobre a linguagem de consulta Olá você pode usar regras de roteamento de toodefine, consulte [linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="04a8a-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="04a8a-134">Olá [mensagens de dispositivo para nuvem processo IoT Hub usando rotas] [ lnk-d2c-tutorial] tutorial mostra como regras de roteamento de toouse e pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="04a8a-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
