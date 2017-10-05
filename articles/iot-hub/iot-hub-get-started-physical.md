---
title: "Introdução à conexão de dispositivos físicos ao Hub IoT do Azure | Microsoft Docs"
description: "Saiba como conectar dispositivos físicos e placas ao Hub IoT do Azure. Seus dispositivos podem enviar telemetria ao Hub IoT e o Hub IoT pode monitorar e gerenciar seus dispositivos."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial do hub iot do azure
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: f4128b6b049aa876e170c56dcf2e40720644dc3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="1bb3a-105">Tutoriais de introdução aos dispositivos físicos no Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="1bb3a-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="1bb3a-106">Estes tutoriais apresentam a você o Hub IoT do Azure e os SDKs do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1bb3a-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="1bb3a-107">Os tutoriais abordam os cenários comuns de IoT para demonstrar os recursos do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1bb3a-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="1bb3a-108">Os tutoriais também ilustram como combinar o Hub IoT com outros serviços e ferramentas do Azure para criar soluções de IoT mais eficazes.</span><span class="sxs-lookup"><span data-stu-id="1bb3a-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="1bb3a-109">Os tutoriais listados na tabela a seguir mostram como criar dispositivos IoT físicos.</span><span class="sxs-lookup"><span data-stu-id="1bb3a-109">The tutorials listed in the following table show you how to create physical IoT devices.</span></span>

| <span data-ttu-id="1bb3a-110">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="1bb3a-110">IoT device</span></span>                       | <span data-ttu-id="1bb3a-111">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="1bb3a-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="1bb3a-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="1bb3a-112">Raspberry Pi</span></span>                    | <span data-ttu-id="1bb3a-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="1bb3a-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="1bb3a-114">Kit de Desenvolvimento da IoT</span><span class="sxs-lookup"><span data-stu-id="1bb3a-114">IoT DevKit</span></span>                      | <span data-ttu-id="1bb3a-115">[Arduino no VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="1bb3a-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="1bb3a-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="1bb3a-116">Intel Edison</span></span>                    | <span data-ttu-id="1bb3a-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="1bb3a-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="1bb3a-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="1bb3a-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="1bb3a-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="1bb3a-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="1bb3a-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="1bb3a-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="1bb3a-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="1bb3a-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="1bb3a-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="1bb3a-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="1bb3a-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="1bb3a-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="1bb3a-124">Além disso, você pode usar um gateway IoT Edge para habilitar os dispositivos a conectarem-se ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1bb3a-124">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="1bb3a-125">Dispositivos de gateway</span><span class="sxs-lookup"><span data-stu-id="1bb3a-125">Gateway device</span></span>               | <span data-ttu-id="1bb3a-126">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="1bb3a-126">Programming language</span></span> | <span data-ttu-id="1bb3a-127">Plataforma</span><span class="sxs-lookup"><span data-stu-id="1bb3a-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="1bb3a-128">Intel NUC (modelo DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="1bb3a-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="1bb3a-129">C</span><span class="sxs-lookup"><span data-stu-id="1bb3a-129">C</span></span>                    | <span data-ttu-id="1bb3a-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="1bb3a-130">[Wind River Linux][NUC_Lnx]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]


[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
