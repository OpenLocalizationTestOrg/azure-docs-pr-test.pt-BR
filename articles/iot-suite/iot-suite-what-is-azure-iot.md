---
title: "Soluções do Azure para a Internet das coisas (IoT Suite) | Microsoft Docs"
description: "Visão geral de IoT no Azure, incluindo uma arquitetura da solução do exemplo e como se relaciona com o Azure IoT Suite e soluções pré-configuradas."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 320190488bb4c7b8192421f9dd50a5264f558584
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a><span data-ttu-id="aea44-103">Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="aea44-103">Azure IoT Suite</span></span>
<span data-ttu-id="aea44-104">O Microsoft Azure IoT Suite é uma solução de nível corporativo que permite a você trabalhar rapidamente por meio de um conjunto de soluções pré-configuradas extensíveis.</span><span class="sxs-lookup"><span data-stu-id="aea44-104">The Microsoft Azure IoT Suite is an enterprise-grade solution that enables you to get started quickly through a set of extensible preconfigured solutions.</span></span> <span data-ttu-id="aea44-105">Essas soluções abordam cenários de IoT comuns, como [monitoramento remoto][lnk-preconfigured-solutions] e [manutenção preditiva][lnk-predictive-maintenance] e [fábrica conectada][lnk-connected-factory].</span><span class="sxs-lookup"><span data-stu-id="aea44-105">These solutions address common IoT scenarios, such as [remote monitoring][lnk-preconfigured-solutions], [predictive maintenance][lnk-predictive-maintenance], and [connected factory][lnk-connected-factory].</span></span> <span data-ttu-id="aea44-106">Essas soluções são implementações da arquitetura da solução de IoT, descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="aea44-106">These solutions are implementations of the IoT solution architecture outlined in this article.</span></span>

<span data-ttu-id="aea44-107">As soluções pré-configuradas são completas, funcionais e incluem:</span><span class="sxs-lookup"><span data-stu-id="aea44-107">The preconfigured solutions are complete, working, end-to-end solutions that include:</span></span>

- <span data-ttu-id="aea44-108">Dispositivos simulados para você começar.</span><span class="sxs-lookup"><span data-stu-id="aea44-108">Simulated devices to get you started.</span></span>
- <span data-ttu-id="aea44-109">Serviços do Azure pré-configurado como [Azure IoT Hub][Azure IoT Hub], [Hubs de Eventos do Azure][Azure Event Hubs], [Stream Analytics do Azure][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], e [Armazenamento do Azure][Azure storage].</span><span class="sxs-lookup"><span data-stu-id="aea44-109">Preconfigured Azure services such as [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], and [Azure storage][Azure storage].</span></span>
- <span data-ttu-id="aea44-110">Consoles de gerenciamento específicas à solução.</span><span class="sxs-lookup"><span data-stu-id="aea44-110">Solution-specific management consoles.</span></span>

<span data-ttu-id="aea44-111">As soluções pré-configuradas contêm código comprovado e pronto para produção que você pode personalizar e estender para implementar seus próprios cenários específicos de IoT.</span><span class="sxs-lookup"><span data-stu-id="aea44-111">The preconfigured solutions contain proven, production-ready code that you can customize and extend to implement your own specific IoT scenarios.</span></span>

<span data-ttu-id="aea44-112">Talvez você também tenha interesse no serviço [Hub IoT do Azure][Azure IoT Hub], usado por muitas das soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="aea44-112">You may also be interested in the [Azure IoT Hub][Azure IoT Hub] service that many of the preconfigured solutions use.</span></span> <span data-ttu-id="aea44-113">O [Hub IoT do Azure][Azure IoT Hub] fornece a comunicação bidirecional segura e confiável entre os dispositivos e a nuvem usados na arquitetura da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="aea44-113">[Azure IoT Hub][Azure IoT Hub] provides the secure and reliable bi-directional communications between devices and the cloud used in the preconfigured solution architecture.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aea44-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aea44-114">Next steps</span></span>
<span data-ttu-id="aea44-115">Explore estes recursos para saber mais sobre o IoT Suite e as soluções pré-configuradas:</span><span class="sxs-lookup"><span data-stu-id="aea44-115">Explore these resources to continue learning about IoT Suite and the preconfigured solutions:</span></span>

* <span data-ttu-id="aea44-116">[O que é o Azure IoT Suite?][lnk-whatissuite]</span><span class="sxs-lookup"><span data-stu-id="aea44-116">[What is Azure IoT Suite?][lnk-whatissuite]</span></span>
* <span data-ttu-id="aea44-117">[Quais são as soluções pré-configuradas do Azure IoT Suite?][lnk-whatarepreconfigured]</span><span class="sxs-lookup"><span data-stu-id="aea44-117">[What are the Azure IoT Suite preconfigured solutions?][lnk-whatarepreconfigured]</span></span>

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure Event Hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure Stream Analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure Machine Learning]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-connected-factory]: iot-suite-connected-factory-overview.md