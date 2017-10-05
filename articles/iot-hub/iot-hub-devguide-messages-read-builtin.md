---
title: Entenda o ponto de extremidade interno Azure Hub IoT | Microsoft Docs
description: "Guia do desenvolvedor - descreve como usar o ponto de extremidade compatível com evento interno Hub para ler mensagens de dispositivo para nuvem."
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="3b619-103">Ler mensagens de dispositivo para a nuvem do ponto de extremidade interno</span><span class="sxs-lookup"><span data-stu-id="3b619-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="3b619-104">Por padrão, as mensagens são roteadas para o ponto de extremidade voltado para o serviço interno (**mensagens/eventos**) compatíveis com [Hubs de Eventos][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="3b619-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="3b619-105">Esse ponto de extremidade é atualmente apenas exposto usando o protocolo [AMQP][lnk-amqp] na porta 5671.</span><span class="sxs-lookup"><span data-stu-id="3b619-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="3b619-106">Um Hub IoT expõe as propriedades a seguir para permitir que você controle as **mensagens/eventos** do ponto de extremidade do sistema de mensagens interno compatível com o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3b619-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="3b619-107">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3b619-107">Property</span></span>            | <span data-ttu-id="3b619-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="3b619-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="3b619-109">**Contagem de partição**</span><span class="sxs-lookup"><span data-stu-id="3b619-109">**Partition count**</span></span> | <span data-ttu-id="3b619-110">Defina essa propriedade no momento da criação e define o número de [partições][lnk-event-hub-partitions] para inclusão do evento do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="3b619-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="3b619-111">**Período de retenção**</span><span class="sxs-lookup"><span data-stu-id="3b619-111">**Retention time**</span></span>  | <span data-ttu-id="3b619-112">Esta propriedade especifica por quanto tempo, em dias, as mensagens são retidas pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3b619-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="3b619-113">O padrão é de um dia, mas pode ser aumentado para sete dias.</span><span class="sxs-lookup"><span data-stu-id="3b619-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="3b619-114">O Hub IoT também permite que você gerencie grupos de consumidores no ponto de extremidade de recebimento do dispositivo para a nuvem interno.</span><span class="sxs-lookup"><span data-stu-id="3b619-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="3b619-115">Por padrão, todas as mensagens que não correspondem explicitamente a uma regra de roteamento de mensagem são gravadas no ponto de extremidade interno.</span><span class="sxs-lookup"><span data-stu-id="3b619-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="3b619-116">Se você desabilitar esta rota de fallback, as mensagens que não corresponderão explicitamente a nenhuma regra de roteamento de mensagem são descartadas.</span><span class="sxs-lookup"><span data-stu-id="3b619-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="3b619-117">Você pode modificar o tempo de retenção, seja de maneira programática por meio das [APIs REST do provedor de recursos do Hub IoT][lnk-resource-provider-apis] ou usando o [portal do Azure][lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="3b619-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="3b619-118">O Hub IoT expõe um ponto de extremidade interno de **mensagens/eventos** para os serviços de back-end lerem as mensagens de dispositivo para nuvem recebidas por seu hub.</span><span class="sxs-lookup"><span data-stu-id="3b619-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="3b619-119">Este ponto de extremidade é compatível com o Hub de Eventos, o que permite que você use qualquer um dos mecanismos para os quais o serviço Hubs de Eventos dá suporte para ler as mensagens.</span><span class="sxs-lookup"><span data-stu-id="3b619-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="3b619-120">Leitura do ponto de extremidade interno</span><span class="sxs-lookup"><span data-stu-id="3b619-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="3b619-121">Ao usar o [SDK do Barramento de Serviço do Azure para .NET][lnk-servicebus-sdk] ou [Hubs de Eventos – Host Processador de Evento][lnk-eventprocessorhost], você pode usar qualquer cadeia de conexão do Hub IoT com as permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="3b619-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="3b619-122">Em seguida, use **mensagens/eventos** como o nome do Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3b619-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="3b619-123">Ao usar os SDKs (ou integrações de produtos) que não reconhecem o Hub IoT, será necessário recuperar um ponto de extremidade compatível com os Hubs de Eventos e o nome do Hub de Eventos das configurações do Hub IoT no [Portal do Azure][lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="3b619-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="3b619-124">Na folha de Hub IoT, clique em **Pontos de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="3b619-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="3b619-125">Na seção **Pontos de extremidade internos**, clique em **Eventos**.</span><span class="sxs-lookup"><span data-stu-id="3b619-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="3b619-126">A folha contém os seguintes valores: **Ponto de extremidade compatível com o Hub de Eventos**, **Nome compatível com o Hub de Eventos**, **Partições**, **Ponto de retenção** e **Grupos de consumidores**.</span><span class="sxs-lookup"><span data-stu-id="3b619-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Configurações de dispositivo para a nuvem][img-eventhubcompatible]

<span data-ttu-id="3b619-128">O SDK do Hub IoT requer o nome de ponto de extremidade do Hub IoT, que é **mensagens/eventos** conforme mostrado na folha **Pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="3b619-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="3b619-129">Se o SDK sendo usado exigir um valor de **Nome do host** ou **Namespace**, remova o esquema do **Ponto de extremidade compatível com o Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="3b619-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="3b619-130">Por exemplo, se o ponto de extremidade compatível com o Hub de Eventos fosse **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, o **Nome do host** seria **iothub-ns-myiothub-1234.servicebus.windows.net** e o **Namespace** seria **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="3b619-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="3b619-131">Dessa forma, você poderá usar qualquer política de acesso compartilhado com permissões **ServiceConnect** para se conectar ao Hub de Eventos especificado.</span><span class="sxs-lookup"><span data-stu-id="3b619-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="3b619-132">Caso você precise criar uma cadeia de conexão do Hub de Eventos usando as informações anteriores, use o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="3b619-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="3b619-133">Os SDKs e integrações que você pode usar com os pontos de extremidade compatíveis com o Hub de Eventos expostos pelo Hub IoT incluem os itens a seguir na lista:</span><span class="sxs-lookup"><span data-stu-id="3b619-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="3b619-134">[Cliente Java dos Hubs de Eventos](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="3b619-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="3b619-135">[Spout do Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3b619-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="3b619-136">Você pode exibir a [fonte do spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="3b619-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="3b619-137">[Integração do Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="3b619-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b619-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b619-138">Next steps</span></span>

<span data-ttu-id="3b619-139">Para obter mais informações sobre pontos de extremidade do Hub IoT, consulte [Pontos de extremidade do Hub IoT][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="3b619-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="3b619-140">Os tutoriais [Comece][lnk-get-started] mostram como enviar mensagens de dispositivo para nuvem de dispositivos simulados e ler as mensagens do ponto de extremidade interno.</span><span class="sxs-lookup"><span data-stu-id="3b619-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="3b619-141">Para obter mais informações, confira o tutorial [Como processar as mensagens entre o dispositivo e a nuvem do Hub IoT usando rotas][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="3b619-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="3b619-142">Se você quiser encaminhar as mensagens de dispositivo para nuvem para pontos de extremidade personalizados, consulte [Usar rotas de mensagens e pontos de extremidade personalizados para mensagens de dispositivo para nuvem][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="3b619-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
