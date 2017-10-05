---
title: "Visão geral do Azure IoT Edge | Microsoft Docs"
description: "Descreve os principais conceitos da arquitetura no Azure IoT Edge, como agentes, módulos e gateways."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="58144-103">Conceitos de arquitetura do Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="58144-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="58144-104">Antes de examinar algum código de exemplo ou criar seu próprio gateway de campo usando o IoT Edge, é necessário entender os principais conceitos nos quais se baseia arquitetura do SDK.</span><span class="sxs-lookup"><span data-stu-id="58144-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="58144-105">Módulos do IoT Edge</span><span class="sxs-lookup"><span data-stu-id="58144-105">IoT Edge modules</span></span>

<span data-ttu-id="58144-106">Você cria um gateway com o Azure IoT Edge criando e montando *módulos do IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="58144-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="58144-107">Os módulos usam *mensagens* para trocar dados entre si.</span><span class="sxs-lookup"><span data-stu-id="58144-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="58144-108">Um módulo recebe uma mensagem, executa alguma ação nela, opcionalmente, a transforma em uma nova mensagem e a publica para ser processada por outros módulos.</span><span class="sxs-lookup"><span data-stu-id="58144-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="58144-109">Alguns módulos poderão gerar apenas novas mensagens e nunca processar as mensagens de entrada.</span><span class="sxs-lookup"><span data-stu-id="58144-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="58144-110">Uma cadeia de módulos cria um pipeline de processamento de dados com cada módulo executando uma transformação nos dados em um ponto do pipeline.</span><span class="sxs-lookup"><span data-stu-id="58144-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Uma cadeia de módulos no gateway, compilada com o IoT Edge do Azure][1]

<span data-ttu-id="58144-112">O IoT Edge contém os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="58144-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="58144-113">Módulos pré-gravados que executam funções comuns de gateway.</span><span class="sxs-lookup"><span data-stu-id="58144-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="58144-114">As interfaces que um desenvolvedor pode usar para gravar módulos personalizados.</span><span class="sxs-lookup"><span data-stu-id="58144-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="58144-115">A infraestrutura necessária para implantar e executar um conjunto de módulos.</span><span class="sxs-lookup"><span data-stu-id="58144-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="58144-116">O SDK fornece uma camada de abstração que permite criar gateways para serem executados em vários sistemas operacionais e plataformas.</span><span class="sxs-lookup"><span data-stu-id="58144-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Camada de abstração do IoT Edge do Azure][2]

## <a name="messages"></a><span data-ttu-id="58144-118">Mensagens</span><span class="sxs-lookup"><span data-stu-id="58144-118">Messages</span></span>

<span data-ttu-id="58144-119">Mesmo que pensar sobre os módulos que transmitem mensagens entre si seja uma maneira conveniente de conceitualizar o funcionamento de um gateway, ela não reflete com precisão o que acontece.</span><span class="sxs-lookup"><span data-stu-id="58144-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="58144-120">Módulos do IoT Edge usam um agente para se comunicarem entre si.</span><span class="sxs-lookup"><span data-stu-id="58144-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="58144-121">Os módulos publicam mensagens para o agente (usando padrões de mensagens, como barramento ou publicação/assinatura) e permitem que o agente direcione a mensagem para os módulos conectados a ele.</span><span class="sxs-lookup"><span data-stu-id="58144-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="58144-122">Um módulo usa a função **Broker_Publish** para publicar uma mensagem para o agente.</span><span class="sxs-lookup"><span data-stu-id="58144-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="58144-123">O agente entrega as mensagens para um módulo, invocando uma função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="58144-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="58144-124">Uma mensagem consiste em um conjunto de propriedades de chave/valor e no conteúdo transmitido como um bloco de memória.</span><span class="sxs-lookup"><span data-stu-id="58144-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![A função do Agente no IoT Edge do Azure][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="58144-126">Roteamento e filtragem de mensagens</span><span class="sxs-lookup"><span data-stu-id="58144-126">Message routing and filtering</span></span>

<span data-ttu-id="58144-127">Há duas maneiras de direcionar mensagens para os módulos corretos do IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="58144-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="58144-128">Você pode transmitir um conjunto de links para o agente para que este saiba a origem e o coletor de cada módulo.</span><span class="sxs-lookup"><span data-stu-id="58144-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="58144-129">Um módulo pode filtrar as propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="58144-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="58144-130">Um módulo só deve agir em relação a uma mensagem se a mensagem é destinada a ele.</span><span class="sxs-lookup"><span data-stu-id="58144-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="58144-131">Os links e a filtragem de mensagens criam efetivamente um pipeline de mensagem.</span><span class="sxs-lookup"><span data-stu-id="58144-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58144-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58144-132">Next steps</span></span>

<span data-ttu-id="58144-133">Para ver esses conceitos aplicados em um exemplo que você pode executar, consulte [Explorar arquitetura do Azure IoT Edge][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="58144-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md