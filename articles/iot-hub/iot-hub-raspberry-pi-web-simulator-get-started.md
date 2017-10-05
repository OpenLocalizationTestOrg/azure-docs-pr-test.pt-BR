---
title: "Raspberry Pi simulado para nuvem (Node.js) – Conectar o simulador web Raspberry Pi ao Hub IoT do Azure | Microsoft Docs"
description: Conectar o simulador web Raspberry Pi ao Hub IoT do Azure para que o Raspberry Pi envie dados para a nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: simulador raspberry pi, raspberry pi azure iot, hub iot raspberry pi, raspberry pi enviar dados para a nuvem, raspberry pi para nuvem
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 3b80bf35d6af91d5bdb196d97668dc0f837b92cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="73ff3-104">Conectar o simulador online Raspberry Pi ao Hub IoT do Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="73ff3-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="73ff3-105">Neste tutorial, você começará aprendendo as noções básicas de como trabalhar com o simulador online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="73ff3-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="73ff3-106">Em seguida, aprenderá a conectar o simulador Pi diretamente à nuvem usando o [Hub IoT do Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="73ff3-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="73ff3-107">Se você tiver dispositivos físicos, visite [Conectar ao Raspberry Pi ao Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) para começar.</span><span class="sxs-lookup"><span data-stu-id="73ff3-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="73ff3-108">O que fazer</span><span class="sxs-lookup"><span data-stu-id="73ff3-108">What you do</span></span>

* <span data-ttu-id="73ff3-109">Conheça os fundamentos do simulador online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="73ff3-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="73ff3-110">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73ff3-110">Create an IoT hub.</span></span>
* <span data-ttu-id="73ff3-111">Registre um dispositivo para o Pi em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73ff3-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="73ff3-112">Execute um aplicativo de exemplo no Pi para enviar os dados do sensor simulado para o seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73ff3-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="73ff3-113">Conecte o Raspberry Pi simulado a um Hub IoT criado por você.</span><span class="sxs-lookup"><span data-stu-id="73ff3-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="73ff3-114">Em seguida, você deve executar um aplicativo de exemplo com o simulador para gerar dados de sensor.</span><span class="sxs-lookup"><span data-stu-id="73ff3-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="73ff3-115">Por fim, você envia os dados do sensor para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73ff3-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="73ff3-116">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="73ff3-116">What you learn</span></span>

* <span data-ttu-id="73ff3-117">Como criar um Hub IoT do Azure e obter sua nova cadeia de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="73ff3-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="73ff3-118">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="73ff3-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="73ff3-119">Como trabalhar com o Simulador online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="73ff3-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="73ff3-120">Como enviar dados de sensor ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73ff3-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="73ff3-121">Visão geral do simulador de web do Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="73ff3-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="73ff3-122">Clique no botão para iniciar o simulador online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="73ff3-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="73ff3-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Iniciar o simulador do Raspberry Pi</a></span><span class="sxs-lookup"><span data-stu-id="73ff3-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="73ff3-124">Há três áreas no simulador da web.</span><span class="sxs-lookup"><span data-stu-id="73ff3-124">There are three areas in the web simulator.</span></span>
1. <span data-ttu-id="73ff3-125">Área do assembly - O circuito padrão é que um Pi se conecta com um sensor BME280 e um LED.</span><span class="sxs-lookup"><span data-stu-id="73ff3-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="73ff3-126">A área é bloqueada na versão prévia assim no momento você não pode fazer a personalização.</span><span class="sxs-lookup"><span data-stu-id="73ff3-126">The area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="73ff3-127">Codificação área - Um editor de código online para você no código com Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="73ff3-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="73ff3-128">O aplicativo de exemplo padrão ajuda a coletar dados de sensor do sensor BME280 e envia para o Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="73ff3-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="73ff3-129">O aplicativo é totalmente compatível com dispositivos de Pi reais.</span><span class="sxs-lookup"><span data-stu-id="73ff3-129">The application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="73ff3-130">Janela de console integrado - Mostra a saída do seu código.</span><span class="sxs-lookup"><span data-stu-id="73ff3-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="73ff3-131">Na parte superior da janela, há três botões.</span><span class="sxs-lookup"><span data-stu-id="73ff3-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="73ff3-132">**Executar** - Executar o aplicativo na área de codificação.</span><span class="sxs-lookup"><span data-stu-id="73ff3-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="73ff3-133">**Redefinir** - Redefinir a área de codificação para o aplicativo de exemplo padrão.</span><span class="sxs-lookup"><span data-stu-id="73ff3-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="73ff3-134">**Dobrar/expandir** - No lado direito, há um botão para a dobrar/expandir a janela do console.</span><span class="sxs-lookup"><span data-stu-id="73ff3-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="73ff3-135">O simulador de web do Raspberry Pi agora está disponível na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="73ff3-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="73ff3-136">Gostaríamos de ouvir sua voz no [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="73ff3-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="73ff3-137">O código-fonte é público no [GitHub](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="73ff3-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Visão geral do simulador online de Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="73ff3-139">Executar um aplicativo de exemplo no simulador de web Pi</span><span class="sxs-lookup"><span data-stu-id="73ff3-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="73ff3-140">Na área de codificação, verifique se você está trabalhando no aplicativo de exemplo padrão.</span><span class="sxs-lookup"><span data-stu-id="73ff3-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="73ff3-141">Substitua o espaço reservado na Linha 15 com cadeia de conexão do dispositivo do Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="73ff3-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="73ff3-142">![Substitua a cadeia de conexão do dispositivo](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="73ff3-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="73ff3-143">Clique em **Executar** ou digite `npm start` para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73ff3-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="73ff3-144">Você deverá ver a seguinte saída, mostrando os dados do sensor e as mensagens que são enviadas ao seu Hub IoT ![saída - dados de sensor enviados do Raspberry Pi para o seu Hub IoT](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="73ff3-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="73ff3-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73ff3-145">Next steps</span></span>

<span data-ttu-id="73ff3-146">Você executou um aplicativo de exemplo para coletar dados de sensor e enviá-los ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="73ff3-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
