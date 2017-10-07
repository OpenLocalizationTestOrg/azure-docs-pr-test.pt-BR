---
title: "Connect Intel Edison (C) tooAzure IoT - lição 1: implantar o aplicativo | Microsoft Docs"
description: "Clonar um aplicativo de exemplo C de saudação do GitHub e execute gulp toodeploy tooyour esse aplicativo placa Edison Intel. Este aplicativo de exemplo pisca Olá LED conectado toohello placa a cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projetos led arduino, piscar led arduino, código piscar led arduino, programa de piscar arduino, exemplo de piscar arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="542e5-105">Criar e implantar o aplicativo de intermitência hello</span><span class="sxs-lookup"><span data-stu-id="542e5-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="542e5-106">O que você fará</span><span class="sxs-lookup"><span data-stu-id="542e5-106">What you will do</span></span>
<span data-ttu-id="542e5-107">Clonar o aplicativo de exemplo C de saudação do GitHub e usar Olá gulp ferramenta toodeploy Olá exemplo aplicativo tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="542e5-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="542e5-108">aplicativo de exemplo Hello pisca Olá LED conectado toohello placa a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="542e5-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="542e5-109">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="542e5-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="542e5-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="542e5-110">What you will learn</span></span>
* <span data-ttu-id="542e5-111">Como toodeploy e execução Olá aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="542e5-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="542e5-112">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="542e5-112">What you need</span></span>
<span data-ttu-id="542e5-113">Você deve ter concluído Olá seguintes operações com êxito:</span><span class="sxs-lookup"><span data-stu-id="542e5-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="542e5-114">[Configurar seu dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="542e5-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="542e5-115">[Obter ferramentas Olá][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="542e5-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="542e5-116">Aplicativo de exemplo hello aberto</span><span class="sxs-lookup"><span data-stu-id="542e5-116">Open hello sample application</span></span>
<span data-ttu-id="542e5-117">Olá tooopen aplicativo de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="542e5-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="542e5-118">Clone o repositório de exemplo de saudação do GitHub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="542e5-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="542e5-119">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="542e5-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

<span data-ttu-id="542e5-121">arquivo Olá Olá `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toocontrol Olá LED.</span><span class="sxs-lookup"><span data-stu-id="542e5-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="542e5-122">Instalar dependências de aplicativos</span><span class="sxs-lookup"><span data-stu-id="542e5-122">Install application dependencies</span></span>
<span data-ttu-id="542e5-123">Instale bibliotecas de saudação e outros módulos, que é necessário para o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="542e5-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="542e5-124">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="542e5-124">Configure hello device connection</span></span>
<span data-ttu-id="542e5-125">tooconfigure Olá conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="542e5-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="542e5-126">Gere arquivo de configuração de dispositivo de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="542e5-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="542e5-127">arquivo de configuração de saudação `config-edison.json` contém credenciais do usuário Olá use toolog em tooEdison.</span><span class="sxs-lookup"><span data-stu-id="542e5-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="542e5-128">vazamento de saudação tooavoid de credenciais de usuário, o arquivo de configuração Olá é gerado na subpasta Olá `.iot-hub-getting-started` da pasta base do hello em seu computador.</span><span class="sxs-lookup"><span data-stu-id="542e5-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="542e5-129">Abra o arquivo de configuração de dispositivo de saudação no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="542e5-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="542e5-130">Substitua o espaço reservado de saudação `[device hostname or IP address]` e `[device password]` com endereço IP de saudação e senha marcados para baixo na lição anterior.</span><span class="sxs-lookup"><span data-stu-id="542e5-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="542e5-132">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="542e5-132">Congratulations!</span></span> <span data-ttu-id="542e5-133">Você criou com êxito o primeiro aplicativo de exemplo hello para Edison.</span><span class="sxs-lookup"><span data-stu-id="542e5-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="542e5-134">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="542e5-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="542e5-135">Instalar o hello Azure IoT Hub SDK Edison</span><span class="sxs-lookup"><span data-stu-id="542e5-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="542e5-136">Instale hello Azure IoT Hub SDK em Edison executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="542e5-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="542e5-137">Essa tarefa pode levar um longo tempo toocomplete, dependendo de sua conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="542e5-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="542e5-138">Ela precisa toobe executada apenas uma vez para um Edison.</span><span class="sxs-lookup"><span data-stu-id="542e5-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="542e5-139">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="542e5-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="542e5-140">Implantar e executar o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="542e5-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="542e5-141">Verifique se Olá aplicativo funciona</span><span class="sxs-lookup"><span data-stu-id="542e5-141">Verify hello app works</span></span>
<span data-ttu-id="542e5-142">aplicativo de exemplo Hello encerra automaticamente após Olá LED pisca para 20 vezes.</span><span class="sxs-lookup"><span data-stu-id="542e5-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="542e5-143">Se você não vir Olá LED piscando, consulte Olá [guia de solução de problemas] [ troubleshooting] para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="542e5-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED piscando][led-blinking]

## <a name="summary"></a><span data-ttu-id="542e5-145">Resumo</span><span class="sxs-lookup"><span data-stu-id="542e5-145">Summary</span></span>
<span data-ttu-id="542e5-146">Instalar Olá necessárias ferramentas toowork com Edison e implantado uma saudação do exemplo aplicativo tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="542e5-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="542e5-147">Você pode criar, implantar e executar outro aplicativo de exemplo que se conecta Edison tooAzure toosend de IoT Hub e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="542e5-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="542e5-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="542e5-148">Next steps</span></span>
<span data-ttu-id="542e5-149">[Obter Olá ferramentas do Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="542e5-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
