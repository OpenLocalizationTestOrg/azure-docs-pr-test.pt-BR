---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 3: executar aplicativo de exemplo| Microsoft Docs"
description: Execute uma Bilitar de tooreceive de aplicativo de exemplo de dados de SensorTag Bilitar em seu hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bilitar aplicativo, aplicativo de monitor de sensor, coleta de dados de sensor, dados de sensores, toocloud de dados do sensor
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="5af19-104">Configurar e executar um aplicativo de exemplo BLE</span><span class="sxs-lookup"><span data-stu-id="5af19-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5af19-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="5af19-105">What you will do</span></span>

- <span data-ttu-id="5af19-106">Repositório de exemplo de saudação do clone.</span><span class="sxs-lookup"><span data-stu-id="5af19-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="5af19-107">Configure a conectividade de saudação entre SensorTag e NUC da Intel.</span><span class="sxs-lookup"><span data-stu-id="5af19-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="5af19-108">Use Olá CLI do Azure tooget seu hub IoT e SensorTag informações para um aplicativo de exemplo Bilitar (Bluetooth baixo consumo de energia).</span><span class="sxs-lookup"><span data-stu-id="5af19-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="5af19-109">Configurar e executar o aplicativo de exemplo hello var.</span><span class="sxs-lookup"><span data-stu-id="5af19-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="5af19-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5af19-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5af19-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="5af19-111">What you will learn</span></span>

<span data-ttu-id="5af19-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="5af19-112">In this article, you will learn:</span></span>

- <span data-ttu-id="5af19-113">Como tooconfigure e execução hello Bilitar aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5af19-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5af19-114">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="5af19-114">What you need</span></span>

<span data-ttu-id="5af19-115">Você deve ter concluído com sucesso</span><span class="sxs-lookup"><span data-stu-id="5af19-115">You must have successfully completed</span></span>

- [<span data-ttu-id="5af19-116">Criar um Hub IoT e registrar o SensorTag</span><span class="sxs-lookup"><span data-stu-id="5af19-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="5af19-117">Computador de host do clone Olá exemplo repositório toohello</span><span class="sxs-lookup"><span data-stu-id="5af19-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="5af19-118">repositório de exemplo hello tooclone, siga estas etapas no computador de host hello:</span><span class="sxs-lookup"><span data-stu-id="5af19-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5af19-119">Abra uma janela de Prompt de comando no Windows ou um terminal no macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5af19-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="5af19-120">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="5af19-121">Configurar a conectividade de saudação entre SensorTag e NUC Intel</span><span class="sxs-lookup"><span data-stu-id="5af19-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="5af19-122">tooset conectividade hello, siga estas etapas no computador de host hello:</span><span class="sxs-lookup"><span data-stu-id="5af19-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5af19-123">Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="5af19-124">Abra `config-gateway.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="5af19-125">Olá a seguinte linha de código de localizar e substituir `[device hostname or IP address]` com nome de host ou endereço IP de saudação do NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="5af19-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="5af19-126">![instantâneo do gateway de configuração](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="5af19-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="5af19-127">Instale ferramentas de auxílio no Intel NUC executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="5af19-128">Ative SensorTag pressionando o botão liga / desliga Olá Olá figura abaixo e Olá que LED verde deve piscar.</span><span class="sxs-lookup"><span data-stu-id="5af19-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![ativar Sensor Tag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="5af19-130">Verificar dispositivos SensorTag executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="5af19-131">Testar a conectividade de saudação entre hello SensorTag e Intel NUC executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="5af19-132">Substituir `{mac address}` com endereço MAC que você obteve na etapa anterior de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="5af19-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="5af19-133">Obter cadeia de caracteres de conexão de saudação do SensorTag</span><span class="sxs-lookup"><span data-stu-id="5af19-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="5af19-134">Olá tooget cadeia de conexão de hub IoT do Azure de SensorTag, execute Olá comando no computador de host Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="5af19-135">`{IoT hub name}`é o nome do hub IoT Olá que você usou.</span><span class="sxs-lookup"><span data-stu-id="5af19-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="5af19-136">Usar gateway iot como valor de saudação do `{resource group name}` e usar meudispositivo como valor de saudação do `{device id}` se você não alterar o valor de saudação na lição 2.</span><span class="sxs-lookup"><span data-stu-id="5af19-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="5af19-137">Configurar o aplicativo de exemplo hello Bilitar</span><span class="sxs-lookup"><span data-stu-id="5af19-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="5af19-138">tooconfigure e execução hello aplicativo de exemplo Bilitar, siga estas etapas no computador de host hello:</span><span class="sxs-lookup"><span data-stu-id="5af19-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5af19-139">Abra `config-sensortag.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![instantâneo da configuração da sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="5af19-141">Verifique Olá substituições no código Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="5af19-142">Substituir `[IoT hub name]` com o nome do hub IoT Olá que você usou.</span><span class="sxs-lookup"><span data-stu-id="5af19-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="5af19-143">Substituir `[IoT device connection string]` com a cadeia de caracteres de conexão de saudação do SensorTag que você obteve.</span><span class="sxs-lookup"><span data-stu-id="5af19-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="5af19-144">Substituir `[device_mac_address]` com hello endereço MAC de saudação SensorTag obtido.</span><span class="sxs-lookup"><span data-stu-id="5af19-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="5af19-145">Execute o aplicativo de exemplo hello var.</span><span class="sxs-lookup"><span data-stu-id="5af19-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="5af19-146">Olá toorun aplicativo de exemplo Bilitar, siga estas etapas no computador de host hello:</span><span class="sxs-lookup"><span data-stu-id="5af19-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="5af19-147">Ative a SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5af19-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="5af19-148">Implantar e executar o aplicativo de exemplo hello Bilitar em NUC Intel executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5af19-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="5af19-149">Verifique se o aplicativo de exemplo hello Bilitar funciona</span><span class="sxs-lookup"><span data-stu-id="5af19-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="5af19-150">Agora, você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="5af19-150">You should now see an output like hello following:</span></span>

![Saída do aplicativo de exemplo BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="5af19-152">aplicativo de exemplo Hello mantém a coleta de dados de temperatura e enviou tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5af19-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="5af19-153">aplicativo de exemplo Hello encerra automaticamente após o envio de 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="5af19-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="5af19-154">Resumo</span><span class="sxs-lookup"><span data-stu-id="5af19-154">Summary</span></span>

<span data-ttu-id="5af19-155">Você com êxito configurar conectividade Olá entre SensorTag e NUC Intel e executar um aplicativo de exemplo Bilitar que coleta e envia dados de SensorTag tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5af19-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="5af19-156">Você está pronto toolearn como tooverify que recebeu o hub IoT Olá dados.</span><span class="sxs-lookup"><span data-stu-id="5af19-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5af19-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5af19-157">Next steps</span></span>
[<span data-ttu-id="5af19-158">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="5af19-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)