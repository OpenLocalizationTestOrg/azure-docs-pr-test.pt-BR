---
title: "Soluções do Azure para a Internet das coisas (IoT Suite) | Microsoft Docs"
description: "Visão geral de uma arquitetura de solução de IoT de exemplo e como ela se relaciona com dispositivos, o serviço de Hub IoT do Azure, SDKs de serviço IoT do Azure e outros serviços do Azure."
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
ms.openlocfilehash: 1d54f090a0e07cd5102cb48cd70a1377845d6654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="cd553-103">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd553-103">Next steps</span></span>

<span data-ttu-id="cd553-104">O Hub IoT do Azure é um serviço do Azure que permite comunicações bidirecionais confiáveis e seguras entre a sua solução e milhões de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cd553-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="cd553-105">Ele permite que a solução back-end:</span><span class="sxs-lookup"><span data-stu-id="cd553-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="cd553-106">Receba telemetria em escala de seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cd553-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="cd553-107">Encaminhe os dados de seus dispositivos para um processador de eventos de fluxo.</span><span class="sxs-lookup"><span data-stu-id="cd553-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="cd553-108">Receba carregamentos de arquivos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cd553-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="cd553-109">Envie mensagens da nuvem para o dispositivo para dispositivos específicos.</span><span class="sxs-lookup"><span data-stu-id="cd553-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="cd553-110">Você pode usar o Hub IoT para implementar seu próprio back-end de solução.</span><span class="sxs-lookup"><span data-stu-id="cd553-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="cd553-111">Além disso, o Hub IoT inclui um Registro de identidade usado para provisionar dispositivos, suas credenciais de segurança e os direitos de conexão ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cd553-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="cd553-112">Para saber mais sobre o Hub IoT, confira [O que é o Hub IoT?][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="cd553-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="cd553-113">Para saber como o Hub IoT do Azure permite o gerenciamento de dispositivos baseado em padrões para gerenciar, configurar e atualizar os dispositivos remotamente, consulte [Visão geral do gerenciamento de dispositivos com o Hub IoT][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="cd553-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="cd553-114">Para implementar aplicativos cliente em uma grande variedade de sistemas operacionais e plataformas de hardware do dispositivo, você pode usar os SDKs do dispositivo IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd553-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="cd553-115">Os SDKs do dispositivo incluem bibliotecas que facilitam o envio de telemetria para um hub IoT e o recebimento de mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cd553-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="cd553-116">Ao usar os SDKs de dispositivo, você poderá escolher entre vários protocolos de rede para comunicar-se com o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cd553-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="cd553-117">Para saber mais, confira as [informações sobre SDKs de dispositivo][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="cd553-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="cd553-118">Para começar a escrever código e executar alguns exemplos, confira o tutorial [Introdução ao Hub IoT][lnk-getstarted].</span><span class="sxs-lookup"><span data-stu-id="cd553-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="cd553-119">Você também pode se interessar pelo [Azure IoT Suite][lnk-iot-suite], que é um conjunto de soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="cd553-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="cd553-120">O IoT Suite permite que você comece a trabalhar rapidamente e dimensiona projetos IoT para lidar com cenários comuns de IoT, como o monitoramento remoto, o gerenciamento de ativos e a manutenção preditiva.</span><span class="sxs-lookup"><span data-stu-id="cd553-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
