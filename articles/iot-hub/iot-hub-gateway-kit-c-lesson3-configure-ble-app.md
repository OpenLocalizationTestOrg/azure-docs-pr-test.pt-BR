---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 3: executar aplicativo de exemplo| Microsoft Docs"
description: Execute um aplicativo de exemplo BLE para receber dados do BLE SensorTag em seu Hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: aplicativo ble, aplicativo de monitor de sensor, coleta de dados do sensor, dados de sensores, dados de sensor para a nuvem
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="2ea49-104">Configurar e executar um aplicativo de exemplo BLE</span><span class="sxs-lookup"><span data-stu-id="2ea49-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2ea49-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="2ea49-105">What you will do</span></span>

- <span data-ttu-id="2ea49-106">Clone o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2ea49-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="2ea49-107">Configure a conectividade entre SensorTag e NUC da Intel.</span><span class="sxs-lookup"><span data-stu-id="2ea49-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="2ea49-108">Use a CLI do Azure para obter informações do seu Hub IoT e SensorTag para um aplicativo de exemplo BLE (Bluetooth de Baixa Energia).</span><span class="sxs-lookup"><span data-stu-id="2ea49-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="2ea49-109">Configure e execute o aplicativo de exemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="2ea49-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="2ea49-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2ea49-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2ea49-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="2ea49-111">What you will learn</span></span>

<span data-ttu-id="2ea49-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="2ea49-112">In this article, you will learn:</span></span>

- <span data-ttu-id="2ea49-113">Como configurar e executar o aplicativo de exemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="2ea49-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2ea49-114">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="2ea49-114">What you need</span></span>

<span data-ttu-id="2ea49-115">Você deve ter concluído com sucesso</span><span class="sxs-lookup"><span data-stu-id="2ea49-115">You must have successfully completed</span></span>

- [<span data-ttu-id="2ea49-116">Criar um Hub IoT e registrar o SensorTag</span><span class="sxs-lookup"><span data-stu-id="2ea49-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="2ea49-117">Clonar o repositório de exemplo para o computador host</span><span class="sxs-lookup"><span data-stu-id="2ea49-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="2ea49-118">Para clonar o repositório de exemplo, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="2ea49-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="2ea49-119">Abra uma janela de Prompt de comando no Windows ou um terminal no macOS ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2ea49-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="2ea49-120">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2ea49-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="2ea49-121">Configurar a conectividade entre SensorTag e NUC da Intel</span><span class="sxs-lookup"><span data-stu-id="2ea49-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="2ea49-122">Para configurar a conectividade, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="2ea49-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="2ea49-123">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2ea49-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="2ea49-124">Abra `config-gateway.json` no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2ea49-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="2ea49-125">Localize a seguinte linha de código e substitua `[device hostname or IP address]` pelo nome de host ou endereço IP do NUC da Intel.</span><span class="sxs-lookup"><span data-stu-id="2ea49-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="2ea49-126">![instantâneo do gateway de configuração](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="2ea49-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="2ea49-127">Instale ferramentas de auxílio no NUC da Intel executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2ea49-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="2ea49-128">Ative o SensorTag pressionando o botão de energia como na imagem a seguir e o LED verde deverá piscar.</span><span class="sxs-lookup"><span data-stu-id="2ea49-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![ativar Sensor Tag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="2ea49-130">Verificar dispositivos SensorTag executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2ea49-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="2ea49-131">Teste a conectividade entre a SensorTag e o NUC da Intel executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2ea49-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="2ea49-132">Substitua `{mac address}` pelo endereço MAC obtido na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="2ea49-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="2ea49-133">Obter a cadeia de conexão da SensorTag</span><span class="sxs-lookup"><span data-stu-id="2ea49-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="2ea49-134">Para obter a cadeia de conexão do Hub IoT do Azure da SensorTag, execute o seguinte comando no computador host:</span><span class="sxs-lookup"><span data-stu-id="2ea49-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="2ea49-135">`{IoT hub name}` é o nome do hub IoT usado.</span><span class="sxs-lookup"><span data-stu-id="2ea49-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="2ea49-136">Use o gateway IoT como o valor de `{resource group name}` e use mydevice como o valor de `{device id}` se você não tiver alterado o valor na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="2ea49-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="2ea49-137">Configurar o aplicativo de exemplo BLE</span><span class="sxs-lookup"><span data-stu-id="2ea49-137">Configure the BLE sample application</span></span>

<span data-ttu-id="2ea49-138">Para configurar e executar o aplicativo de exemplo BLE, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="2ea49-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="2ea49-139">Abra `config-sensortag.json` no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2ea49-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![instantâneo da configuração da sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="2ea49-141">Faça as seguintes substituições no código:</span><span class="sxs-lookup"><span data-stu-id="2ea49-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="2ea49-142">Substitua `[IoT hub name]` pelo nome do Hub IoT usado.</span><span class="sxs-lookup"><span data-stu-id="2ea49-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="2ea49-143">Substitua `[IoT device connection string]` pela cadeia de conexão da SensorTag que você obteve.</span><span class="sxs-lookup"><span data-stu-id="2ea49-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="2ea49-144">Substitua `[device_mac_address]` pelo endereço MAC da SensorTag que você obteve.</span><span class="sxs-lookup"><span data-stu-id="2ea49-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="2ea49-145">Execute o aplicativo de exemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="2ea49-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="2ea49-146">Para executar o aplicativo de exemplo BLE, siga estas etapas no computador host:</span><span class="sxs-lookup"><span data-stu-id="2ea49-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="2ea49-147">Ative a SensorTag.</span><span class="sxs-lookup"><span data-stu-id="2ea49-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="2ea49-148">Implante e execute o aplicativo de exemplo BLE no NUC da Intel executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2ea49-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="2ea49-149">Verificar se o aplicativo de exemplo BLE funciona</span><span class="sxs-lookup"><span data-stu-id="2ea49-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="2ea49-150">Você verá agora algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ea49-150">You should now see an output like the following:</span></span>

![Saída do aplicativo de exemplo BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="2ea49-152">O aplicativo de exemplo continua coletando dados de temperatura e enviando-os para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2ea49-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="2ea49-153">O aplicativo de exemplo é encerrado automaticamente após 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="2ea49-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="2ea49-154">Resumo</span><span class="sxs-lookup"><span data-stu-id="2ea49-154">Summary</span></span>

<span data-ttu-id="2ea49-155">Você configurou com êxito a conectividade entre a SensorTag e o NUC da Intel e executou um aplicativo de exemplo BLE que coleta e envia dados da SensorTag para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2ea49-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="2ea49-156">Você está pronto para aprender a verificar se o seu Hub IoT recebeu os dados.</span><span class="sxs-lookup"><span data-stu-id="2ea49-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ea49-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ea49-157">Next steps</span></span>
[<span data-ttu-id="2ea49-158">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="2ea49-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)