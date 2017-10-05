---
title: "Conectar o Raspberry Pi (C) ao IoT do Azure - Lição 1: implantar aplicativo | Microsoft Docs"
description: "Clone o aplicativo C de exemplo do GitHub e use gulp para implantar esse aplicativo na placa do Raspberry Pi 3. Esse aplicativo de exemplo pisca o LED conectado à placa a cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: piscar led raspberry pi, piscar led com raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2ae409c6a39521711777ec329d2507a2801cc985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="1ba67-105">Criar e implantar o aplicativo de piscar</span><span class="sxs-lookup"><span data-stu-id="1ba67-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1ba67-106">O que você fará</span><span class="sxs-lookup"><span data-stu-id="1ba67-106">What you will do</span></span>
<span data-ttu-id="1ba67-107">Clone o aplicativo C de exemplo do GitHub e use a ferramenta gulp para implantar o aplicativo de exemplo no Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="1ba67-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Raspberry Pi 3.</span></span> <span data-ttu-id="1ba67-108">O aplicativo de exemplo pisca o LED conectado à placa a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="1ba67-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="1ba67-109">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1ba67-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1ba67-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="1ba67-110">What you will learn</span></span>
<span data-ttu-id="1ba67-111">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="1ba67-111">In this article, you will learn:</span></span>

* <span data-ttu-id="1ba67-112">Como usar a ferramenta `device-discover-cli` para recuperar informações de rede sobre seu Pi.</span><span class="sxs-lookup"><span data-stu-id="1ba67-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="1ba67-113">Como implantar e executar o aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="1ba67-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="1ba67-114">Como implantar e depurar aplicativos executados remotamente no Pi.</span><span class="sxs-lookup"><span data-stu-id="1ba67-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1ba67-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="1ba67-115">What you need</span></span>
<span data-ttu-id="1ba67-116">Você deve ter concluído com sucesso as seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ba67-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="1ba67-117">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="1ba67-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="1ba67-118">Obter as ferramentas</span><span class="sxs-lookup"><span data-stu-id="1ba67-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="1ba67-119">Obter o nome de host e o endereço IP do Pi</span><span class="sxs-lookup"><span data-stu-id="1ba67-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="1ba67-120">Abra um prompt de comando no Windows ou em um terminal no macOS ou Ubuntu e, em seguida, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1ba67-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="1ba67-121">Você deverá ver uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="1ba67-121">You should see an output that is similar to the following:</span></span>

