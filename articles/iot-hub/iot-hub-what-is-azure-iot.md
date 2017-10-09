---
title: "soluções de aaaAzure para Internet das coisas (IoT Suite) | Microsoft Docs"
description: "Visão geral da arquitetura de solução de IoT um exemplo e como ele se relaciona toodevices, Olá serviço Azure IoT Hub, SDKs de dispositivo IoT do Azure, SDKs do Azure IoT serviço e outros serviços do Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="3573b-103">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3573b-103">Next steps</span></span>

<span data-ttu-id="3573b-104">O Hub IoT do Azure é um serviço do Azure que permite comunicações bidirecionais confiáveis e seguras entre a sua solução e milhões de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3573b-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="3573b-105">Ele permite Olá solução back-end para:</span><span class="sxs-lookup"><span data-stu-id="3573b-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="3573b-106">Receba telemetria em escala de seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3573b-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="3573b-107">Dados de rota do processador de evento de fluxo de tooa de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3573b-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="3573b-108">Receba carregamentos de arquivos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3573b-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="3573b-109">Envie mensagens de nuvem para dispositivo toospecific dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3573b-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="3573b-110">Você pode usar o IoT Hub tooimplement terminar sua própria solução de volta.</span><span class="sxs-lookup"><span data-stu-id="3573b-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="3573b-111">Além disso, o IoT Hub inclui dispositivos de tooprovision de registro usado uma identidade, suas credenciais de segurança e seu hub IoT de toohello de tooconnect de direitos.</span><span class="sxs-lookup"><span data-stu-id="3573b-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="3573b-112">toolearn mais sobre o IoT Hub, consulte [o que é o IoT Hub?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="3573b-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="3573b-113">toolearn como Azure IoT Hub permite o gerenciamento de dispositivo baseado em padrões para você tooremotely gerenciar, configurar e atualizar seus dispositivos, consulte [visão geral do gerenciamento de dispositivos com o IoT Hub][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="3573b-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="3573b-114">aplicativos de cliente tooimplement em uma ampla variedade de plataformas de hardware de dispositivos e sistemas operacionais, você pode usar o dispositivo de IoT do Azure de saudação SDKs.</span><span class="sxs-lookup"><span data-stu-id="3573b-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="3573b-115">dispositivo Olá SDKs incluem bibliotecas que facilitam a telemetria tooan IoT hub e o recebimento de nuvem para dispositivo as mensagens enviadas.</span><span class="sxs-lookup"><span data-stu-id="3573b-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="3573b-116">Quando você usa o dispositivo de saudação SDKs, você pode escolher entre vários toocommunicate de protocolos de rede com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3573b-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="3573b-117">toolearn mais, consulte Olá [informações sobre dispositivo SDKs][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="3573b-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="3573b-118">tooget iniciado gravar um código e executar alguns exemplos, consulte Olá [começar com o IoT Hub] [ lnk-getstarted] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3573b-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="3573b-119">Você também pode se interessar pelo [Azure IoT Suite][lnk-iot-suite], que é um conjunto de soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="3573b-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="3573b-120">IoT Suite permite que você tooget iniciado rapidamente e escalar IoT projetos tooaddress cenários comuns de IoT – como de monitoramento remoto, gerenciamento de ativos e manutenção preditiva.</span><span class="sxs-lookup"><span data-stu-id="3573b-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
