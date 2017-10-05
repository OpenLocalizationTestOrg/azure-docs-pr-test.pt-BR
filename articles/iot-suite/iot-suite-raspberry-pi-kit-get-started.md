---
title: Conectar um Raspberry Pi ao Azure IoT Suite | Microsoft Docs
description: "Tutoriais que usam Node.js ou C para ajudar você a aprender a usar o Microsoft Azure IoT Starter Kit for the Raspberry Pi 3 e a solução de monitoramento remoto do IoT Suite. Você pode escolher um tutorial que simula a telemetria ou que usa sensores reais ou permite atualizações de firmware remoto."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="df9df-104">Conectar o Microsoft Azure IoT Raspberry Pi 3 Starter Kit à solução de monitoramento remota</span><span class="sxs-lookup"><span data-stu-id="df9df-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="df9df-105">Os tutoriais nesta seção ajudam você a aprender a conectar um dispositivo Raspberry Pi 3 à solução de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="df9df-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="df9df-106">Escolha o tutorial apropriado à linguagem de programação preferencial e se você tem o hardware do sensor disponível para uso com o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="df9df-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="df9df-107">Os tutoriais</span><span class="sxs-lookup"><span data-stu-id="df9df-107">The tutorials</span></span>

| <span data-ttu-id="df9df-108">Tutorial</span><span class="sxs-lookup"><span data-stu-id="df9df-108">Tutorial</span></span> | <span data-ttu-id="df9df-109">Observações</span><span class="sxs-lookup"><span data-stu-id="df9df-109">Notes</span></span> | <span data-ttu-id="df9df-110">Linguagens</span><span class="sxs-lookup"><span data-stu-id="df9df-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="df9df-111">Telemetria simulada (básica)</span><span class="sxs-lookup"><span data-stu-id="df9df-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="df9df-112">Simula os dados do sensor.</span><span class="sxs-lookup"><span data-stu-id="df9df-112">Simulates sensor data.</span></span> <span data-ttu-id="df9df-113">Usa um Raspberry Pi autônomo.</span><span class="sxs-lookup"><span data-stu-id="df9df-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="df9df-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="df9df-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="df9df-115">Sensor real (intermediário)</span><span class="sxs-lookup"><span data-stu-id="df9df-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="df9df-116">Usa dados de um sensor BME280 conectado ao seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="df9df-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="df9df-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="df9df-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="df9df-118">Implementar atualização do firmware (avançado)</span><span class="sxs-lookup"><span data-stu-id="df9df-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="df9df-119">Usa dados de um sensor BME280 conectado ao seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="df9df-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="df9df-120">Permite atualizações de firmware remoto em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="df9df-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="df9df-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="df9df-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="df9df-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df9df-122">Next steps</span></span>

<span data-ttu-id="df9df-123">Visite o [Centro de Desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e a documentação sobre o Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="df9df-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md