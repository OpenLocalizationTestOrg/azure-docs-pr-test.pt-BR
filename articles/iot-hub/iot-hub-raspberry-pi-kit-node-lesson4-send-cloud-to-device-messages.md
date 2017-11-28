---
featureFlags: usabilla
title: "Conectar o Raspberry Pi (Nó) ao IoT do Azure - Lição 4: nuvem para o dispositivo | Microsoft Docs"
description: "O aplicativo de exemplo é executado em seu Pi e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens para seu Pi de seu Hub IoT para piscar o LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: nuvem para o dispositivo, mensagem da nuvem
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
ms.openlocfilehash: b8e9e51391f9b6737762b3404658297ab4c82783
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-the-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="af3d6-105">Executar o aplicativo de exemplo para receber mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="af3d6-105">Run the sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="af3d6-106">Neste artigo, implante um aplicativo de exemplo no Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="af3d6-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="af3d6-107">O aplicativo de exemplo monitora mensagens recebidas do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="af3d6-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="af3d6-108">Você também executa uma tarefa gulp no computador para enviar mensagens para o Pi do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="af3d6-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="af3d6-109">Quando o aplicativo de exemplo recebe uma a mensagem, ele pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="af3d6-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="af3d6-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="af3d6-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="af3d6-111">O que você fará</span><span class="sxs-lookup"><span data-stu-id="af3d6-111">What you will do</span></span>
* <span data-ttu-id="af3d6-112">Conectar o aplicativo de exemplo ao hub IoT.</span><span class="sxs-lookup"><span data-stu-id="af3d6-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="af3d6-113">Implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="af3d6-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="af3d6-114">Enviar mensagens do hub IoT para o Pi para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="af3d6-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="af3d6-115">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="af3d6-115">What you will learn</span></span>
<span data-ttu-id="af3d6-116">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="af3d6-116">In this article, you will learn:</span></span>
* <span data-ttu-id="af3d6-117">Como monitorar mensagens recebidas do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="af3d6-117">How to monitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="af3d6-118">Como enviar mensagens de nuvem para dispositivo do hub IoT para o Pi.</span><span class="sxs-lookup"><span data-stu-id="af3d6-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="af3d6-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="af3d6-119">What you need</span></span>
* <span data-ttu-id="af3d6-120">Raspberry Pi 3, configuração para uso.</span><span class="sxs-lookup"><span data-stu-id="af3d6-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="af3d6-121">Para saber como configurar o Pi, consulte [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="af3d6-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="af3d6-122">Um hub IoT criado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="af3d6-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="af3d6-123">Para saber como criar seu Hub IoT, consulte [Criar seu Hub IoT e registrar o Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="af3d6-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="af3d6-124">Conectar o aplicativo de exemplo ao Hub IoT</span><span class="sxs-lookup"><span data-stu-id="af3d6-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="af3d6-125">Verifique se você está na pasta de repositório `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="af3d6-125">Make sure that you're in the repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="af3d6-126">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="af3d6-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="af3d6-127">Observe o arquivo `app.js` na subpasta `app`.</span><span class="sxs-lookup"><span data-stu-id="af3d6-127">Notice the `app.js` file in the `app` subfolder.</span></span> <span data-ttu-id="af3d6-128">O arquivo `app.js` é o arquivo de origem principal que contém o código para monitorar mensagens recebidas do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="af3d6-128">The `app.js` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="af3d6-129">A função `blinkLED` pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="af3d6-129">The `blinkLED` function blinks the LED.</span></span>
   
   ![Estrutura do repositório no aplicativo de exemplo](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="af3d6-131">Inicialize o arquivo de configuração usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="af3d6-131">Initialize the configuration file by using the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="af3d6-132">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) neste computador, todas as configurações serão herdadas, portanto você pode ignorar a tarefa de implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="af3d6-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to the task of deploying and running the sample application.</span></span> <span data-ttu-id="af3d6-133">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) em um computador diferente, será necessário substituir os espaços reservados no arquivo `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="af3d6-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="af3d6-134">O arquivo `config-raspberrypi.json` está na subpasta da pasta base.</span><span class="sxs-lookup"><span data-stu-id="af3d6-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>
   
   ![Conteúdo do arquivo config-raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="af3d6-136">Substitua **[nome de host ou endereço IP do dispositivo]** pelo endereço IP do Pi ou o nome de host que você obtém executando o comando `devdisco list --eth`.</span><span class="sxs-lookup"><span data-stu-id="af3d6-136">Replace **[device hostname or IP address]** with the IP address of Pi or the host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="af3d6-137">Substitua **[cadeia de conexão do dispositivo IoT]** pela cadeia de conexão do dispositivo que você obtém executando o comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="af3d6-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="af3d6-138">Substitua **[cadeia de conexão do hub IoT]** pela cadeia de conexão do hub IoT que você obtém executando o comando `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="af3d6-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="af3d6-139">Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.</span><span class="sxs-lookup"><span data-stu-id="af3d6-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="af3d6-140">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="af3d6-140">Deploy and run the sample application</span></span>
<span data-ttu-id="af3d6-141">Implante e execute o aplicativo de exemplo no Pi executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="af3d6-141">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="af3d6-142">O comando implanta o aplicativo de exemplo para o Pi.</span><span class="sxs-lookup"><span data-stu-id="af3d6-142">The command deploys the sample application to Pi.</span></span> <span data-ttu-id="af3d6-143">Em seguida, ele executa o aplicativo no Pi e uma tarefa separada no computador host para enviar 20 mensagens de piscar para o Pi do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="af3d6-143">Then, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="af3d6-144">Após a execução, o aplicativo de exemplo começa a escutar as mensagens do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="af3d6-144">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="af3d6-145">Enquanto isso, a tarefa gulp envia várias mensagens de "piscar" do Hub IoT para o Pi.</span><span class="sxs-lookup"><span data-stu-id="af3d6-145">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="af3d6-146">Para cada mensagem de piscar recebida, o aplicativo de exemplo chama a função `blinkLED` para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="af3d6-146">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="af3d6-147">Você deve ver o LED piscar a cada dois segundos, uma vez que a tarefa gulp está enviando 20 mensagens do Hub IoT ao Pi.</span><span class="sxs-lookup"><span data-stu-id="af3d6-147">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="af3d6-148">A última é uma mensagem de “parar” que diz para o aplicativo interromper a execução.</span><span class="sxs-lookup"><span data-stu-id="af3d6-148">The last one is a "stop" message that tells the application to stop running.</span></span>

![Exemplo de aplicativo com o comando gulp e mensagens de piscar](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="af3d6-150">Resumo</span><span class="sxs-lookup"><span data-stu-id="af3d6-150">Summary</span></span>
<span data-ttu-id="af3d6-151">Você enviou com êxito mensagens do Hub IoT para o Pi para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="af3d6-151">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="af3d6-152">A próxima tarefa é opcional: alterar o comportamento de liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="af3d6-152">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af3d6-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af3d6-153">Next steps</span></span>
[<span data-ttu-id="af3d6-154">Alterar o comportamento de ligar e desligar do LED</span><span class="sxs-lookup"><span data-stu-id="af3d6-154">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

