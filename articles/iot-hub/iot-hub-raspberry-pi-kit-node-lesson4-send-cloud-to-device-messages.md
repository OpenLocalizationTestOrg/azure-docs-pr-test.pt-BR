---
featureFlags: usabilla
title: "Conecte-se framboesa Pi (nó) tooAzure IoT – lição 4: dispositivos de nuvem | Microsoft Docs"
description: "aplicativo de exemplo Hello executa em Pi e monitora mensagens de entrada de seu hub IoT. Uma nova tarefa gulp envia mensagens tooPi do seu Olá de tooblink de hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: nuvem toodevice, mensagem de nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="12f03-105">Executar mensagens de nuvem para dispositivo tooreceive do aplicativo de exemplo de hello</span><span class="sxs-lookup"><span data-stu-id="12f03-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="12f03-106">Neste artigo, implante um aplicativo de exemplo no Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="12f03-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="12f03-107">aplicativo de exemplo Hello monitora mensagens de entrada de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12f03-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="12f03-108">Você também executar uma tarefa de vez em seu tooPi de mensagens do computador toosend do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12f03-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="12f03-109">Quando o aplicativo de exemplo hello recebe mensagens de saudação, pisca Olá LED.</span><span class="sxs-lookup"><span data-stu-id="12f03-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="12f03-110">Se você tiver problemas, buscar soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="12f03-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="12f03-111">O que você fará</span><span class="sxs-lookup"><span data-stu-id="12f03-111">What you will do</span></span>
* <span data-ttu-id="12f03-112">Conecte-se o hub IoT do hello exemplo aplicativo tooyour.</span><span class="sxs-lookup"><span data-stu-id="12f03-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="12f03-113">Implante e execute o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="12f03-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="12f03-114">Envie mensagens de seu saudação do IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="12f03-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="12f03-115">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="12f03-115">What you will learn</span></span>
<span data-ttu-id="12f03-116">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="12f03-116">In this article, you will learn:</span></span>
* <span data-ttu-id="12f03-117">Como mensagens de entrada toomonitor do seu hub IoT</span><span class="sxs-lookup"><span data-stu-id="12f03-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="12f03-118">Como toosend de nuvem para dispositivo mensagens de seu tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12f03-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="12f03-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="12f03-119">What you need</span></span>
* <span data-ttu-id="12f03-120">Raspberry Pi 3, configuração para uso.</span><span class="sxs-lookup"><span data-stu-id="12f03-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="12f03-121">toolearn como tooset o Pi, consulte [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="12f03-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="12f03-122">Um hub IoT criado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="12f03-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="12f03-123">toolearn como toocreate seu hub IoT, consulte [criar o hub IoT e registrar framboesa Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="12f03-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="12f03-124">Conecte Olá exemplo aplicativo tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="12f03-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="12f03-125">Certifique-se de que você está na pasta do repositório de saudação `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="12f03-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="12f03-126">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f03-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="12f03-127">Saudação de aviso `app.js` arquivo hello `app` subpasta.</span><span class="sxs-lookup"><span data-stu-id="12f03-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="12f03-128">Olá `app.js` é arquivo de origem da chave de saudação que contém Olá código toomonitor mensagens de entrada de hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="12f03-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="12f03-129">Olá `blinkLED` função pisca Olá LED.</span><span class="sxs-lookup"><span data-stu-id="12f03-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Estrutura do repositório no aplicativo de exemplo hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="12f03-131">Inicialize o arquivo de configuração de saudação usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f03-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="12f03-132">Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) neste computador, todas as configurações de saudação são herdadas, para que você possa ignorar toohello tarefas de implantação e execução de aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="12f03-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="12f03-133">Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) em um computador diferente, você precisa espaços reservados Olá tooreplace Olá `config-raspberrypi.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="12f03-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="12f03-134">Olá `config-raspberrypi.json` arquivo está na subpasta de saudação da sua pasta base.</span><span class="sxs-lookup"><span data-stu-id="12f03-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Conteúdo do arquivo de configuração raspberrypi.json Olá](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="12f03-136">Substituir **[nome de host do dispositivo ou endereço IP]** com endereço IP hello Pi ou hello nome de host que você obtém executando Olá `devdisco list --eth` comando.</span><span class="sxs-lookup"><span data-stu-id="12f03-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="12f03-137">Substituir **[cadeia de conexão de dispositivo IoT]** com cadeia de conexão do dispositivo Olá obter executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="12f03-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="12f03-138">Substituir **[cadeia de conexão de hub IoT]** com hello cadeia de conexão de hub IoT que você obtém executando Olá `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.</span><span class="sxs-lookup"><span data-stu-id="12f03-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="12f03-139">Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.</span><span class="sxs-lookup"><span data-stu-id="12f03-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="12f03-140">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="12f03-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="12f03-141">Implantar e executar o aplicativo de exemplo hello em Pi executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f03-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="12f03-142">comando Olá implanta Olá tooPi de aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="12f03-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="12f03-143">Em seguida, ele é executado aplicativo hello Pi e uma tarefa separada em seu host tooPi de mensagens do computador toosend 20 intermitência de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12f03-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="12f03-144">Depois que o aplicativo de exemplo hello é executado, ele inicia a escuta toomessages do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12f03-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="12f03-145">Enquanto isso, a tarefa de gulp de saudação envia várias mensagens de "intermitência" de seu tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12f03-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="12f03-146">Para cada mensagem de intermitência que recebe de Pi, o aplicativo de exemplo hello chama Olá `blinkLED` Olá tooblink de função LED.</span><span class="sxs-lookup"><span data-stu-id="12f03-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="12f03-147">Você deve ver intermitência de LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens de seu tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12f03-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="12f03-148">Olá última um é uma mensagem "stop" que informa Olá toostop de aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="12f03-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![Exemplo de aplicativo com o comando gulp e mensagens de piscar](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="12f03-150">Resumo</span><span class="sxs-lookup"><span data-stu-id="12f03-150">Summary</span></span>
<span data-ttu-id="12f03-151">Você enviou com êxito as mensagens de seu saudação do IoT hub tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="12f03-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="12f03-152">Olá próxima tarefa é opcional: altere Olá ativa e desativa o comportamento de saudação LED.</span><span class="sxs-lookup"><span data-stu-id="12f03-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12f03-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12f03-153">Next steps</span></span>
[<span data-ttu-id="12f03-154">Alterar Olá ativa e desativa o comportamento de saudação LED</span><span class="sxs-lookup"><span data-stu-id="12f03-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

