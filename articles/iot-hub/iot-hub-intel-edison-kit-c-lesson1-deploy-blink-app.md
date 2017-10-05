---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 1: implantar aplicativo| Microsoft Docs"
description: "Clone o aplicativo C de exemplo do GitHub e execute o gulp para implantar esse aplicativo na placa do Intel Edison. Esse aplicativo de exemplo pisca o LED conectado à placa a cada dois segundos."
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
ms.openlocfilehash: c45ff5f41bdbc78da8532ffdcaaeec15c695f531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="d87c5-105">Criar e implantar o aplicativo de piscar</span><span class="sxs-lookup"><span data-stu-id="d87c5-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d87c5-106">O que você fará</span><span class="sxs-lookup"><span data-stu-id="d87c5-106">What you will do</span></span>
<span data-ttu-id="d87c5-107">Clonar o aplicativo C de exemplo do GitHub e usar a ferramenta gulp para implantar o aplicativo de exemplo no Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="d87c5-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="d87c5-108">O aplicativo de exemplo pisca o LED conectado à placa a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="d87c5-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="d87c5-109">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="d87c5-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d87c5-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="d87c5-110">What you will learn</span></span>
* <span data-ttu-id="d87c5-111">Como implantar e executar o aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="d87c5-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d87c5-112">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="d87c5-112">What you need</span></span>
<span data-ttu-id="d87c5-113">Você deve ter concluído com sucesso as seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="d87c5-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="d87c5-114">[Configurar seu dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="d87c5-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="d87c5-115">[Obter as ferramentas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="d87c5-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="d87c5-116">Abrir o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="d87c5-116">Open the sample application</span></span>
<span data-ttu-id="d87c5-117">Para abrir o aplicativo de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d87c5-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="d87c5-118">Clone o repositório de exemplo do GitHub executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d87c5-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="d87c5-119">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d87c5-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

<span data-ttu-id="d87c5-121">O arquivo na subpasta `app` é o arquivo de origem principal que contém o código para controlar o LED.</span><span class="sxs-lookup"><span data-stu-id="d87c5-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="d87c5-122">Instalar dependências de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d87c5-122">Install application dependencies</span></span>
<span data-ttu-id="d87c5-123">Instale as bibliotecas e outros módulos necessários para o aplicativo de exemplo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d87c5-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="d87c5-124">Configurar a conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="d87c5-124">Configure the device connection</span></span>
<span data-ttu-id="d87c5-125">Para configurar a conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d87c5-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="d87c5-126">Gere o arquivo de configuração do dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d87c5-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="d87c5-127">O arquivo de configuração `config-edison.json` contém as credenciais do usuário que você usa para fazer logon no Edison.</span><span class="sxs-lookup"><span data-stu-id="d87c5-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="d87c5-128">Para evitar a perda de credenciais de usuário, o arquivo de configuração é gerado na subpasta `.iot-hub-getting-started` da pasta base em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d87c5-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="d87c5-129">Abra o arquivo de configuração do dispositivo no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d87c5-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="d87c5-130">Substitua o espaço reservado `[device hostname or IP address]` e `[device password]` pelo endereço IP e pela senha que você marcou na lição anterior.</span><span class="sxs-lookup"><span data-stu-id="d87c5-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="d87c5-132">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d87c5-132">Congratulations!</span></span> <span data-ttu-id="d87c5-133">Você criou com êxito o primeiro aplicativo de exemplo para o Edison.</span><span class="sxs-lookup"><span data-stu-id="d87c5-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="d87c5-134">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="d87c5-134">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="d87c5-135">Instalar o SDK do Hub IoT do Azure no Edison</span><span class="sxs-lookup"><span data-stu-id="d87c5-135">Install the Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="d87c5-136">Instale o SDK do Hub IoT do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d87c5-136">Install the Azure IoT Hub SDK on Edison by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="d87c5-137">Essa tarefa pode levar muito tempo para ser concluída, dependendo da sua conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="d87c5-137">This task might take a long time to complete, depending on your network connection.</span></span> <span data-ttu-id="d87c5-138">Ela precisa ser executada apenas uma vez para um Edison.</span><span class="sxs-lookup"><span data-stu-id="d87c5-138">It needs to be run only once for one Edison.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="d87c5-139">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="d87c5-139">Deploy and run the sample app</span></span>
<span data-ttu-id="d87c5-140">Implantar e executar o aplicativo de exemplo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d87c5-140">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="d87c5-141">Verificar se o aplicativo funciona</span><span class="sxs-lookup"><span data-stu-id="d87c5-141">Verify the app works</span></span>
<span data-ttu-id="d87c5-142">O aplicativo de exemplo é encerrado automaticamente após o LED piscar 20 vezes.</span><span class="sxs-lookup"><span data-stu-id="d87c5-142">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="d87c5-143">Se você não vir o LED piscar, consulte o [guia de solução de problemas][troubleshooting] para ver soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="d87c5-143">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED piscando][led-blinking]

## <a name="summary"></a><span data-ttu-id="d87c5-145">Resumo</span><span class="sxs-lookup"><span data-stu-id="d87c5-145">Summary</span></span>
<span data-ttu-id="d87c5-146">Você instalou as ferramentas necessárias para trabalhar com o Edison e implantou um aplicativo de exemplo no Edison para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="d87c5-146">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="d87c5-147">Agora, você pode criar, implantar e executar outro aplicativo de exemplo que conecta o Edison ao Hub IoT do Azure para enviar e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="d87c5-147">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d87c5-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d87c5-148">Next steps</span></span>
<span data-ttu-id="d87c5-149">[Obter as ferramentas do Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="d87c5-149">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
