---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 4: receber mensagens | Microsoft Docs"
description: "Um aplicativo de exemplo é executado no Edison e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens tooEdison do seu Olá de tooblink de hub IoT LED."
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
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="a770e-105">Executar um tooreceive do aplicativo de exemplo mensagens de nuvem para dispositivo</span><span class="sxs-lookup"><span data-stu-id="a770e-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="a770e-106">Neste artigo, você implanta um aplicativo de exemplo no Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="a770e-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="a770e-107">aplicativo de exemplo Hello monitora mensagens de entrada de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="a770e-108">Você também executar uma tarefa de vez em seu tooEdison de mensagens do computador toosend do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="a770e-109">Quando o aplicativo de exemplo hello recebe mensagens de saudação, pisca Olá LED.</span><span class="sxs-lookup"><span data-stu-id="a770e-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="a770e-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a770e-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a770e-111">O que você fará</span><span class="sxs-lookup"><span data-stu-id="a770e-111">What you will do</span></span>
* <span data-ttu-id="a770e-112">Conecte-se o hub IoT do hello exemplo aplicativo tooyour.</span><span class="sxs-lookup"><span data-stu-id="a770e-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="a770e-113">Implante e execute o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="a770e-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="a770e-114">Envie mensagens de seu saudação do IoT hub tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="a770e-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a770e-115">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="a770e-115">What you will learn</span></span>
<span data-ttu-id="a770e-116">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="a770e-116">In this article, you will learn:</span></span>
* <span data-ttu-id="a770e-117">Como toomonitor de mensagens de entrada do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="a770e-118">Como toosend de nuvem para dispositivo mensagens de seu tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a770e-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="a770e-119">What you need</span></span>
* <span data-ttu-id="a770e-120">Intel Edison, configurado para uso.</span><span class="sxs-lookup"><span data-stu-id="a770e-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="a770e-121">toolearn como tooset backup Edison, consulte [configurar seu dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="a770e-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="a770e-122">Um hub IoT criado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a770e-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="a770e-123">toolearn como toocreate seu hub IoT, consulte [criar o Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="a770e-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="a770e-124">Conecte Olá exemplo aplicativo tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="a770e-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="a770e-125">Certifique-se de que você está na pasta do repositório de saudação `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="a770e-125">Make sure that you're in hello repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="a770e-126">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a770e-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="a770e-127">arquivo Olá Olá `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toomonitor mensagens de entrada de hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="a770e-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="a770e-128">Olá `blinkLED` função pisca Olá LED.</span><span class="sxs-lookup"><span data-stu-id="a770e-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Estrutura do repositório no aplicativo de exemplo hello][repo-structure]
2. <span data-ttu-id="a770e-130">Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a770e-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="a770e-131">Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] neste computador, todas as configurações de saudação são herdadas, portanto você pode ignorar a tarefa de toohello Olá etapa de implantação e executando o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="a770e-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="a770e-132">Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] em um computador diferente, você precisa espaços reservados Olá tooreplace Olá `config-edison.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a770e-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="a770e-133">Olá `config-edison.json` arquivo está na subpasta de saudação da sua pasta base.</span><span class="sxs-lookup"><span data-stu-id="a770e-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Conteúdo do arquivo de configuração edison.json Olá](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="a770e-135">Substituir **[nome de host do dispositivo ou endereço IP]** com endereço IP do dispositivo Olá marcado para baixo, quando você configurou seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a770e-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="a770e-136">Substituir **[cadeia de conexão de dispositivo IoT]** com cadeia de conexão do dispositivo Olá obter executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.</span><span class="sxs-lookup"><span data-stu-id="a770e-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="a770e-137">Substituir **[cadeia de conexão de hub IoT]** com hello cadeia de conexão de hub IoT que você obtém executando Olá `az iot hub show-connection-string --name {my hub name}` comando.</span><span class="sxs-lookup"><span data-stu-id="a770e-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="a770e-138">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="a770e-138">Deploy and run hello sample application</span></span>
<span data-ttu-id="a770e-139">Implantar e executar o aplicativo de exemplo hello Edison executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a770e-139">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="a770e-140">comando de gulp Olá implanta Olá tooEdison de aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a770e-140">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="a770e-141">Em seguida, ele é executado aplicativo hello Edison e uma tarefa separada em seu host tooEdison de mensagens do computador toosend 20 intermitência de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-141">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="a770e-142">Depois que o aplicativo de exemplo hello é executado, ele inicia a escuta toomessages do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-142">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="a770e-143">Enquanto isso, a tarefa de gulp de saudação envia várias mensagens de "intermitência" de seu tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-143">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="a770e-144">Para cada mensagem de intermitência Edison recebe, o aplicativo de exemplo hello chama Olá `blinkLED` Olá tooblink de função LED.</span><span class="sxs-lookup"><span data-stu-id="a770e-144">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="a770e-145">Você deve ver intermitência de LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens de seu tooEdison de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a770e-145">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="a770e-146">Hello última um é uma mensagem "stop" que interrompe a execução do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a770e-146">hello last one is a "stop" message that stops hello application from running.</span></span>

![Exemplo de aplicativo com o comando gulp e mensagens de piscar][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="a770e-148">Resumo</span><span class="sxs-lookup"><span data-stu-id="a770e-148">Summary</span></span>
<span data-ttu-id="a770e-149">Você enviou com êxito as mensagens de seu saudação do IoT hub tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="a770e-149">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="a770e-150">Olá próxima tarefa é opcional: altere Olá ativa e desativa o comportamento de saudação LED.</span><span class="sxs-lookup"><span data-stu-id="a770e-150">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a770e-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a770e-151">Next steps</span></span>
<span data-ttu-id="a770e-152">[Alterar Olá ativa e desativa o comportamento de saudação LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="a770e-152">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md