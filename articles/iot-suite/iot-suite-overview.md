---
title: "Visão geral do Azure IoT Suite aaaMicrosoft | Microsoft Docs"
description: "Visão geral de como o Azure IoT Suite agrega internet das coisas soluções pré-configuradas toocollect, analisar, armazenar dados, fornecer visualizações e integrar com outros sistemas."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="d883e-103">Visão geral do Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="d883e-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="d883e-104">Hello Azure internet dos serviços de coisas (IoT) oferecem uma ampla variedade de recursos.</span><span class="sxs-lookup"><span data-stu-id="d883e-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="d883e-105">Esses serviços de nível corporativo permitem que você:</span><span class="sxs-lookup"><span data-stu-id="d883e-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="d883e-106">Colete dados de dispositivos</span><span class="sxs-lookup"><span data-stu-id="d883e-106">Collect data from devices</span></span>
* <span data-ttu-id="d883e-107">Analise fluxos de dados em movimento</span><span class="sxs-lookup"><span data-stu-id="d883e-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="d883e-108">Armazene e consulte grandes conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="d883e-108">Store and query large data sets</span></span>
* <span data-ttu-id="d883e-109">Visualize dados históricos e em tempo real</span><span class="sxs-lookup"><span data-stu-id="d883e-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="d883e-110">Realize a integração com sistemas de back-office</span><span class="sxs-lookup"><span data-stu-id="d883e-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="d883e-111">Gerenciar seus dispositivos</span><span class="sxs-lookup"><span data-stu-id="d883e-111">Manage your devices</span></span>

<span data-ttu-id="d883e-112">toodeliver, esses recursos, o Azure IoT Suite pacotes juntos em vários serviços do Azure com extensões personalizadas como *soluções pré-configuradas*.</span><span class="sxs-lookup"><span data-stu-id="d883e-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="d883e-113">Essas soluções pré-configuradas são as implementações básicas dos padrões comuns de solução de IoT que ajudam a tooreduce Olá tempo você toodeliver suas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="d883e-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="d883e-114">Usando Olá [kits de desenvolvimento de software IoT][lnk-sdks], você pode personalizar e estender essas soluções toomeet seus próprios requisitos.</span><span class="sxs-lookup"><span data-stu-id="d883e-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="d883e-115">Você também pode usar essas soluções como exemplos ou modelos no desenvolvimento de novas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="d883e-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="d883e-116">Olá vídeo a seguir fornece uma introdução tooAzure IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="d883e-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="d883e-117">Serviços do Azure IoT no Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="d883e-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="d883e-118">as soluções de saudação pré-configurado geralmente usam Olá serviços a seguir:</span><span class="sxs-lookup"><span data-stu-id="d883e-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="d883e-119">Núcleo tooAzure IoT Suite é hello [Azure IoT Hub] [ lnk-iot-hub] service.</span><span class="sxs-lookup"><span data-stu-id="d883e-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="d883e-120">Esse serviço fornece Olá dispositivo para nuvem e recursos de nuvem para dispositivo mensagens e age como Olá toohello de gateway de nuvem e Olá outros serviços importantes do IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="d883e-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="d883e-121">Olá serviço permite que as mensagens de tooreceive de seus dispositivos em grande escala e enviar comandos tooyour dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d883e-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="d883e-122">Olá serviço também permite que você muito[gerenciar seus dispositivos][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="d883e-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="d883e-123">Por exemplo, configurar, reinicializar ou executar uma redefinição de fábrica em um ou mais hub de toohello conectado de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d883e-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="d883e-124">O [Stream Analytics do Azure][lnk-asa] fornece análise de dados em movimento.</span><span class="sxs-lookup"><span data-stu-id="d883e-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="d883e-125">IoT Suite usa essa telemetria de entrada de tooprocess de serviço, executar agregação e detecção de eventos.</span><span class="sxs-lookup"><span data-stu-id="d883e-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="d883e-126">soluções de Olá pré-configurado também usam o stream analytics tooprocess mensagens informativas que contêm dados como metadados ou comando respostas de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d883e-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="d883e-127">soluções de saudação usam mensagens de saudação do Stream Analytics tooprocess de dispositivos e entregar as mensagens tooother serviços.</span><span class="sxs-lookup"><span data-stu-id="d883e-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="d883e-128">[Armazenamento do Azure] [ lnk-azure-storage] e [o banco de dados do Azure Cosmos] [ lnk-document-db] fornecer recursos de armazenamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d883e-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="d883e-129">Olá soluções pré-configuradas usam telemetria de toostore de armazenamento de blob e toomake-las disponíveis para análise.</span><span class="sxs-lookup"><span data-stu-id="d883e-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="d883e-130">soluções de saudação usam metadados do banco de dados do Cosmos toostore dispositivo e habilitam os recursos de gerenciamento de dispositivo Olá das soluções de saudação.</span><span class="sxs-lookup"><span data-stu-id="d883e-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="d883e-131">[Os aplicativos Web do Azure] [ lnk-web-apps] e [Microsoft Power BI] [ lnk-power-bi] fornecer Olá recursos de visualização de dados.</span><span class="sxs-lookup"><span data-stu-id="d883e-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="d883e-132">flexibilidade de saudação do Power BI permite que você tooquickly criar seus próprios painéis interativos que usam dados do IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="d883e-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="d883e-133">Para obter uma visão geral da arquitetura de saudação de uma solução de IoT típica, consulte [Microsoft Azure e hello Internet das coisas (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="d883e-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="d883e-134">Soluções pré-configuradas</span><span class="sxs-lookup"><span data-stu-id="d883e-134">Preconfigured solutions</span></span>

<span data-ttu-id="d883e-135">IoT Suite inclui soluções pré-configuradas que habilitar tooquickly você começar a usar e tooexplore Olá cenários IoT comuns, como:</span><span class="sxs-lookup"><span data-stu-id="d883e-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="d883e-136">Monitoramento remoto</span><span class="sxs-lookup"><span data-stu-id="d883e-136">Remote monitoring</span></span>
* <span data-ttu-id="d883e-137">Manutenção preditiva</span><span class="sxs-lookup"><span data-stu-id="d883e-137">Predictive maintenance</span></span>
* <span data-ttu-id="d883e-138">Fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="d883e-138">Connected factory</span></span>

<span data-ttu-id="d883e-139">Você pode implantar essas soluções tooyour assinatura do Azure e, em seguida, executar um cenário IoT completo, de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="d883e-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d883e-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d883e-140">Next steps</span></span>

<span data-ttu-id="d883e-141">Agora que você tem uma visão geral do IoT Suite que pode fazer e quais são seus principais componentes, você pode aprender mais sobre as soluções de saudação pré-configurados em IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="d883e-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="d883e-142">Para obter mais informações, consulte [quais são hello Azure IoT soluções pré-configuradas?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="d883e-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
