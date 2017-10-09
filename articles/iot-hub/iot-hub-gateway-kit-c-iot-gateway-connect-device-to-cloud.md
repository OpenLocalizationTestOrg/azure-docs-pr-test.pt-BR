---
title: aaaUse um gateway de IoT tooconnect tooAzure um dispositivo IoT Hub | Microsoft Docs
description: "Saiba como toouse NUC Intel como um gateway de IoT tooconnect um SensorTag de TI e enviar os dados sensor tooAzure IoT Hub em Olá de nuvem."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conexão de gateway de IOT toocloud do dispositivo"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="4ba18-104">Usar IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4ba18-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="4ba18-105">Antes de iniciar este tutorial, conclua a [Configurar o Intel NUC como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="4ba18-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="4ba18-106">Em [configurar NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), configurar Olá Intel NUC dispositivo como um gateway de IoT.</span><span class="sxs-lookup"><span data-stu-id="4ba18-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4ba18-107">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="4ba18-107">What you will learn</span></span>

<span data-ttu-id="4ba18-108">Você aprenderá como toouse um gateway de IoT tooconnect um tooAzure Texas instrumentos SensorTag (CC2650STK) IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba18-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="4ba18-109">gateway de IoT Olá envia temperatura e umidade os dados coletados de saudação SensorTag tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba18-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4ba18-110">O que você fará</span><span class="sxs-lookup"><span data-stu-id="4ba18-110">What you will do</span></span>

- <span data-ttu-id="4ba18-111">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4ba18-111">Create an IoT hub.</span></span>
- <span data-ttu-id="4ba18-112">Registre um dispositivo no hub IoT de saudação para Olá SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4ba18-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="4ba18-113">Habilite conexão Olá entre o gateway de IoT hello e Olá SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4ba18-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="4ba18-114">Execute um Bilitar exemplo aplicativo toosend SensorTag tooyour IoT hub de dados.</span><span class="sxs-lookup"><span data-stu-id="4ba18-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4ba18-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="4ba18-115">What you need</span></span>

