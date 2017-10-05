---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 3: executar aplicativo de exemplo| Microsoft Docs"
description: Executar um aplicativo de exemplo do dispositivo simulado para enviar dados de temperatura para o Hub IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dados para a nuvem
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="c73cf-104">Configurar e executar um aplicativo de exemplo do dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="c73cf-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c73cf-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="c73cf-105">What you will do</span></span>

- <span data-ttu-id="c73cf-106">Clone o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c73cf-106">Clone the sample repository.</span></span>
- <span data-ttu-id="c73cf-107">Use a CLI do Azure para obter as informações de dispositivo lógico e do seu Hub IoT para o aplicativo de exemplo do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="c73cf-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="c73cf-108">Configure e execute o aplicativo de exemplo do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="c73cf-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="c73cf-109">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c73cf-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c73cf-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c73cf-110">What you will learn</span></span>

<span data-ttu-id="c73cf-111">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="c73cf-111">In this article, you will learn:</span></span>

- <span data-ttu-id="c73cf-112">Como configurar e executar o aplicativo de exemplo do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="c73cf-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c73cf-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="c73cf-113">What you need</span></span>

<span data-ttu-id="c73cf-114">Você deve ter concluído com sucesso</span><span class="sxs-lookup"><span data-stu-id="c73cf-114">You must have successfully completed</span></span>

- [<span data-ttu-id="c73cf-115">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="c73cf-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="c73cf-116">Clonar o repositório de exemplo para o computador host</span><span class="sxs-lookup"><span data-stu-id="c73cf-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="c73cf-117">Para clonar o repositório de exemplo, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="c73cf-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="c73cf-118">Abra um Prompt de Comando no Windows ou um terminal no macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c73cf-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="c73cf-119">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c73cf-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="c73cf-120">Configurar o dispositivo simulado e sua NUC</span><span class="sxs-lookup"><span data-stu-id="c73cf-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="c73cf-121">Abra o arquivo de configuração `config.json` no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c73cf-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="c73cf-122">Substitua `"has_sensortag": true` por `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="c73cf-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Configurar que você não tem um dispositivo de TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="c73cf-124">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c73cf-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="c73cf-125">Abra `config-gateway.json` no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c73cf-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="c73cf-126">Localize a seguinte linha de código e substitua `[device hostname or IP address]` pelo nome de host ou endereço IP da NUC da Intel.</span><span class="sxs-lookup"><span data-stu-id="c73cf-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="c73cf-127">![instantâneo do gateway de configuração](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="c73cf-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="c73cf-128">Obter a cadeia de conexão do dispositivo lógico de Hub IoT</span><span class="sxs-lookup"><span data-stu-id="c73cf-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="c73cf-129">Para obter a cadeia de conexão do Hub IoT do Azure do dispositivo lógico, execute o seguinte comando no computador host:</span><span class="sxs-lookup"><span data-stu-id="c73cf-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="c73cf-130">`{IoT hub name}` é o nome do hub IoT usado.</span><span class="sxs-lookup"><span data-stu-id="c73cf-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="c73cf-131">Use o gateway IoT como o valor de `{resource group name}` e use mydevice como o valor de `{device id}` se você não tiver alterado o valor na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="c73cf-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="c73cf-132">Configurar o aplicativo de exemplo de upload de nuvem de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="c73cf-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="c73cf-133">Para configurar e executar o aplicativo de exemplo de upload de nuvem de dispositivo simulado, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="c73cf-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="c73cf-134">Abra `config-sensortag.json` no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c73cf-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![instantâneo da configuração da sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="c73cf-136">Faça as seguintes substituições no código:</span><span class="sxs-lookup"><span data-stu-id="c73cf-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="c73cf-137">Substitua `[IoT hub name]` pelo nome do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c73cf-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="c73cf-138">Substitua `[IoT device connection string]` pela cadeia de conexão do dispositivo lógico do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c73cf-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="c73cf-139">Execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c73cf-139">Run the application.</span></span>

   <span data-ttu-id="c73cf-140">Implantar e executar o aplicativo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c73cf-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="c73cf-141">Verificar se o aplicativo de exemplo funciona</span><span class="sxs-lookup"><span data-stu-id="c73cf-141">Verify the sample application works</span></span>

<span data-ttu-id="c73cf-142">Você verá agora uma saída semelhante à mostrada a seguir:</span><span class="sxs-lookup"><span data-stu-id="c73cf-142">You should now see output like the following:</span></span>

![saída do aplicativo de exemplo de dispositivo simulado](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="c73cf-144">O aplicativo envia dados de temperatura ao seu Hub IoT, o que dura 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="c73cf-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="c73cf-145">Resumo</span><span class="sxs-lookup"><span data-stu-id="c73cf-145">Summary</span></span>

<span data-ttu-id="c73cf-146">Você configurou e executou com êxito o aplicativo de exemplo de upload de nuvem de dispositivo simulado que envia dados ao seu Hub IoT com dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="c73cf-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c73cf-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c73cf-147">Next steps</span></span>
[<span data-ttu-id="c73cf-148">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="c73cf-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)