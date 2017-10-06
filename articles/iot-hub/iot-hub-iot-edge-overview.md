---
title: aaaOverview da borda do IoT do Azure | Microsoft Docs
description: "Descreve os conceitos arquitetura no Azure IoT Edge Olá chave como agentes, módulos e gateways."
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
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="e4e63-103">Conceitos de arquitetura do Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="e4e63-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="e4e63-104">Antes de examinar um código de exemplo ou criar seu próprio gateway de campo usando borda IoT, você deve entender os conceitos de chave de saudação que são a base de arquitetura de saudação da borda de IoT.</span><span class="sxs-lookup"><span data-stu-id="e4e63-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="e4e63-105">Módulos do IoT Edge</span><span class="sxs-lookup"><span data-stu-id="e4e63-105">IoT Edge modules</span></span>

<span data-ttu-id="e4e63-106">Você cria um gateway com o Azure IoT Edge criando e montando *módulos do IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="e4e63-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="e4e63-107">Os módulos usam *mensagens* tooexchange dados entre si.</span><span class="sxs-lookup"><span data-stu-id="e4e63-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="e4e63-108">Um módulo recebe uma mensagem, executa alguma ação nele, opcionalmente o transforma em uma nova mensagem e, em seguida, publica para outros módulos tooprocess.</span><span class="sxs-lookup"><span data-stu-id="e4e63-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="e4e63-109">Alguns módulos poderão gerar apenas novas mensagens e nunca processar as mensagens de entrada.</span><span class="sxs-lookup"><span data-stu-id="e4e63-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="e4e63-110">Uma cadeia de módulos cria um pipeline de processamento de dados com cada módulo executar uma transformação nos dados de saudação em um ponto em que o pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4e63-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Uma cadeia de módulos no gateway, compilada com o IoT Edge do Azure][1]

<span data-ttu-id="e4e63-112">Borda de IoT contém Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="e4e63-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="e4e63-113">Módulos pré-gravados que executam funções comuns de gateway.</span><span class="sxs-lookup"><span data-stu-id="e4e63-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="e4e63-114">interfaces de saudação um desenvolvedor podem usar módulos personalizados toowrite.</span><span class="sxs-lookup"><span data-stu-id="e4e63-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="e4e63-115">Olá toodeploy necessário de infraestrutura e executar um conjunto de módulos.</span><span class="sxs-lookup"><span data-stu-id="e4e63-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="e4e63-116">Olá SDK fornece uma camada de abstração que permite que você toobuild gateways toorun em vários sistemas operacionais e plataformas.</span><span class="sxs-lookup"><span data-stu-id="e4e63-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Camada de abstração do IoT Edge do Azure][2]

## <a name="messages"></a><span data-ttu-id="e4e63-118">Mensagens</span><span class="sxs-lookup"><span data-stu-id="e4e63-118">Messages</span></span>

<span data-ttu-id="e4e63-119">Embora pensar módulos transmitindo mensagens tooeach outros é uma maneira conveniente de tooconceptualize como funções um gateway, ele não refletir precisamente o que acontece.</span><span class="sxs-lookup"><span data-stu-id="e4e63-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="e4e63-120">Módulos de borda IoT usam toocommunicate um agente com o outro.</span><span class="sxs-lookup"><span data-stu-id="e4e63-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="e4e63-121">Módulos publicar broker toohello de mensagens (usando padrões de mensagens, como de barramento ou a publicação/assinatura) e deixe Olá broker rota Olá mensagem toohello módulos conectados tooit.</span><span class="sxs-lookup"><span data-stu-id="e4e63-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="e4e63-122">Um módulo usa Olá **Broker_Publish** toopublish um agente de mensagens toohello de função.</span><span class="sxs-lookup"><span data-stu-id="e4e63-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="e4e63-123">broker Olá oferece módulo de tooa de mensagens, chamando uma função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="e4e63-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="e4e63-124">Uma mensagem consiste em um conjunto de propriedades de chave/valor e no conteúdo transmitido como um bloco de memória.</span><span class="sxs-lookup"><span data-stu-id="e4e63-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![função Hello de saudação do Broker no Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="e4e63-126">Roteamento e filtragem de mensagens</span><span class="sxs-lookup"><span data-stu-id="e4e63-126">Message routing and filtering</span></span>

<span data-ttu-id="e4e63-127">Há duas maneiras de módulos toohello IoT borda corretos mensagens toodirect:</span><span class="sxs-lookup"><span data-stu-id="e4e63-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="e4e63-128">Você pode passar um conjunto de links podem ser passados toohello agente para agente Olá Saiba fonte hello e coletor para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="e4e63-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="e4e63-129">Um módulo pode filtrar em Propriedades de saudação de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4e63-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="e4e63-130">Um módulo só deve agir sobre uma mensagem se a mensagem de saudação é destinada.</span><span class="sxs-lookup"><span data-stu-id="e4e63-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="e4e63-131">Os links e a filtragem de mensagens criam efetivamente um pipeline de mensagem.</span><span class="sxs-lookup"><span data-stu-id="e4e63-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4e63-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4e63-132">Next steps</span></span>

<span data-ttu-id="e4e63-133">toosee esses conceitos aplicados em um exemplo que você pode executar, consulte [arquitetura de explorar o Azure IoT borda][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="e4e63-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md