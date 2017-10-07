---
title: aaaUnderstand hello Azure IoT Hub interno ponto de extremidade | Microsoft Docs
description: "Guia do desenvolvedor - descreve como toouse Olá interno, mensagens de dispositivo para nuvem compatível com o evento Hub endpoint toread."
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
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="4fa9a-103">Ler mensagens de dispositivo para a nuvem de ponto de extremidade internos Olá</span><span class="sxs-lookup"><span data-stu-id="4fa9a-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="4fa9a-104">Por padrão, as mensagens são roteadas toohello internos voltados para o serviço endpoint (**mensagens de eventos**), que é compatível com [Hubs de eventos][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="4fa9a-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="4fa9a-105">Esse ponto de extremidade está exposta somente usando Olá [AMQP] [ lnk-amqp] protocolo na porta 5671.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="4fa9a-106">Um hub IoT expõe Olá seguintes propriedades tooenable toocontrol você Olá compatível com o evento Hub mensagens ponto de extremidade integrado **mensagens de eventos**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="4fa9a-107">Propriedade</span><span class="sxs-lookup"><span data-stu-id="4fa9a-107">Property</span></span>            | <span data-ttu-id="4fa9a-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="4fa9a-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="4fa9a-109">**Contagem de partição**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-109">**Partition count**</span></span> | <span data-ttu-id="4fa9a-110">Defina essa propriedade no número de saudação toodefine criação de [partições] [ lnk-event-hub-partitions] para inclusão de eventos de dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="4fa9a-111">**Período de retenção**</span><span class="sxs-lookup"><span data-stu-id="4fa9a-111">**Retention time**</span></span>  | <span data-ttu-id="4fa9a-112">Esta propriedade especifica por quanto tempo, em dias, as mensagens são retidas pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="4fa9a-113">saudação padrão é um dia, mas pode ser aumentada tooseven dias.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="4fa9a-114">IoT Hub também permite que você toomanage grupos de consumidores no hello internos dispositivo para nuvem receber o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="4fa9a-115">Por padrão, todas as mensagens que não coincidem explicitamente uma regra de roteamento de mensagem são gravadas toohello ponto de extremidade internos.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="4fa9a-116">Se você desabilitar esta rota de fallback, as mensagens que não corresponderão explicitamente a nenhuma regra de roteamento de mensagem são descartadas.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="4fa9a-117">Você pode modificar o tempo de retenção de saudação programaticamente por meio de saudação [APIs REST de provedor de recursos do IoT Hub][lnk-resource-provider-apis], ou usando Olá [portal do Azure] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="4fa9a-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="4fa9a-118">IoT Hub expõe Olá **mensagens de eventos** mensagens de dispositivo para nuvem saudação tooread recebidas pelo seu hub de serviços de ponto de extremidade interno para o back-end.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="4fa9a-119">Esse ponto de extremidade é um evento de Hub compatível, que permite que você toouse qualquer serviço de Hubs de eventos de Olá Olá mecanismos oferece suporte para leitura de mensagens.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="4fa9a-120">Leitura do ponto de extremidade internos Olá</span><span class="sxs-lookup"><span data-stu-id="4fa9a-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="4fa9a-121">Quando você usa Olá [SDK do barramento de serviço do Azure para .NET] [ lnk-servicebus-sdk] ou hello [Hubs de eventos - evento processador Host][lnk-eventprocessorhost], você pode usar qualquer conexão de IoT Hub cadeias de caracteres com as permissões corretas hello.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="4fa9a-122">Em seguida, use **mensagens de eventos** como nome do Hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="4fa9a-123">Quando você usa SDKs (ou integrações de produto) que não estiver ciente de IoT Hub, você deve recuperar um ponto de extremidade compatível com o evento Hub e um nome compatível com o evento Hub das configurações de Hub IoT Olá Olá [portal do Azure] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="4fa9a-124">Na folha de hub do IoT hello, clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="4fa9a-125">Em Olá **pontos de extremidade internos** seção, clique em **eventos**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="4fa9a-126">Olá, folha contém Olá valores a seguir: **ponto de extremidade de Hub de eventos-compatível com**, **nome compatível com o evento Hub**, **partições**, **detempoderetenção**, e **grupos de consumidores**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Configurações de dispositivo para a nuvem][img-eventhubcompatible]

<span data-ttu-id="4fa9a-128">Olá IoT Hub SDK requer Olá nome de ponto de extremidade de IoT Hub, que é **mensagens de eventos** conforme Olá **pontos de extremidade** folha.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="4fa9a-129">Se Olá SDK que você está usando requer um **Hostname** ou **Namespace** valor, remova o esquema de saudação da saudação **ponto de extremidade compatível com o evento Hub**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="4fa9a-130">Por exemplo, se o ponto de extremidade compatível com o evento Hub é **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, Olá **Hostname** seria  **Hub IOT ns-myiothub 1234.servicebus.windows.net**e hello **Namespace** seria **ns hub IOT-1234 myiothub**.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="4fa9a-131">Você pode usar qualquer política de acesso compartilhado que tenha Olá **ServiceConnect** toohello de tooconnect de permissões especificado de Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="4fa9a-132">Se você precisar toobuild uma cadeia de caracteres de conexão do Hub de eventos usando as informações anteriores Olá, use o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="4fa9a-133">Olá SDKs e integrações que você pode usar com pontos de extremidade compatível com o evento Hub IoT Hub expõe inclui os itens Olá Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fa9a-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="4fa9a-134">[Cliente Java dos Hubs de Eventos](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="4fa9a-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="4fa9a-135">[Spout do Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4fa9a-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="4fa9a-136">Você pode exibir uma saudação [spout origem](https://github.com/apache/storm/tree/master/external/storm-eventhubs) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="4fa9a-137">[Integração do Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="4fa9a-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fa9a-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fa9a-138">Next steps</span></span>

<span data-ttu-id="4fa9a-139">Para saber mais sobre pontos de extremidade do Hub IoT, confira [Pontos de extremidade do Hub IoT][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="4fa9a-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="4fa9a-140">Olá [começar] [ lnk-get-started] tutoriais mostram como mensagens de dispositivo para nuvem toosend de simulados dispositivos e leem mensagens de saudação do ponto de extremidade internos hello.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="4fa9a-141">Para obter mais detalhes, consulte Olá [mensagens de dispositivo para nuvem processo IoT Hub usando rotas] [ lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4fa9a-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="4fa9a-142">Se você quiser tooroute seu dispositivo para nuvem mensagens toocustom pontos de extremidade, consulte [usar rotas de mensagens e pontos de extremidade personalizados para mensagens de dispositivo para nuvem][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="4fa9a-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
