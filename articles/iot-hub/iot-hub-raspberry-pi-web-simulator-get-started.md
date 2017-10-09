---
title: aaaSimulated framboesa Pi toocloud (Node. js) - conectar framboesa Pi web simulador tooAzure IoT Hub | Microsoft Docs
description: Conecte-se tooAzure simulador de web Pi framboesa IoT Hub para Pi framboesa toosend dados toohello nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi framboesa simulador, azure iot framboesa pi, framboesa pi iot hub pi framboesa enviar dados toocloud, framboesa pi toocloud
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="f0d9f-104">Conecte-se framboesa Pi online simulador tooAzure IoT Hub (Node. js)</span><span class="sxs-lookup"><span data-stu-id="f0d9f-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="f0d9f-105">Neste tutorial, você começar a aprender Noções básicas de saudação de trabalhar com o simulador online framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="f0d9f-106">Em seguida, você aprenderá como tooseamlessly se conectam a nuvem de toohello Olá Pi simulador usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f0d9f-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="f0d9f-107">Se você tiver dispositivos físicos, visite [tooAzure conectar framboesa Pi IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="f0d9f-108">O que fazer</span><span class="sxs-lookup"><span data-stu-id="f0d9f-108">What you do</span></span>

* <span data-ttu-id="f0d9f-109">Conheça os fundamentos de saudação do simulator online framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="f0d9f-110">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-110">Create an IoT hub.</span></span>
* <span data-ttu-id="f0d9f-111">Registre um dispositivo para o Pi em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="f0d9f-112">Execute um aplicativo de exemplo em dados de sensor do Pi toosend simulado tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="f0d9f-113">Conecte o hub de IoT simulada de tooan de framboesa Pi que você criar.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="f0d9f-114">Em seguida, você executar um aplicativo de exemplo com os dados do sensor toogenerate Olá simulador.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="f0d9f-115">Por fim, você pode enviar hub IoT do hello sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="f0d9f-116">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f0d9f-116">What you learn</span></span>

* <span data-ttu-id="f0d9f-117">Como toocreate um hub IoT do Azure e obter sua nova cadeia de caracteres de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="f0d9f-118">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f0d9f-119">Como toowork com o simulador online framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="f0d9f-120">Como hub IoT do toosend sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="f0d9f-121">Visão geral do simulador de web do Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="f0d9f-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="f0d9f-122">Clique em simulador on-line do hello botão toolaunch framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="f0d9f-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Iniciar o simulador do Raspberry Pi</a></span><span class="sxs-lookup"><span data-stu-id="f0d9f-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="f0d9f-124">Há três áreas no simulador do Olá web.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-124">There are three areas in hello web simulator.</span></span>
1. <span data-ttu-id="f0d9f-125">Área do assembly - circuito do saudação padrão é que um Pi se conecta com um sensor BME280 e um LED.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="f0d9f-126">área de saudação é bloqueada na versão de visualização assim no momento você não pode fazer a personalização.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="f0d9f-127">Codificação área - um editor de código online para você toocode com framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="f0d9f-128">aplicativo de exemplo Hello padrão ajuda a toocollect os dados do sensor do sensor BME280 e envia tooyour Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="f0d9f-129">aplicativo Hello é totalmente compatível com dispositivos de Pi reais.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-129">hello application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="f0d9f-130">Janela de console integrado - ele mostra a saída de saudação do seu código.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="f0d9f-131">Na parte superior do hello desta janela, há três botões.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="f0d9f-132">**Executar** -executar o aplicativo hello em Olá codificação área.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="f0d9f-133">**Redefinir** -Olá de redefinição de aplicativo de exemplo área toohello padrão de codificação.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="f0d9f-134">**Dobra/expandir** - nas Olá direita lado existe é um botão para você toofold/expanda Olá janela do console.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="f0d9f-135">simulador de web Pi framboesa Olá agora está disponível na versão de visualização.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="f0d9f-136">Gostaríamos toohear sua voz Olá [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="f0d9f-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="f0d9f-137">código-fonte Olá é público no [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="f0d9f-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Visão geral do simulador online de Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="f0d9f-139">Executar um aplicativo de exemplo no simulador de web Pi</span><span class="sxs-lookup"><span data-stu-id="f0d9f-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="f0d9f-140">Na área de codificação, verifique se que você estiver trabalhando no aplicativo de exemplo hello padrão.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="f0d9f-141">Substitua o espaço reservado de saudação em 15 de linha com hello cadeia de conexão de dispositivo de hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="f0d9f-142">![Substitua a cadeia de caracteres de conexão de dispositivo Olá](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="f0d9f-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="f0d9f-143">Clique em **executar** ou tipo `npm start` toorun aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="f0d9f-144">Você deve ver a saída de hello a seguir que mostra dados de sensor hello e mensagens de saudação enviadas tooyour IoT hub ![saída - dados de sensor enviados do hub de IoT tooyour framboesa Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="f0d9f-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="f0d9f-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0d9f-145">Next steps</span></span>

<span data-ttu-id="f0d9f-146">Executar dados de sensor de toocollect do aplicativo de exemplo e enviá-lo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f0d9f-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