- <span data-ttu-id="4ba18-116">Do tutorial [Configurar o Intel NUC como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) concluído, no qual você configura o Intel NUC como um gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="4ba18-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="4ba18-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba18-117">An active Azure subscription.</span></span> <span data-ttu-id="4ba18-118">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="4ba18-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="4ba18-119">Um cliente SSH executado no computador host.</span><span class="sxs-lookup"><span data-stu-id="4ba18-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="4ba18-120">Recomenda-se o PuTTY no Windows.</span><span class="sxs-lookup"><span data-stu-id="4ba18-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="4ba18-121">O Linux e o macOS já vêm com um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="4ba18-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="4ba18-122">Olá endereço IP e Olá username e password tooaccess Olá gateway de cliente SSH hello.</span><span class="sxs-lookup"><span data-stu-id="4ba18-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="4ba18-123">Uma conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="4ba18-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="4ba18-124">Aqui você registra esse novo dispositivo para o seu SensorTag</span><span class="sxs-lookup"><span data-stu-id="4ba18-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="4ba18-125">Habilitar conexão Olá entre o gateway de IoT hello e Olá SensorTag</span><span class="sxs-lookup"><span data-stu-id="4ba18-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="4ba18-126">Nesta seção, você executará Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="4ba18-127">Obter endereço MAC Olá Olá SensorTag conexão Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="4ba18-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="4ba18-128">Inicie uma conexão de Bluetooth do hello IoT gateway toohello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4ba18-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="4ba18-129">Obter o endereço MAC Olá Olá SensorTag para conexão de Bluetooth</span><span class="sxs-lookup"><span data-stu-id="4ba18-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="4ba18-130">No computador de host Olá, execute o cliente SSH hello e conecte-se toohello IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="4ba18-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="4ba18-131">Desbloquear Bluetooth executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="4ba18-132">Iniciar serviço de Bluetooth do hello no gateway do IoT hello e insira um tooconfigure de shell Bluetooth Bluetooth executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="4ba18-133">Ligar o controlador de Bluetooth Olá executando Olá comando no hello shell Bluetooth a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![ligar o controlador de Bluetooth Olá no gateway do IoT Olá com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="4ba18-135">Inicie a varredura para dispositivos Bluetooth próximos executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![Procurar dispositivos Bluetooth próximos com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="4ba18-137">Pressione Olá emparelhamento botão Olá SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4ba18-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="4ba18-138">Olá verde LED no hello SensorTag pisca.</span><span class="sxs-lookup"><span data-stu-id="4ba18-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="4ba18-139">Em Olá Bluetooth shell, você deve ver Olá que sensortag foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="4ba18-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="4ba18-140">Anote Olá Olá SensorTag endereço MAC.</span><span class="sxs-lookup"><span data-stu-id="4ba18-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="4ba18-141">Neste exemplo, Olá endereço MAC de saudação SensorTag é `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="4ba18-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="4ba18-142">Desative a verificação de saudação executando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="4ba18-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![Interromper a varredura de dispositivos Bluetooth próximos com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="4ba18-144">Iniciar uma conexão de Bluetooth do hello IoT gateway toohello SensorTag</span><span class="sxs-lookup"><span data-stu-id="4ba18-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="4ba18-145">Conecte-se toohello SensorTag executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Conecte-se toohello SensorTag com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="4ba18-147">Desconectar Olá SensorTag e sair do shell de Bluetooth Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Desconectar Olá SensorTag com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="4ba18-149">Conexão Olá entre o gateway de IoT hello e Olá SensorTag estiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="4ba18-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="4ba18-150">Executar um Bilitar exemplo aplicativo toosend SensorTag tooyour IoT hub de dados</span><span class="sxs-lookup"><span data-stu-id="4ba18-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="4ba18-151">Olá aplicativo de exemplo de Bluetooth baixa energia (var) é fornecido pelo Azure IoT borda.</span><span class="sxs-lookup"><span data-stu-id="4ba18-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="4ba18-152">aplicativo de exemplo Hello coleta dados de conexão Bilitar e enviar o hub IoT do hello dados tooyou.</span><span class="sxs-lookup"><span data-stu-id="4ba18-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="4ba18-153">aplicativo de exemplo hello toorun, você precisa:</span><span class="sxs-lookup"><span data-stu-id="4ba18-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="4ba18-154">Configure o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="4ba18-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="4ba18-155">Execute o aplicativo de exemplo hello no gateway do IoT hello.</span><span class="sxs-lookup"><span data-stu-id="4ba18-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="4ba18-156">Configurar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="4ba18-156">Configure hello sample application</span></span>

1. <span data-ttu-id="4ba18-157">Vá toohello pasta do aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="4ba18-158">Abra o arquivo de configuração de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="4ba18-159">No arquivo de configuração hello, preencha Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="4ba18-160">**IoTHubName**: nome de saudação do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4ba18-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="4ba18-161">**IoTHubSuffix**: IoTHubSuffix obter da saudação chave primária da cadeia de caracteres de conexão de dispositivo Olá que você anotou para baixo.</span><span class="sxs-lookup"><span data-stu-id="4ba18-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="4ba18-162">Certifique-se de que você obter a chave primária de saudação da cadeia de caracteres de conexão de dispositivo hello, Olá não chave primária de sua cadeia de conexão de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4ba18-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="4ba18-163">chave primária de saudação da cadeia de caracteres de conexão de dispositivo hello está no formato de saudação do `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="4ba18-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="4ba18-164">**Transporte**: valor de padrão de saudação é `amqp`.</span><span class="sxs-lookup"><span data-stu-id="4ba18-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="4ba18-165">Esse valor mostra o protocolo de saudação durante transpotation.</span><span class="sxs-lookup"><span data-stu-id="4ba18-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="4ba18-166">Ele pode ser `http`, `amqp` ou `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="4ba18-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="4ba18-167">**macAddress**: Olá endereço MAC de saudação SensorTag que você anotou para baixo.</span><span class="sxs-lookup"><span data-stu-id="4ba18-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="4ba18-168">**deviceID**: ID do dispositivo Olá que você criou em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4ba18-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="4ba18-169">**deviceKey**: chave primária de saudação da cadeia de caracteres de conexão de dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4ba18-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Arquivo de configuração de saudação completa de saudação aplicativo de exemplo Bilitar](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="4ba18-171">Pressione `ESC` e tipo `:wq` toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ba18-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="4ba18-172">Executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="4ba18-172">Run hello sample application</span></span>

1. <span data-ttu-id="4ba18-173">Verifique se Olá que sensortag está ligado.</span><span class="sxs-lookup"><span data-stu-id="4ba18-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="4ba18-174">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba18-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="4ba18-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ba18-175">Next steps</span></span>

[<span data-ttu-id="4ba18-176">Usar o gateway IoT para transformação dos dados de sensor com o Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="4ba18-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
