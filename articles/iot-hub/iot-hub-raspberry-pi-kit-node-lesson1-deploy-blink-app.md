---
featureFlags: usabilla
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 1: implantar o aplicativo | Microsoft Docs"
description: "Clonar um aplicativo de Node.js do exemplo hello do GitHub e gulp toodeploy deste quadro de tooyour framboesa Pi 3 do aplicativo. Este aplicativo de exemplo pisca Olá LED conectado toohello placa a cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: piscar led raspberry pi, piscar led com raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="40470-105">Criar e implantar o aplicativo de intermitência hello</span><span class="sxs-lookup"><span data-stu-id="40470-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="40470-106">O que você fará</span><span class="sxs-lookup"><span data-stu-id="40470-106">What you will do</span></span>
<span data-ttu-id="40470-107">Clonar um aplicativo de Node.js do exemplo hello do GitHub e use Olá gulp ferramenta toodeploy Olá exemplo aplicativo tooyour framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="40470-107">Clone hello sample Node.js application from GitHub and use hello gulp tool toodeploy hello sample application tooyour Raspberry Pi 3.</span></span> <span data-ttu-id="40470-108">aplicativo de exemplo Hello pisca Olá LED conectado toohello placa a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="40470-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="40470-109">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="40470-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="40470-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="40470-110">What you will learn</span></span>
<span data-ttu-id="40470-111">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="40470-111">In this article, you will learn:</span></span>

* <span data-ttu-id="40470-112">Como Olá toouse `device-discover-cli` ferramenta tooretrieve obter informações sobre o Pi da rede.</span><span class="sxs-lookup"><span data-stu-id="40470-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="40470-113">Como toodeploy e execução Olá aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="40470-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="40470-114">Como toodeploy e depurar aplicativos em execução remotamente no Pi.</span><span class="sxs-lookup"><span data-stu-id="40470-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="40470-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="40470-115">What you need</span></span>
<span data-ttu-id="40470-116">Você deve ter concluído Olá seguintes operações com êxito:</span><span class="sxs-lookup"><span data-stu-id="40470-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="40470-117">Configurar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="40470-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="40470-118">Obter ferramentas Olá</span><span class="sxs-lookup"><span data-stu-id="40470-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="40470-119">Obter o nome de host e endereço IP de saudação do Pi</span><span class="sxs-lookup"><span data-stu-id="40470-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="40470-120">Abra um prompt de comando no Windows ou um terminal macOS ou Ubuntu e, em seguida, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="40470-121">Você verá uma saída que é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="40470-121">You should see an output that is similar toohello following:</span></span>

![Descoberta de dispositivo](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="40470-123">Anote Olá `IP address` e `hostname` de Pi.</span><span class="sxs-lookup"><span data-stu-id="40470-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="40470-124">Você precisará dessas informações mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="40470-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="40470-125">Certifique-se de Pi é conectado toohello mesmo de rede do computador.</span><span class="sxs-lookup"><span data-stu-id="40470-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="40470-126">Por exemplo, se o computador estiver rede sem fio conectada tooa enquanto Pi é conectado tooa rede com fio, talvez você não veja Olá IP endereço na saída de devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="40470-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="40470-127">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="40470-127">Clone hello sample application</span></span>
<span data-ttu-id="40470-128">Olá tooopen código de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="40470-128">tooopen hello sample code, follow these steps:</span></span>

1. <span data-ttu-id="40470-129">Clone o repositório de exemplo de saudação do GitHub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="40470-130">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Estrutura do repositório](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="40470-132">Olá `app.js` arquivo hello `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toocontrol Olá LED.</span><span class="sxs-lookup"><span data-stu-id="40470-132">hello `app.js` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="40470-133">Instalar dependências de aplicativos</span><span class="sxs-lookup"><span data-stu-id="40470-133">Install application dependencies</span></span>
<span data-ttu-id="40470-134">Instale bibliotecas de saudação e outros módulos, que é necessário para o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="40470-135">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="40470-135">Configure hello device connection</span></span>
<span data-ttu-id="40470-136">tooconfigure Olá conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="40470-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="40470-137">Gere arquivo de configuração de dispositivo de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="40470-138">arquivo de configuração de saudação `config-raspberrypi.json` contém credenciais do usuário Olá use toolog em tooPi.</span><span class="sxs-lookup"><span data-stu-id="40470-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="40470-139">vazamento de saudação tooavoid de credenciais de usuário, o arquivo de configuração Olá é gerado na subpasta Olá `.iot-hub-getting-started` da pasta base do hello em seu computador.</span><span class="sxs-lookup"><span data-stu-id="40470-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="40470-140">Abra o arquivo de configuração de dispositivo de saudação no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="40470-141">Substitua o espaço reservado de saudação `[device hostname or IP address]` com o endereço IP hello ou nome de host de saudação que você obteve anteriormente em "Obter Olá IP endereço e nome do host de Pi."</span><span class="sxs-lookup"><span data-stu-id="40470-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="40470-143">Você pode usar a chave SSH, em vez de nome de usuário e senha ao conectar-se tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="40470-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="40470-144">Em ordem toodo isso você terá toogenerate Olá chave usando **ssh-keygen** e **pi ssh-copy-id @\<endereço do dispositivo\>**.</span><span class="sxs-lookup"><span data-stu-id="40470-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="40470-145">No Windows, esses comandos estão disponíveis em **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="40470-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="40470-146">Em MacOS precisar toorun **brew instalar ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="40470-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="40470-147">Depois de carregar com êxito Olá chave toohello framboesa Pi, substitua **device_password** com **device_key_path** propriedade **raspberrypi.json config**.</span><span class="sxs-lookup"><span data-stu-id="40470-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="40470-148">As linhas atualizadas devem parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="40470-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="40470-149">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="40470-149">Congratulations!</span></span> <span data-ttu-id="40470-150">Você criou com êxito o primeiro aplicativo de exemplo hello de Pi.</span><span class="sxs-lookup"><span data-stu-id="40470-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="40470-151">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="40470-151">Deploy and run hello sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="40470-152">Instalar o Node.js e o NPM no Pi</span><span class="sxs-lookup"><span data-stu-id="40470-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="40470-153">Instale o Node. js e NPM em Pi executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-153">Install Node.js and NPM on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="40470-154">Essa tarefa pode demorar Olá de toocomplete de 10 minutos primeiro que você executá-lo.</span><span class="sxs-lookup"><span data-stu-id="40470-154">This task might take 10 minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="40470-155">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="40470-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="40470-156">Implantar e executar o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="40470-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="40470-157">Verifique se Olá aplicativo funciona</span><span class="sxs-lookup"><span data-stu-id="40470-157">Verify hello app works</span></span>
<span data-ttu-id="40470-158">Agora você deve ver Olá LED no Pi piscando a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="40470-158">You should now see hello LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="40470-159">Se você não vir Olá LED piscando, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="40470-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="40470-160">![LED piscando](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="40470-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="40470-161">Resumo</span><span class="sxs-lookup"><span data-stu-id="40470-161">Summary</span></span>
<span data-ttu-id="40470-162">Instalar Olá necessárias ferramentas toowork com Pi e implantado uma saudação do exemplo aplicativo tooPi tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="40470-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="40470-163">Você pode criar, implantar e executar outro aplicativo de exemplo que se conecta Pi tooAzure toosend de IoT Hub e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="40470-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40470-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40470-164">Next steps</span></span>
[<span data-ttu-id="40470-165">Obter Olá ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="40470-165">Get hello Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

