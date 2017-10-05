---
title: "Conectar o Intel Edison (Nó) ao IoT do Azure - Lição 4: receber mensagens| Microsoft Docs"
description: "Um aplicativo de exemplo é executado no Edison e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens para o Edison de seu Hub IoT para piscar o LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: controlar led pela web com arduino, controlar led via web com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="0aefb-105">Executar um aplicativo de exemplo para receber mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="0aefb-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="0aefb-106">Neste artigo, você implanta um aplicativo de exemplo no Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="0aefb-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="0aefb-107">O aplicativo de exemplo monitora mensagens recebidas do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0aefb-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="0aefb-108">Você também executa uma tarefa gulp no computador para enviar mensagens para o Edison do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0aefb-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="0aefb-109">Quando o aplicativo de exemplo recebe uma a mensagem, ele pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="0aefb-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="0aefb-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="0aefb-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0aefb-111">O que você fará</span><span class="sxs-lookup"><span data-stu-id="0aefb-111">What you will do</span></span>
* <span data-ttu-id="0aefb-112">Conectar o aplicativo de exemplo ao hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0aefb-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="0aefb-113">Implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0aefb-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="0aefb-114">Enviar mensagens do Hub IoT para o Edison para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="0aefb-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0aefb-115">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="0aefb-115">What you will learn</span></span>
<span data-ttu-id="0aefb-116">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="0aefb-116">In this article, you will learn:</span></span>
* <span data-ttu-id="0aefb-117">Como monitorar mensagens recebidas do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0aefb-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="0aefb-118">Como enviar mensagens da nuvem para o dispositivo do Hub IoT para o Edison.</span><span class="sxs-lookup"><span data-stu-id="0aefb-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0aefb-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="0aefb-119">What you need</span></span>
* <span data-ttu-id="0aefb-120">Intel Edison, configurado para uso.</span><span class="sxs-lookup"><span data-stu-id="0aefb-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="0aefb-121">Para saber como configurar o Edison, consulte [Configurar seu dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="0aefb-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="0aefb-122">Um hub IoT criado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0aefb-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="0aefb-123">Para aprender a criar seu Hub IoT, consulte [Criar seu Hub IoT do Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="0aefb-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="0aefb-124">Conectar o aplicativo de exemplo ao Hub IoT</span><span class="sxs-lookup"><span data-stu-id="0aefb-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="0aefb-125">Verifique se você está na pasta de repositório `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="0aefb-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="0aefb-126">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0aefb-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="0aefb-127">O arquivo na subpasta `app` é o arquivo de origem principal que contém o código para monitorar mensagens recebidas do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0aefb-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="0aefb-128">A função `blinkLED` pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="0aefb-128">The `blinkLED` function blinks the LED.</span></span>

   ![Estrutura do repositório no aplicativo de exemplo][repo-structure]
2. <span data-ttu-id="0aefb-130">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0aefb-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="0aefb-131">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de funções do Azure][create-an-azure-function-app-and-storage-account] neste computador, todas as configurações serão herdadas, portanto você pode ignorar a tarefa de implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0aefb-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="0aefb-132">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de funções do Azure][create-an-azure-function-app-and-storage-account] em um computador diferente, será necessário substituir os espaços reservados no arquivo `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="0aefb-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="0aefb-133">O arquivo `config-edison.json` está na subpasta da pasta base.</span><span class="sxs-lookup"><span data-stu-id="0aefb-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Conteúdo do arquivo config-edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="0aefb-135">Substitua **[nome de host ou endereço IP do dispositivo]** pelo endereço IP do dispositivo que você marcou quando configurou seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0aefb-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="0aefb-136">Substitua **[cadeia de conexão do dispositivo IoT]** pela cadeia de conexão do dispositivo que você obtém executando o comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="0aefb-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="0aefb-137">Substitua **[cadeia de conexão do hub IoT]** pela cadeia de conexão do hub IoT que você obtém executando o comando `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="0aefb-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="0aefb-138">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="0aefb-138">Deploy and run the sample application</span></span>
<span data-ttu-id="0aefb-139">Implante e execute o aplicativo de exemplo no Edison executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0aefb-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="0aefb-140">O comando gulp implanta o aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="0aefb-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="0aefb-141">Em seguida, ele executa o aplicativo no Edison e uma tarefa separada no computador host para enviar 20 mensagens de piscar para o Edison do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0aefb-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="0aefb-142">Após a execução, o aplicativo de exemplo começa a escutar as mensagens do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0aefb-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="0aefb-143">Enquanto isso, a tarefa gulp envia várias mensagens de "piscar" do Hub IoT para o Edison.</span><span class="sxs-lookup"><span data-stu-id="0aefb-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="0aefb-144">Para cada mensagem de piscar recebida pelo Edison, o aplicativo de exemplo chama a função `blinkLED` para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="0aefb-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="0aefb-145">Você deve ver o LED piscar a cada dois segundos, uma vez que a tarefa gulp envia 20 mensagens do Hub IoT ao Edison.</span><span class="sxs-lookup"><span data-stu-id="0aefb-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="0aefb-146">A última é uma mensagem de “parar” que interrompe a execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0aefb-146">The last one is a "stop" message that stops the application from running.</span></span>

![Exemplo de aplicativo com o comando gulp e mensagens de piscar][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="0aefb-148">Resumo</span><span class="sxs-lookup"><span data-stu-id="0aefb-148">Summary</span></span>
<span data-ttu-id="0aefb-149">Você enviou com êxito mensagens do Hub IoT para o Edison para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="0aefb-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="0aefb-150">A próxima tarefa é opcional: alterar o comportamento de liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="0aefb-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aefb-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0aefb-151">Next steps</span></span>
<span data-ttu-id="0aefb-152">[Alterar o comportamento de ligar e desligar do LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="0aefb-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md