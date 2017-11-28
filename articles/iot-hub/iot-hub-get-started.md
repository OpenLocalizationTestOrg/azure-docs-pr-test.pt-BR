---
title: "Hub IoT do Azure – introdução à conexão de dispositivos IoT à nuvem | Microsoft Docs"
description: "Saiba como conectar seus quadros IoT e kits de início ao Hub IoT do Azure. Seus dispositivos podem enviar telemetria ao Hub IoT e o Hub IoT pode monitorar e gerenciar seus dispositivos."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial do hub iot do azure
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 45016e6383761ffe78f13ccef1112ab3d9753498
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="e1dee-105">Tutoriais de introdução ao Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="e1dee-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="e1dee-106">Você pode usar o Hub IoT do Azure e os SDKs do dispositivo IoT do Azure para criar soluções de IoT (Internet das Coisas):</span><span class="sxs-lookup"><span data-stu-id="e1dee-106">You can use Azure IoT Hub and the Azure IoT device SDKs to build Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="e1dee-107">O Hub IoT do Azure é um serviço completamente gerenciado na nuvem que se conecta com segurança aos seus dispositivos IoT, monitorando-os e gerenciando-os.</span><span class="sxs-lookup"><span data-stu-id="e1dee-107">Azure IoT Hub is a fully managed service in the cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="e1dee-108">Use os SDKs do dispositivo IoT do Azure para implementar os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="e1dee-108">Use the Azure IoT Device SDKs to implement your IoT devices.</span></span>
* <span data-ttu-id="e1dee-109">Use um gateway IoT em cenários de IoT mais complexos.</span><span class="sxs-lookup"><span data-stu-id="e1dee-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="e1dee-110">Por exemplo, quando você precisa considerar fatores como dispositivos herdados, custos de largura de banda, políticas de segurança e privacidade ou processamento de dados de borda.</span><span class="sxs-lookup"><span data-stu-id="e1dee-110">For example, where you need to consider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="e1dee-111">Nesses cenários, você pode usar o Azure IoT Edge para implementar um gateway que conecte dispositivos ao seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e1dee-111">In these scenarios, you use Azure IoT Edge to implement a gateway that connects devices to your IoT hub.</span></span>

## <a name="what-the-tutorials-cover"></a><span data-ttu-id="e1dee-112">O que os tutoriais abordam</span><span class="sxs-lookup"><span data-stu-id="e1dee-112">What the tutorials cover</span></span>

<span data-ttu-id="e1dee-113">Estes tutoriais apresentam a você o Hub IoT do Azure e os SDKs do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e1dee-113">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="e1dee-114">Os tutoriais abordam os cenários comuns de IoT para demonstrar os recursos do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e1dee-114">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="e1dee-115">Os tutoriais também ilustram como combinar o Hub IoT com outros serviços e ferramentas do Azure para criar soluções de IoT mais eficazes.</span><span class="sxs-lookup"><span data-stu-id="e1dee-115">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="e1dee-116">Nos tutoriais, você pode optar por usar dispositivos IoT simulados ou reais.</span><span class="sxs-lookup"><span data-stu-id="e1dee-116">In the tutorials, you can choose to use either simulated or real IoT devices.</span></span> <span data-ttu-id="e1dee-117">Além disso, você pode aprender como usar um gateway de modo a habilitar dispositivos para conectar ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e1dee-117">In addition, you can learn how to use a gateway to enable devices to connect to your IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="e1dee-118">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="e1dee-118">Set up your device</span></span>

<span data-ttu-id="e1dee-119">Conecte um dispositivo IoT ou gateway ao Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1dee-119">Connect an IoT device or gateway to Azure IoT Hub.</span></span> <span data-ttu-id="e1dee-120">Você pode escolher um dispositivo real ou simulado para começar:</span><span class="sxs-lookup"><span data-stu-id="e1dee-120">You can choose a physical or simulated device to get started:</span></span>

| <span data-ttu-id="e1dee-121">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="e1dee-121">IoT device</span></span>                       | <span data-ttu-id="e1dee-122">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="e1dee-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="e1dee-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="e1dee-123">Raspberry Pi</span></span>                     | <span data-ttu-id="e1dee-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="e1dee-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="e1dee-125">Kit de Desenvolvimento da IoT</span><span class="sxs-lookup"><span data-stu-id="e1dee-125">IoT DevKit</span></span>                       | <span data-ttu-id="e1dee-126">[Arduino no VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="e1dee-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="e1dee-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="e1dee-127">Intel Edison</span></span>                     | <span data-ttu-id="e1dee-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="e1dee-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="e1dee-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="e1dee-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="e1dee-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="e1dee-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="e1dee-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="e1dee-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="e1dee-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="e1dee-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="e1dee-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="e1dee-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="e1dee-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="e1dee-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="e1dee-135">Dispositivo simulado no computador</span><span class="sxs-lookup"><span data-stu-id="e1dee-135">Simulated device on PC</span></span>           | <span data-ttu-id="e1dee-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="e1dee-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="e1dee-137">Simulador de dispositivo online</span><span class="sxs-lookup"><span data-stu-id="e1dee-137">Online device simulator</span></span>         | <span data-ttu-id="e1dee-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="e1dee-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="e1dee-139">Além disso, você pode usar um gateway IoT Edge para habilitar os dispositivos a conectarem-se ao seu Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="e1dee-139">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub:</span></span>

| <span data-ttu-id="e1dee-140">Dispositivos de gateway</span><span class="sxs-lookup"><span data-stu-id="e1dee-140">Gateway device</span></span>               | <span data-ttu-id="e1dee-141">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="e1dee-141">Programming language</span></span> | <span data-ttu-id="e1dee-142">Plataforma</span><span class="sxs-lookup"><span data-stu-id="e1dee-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="e1dee-143">Intel NUC (modelo DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="e1dee-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="e1dee-144">C</span><span class="sxs-lookup"><span data-stu-id="e1dee-144">C</span></span>                    | <span data-ttu-id="e1dee-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="e1dee-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="e1dee-146">Gateway simulado</span><span class="sxs-lookup"><span data-stu-id="e1dee-146">Simulated gateway</span></span>            | <span data-ttu-id="e1dee-147">C</span><span class="sxs-lookup"><span data-stu-id="e1dee-147">C</span></span>                    | <span data-ttu-id="e1dee-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="e1dee-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

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
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
