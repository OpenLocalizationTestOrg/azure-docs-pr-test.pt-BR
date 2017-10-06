---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 3: executar aplicativo de exemplo| Microsoft Docs"
description: Executar um dispositivo simulado exemplo aplicativo toosend temperatura tooyour IoT hub de dados
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dados toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="08434-104">Configurar e executar um aplicativo de exemplo do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="08434-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="08434-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="08434-105">What you will do</span></span>

- <span data-ttu-id="08434-106">Repositório de exemplo de saudação do clone.</span><span class="sxs-lookup"><span data-stu-id="08434-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="08434-107">Use Olá CLI do Azure tooget seu hub IoT e informações de dispositivo lógico para o aplicativo de exemplo do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="08434-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="08434-108">Configurar e executar o aplicativo de exemplo do dispositivo Olá simulada.</span><span class="sxs-lookup"><span data-stu-id="08434-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="08434-109">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="08434-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="08434-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="08434-110">What you will learn</span></span>

<span data-ttu-id="08434-111">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="08434-111">In this article, you will learn:</span></span>

- <span data-ttu-id="08434-112">Como tooconfigure e hello execução simulado aplicativo de exemplo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="08434-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="08434-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="08434-113">What you need</span></span>

<span data-ttu-id="08434-114">Você deve ter concluído com sucesso</span><span class="sxs-lookup"><span data-stu-id="08434-114">You must have successfully completed</span></span>

- [<span data-ttu-id="08434-115">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="08434-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="08434-116">Computador de host do clone Olá exemplo repositório toohello</span><span class="sxs-lookup"><span data-stu-id="08434-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="08434-117">repositório de exemplo hello tooclone, siga estas etapas no computador de host hello:</span><span class="sxs-lookup"><span data-stu-id="08434-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="08434-118">Abra um Prompt de Comando no Windows ou um terminal no macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="08434-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="08434-119">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="08434-120">Configurar dispositivo simulado hello e seu NUC</span><span class="sxs-lookup"><span data-stu-id="08434-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="08434-121">Arquivo de configuração de saudação abrir `config.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="08434-122">Substitua `"has_sensortag": true` por `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="08434-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configurar que você não tem um dispositivo de TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="08434-124">Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="08434-125">Abra `config-gateway.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="08434-126">Olá a seguinte linha de código de localizar e substituir `[device hostname or IP address]` com o nome de host ou endereço IP de saudação NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="08434-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="08434-127">![instantâneo do gateway de configuração](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="08434-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="08434-128">Obter cadeia de caracteres de conexão de saudação do seu dispositivo lógico de hub IoT</span><span class="sxs-lookup"><span data-stu-id="08434-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="08434-129">Olá tooget cadeia de conexão de hub IoT do Azure do seu dispositivo lógico, execute Olá comando no computador de host Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="08434-130">`{IoT hub name}`é o nome do hub IoT Olá que você usou.</span><span class="sxs-lookup"><span data-stu-id="08434-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="08434-131">Usar gateway iot como valor de saudação do `{resource group name}` e usar meudispositivo como valor de saudação do `{device id}` se você não alterar o valor de saudação na lição 2.</span><span class="sxs-lookup"><span data-stu-id="08434-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="08434-132">Configurar o aplicativo de exemplo de carregamento do hello simulado dispositivo nuvem</span><span class="sxs-lookup"><span data-stu-id="08434-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="08434-133">tooconfigure e na nuvem de dispositivo de execução Olá simulado carregar o aplicativo de exemplo, siga estas etapas no computador de host hello:</span><span class="sxs-lookup"><span data-stu-id="08434-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="08434-134">Abra `config-sensortag.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![instantâneo da configuração da sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="08434-136">Verifique Olá substituições no código Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="08434-137">Substituir `[IoT hub name]` com o nome do hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="08434-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="08434-138">Substituir `[IoT device connection string]` com a cadeia de caracteres de conexão de saudação do seu dispositivo lógico de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="08434-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="08434-139">Execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="08434-139">Run hello application.</span></span>

   <span data-ttu-id="08434-140">Implantar e executar o aplicativo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="08434-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="08434-141">Verifique se o aplicativo de exemplo hello funciona</span><span class="sxs-lookup"><span data-stu-id="08434-141">Verify hello sample application works</span></span>

<span data-ttu-id="08434-142">Agora você deve ver a saída como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="08434-142">You should now see output like hello following:</span></span>

![saída do aplicativo de exemplo de dispositivo simulado](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="08434-144">aplicativo Hello envia hub IoT de temperatura dados tooyour, que tem duração de 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="08434-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="08434-145">Resumo</span><span class="sxs-lookup"><span data-stu-id="08434-145">Summary</span></span>

<span data-ttu-id="08434-146">Você configurou com êxito e execução Olá simulados dispositivo nuvem carregar aplicativo de exemplo que envia o hub de IoT tooyour dados com dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="08434-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08434-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08434-147">Next steps</span></span>
[<span data-ttu-id="08434-148">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="08434-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)