![Descoberta de dispositivo](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="1ba67-123">Anote `IP address` e `hostname` do Pi.</span><span class="sxs-lookup"><span data-stu-id="1ba67-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="1ba67-124">Você precisará dessas informações mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="1ba67-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba67-125">Verifique se o Pi está conectado à mesma rede que o computador.</span><span class="sxs-lookup"><span data-stu-id="1ba67-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="1ba67-126">Por exemplo, se o computador estiver conectado a uma rede sem fio enquanto o Pi estiver conectado a uma rede com fio, talvez você não veja o endereço IP na saída devdisco.</span><span class="sxs-lookup"><span data-stu-id="1ba67-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="1ba67-127">Abrir o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="1ba67-127">Open the sample application</span></span>
<span data-ttu-id="1ba67-128">Para abrir o aplicativo de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1ba67-128">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="1ba67-129">Clone o repositório de exemplo do GitHub executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1ba67-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="1ba67-130">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="1ba67-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Estrutura do repositório](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="1ba67-132">O arquivo `main.c` na subpasta `app` é o arquivo de origem principal que contém o código para controlar o LED.</span><span class="sxs-lookup"><span data-stu-id="1ba67-132">The `main.c` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="1ba67-133">Instalar dependências de aplicativos</span><span class="sxs-lookup"><span data-stu-id="1ba67-133">Install application dependencies</span></span>
<span data-ttu-id="1ba67-134">Instale as bibliotecas e outros módulos necessários para o aplicativo de exemplo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1ba67-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="1ba67-135">Configurar a conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="1ba67-135">Configure the device connection</span></span>
<span data-ttu-id="1ba67-136">Para configurar a conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1ba67-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="1ba67-137">Gere o arquivo de configuração do dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1ba67-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="1ba67-138">O arquivo de configuração `config-raspberrypi.json` contém as credenciais do usuário que você usa para fazer logon no Pi.</span><span class="sxs-lookup"><span data-stu-id="1ba67-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="1ba67-139">Para evitar a perda de credenciais de usuário, o arquivo de configuração é gerado na subpasta `.iot-hub-getting-started` da pasta base em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1ba67-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="1ba67-140">Abra o arquivo de configuração do dispositivo no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1ba67-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="1ba67-141">Substitua o espaço reservado `[device hostname or IP address]` pelo endereço IP ou o nome do host que você obteve anteriormente em "Obter o nome de host e endereço IP de Pi."</span><span class="sxs-lookup"><span data-stu-id="1ba67-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="1ba67-143">Você pode usar a chave SSH, em vez do nome de usuário e senha ao se conectar ao Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="1ba67-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="1ba67-144">Para fazer isso, você precisará gerar a chave usando **ssh-keygen** e **pi ssh-copy-id @\<endereço do dispositivo\>**.</span><span class="sxs-lookup"><span data-stu-id="1ba67-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="1ba67-145">No Windows, esses comandos estão disponíveis em **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="1ba67-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="1ba67-146">No MacOS, você precisa executar **brew install ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="1ba67-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="1ba67-147">Depois de carregar com êxito a chave no Raspberry Pi, substitua **device_password** pela propriedade **device_key_path** no **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="1ba67-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="1ba67-148">As linhas atualizadas devem parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1ba67-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="1ba67-149">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="1ba67-149">Congratulations!</span></span> <span data-ttu-id="1ba67-150">Você criou com êxito o primeiro aplicativo de exemplo para o Pi.</span><span class="sxs-lookup"><span data-stu-id="1ba67-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="1ba67-151">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="1ba67-151">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="1ba67-152">Instalar o SDK do Hub IoT do Azure no Pi</span><span class="sxs-lookup"><span data-stu-id="1ba67-152">Install the Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="1ba67-153">Instale o SDK do Hub IoT do Azure no Pi executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1ba67-153">Install the Azure IoT Hub SDK on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="1ba67-154">A conclusão da execução inicial desta tarefa pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="1ba67-154">This task might take a few minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="1ba67-155">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="1ba67-155">Deploy and run the sample app</span></span>
<span data-ttu-id="1ba67-156">Implantar e executar o aplicativo de exemplo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1ba67-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="1ba67-157">Verificar se o aplicativo funciona</span><span class="sxs-lookup"><span data-stu-id="1ba67-157">Verify the app works</span></span>
<span data-ttu-id="1ba67-158">O aplicativo de exemplo é encerrado automaticamente após o LED piscar 20 vezes.</span><span class="sxs-lookup"><span data-stu-id="1ba67-158">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="1ba67-159">Se você não vir o LED piscar, consulte o [guia de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="1ba67-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="1ba67-160">![LED piscando](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="1ba67-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="1ba67-161">Resumo</span><span class="sxs-lookup"><span data-stu-id="1ba67-161">Summary</span></span>
<span data-ttu-id="1ba67-162">Você instalou as ferramentas necessárias para trabalhar com o Pi e implantou um aplicativo de exemplo para o Pi para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="1ba67-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="1ba67-163">Agora você pode criar, implantar e executar outro aplicativo de exemplo que conecta seu Pi ao Hub IoT do Azure para enviar e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="1ba67-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ba67-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ba67-164">Next steps</span></span>
[<span data-ttu-id="1ba67-165">Obter ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="1ba67-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

