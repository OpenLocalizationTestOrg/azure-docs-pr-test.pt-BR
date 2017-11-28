---
title: Compreender os pontos de extremidade personalizados do Hub IoT do Azure | Microsoft Docs
description: "Guia do desenvolvedor – regras de direcionamento para direcionar mensagens de dispositivo para a nuvem para pontos de extremidade personalizados."
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
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="c1e59-103">Usar rotas de mensagens e pontos de extremidade personalizados para mensagens de dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="c1e59-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="c1e59-104">O Hub IoT habilita o direcionamento de [mensagens de dispositivo para a nuvem][lnk-device-to-cloud] para pontos de extremidade voltados para o serviço do Hub IoT com base nas propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="c1e59-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="c1e59-105">As regras de roteamento oferecem a flexibilidade para enviar mensagens para onde elas precisam ir sem a necessidade de serviços adicionais para processar mensagens ou escrever código adicional.</span><span class="sxs-lookup"><span data-stu-id="c1e59-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="c1e59-106">Cada regra de roteamento que você configurar tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c1e59-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="c1e59-107">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c1e59-107">Property</span></span>      | <span data-ttu-id="c1e59-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e59-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="c1e59-109">**Nome**</span><span class="sxs-lookup"><span data-stu-id="c1e59-109">**Name**</span></span>      | <span data-ttu-id="c1e59-110">O nome exclusivo que identifica a regra.</span><span class="sxs-lookup"><span data-stu-id="c1e59-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="c1e59-111">**Fonte**</span><span class="sxs-lookup"><span data-stu-id="c1e59-111">**Source**</span></span>    | <span data-ttu-id="c1e59-112">A origem do fluxo de dados a ser afetado.</span><span class="sxs-lookup"><span data-stu-id="c1e59-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="c1e59-113">Por exemplo, telemetria do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c1e59-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="c1e59-114">**Condição**</span><span class="sxs-lookup"><span data-stu-id="c1e59-114">**Condition**</span></span> | <span data-ttu-id="c1e59-115">A expressão de consulta para a regra de roteamento que é executada em relação ao cabeçalho e ao corpo da mensagem e usada para determinar se ela é uma correspondência para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="c1e59-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="c1e59-116">Para obter mais informações sobre como construir uma condição de rota, consulte o [Referência – linguagem de consulta para dispositivos gêmeos e trabalhos][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="c1e59-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="c1e59-117">**Ponto de extremidade**</span><span class="sxs-lookup"><span data-stu-id="c1e59-117">**Endpoint**</span></span>  | <span data-ttu-id="c1e59-118">O nome do ponto de extremidade em que Hub IoT envia as mensagens que correspondem à condição.</span><span class="sxs-lookup"><span data-stu-id="c1e59-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="c1e59-119">Os pontos de extremidade devem estar na mesma região que o Hub IoT, caso contrário, você pode ser cobrado por gravações entre regiões.</span><span class="sxs-lookup"><span data-stu-id="c1e59-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="c1e59-120">Uma única mensagem pode corresponder à condição em várias regras de roteamentos, caso em que o Hub IoT entrega a mensagem para o ponto de extremidade associado a cada regra correspondente.</span><span class="sxs-lookup"><span data-stu-id="c1e59-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="c1e59-121">O Hub IoT também elimina a duplicação da entrega de mensagem automaticamente, portanto, se uma mensagem corresponder a várias regras que têm o mesmo destino, ela será gravada apenas uma vez no destino.</span><span class="sxs-lookup"><span data-stu-id="c1e59-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="c1e59-122">Um hub IoT tem um [ponto de extremidade interno][lnk-built-in] padrão.</span><span class="sxs-lookup"><span data-stu-id="c1e59-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="c1e59-123">Você pode criar pontos de extremidade personalizados para direcionar mensagens ou vinculando outros serviços em sua assinatura ao hub.</span><span class="sxs-lookup"><span data-stu-id="c1e59-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="c1e59-124">O Hub IoT atualmente dá suporte aos Hubs de Eventos, filas do Barramento de Serviço e tópicos do Barramento de Serviço como pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="c1e59-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="c1e59-125">As filas e os tópicos do Barramento de Serviço com **Sessões** ou **Detecção de Duplicidades** habilitadas não têm suporte como pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="c1e59-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="c1e59-126">Para obter mais informações sobre a criação de pontos de extremidade personalizados no Hub IoT, consulte [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="c1e59-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="c1e59-127">Para saber mais sobre a leitura de pontos de extremidade personalizados, confira:</span><span class="sxs-lookup"><span data-stu-id="c1e59-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="c1e59-128">Leitura de [Hubs de Eventos][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="c1e59-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="c1e59-129">Leitura de [filas do Barramento de Serviço][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="c1e59-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="c1e59-130">Leitura de [tópicos do Barramento de Serviço][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="c1e59-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="c1e59-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1e59-131">Next steps</span></span>

<span data-ttu-id="c1e59-132">Para saber mais sobre pontos de extremidade do Hub IoT, confira [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="c1e59-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="c1e59-133">Para saber mais sobre a linguagem de consulta que você usa para definir regras de direcionamento, confira [Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e direcionamento de mensagens][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="c1e59-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="c1e59-134">O tutorial [Processar mensagens de dispositivo para a nuvem do Hub IoT usando rotas][lnk-d2c-tutorial] mostra como usar regras de direcionamento e pontos de extremidade personalizados.</span><span class="sxs-lookup"><span data-stu-id="c1e59-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
