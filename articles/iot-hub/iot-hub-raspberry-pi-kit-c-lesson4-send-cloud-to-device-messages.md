---
title: "Conectar Raspberry Pi (C) ao IoT do Azure – Lição 4: nuvem para o dispositivo | Microsoft Docs"
description: "Um aplicativo de exemplo é executado em seu Pi e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens para seu Pi de seu Hub IoT para piscar o LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: nuvem para o dispositivo, mensagem da nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="13d17-105">Executar um aplicativo de exemplo para receber mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="13d17-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="13d17-106">Neste artigo, implante um aplicativo de exemplo no Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="13d17-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="13d17-107">O aplicativo de exemplo monitora mensagens recebidas do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="13d17-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="13d17-108">Você também executa uma tarefa gulp no computador para enviar mensagens para o Pi do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="13d17-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="13d17-109">Quando o aplicativo de exemplo recebe uma a mensagem, ele pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="13d17-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="13d17-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="13d17-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="13d17-111">O que você fará</span><span class="sxs-lookup"><span data-stu-id="13d17-111">What you will do</span></span>
* <span data-ttu-id="13d17-112">Conectar o aplicativo de exemplo ao hub IoT.</span><span class="sxs-lookup"><span data-stu-id="13d17-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="13d17-113">Implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="13d17-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="13d17-114">Enviar mensagens do hub IoT para o Pi para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="13d17-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="13d17-115">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="13d17-115">What you will learn</span></span>
<span data-ttu-id="13d17-116">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="13d17-116">In this article, you will learn:</span></span>
* <span data-ttu-id="13d17-117">Como monitorar mensagens recebidas do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="13d17-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="13d17-118">Como enviar mensagens de nuvem para dispositivo do hub IoT para o Pi.</span><span class="sxs-lookup"><span data-stu-id="13d17-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="13d17-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="13d17-119">What you need</span></span>
* <span data-ttu-id="13d17-120">Raspberry Pi 3, configuração para uso.</span><span class="sxs-lookup"><span data-stu-id="13d17-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="13d17-121">Para saber como configurar o Pi, consulte [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="13d17-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="13d17-122">Um hub IoT criado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="13d17-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="13d17-123">Para saber como criar seu Hub IoT, consulte [Criar seu Hub IoT e registrar o Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="13d17-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="13d17-124">Conectar o aplicativo de exemplo ao Hub IoT</span><span class="sxs-lookup"><span data-stu-id="13d17-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="13d17-125">Verifique se você está na pasta de repositório `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="13d17-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="13d17-126">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="13d17-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="13d17-127">Observe o arquivo `app.c` na subpasta `app`.</span><span class="sxs-lookup"><span data-stu-id="13d17-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="13d17-128">O arquivo `app.c` é o arquivo de origem principal que contém o código para monitorar mensagens recebidas do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="13d17-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="13d17-129">A função `blinkLED` pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="13d17-129">The `blinkLED` function blinks the LED.</span></span>

   ![Estrutura do repositório no aplicativo de exemplo](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="13d17-131">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="13d17-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="13d17-132">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de funções do Azure](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) neste computador, todas as configurações serão herdadas, portanto você pode pular para a etapa da tarefa de implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="13d17-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="13d17-133">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de função do Azure](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) em um computador diferente, será necessário substituir os espaços reservados no arquivo `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="13d17-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="13d17-134">O arquivo `config-raspberrypi.json` está na subpasta da pasta base.</span><span class="sxs-lookup"><span data-stu-id="13d17-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![Conteúdo do arquivo config-raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="13d17-136">Substitua **[nome de host ou endereço IP do dispositivo]** pelo nome de host ou o endereço IP do Pi obtido executando o comando `devdisco list --eth`.</span><span class="sxs-lookup"><span data-stu-id="13d17-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="13d17-137">Substitua **[cadeia de conexão do dispositivo IoT]** pela cadeia de conexão do dispositivo que você obtém executando o comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="13d17-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="13d17-138">Substitua **[cadeia de conexão do hub IoT]** pela cadeia de conexão do hub IoT que você obtém executando o comando `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="13d17-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="13d17-139">Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.</span><span class="sxs-lookup"><span data-stu-id="13d17-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="13d17-140">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="13d17-140">Deploy and run the sample application</span></span>
<span data-ttu-id="13d17-141">Implante e execute o aplicativo de exemplo no Pi executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="13d17-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="13d17-142">O comando gulp executa a tarefa install-tools primeiro.</span><span class="sxs-lookup"><span data-stu-id="13d17-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="13d17-143">Em seguida, ele implanta o aplicativo de exemplo para o Pi.</span><span class="sxs-lookup"><span data-stu-id="13d17-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="13d17-144">Por fim, ele executa o aplicativo no Pi e uma tarefa separada no computador host para enviar 20 mensagens de piscar para o Pi do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="13d17-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="13d17-145">Após a execução, o aplicativo de exemplo começa a escutar as mensagens do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="13d17-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="13d17-146">Enquanto isso, a tarefa gulp envia várias mensagens de "piscar" do Hub IoT para o Pi.</span><span class="sxs-lookup"><span data-stu-id="13d17-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="13d17-147">Para cada mensagem de piscar recebida, o aplicativo de exemplo chama a função `blinkLED` para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="13d17-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="13d17-148">Você deve ver o LED piscar a cada dois segundos, uma vez que a tarefa gulp está enviando 20 mensagens do Hub IoT ao Pi.</span><span class="sxs-lookup"><span data-stu-id="13d17-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="13d17-149">A última é uma mensagem de “parar” que interrompe a execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="13d17-149">The last one is a "stop" message that stops the application from running.</span></span>

![Exemplo de aplicativo com o comando gulp e mensagens de piscar](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="13d17-151">Resumo</span><span class="sxs-lookup"><span data-stu-id="13d17-151">Summary</span></span>
<span data-ttu-id="13d17-152">Você enviou com êxito mensagens do Hub IoT para o Pi para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="13d17-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="13d17-153">A próxima tarefa é opcional: alterar o comportamento de liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="13d17-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13d17-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13d17-154">Next steps</span></span>
[<span data-ttu-id="13d17-155">Alterar o comportamento de ligar e desligar do LED</span><span class="sxs-lookup"><span data-stu-id="13d17-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
