---
title: Usar um gateway IoT para conectar um dispositivo ao Hub IoT do Azure | Microsoft Docs
description: Saiba como usar o Intel NUC como um gateway IoT para conectar um SensorTag da TI e enviar dados de sensor ao Hub IoT do Azure na nuvem.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gateway iot conectar dispositivo para a nuvem
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="c4d33-104">Usar o gateway IoT para conectar as coisas à nuvem – SensorTag para o Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="c4d33-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="c4d33-105">Antes de iniciar este tutorial, conclua a [Configurar o Intel NUC como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="c4d33-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="c4d33-106">Em [Configurar o Intel NUC como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), você configura o dispositivo Intel NUC como um gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c4d33-107">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c4d33-107">What you will learn</span></span>

<span data-ttu-id="c4d33-108">Você aprende a usar um gateway IoT para conectar um SensorTag da Texas Instruments (CC2650STK) ao Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d33-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="c4d33-109">O gateway IoT envia dados de temperatura e umidade coletados do SensorTag para o Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d33-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c4d33-110">O que você fará</span><span class="sxs-lookup"><span data-stu-id="c4d33-110">What you will do</span></span>

- <span data-ttu-id="c4d33-111">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-111">Create an IoT hub.</span></span>
- <span data-ttu-id="c4d33-112">Registrar um dispositivo no Hub IoT para o SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c4d33-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="c4d33-113">Habilitar a conexão entre o gateway IoT e o SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c4d33-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="c4d33-114">Executar um aplicativo de exemplo BLE para enviar dados do SensorTag para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c4d33-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="c4d33-115">What you need</span></span>

- <span data-ttu-id="c4d33-116">Do tutorial [Configurar o Intel NUC como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) concluído, no qual você configura o Intel NUC como um gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="c4d33-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d33-117">An active Azure subscription.</span></span> <span data-ttu-id="c4d33-118">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c4d33-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="c4d33-119">Um cliente SSH executado no computador host.</span><span class="sxs-lookup"><span data-stu-id="c4d33-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="c4d33-120">Recomenda-se o PuTTY no Windows.</span><span class="sxs-lookup"><span data-stu-id="c4d33-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="c4d33-121">O Linux e o macOS já vêm com um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="c4d33-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="c4d33-122">Do endereço IP e do nome de usuário e a senha para acessar o gateway no cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="c4d33-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="c4d33-123">Uma conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="c4d33-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="c4d33-124">Aqui você registra esse novo dispositivo para o seu SensorTag</span><span class="sxs-lookup"><span data-stu-id="c4d33-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="c4d33-125">Habilitar a conexão entre o gateway IoT e o SensorTag</span><span class="sxs-lookup"><span data-stu-id="c4d33-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="c4d33-126">Nesta seção, você realiza as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="c4d33-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="c4d33-127">Obtém o endereço MAC do SensorTag para a conexão Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="c4d33-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="c4d33-128">Inicia uma conexão Bluetooth do gateway IoT com o SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c4d33-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="c4d33-129">Obter o endereço MAC do SensorTag para a conexão Bluetooth</span><span class="sxs-lookup"><span data-stu-id="c4d33-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="c4d33-130">No computador host, execute o cliente SSH e conecte-se ao gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="c4d33-131">Desbloqueie o Bluetooth, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4d33-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="c4d33-132">Inicie o serviço Bluetooth no gateway IoT e insira um shell de Bluetooth para configurar o Bluetooth, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c4d33-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="c4d33-133">Ligue o controlador Bluetooth, executando o seguinte comando no shell do Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="c4d33-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![ligar o controlador Bluetooth no gateway IoT com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="c4d33-135">Inicie a varredura por dispositivos Bluetooth próximos, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4d33-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![Procurar dispositivos Bluetooth próximos com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="c4d33-137">Pressione o botão de emparelhamento no SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c4d33-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="c4d33-138">O LED verde no SensorTag pisca.</span><span class="sxs-lookup"><span data-stu-id="c4d33-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="c4d33-139">No shell do Bluetooth, você verá que o SensorTag foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="c4d33-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="c4d33-140">Anote o endereço MAC do SensorTag.</span><span class="sxs-lookup"><span data-stu-id="c4d33-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="c4d33-141">Neste exemplo, o endereço MAC do SensorTag é `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="c4d33-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="c4d33-142">Desative a varredura, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4d33-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![Interromper a varredura de dispositivos Bluetooth próximos com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="c4d33-144">Iniciar uma conexão Bluetooth do gateway IoT com o SensorTag</span><span class="sxs-lookup"><span data-stu-id="c4d33-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="c4d33-145">Conecte-se ao SensorTag executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4d33-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Conectar ao SensorTag com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="c4d33-147">Desconecte do SensorTag e saia do shell do Bluetooth, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c4d33-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Desconectar do SensorTag com bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="c4d33-149">Você habilitou com êxito a conexão entre o SensorTag e o gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="c4d33-150">Executar um aplicativo de exemplo BLE para enviar dados do SensorTag para o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="c4d33-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="c4d33-151">O aplicativo de exemplo BLE (Bluetooth de Baixa Energia) é fornecido pelo Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="c4d33-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="c4d33-152">O aplicativo de exemplo coleta dados da conexão BLE e os envia ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="c4d33-153">Para executar o aplicativo de exemplo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="c4d33-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="c4d33-154">Configurar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c4d33-154">Configure the sample application.</span></span>
1. <span data-ttu-id="c4d33-155">Executar o aplicativo de exemplo no gateway IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="c4d33-156">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="c4d33-156">Configure the sample application</span></span>

1. <span data-ttu-id="c4d33-157">Acesse a pasta do aplicativo de exemplo, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4d33-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="c4d33-158">Abra o arquivo de configuração, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c4d33-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="c4d33-159">No arquivo de configuração, preencha os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="c4d33-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="c4d33-160">**IoTHubName**: o nome do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="c4d33-161">**IoTHubSuffix**: obtenha o IoTHubSuffix da chave primária da cadeia de conexão do dispositivo que você anotou.</span><span class="sxs-lookup"><span data-stu-id="c4d33-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="c4d33-162">Certifique-se de obter a chave primária da cadeia de conexão do dispositivo e não a chave primária da cadeia de conexão do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="c4d33-163">A chave primária da cadeia de conexão do dispositivo é no formato `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="c4d33-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="c4d33-164">**Transport**: o valor padrão é `amqp`.</span><span class="sxs-lookup"><span data-stu-id="c4d33-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="c4d33-165">Este valor mostra o protocolo durante o transporte.</span><span class="sxs-lookup"><span data-stu-id="c4d33-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="c4d33-166">Ele pode ser `http`, `amqp` ou `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="c4d33-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="c4d33-167">**macAddress**: o endereço MAC do SensorTag que você anotou.</span><span class="sxs-lookup"><span data-stu-id="c4d33-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="c4d33-168">**deviceID**: ID do dispositivo que você criou em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c4d33-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="c4d33-169">**deviceKey**: a chave primária da cadeia de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c4d33-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Concluir o arquivo de configuração do aplicativo BLE de exemplo](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="c4d33-171">Pressione `ESC` e digite `:wq` para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c4d33-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="c4d33-172">Executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="c4d33-172">Run the sample application</span></span>

1. <span data-ttu-id="c4d33-173">Verifique se o SensorTag está ligado.</span><span class="sxs-lookup"><span data-stu-id="c4d33-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="c4d33-174">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4d33-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="c4d33-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4d33-175">Next steps</span></span>

[<span data-ttu-id="c4d33-176">Usar o gateway IoT para transformação dos dados de sensor com o Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="c4d33-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
