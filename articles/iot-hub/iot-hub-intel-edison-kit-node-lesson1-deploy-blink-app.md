---
title: "Conecte-se Edison Intel (nó) tooAzure IoT - lição 1: implantar o aplicativo | Microsoft Docs"
description: "Clonar um aplicativo de exemplo C de saudação do GitHub e execute gulp toodeploy tooyour esse aplicativo placa Edison Intel. Este aplicativo de exemplo pisca Olá LED conectado toohello placa a cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projetos led arduino, piscar led arduino, código piscar led arduino, programa de piscar arduino, exemplo de piscar arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="c10c1-105">Criar e implantar o aplicativo de intermitência hello</span><span class="sxs-lookup"><span data-stu-id="c10c1-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c10c1-106">O que você fará</span><span class="sxs-lookup"><span data-stu-id="c10c1-106">What you will do</span></span>
<span data-ttu-id="c10c1-107">Clonar o aplicativo de exemplo C de saudação do GitHub e usar Olá gulp ferramenta toodeploy Olá exemplo aplicativo tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="c10c1-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="c10c1-108">aplicativo de exemplo Hello pisca Olá LED conectado toohello placa a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="c10c1-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="c10c1-109">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c10c1-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c10c1-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c10c1-110">What you will learn</span></span>
* <span data-ttu-id="c10c1-111">Como toodeploy e execução Olá aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="c10c1-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c10c1-112">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="c10c1-112">What you need</span></span>
<span data-ttu-id="c10c1-113">Você deve ter concluído Olá seguintes operações com êxito:</span><span class="sxs-lookup"><span data-stu-id="c10c1-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="c10c1-114">[Configurar seu dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="c10c1-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="c10c1-115">[Obter ferramentas Olá][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="c10c1-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="c10c1-116">Aplicativo de exemplo hello aberto</span><span class="sxs-lookup"><span data-stu-id="c10c1-116">Open hello sample application</span></span>
<span data-ttu-id="c10c1-117">Olá tooopen aplicativo de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c10c1-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="c10c1-118">Clone o repositório de exemplo de saudação do GitHub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c10c1-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="c10c1-119">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c10c1-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

<span data-ttu-id="c10c1-121">arquivo Olá Olá `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toocontrol Olá LED.</span><span class="sxs-lookup"><span data-stu-id="c10c1-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="c10c1-122">Instalar dependências de aplicativos</span><span class="sxs-lookup"><span data-stu-id="c10c1-122">Install application dependencies</span></span>
<span data-ttu-id="c10c1-123">Instale bibliotecas de saudação e outros módulos, que é necessário para o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c10c1-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="c10c1-124">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="c10c1-124">Configure hello device connection</span></span>
<span data-ttu-id="c10c1-125">tooconfigure Olá conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c10c1-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="c10c1-126">Gere arquivo de configuração de dispositivo de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c10c1-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="c10c1-127">arquivo de configuração de saudação `config-edison.json` contém credenciais do usuário Olá use toolog em tooEdison.</span><span class="sxs-lookup"><span data-stu-id="c10c1-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="c10c1-128">vazamento de saudação tooavoid de credenciais de usuário, o arquivo de configuração Olá é gerado na subpasta Olá `.iot-hub-getting-started` da pasta base do hello em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c10c1-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="c10c1-129">Abra o arquivo de configuração de dispositivo de saudação no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c10c1-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="c10c1-130">Substitua o espaço reservado de saudação `[device hostname or IP address]` e `[device password]` com endereço IP de saudação e senha marcados para baixo na lição anterior.</span><span class="sxs-lookup"><span data-stu-id="c10c1-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="c10c1-132">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="c10c1-132">Congratulations!</span></span> <span data-ttu-id="c10c1-133">Você criou com êxito o primeiro aplicativo de exemplo hello para Edison.</span><span class="sxs-lookup"><span data-stu-id="c10c1-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c10c1-134">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="c10c1-134">Deploy and run hello sample application</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="c10c1-135">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="c10c1-135">Deploy and run hello sample app</span></span>
<span data-ttu-id="c10c1-136">Implantar e executar o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c10c1-136">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="c10c1-137">Verifique se Olá aplicativo funciona</span><span class="sxs-lookup"><span data-stu-id="c10c1-137">Verify hello app works</span></span>
<span data-ttu-id="c10c1-138">aplicativo de exemplo Hello encerra automaticamente após Olá LED pisca para 20 vezes.</span><span class="sxs-lookup"><span data-stu-id="c10c1-138">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="c10c1-139">Se você não vir Olá LED piscando, consulte Olá [guia de solução de problemas] [ troubleshooting] para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="c10c1-139">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED piscando][led-blinking]

## <a name="summary"></a><span data-ttu-id="c10c1-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="c10c1-141">Summary</span></span>
<span data-ttu-id="c10c1-142">Instalar Olá necessárias ferramentas toowork com Edison e implantado uma saudação do exemplo aplicativo tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="c10c1-142">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="c10c1-143">Você pode criar, implantar e executar outro aplicativo de exemplo que se conecta Edison tooAzure toosend de IoT Hub e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="c10c1-143">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c10c1-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c10c1-144">Next steps</span></span>
<span data-ttu-id="c10c1-145">[Obter Olá ferramentas do Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="c10c1-145">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
