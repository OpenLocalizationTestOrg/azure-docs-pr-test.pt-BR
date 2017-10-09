---
title: "IoT Hub do Azure - começar a conectar-se a nuvem do IoT dispositivos toohello | Microsoft Docs"
description: Saiba como tooconnect seus quadros IoT e starter kits tooAzure IoT Hub. Seus dispositivos podem enviar telemetria tooIoT Hub e IoT Hub podem monitorar e gerenciar seus dispositivos.
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
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="55b47-105">Tutoriais de introdução ao Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="55b47-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="55b47-106">Você pode usar o Azure IoT Hub hello Azure IoT soluções de dispositivos e SDKs toobuild Internet das coisas (IoT):</span><span class="sxs-lookup"><span data-stu-id="55b47-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="55b47-107">IoT Hub do Azure é um serviço totalmente gerenciado na nuvem de saudação que se conecta com segurança, monitora e gerencia os dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="55b47-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="55b47-108">Use Olá SDKs do Azure IoT dispositivo tooimplement seus dispositivos IoT.</span><span class="sxs-lookup"><span data-stu-id="55b47-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="55b47-109">Use um gateway IoT em cenários de IoT mais complexos.</span><span class="sxs-lookup"><span data-stu-id="55b47-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="55b47-110">Por exemplo, em que você precisa tooconsider fatores como dispositivos herdados, os custos de largura de banda, as políticas de segurança e privacidade ou processamento de dados de borda.</span><span class="sxs-lookup"><span data-stu-id="55b47-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="55b47-111">Nesses cenários, você deve usar Azure IoT borda tooimplement um gateway que se conecta o hub de IoT tooyour dispositivos.</span><span class="sxs-lookup"><span data-stu-id="55b47-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="55b47-112">O que abordam os tutoriais de saudação</span><span class="sxs-lookup"><span data-stu-id="55b47-112">What hello tutorials cover</span></span>

<span data-ttu-id="55b47-113">Estes tutoriais apresentam tooAzure IoT Hub e o dispositivo Olá SDKs.</span><span class="sxs-lookup"><span data-stu-id="55b47-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="55b47-114">tutoriais de saudação abordam recursos comuns de IoT cenários toodemonstrate saudação do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="55b47-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="55b47-115">Olá tutoriais também ilustram como toocombine IoT Hub com outros Azure serviços e as ferramentas toobuild mais poderosas soluções de IoT.</span><span class="sxs-lookup"><span data-stu-id="55b47-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="55b47-116">Tutoriais de saudação, você pode escolher toouse os dispositivos IoT reais ou simulados.</span><span class="sxs-lookup"><span data-stu-id="55b47-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="55b47-117">Além disso, você pode aprender como toouse um hub IoT gateway tooenable dispositivos tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="55b47-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="55b47-118">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="55b47-118">Set up your device</span></span>

<span data-ttu-id="55b47-119">Conecte-se uma IoT dispositivo ou gateway tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="55b47-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="55b47-120">Você pode escolher um tooget do dispositivo físico ou simulada iniciado:</span><span class="sxs-lookup"><span data-stu-id="55b47-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="55b47-121">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="55b47-121">IoT device</span></span>                       | <span data-ttu-id="55b47-122">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="55b47-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="55b47-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="55b47-123">Raspberry Pi</span></span>                     | <span data-ttu-id="55b47-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="55b47-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="55b47-125">Kit de Desenvolvimento da IoT</span><span class="sxs-lookup"><span data-stu-id="55b47-125">IoT DevKit</span></span>                       | <span data-ttu-id="55b47-126">[Arduino no VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="55b47-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="55b47-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="55b47-127">Intel Edison</span></span>                     | <span data-ttu-id="55b47-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="55b47-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="55b47-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="55b47-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="55b47-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="55b47-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="55b47-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="55b47-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="55b47-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="55b47-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="55b47-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="55b47-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="55b47-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="55b47-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="55b47-135">Dispositivo simulado no computador</span><span class="sxs-lookup"><span data-stu-id="55b47-135">Simulated device on PC</span></span>           | <span data-ttu-id="55b47-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="55b47-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="55b47-137">Simulador de dispositivo online</span><span class="sxs-lookup"><span data-stu-id="55b47-137">Online device simulator</span></span>         | <span data-ttu-id="55b47-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="55b47-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="55b47-139">Além disso, você pode usar um hub IoT borda gateway tooenable dispositivos tooconnect tooyour IoT:</span><span class="sxs-lookup"><span data-stu-id="55b47-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="55b47-140">Dispositivos de gateway</span><span class="sxs-lookup"><span data-stu-id="55b47-140">Gateway device</span></span>               | <span data-ttu-id="55b47-141">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="55b47-141">Programming language</span></span> | <span data-ttu-id="55b47-142">Plataforma</span><span class="sxs-lookup"><span data-stu-id="55b47-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="55b47-143">Intel NUC (modelo DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="55b47-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="55b47-144">C</span><span class="sxs-lookup"><span data-stu-id="55b47-144">C</span></span>                    | <span data-ttu-id="55b47-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="55b47-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="55b47-146">Gateway simulado</span><span class="sxs-lookup"><span data-stu-id="55b47-146">Simulated gateway</span></span>            | <span data-ttu-id="55b47-147">C</span><span class="sxs-lookup"><span data-stu-id="55b47-147">C</span></span>                    | <span data-ttu-id="55b47-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="55b47-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

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
