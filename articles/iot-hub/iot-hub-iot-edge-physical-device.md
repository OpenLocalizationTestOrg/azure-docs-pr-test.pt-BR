---
title: "Usar um dispositivo físico o Azure IoT Edge | Microsoft Docs"
description: "Como usar um dispositivo Texas Instruments SensorTag para enviar dados para um Hub IoT por meio de um gateway IoT Edge que executa em um dispositivo Raspberry Pi 3. O gateway é criado usando o Azure IoT Edge."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="aff93-104">Usar o Azure IoT Edge em um Raspberry Pi para encaminhar mensagens de dispositivo para nuvem para o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="aff93-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="aff93-105">Este passo a passo do [Exemplo de Bluetooth de baixa energia][lnk-ble-samplecode] demonstra como usar o [Azure IoT Edge][lnk-sdk] para:</span><span class="sxs-lookup"><span data-stu-id="aff93-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="aff93-106">Encaminhar telemetria do dispositivo para a nuvem para o Hub IoT de um dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="aff93-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="aff93-107">Rotear comandos do Hub IoT para um dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="aff93-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="aff93-108">Este passo a passo aborda:</span><span class="sxs-lookup"><span data-stu-id="aff93-108">This walkthrough covers:</span></span>

* <span data-ttu-id="aff93-109">**Arquitetura**: informações importantes de arquitetura sobre o exemplo de Bluetooth de baixa energia.</span><span class="sxs-lookup"><span data-stu-id="aff93-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="aff93-110">**Criar e executar**: as etapas necessárias para criar e executar a amostra.</span><span class="sxs-lookup"><span data-stu-id="aff93-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="aff93-111">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="aff93-111">Architecture</span></span>

<span data-ttu-id="aff93-112">O passo a passo mostra como criar e executar um gateway do IoT Edge em um Raspberry Pi 3 que execute o Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="aff93-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="aff93-113">O gateway é criado usando o IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="aff93-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="aff93-114">O exemplo usa um dispositivo BLE (Bluetooth de baixa energia) Texas Instruments SensorTag para coletar dados de temperatura.</span><span class="sxs-lookup"><span data-stu-id="aff93-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="aff93-115">Ao executar o gateway do IoT Edge, ele:</span><span class="sxs-lookup"><span data-stu-id="aff93-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="aff93-116">Conecta-se a um dispositivo SensorTag usando o protocolo de BLE (Bluetooth de baixa energia).</span><span class="sxs-lookup"><span data-stu-id="aff93-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="aff93-117">Conecta-se ao Hub IoT usando o protocolo HTTP.</span><span class="sxs-lookup"><span data-stu-id="aff93-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="aff93-118">Encaminha a telemetria do dispositivo SensorTag ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="aff93-119">Roteia comandos do Hub IoT para o dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="aff93-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="aff93-120">O gateway contém os seguintes módulos do IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="aff93-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="aff93-121">Um *módulo BLE* que interage com um dispositivo BLE para receber dados de temperatura do dispositivo e envia comandos para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aff93-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="aff93-122">Um *módulo BLE nuvem para dispositivo* que converte as mensagens JSON enviadas do Hub IoT em instruções BLE para o *módulo BLE*.</span><span class="sxs-lookup"><span data-stu-id="aff93-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="aff93-123">Um *módulo de agente* que registra todas as mensagens do gateway em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="aff93-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="aff93-124">Um *módulo de mapeamento de identidade* que faz a conversão entre endereços MAC dos dispositivos BLE e identidades de dispositivos do Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff93-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="aff93-125">Um *módulo do Hub IoT* que carrega dados de telemetria para um Hub IoT e recebe comandos de dispositivo de um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="aff93-126">Um *módulo de impressora BLE* que interpreta a telemetria do dispositivo BLE e imprime dados formatados para o console para habilitar a solução de problemas e depuração.</span><span class="sxs-lookup"><span data-stu-id="aff93-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="aff93-127">Como os dados fluem pelo gateway</span><span class="sxs-lookup"><span data-stu-id="aff93-127">How data flows through the gateway</span></span>

<span data-ttu-id="aff93-128">O diagrama de bloco a seguir ilustra o pipeline do fluxo de dados de upload de telemetria:</span><span class="sxs-lookup"><span data-stu-id="aff93-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![Pipeline de gateway de upload de telemetria](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="aff93-130">As etapas que um item de telemetria realiza ao viajar de um dispositivo BLE para o Hub IoT são:</span><span class="sxs-lookup"><span data-stu-id="aff93-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="aff93-131">O dispositivo BLE gera uma amostra de temperatura e a envia por Bluetooth para o módulo BLE no gateway.</span><span class="sxs-lookup"><span data-stu-id="aff93-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="aff93-132">O módulo BLE recebe a amostra e a publica para o agente com o endereço MAC do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aff93-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="aff93-133">O módulo de mapeamento de identidade capta essa mensagem e usa uma tabela interna para converter o endereço MAC do dispositivo em uma identidade de dispositivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="aff93-134">Uma identidade de dispositivo do Hub IoT consiste em uma ID de dispositivo e na chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aff93-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="aff93-135">O módulo de mapeamento de identidade publica uma nova mensagem que contém os dados de exemplo de temperatura, além do endereço MAC, a ID e a chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aff93-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="aff93-136">O módulo de Hub IoT recebe essa nova mensagem (gerada pelo módulo de mapeamento de identidade) e a publica no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="aff93-137">O módulo de agente registra todas as mensagens do agente em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="aff93-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="aff93-138">O diagrama de bloco a seguir ilustra o pipeline do fluxo de dados de comando do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="aff93-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![Pipeline do gateway de comando do dispositivo](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="aff93-140">O módulo de Hub IoT periodicamente sonda o Hub IoT quanto a novas mensagens de comando.</span><span class="sxs-lookup"><span data-stu-id="aff93-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="aff93-141">Quando o módulo de Hub IoT recebe uma nova mensagem de comando, ele a publica no agente.</span><span class="sxs-lookup"><span data-stu-id="aff93-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="aff93-142">O módulo de mapeamento de identidade capta a mensagem de comando e usa uma tabela interna para converter a ID do dispositivo Hub IoT para um endereço MAC do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aff93-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="aff93-143">Em seguida, ele publica uma nova mensagem que inclui o endereço MAC do dispositivo de destino no mapa de propriedades da mensagem.</span><span class="sxs-lookup"><span data-stu-id="aff93-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="aff93-144">O módulo Nuvem para dispositivo BLE pega essa mensagem e a converte na instrução BLE adequada para o módulo BLE.</span><span class="sxs-lookup"><span data-stu-id="aff93-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="aff93-145">Em seguida, ele publica uma nova mensagem.</span><span class="sxs-lookup"><span data-stu-id="aff93-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="aff93-146">O módulo BLE capta essa mensagem e executa a instrução de E/S se comunicando com o dispositivo BLE.</span><span class="sxs-lookup"><span data-stu-id="aff93-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="aff93-147">O módulo de agente registra todas as mensagens do agente em um arquivo de disco.</span><span class="sxs-lookup"><span data-stu-id="aff93-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aff93-148">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aff93-148">Prerequisites</span></span>

<span data-ttu-id="aff93-149">Para concluir este tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff93-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="aff93-150">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="aff93-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="aff93-151">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="aff93-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="aff93-152">É necessário um cliente SSH em seu computador desktop para que você possa acessar remotamente a linha de comando no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="aff93-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="aff93-153">O Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="aff93-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="aff93-154">Recomendamos o uso de [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="aff93-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="aff93-155">A maioria das distribuições do Linux e Mac OS incluem o utilitário de linha de comando do SSH.</span><span class="sxs-lookup"><span data-stu-id="aff93-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="aff93-156">Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="aff93-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="aff93-157">Prepare seu hardware</span><span class="sxs-lookup"><span data-stu-id="aff93-157">Prepare your hardware</span></span>

<span data-ttu-id="aff93-158">Este tutorial presume que você esteja usando um dispositivo [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) conectado a um Raspberry Pi 3 que executa o Raspbian.</span><span class="sxs-lookup"><span data-stu-id="aff93-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="aff93-159">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="aff93-159">Install Raspbian</span></span>

<span data-ttu-id="aff93-160">Você pode usar uma das opções a seguir para instalar o Raspbian em seu dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="aff93-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="aff93-161">Para instalar a versão mais recente do Raspbian, use a interface do usuário gráfica [NOOBS][lnk-noobs].</span><span class="sxs-lookup"><span data-stu-id="aff93-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="aff93-162">[Baixe][lnk-raspbian] e grave manualmente a imagem mais recente do sistema operacional Raspbian em um cartão SD.</span><span class="sxs-lookup"><span data-stu-id="aff93-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="aff93-163">Entre e acesse o terminal</span><span class="sxs-lookup"><span data-stu-id="aff93-163">Sign in and access the terminal</span></span>

<span data-ttu-id="aff93-164">Você tem duas opções para acessar um ambiente de terminal no seu Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="aff93-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="aff93-165">Se você tiver um teclado e um monitor conectado ao seu Raspberry Pi, você pode usar a GUI do Raspbian para acessar uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="aff93-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="aff93-166">Acesse a linha de comando em seu Raspberry Pi usando o SSH em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="aff93-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="aff93-167">Use uma janela de terminal na GUI</span><span class="sxs-lookup"><span data-stu-id="aff93-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="aff93-168">As credenciais padrões para Raspbian são o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="aff93-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="aff93-169">Na barra de tarefas na GUI, você pode iniciar o utilitário **Terminal** usando o ícone que se parece com um monitor.</span><span class="sxs-lookup"><span data-stu-id="aff93-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="aff93-170">Entre com o SSH</span><span class="sxs-lookup"><span data-stu-id="aff93-170">Sign in with SSH</span></span>

<span data-ttu-id="aff93-171">Você pode usar o SSH para acesso de linha de comando para o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="aff93-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="aff93-172">O artigo [SSH (Secure Shell)][lnk-pi-ssh] descreve como configurar SSH em seu Raspberry Pi e como conectar-se a partir do [Windows][lnk-ssh-windows] ou [Linux e Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="aff93-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="aff93-173">Entre com o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="aff93-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="aff93-174">Instalar o BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="aff93-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="aff93-175">Os módulos BLE se comunicar com o hardware de Bluetooth usando a pilha de BlueZ.</span><span class="sxs-lookup"><span data-stu-id="aff93-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="aff93-176">Você precisa ter a versão 5.37 do BlueZ para que os módulos funcionem corretamente.</span><span class="sxs-lookup"><span data-stu-id="aff93-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="aff93-177">Essas instruções fazem com que a versão correta do BlueZ esteja instalada.</span><span class="sxs-lookup"><span data-stu-id="aff93-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="aff93-178">Pare o daemon do bluetooth atual:</span><span class="sxs-lookup"><span data-stu-id="aff93-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="aff93-179">Instale as dependências de BlueZ:</span><span class="sxs-lookup"><span data-stu-id="aff93-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="aff93-180">Baixe o código-fonte do BlueZ de bluez.org:</span><span class="sxs-lookup"><span data-stu-id="aff93-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="aff93-181">Descompacte o código-fonte:</span><span class="sxs-lookup"><span data-stu-id="aff93-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="aff93-182">Altere os diretórios para a pasta recém-criada:</span><span class="sxs-lookup"><span data-stu-id="aff93-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="aff93-183">Configure o código BlueZ a ser compilado:</span><span class="sxs-lookup"><span data-stu-id="aff93-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="aff93-184">Compile o BlueZ:</span><span class="sxs-lookup"><span data-stu-id="aff93-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="aff93-185">Após compilar o BlueZ, instale-o:</span><span class="sxs-lookup"><span data-stu-id="aff93-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="aff93-186">Altere a configuração de serviço systemd para o bluetooth a fim de que ele aponte para o novo daemon de bluetooth no arquivo `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="aff93-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="aff93-187">Substitua a linha 'ExecStart' pelo seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="aff93-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="aff93-188">Habilitar conectividade para o dispositivo SensorTag de seu dispositivo Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="aff93-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="aff93-189">Antes de executar o exemplo, você precisa verificar se seu Raspberry Pi 3 pode se conectar ao dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="aff93-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="aff93-190">Verifique se o utilitário `rfkill` está instalado:</span><span class="sxs-lookup"><span data-stu-id="aff93-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="aff93-191">Desbloqueie o Bluetooth no Raspberry Pi 3 e verifique se o número de versão é **5.37**:</span><span class="sxs-lookup"><span data-stu-id="aff93-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="aff93-192">Para acessar o shell de bluetooth interativo, inicie o serviço de bluetooth e execute o comando **bluetoothctl**:</span><span class="sxs-lookup"><span data-stu-id="aff93-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="aff93-193">Digite o comando **power on** para ligar o controlador bluetooth.</span><span class="sxs-lookup"><span data-stu-id="aff93-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="aff93-194">O comando retorna saídas semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="aff93-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="aff93-195">No shell interativo bluetooth, digite o comando **scan on** para verificar se há dispositivos bluetooth.</span><span class="sxs-lookup"><span data-stu-id="aff93-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="aff93-196">O comando retorna saídas semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="aff93-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="aff93-197">Torne o dispositivo SensorTag detectável pressionando o botão pequeno (o LED verde deve piscar).</span><span class="sxs-lookup"><span data-stu-id="aff93-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="aff93-198">O Raspberry Pi 3 deve detectar o dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="aff93-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="aff93-199">Neste exemplo, você pode ver que é o endereço MAC do dispositivo SensorTag é **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="aff93-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="aff93-200">Desligue a verificação inserindo o comando **scan off**:</span><span class="sxs-lookup"><span data-stu-id="aff93-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="aff93-201">Conecte-se ao dispositivo SensorTag usando seu endereço MAC inserindo **connect \<endereço MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="aff93-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="aff93-202">A saída de exemplo a seguir é abreviada para fins de esclarecimento:</span><span class="sxs-lookup"><span data-stu-id="aff93-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="aff93-203">Você pode listar as características do GATT do dispositivo novamente usando o comando **list-attributes**.</span><span class="sxs-lookup"><span data-stu-id="aff93-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="aff93-204">Agora você pode se desconectar do dispositivo usando o comando **disconnect** e sair do shell Bluetooth usando o comando **quit**:</span><span class="sxs-lookup"><span data-stu-id="aff93-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="aff93-205">Agora você está pronto para executar o exemplo de BLE IoT Edge no Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="aff93-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="aff93-206">Executar o exemplo de IoT Edge BLE</span><span class="sxs-lookup"><span data-stu-id="aff93-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="aff93-207">Para executar o exemplo de IoT Edge BLE, você precisará concluir três tarefas:</span><span class="sxs-lookup"><span data-stu-id="aff93-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="aff93-208">Configurar dois dispositivos de exemplo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="aff93-209">Crie o IoT Edge em seu dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="aff93-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="aff93-210">Configure e execute o exemplo de BLE no dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="aff93-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="aff93-211">No momento da redação desse artigo, o IoT Edge dava suporte apenas a módulos BLE em gateways em execução no Linux.</span><span class="sxs-lookup"><span data-stu-id="aff93-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="aff93-212">Configurar dois dispositivos de exemplo em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="aff93-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="aff93-213">[Crie um Hub IoT][lnk-create-hub] em sua assinatura do Azure. Você precisará do nome do hub para concluir este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="aff93-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="aff93-214">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="aff93-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="aff93-215">Adicione um dispositivo chamado **SensorTag_01** ao hub IoT e anote sua ID e chave de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aff93-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="aff93-216">Você pode usar as ferramentas do [iothub-explorer ou o Gerenciador de Dispositivos][lnk-explorer-tools] para adicionar esse dispositivo ao Hub IoT que criou na etapa anterior e para recuperar sua chave.</span><span class="sxs-lookup"><span data-stu-id="aff93-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="aff93-217">Você mapeia este dispositivo para o dispositivo SensorTag quando configura o gateway.</span><span class="sxs-lookup"><span data-stu-id="aff93-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="aff93-218">Criar o Azure IoT Edge no Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="aff93-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="aff93-219">Instalar dependências para o Azure IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="aff93-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="aff93-220">Use os seguintes comandos para clonar o IoT Edge e todos os seus submódulos em seu diretório inicial:</span><span class="sxs-lookup"><span data-stu-id="aff93-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="aff93-221">Quando você tiver uma cópia completa do repositório do IoT Edge em seu Raspberry Pi 3, poderá criá-lo usando o comando a seguir na pasta que contém o SDK:</span><span class="sxs-lookup"><span data-stu-id="aff93-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="aff93-222">Configurar e execute o exemplo de BLE em seu Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="aff93-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="aff93-223">Para inicializar e executar o exemplo, configure cada módulo IoT Edge que participe do gateway.</span><span class="sxs-lookup"><span data-stu-id="aff93-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="aff93-224">Essa configuração é fornecida em um arquivo JSON e você precisa configurar todos os cinco módulos IoT Edge participantes.</span><span class="sxs-lookup"><span data-stu-id="aff93-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="aff93-225">Há um arquivo JSON de exemplo no repositório chamado **gateway\_sample.json**, que pode ser usado como ponto de partida para criar seu próprio arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="aff93-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="aff93-226">Esse arquivo está na pasta **samples/ble_gateway/src** na cópia local do repositório do IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="aff93-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="aff93-227">As seções a seguir descrevem como editar esse arquivo de configuração para o exemplo de BLE e pressupõem que o repositório do IoT Edge está na pasta **/home/pi/azure-iot-gateway-sdk/** do Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="aff93-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="aff93-228">Se o repositório estiver em outro lugar, ajuste os caminhos adequadamente.</span><span class="sxs-lookup"><span data-stu-id="aff93-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="aff93-229">Configuração do agente</span><span class="sxs-lookup"><span data-stu-id="aff93-229">Logger configuration</span></span>

<span data-ttu-id="aff93-230">Pressupondo que o repositório de gateway esteja localizado na pasta **/home/pi/iot-edge/**, configure o módulo de agente da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="aff93-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="aff93-231">Configuração do módulo BLE</span><span class="sxs-lookup"><span data-stu-id="aff93-231">BLE module configuration</span></span>

<span data-ttu-id="aff93-232">A configuração de exemplo do dispositivo BLE pressupõe um dispositivo Texas Instruments SensorTag.</span><span class="sxs-lookup"><span data-stu-id="aff93-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="aff93-233">Qualquer dispositivo BLE padrão que pode operar como um GATT periférico deve funcionar, mas você talvez precise atualizar as IDs de característica GATT e os dados.</span><span class="sxs-lookup"><span data-stu-id="aff93-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="aff93-234">Adicione o endereço MAC do dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="aff93-234">Add the MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="aff93-235">Se você não estiver usando um dispositivo SensorTag, leia a documentação do seu dispositivo BLE para determinar se é necessário atualizar os valores de dados e IDs características GATT.</span><span class="sxs-lookup"><span data-stu-id="aff93-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="aff93-236">módulo do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="aff93-236">IoT Hub module</span></span>

<span data-ttu-id="aff93-237">Adicione o nome do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="aff93-238">O valor do sufixo é geralmente **azure-devices.net**:</span><span class="sxs-lookup"><span data-stu-id="aff93-238">The suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="aff93-239">Configuração do módulo de mapeamento de identidade</span><span class="sxs-lookup"><span data-stu-id="aff93-239">Identity mapping module configuration</span></span>

<span data-ttu-id="aff93-240">Adicione o endereço MAC do dispositivo SensorTag e a ID e a chave do dispositivo **SensorTag_01** adicionado ao seu Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="aff93-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="aff93-241">Configuração do módulo de impressora BLE</span><span class="sxs-lookup"><span data-stu-id="aff93-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="aff93-242">Configuração do módulo BLEC2D</span><span class="sxs-lookup"><span data-stu-id="aff93-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="aff93-243">Configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="aff93-243">Routing Configuration</span></span>

<span data-ttu-id="aff93-244">A configuração abaixo garante o seguinte roteamento entre módulos IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="aff93-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="aff93-245">O módulo **Agente** recebe e registra todas as mensagens.</span><span class="sxs-lookup"><span data-stu-id="aff93-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="aff93-246">O módulo **SensorTag** envia mensagens para os módulos **mapeamento** e **Impressora BLE**.</span><span class="sxs-lookup"><span data-stu-id="aff93-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="aff93-247">O módulo **mapeamento** envia mensagens ao módulo **IoTHub** a ser enviado ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="aff93-248">O módulo **IoTHub** envia as mensagens de volta para o módulo **mapeamento**.</span><span class="sxs-lookup"><span data-stu-id="aff93-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="aff93-249">O módulo **mapeamento** envia mensagens para o módulo **BLEC2D**.</span><span class="sxs-lookup"><span data-stu-id="aff93-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="aff93-250">O módulo **BLEC2D** envia as mensagens de volta para o módulo **SensorTag**.</span><span class="sxs-lookup"><span data-stu-id="aff93-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="aff93-251">Para executar o exemplo, passe o caminho até o arquivo de configuração JSON como um parâmetro para o binário **ble\_gateway**.</span><span class="sxs-lookup"><span data-stu-id="aff93-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="aff93-252">O comando a seguir pressupõe que você esteja usando o arquivo de configuração **gateway_sample.json**.</span><span class="sxs-lookup"><span data-stu-id="aff93-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="aff93-253">Execute este comando da pasta **iot-edge** no Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="aff93-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="aff93-254">Talvez seja necessário pressionar o botão pequeno no dispositivo SensorTag para torná-lo detectável antes de executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="aff93-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="aff93-255">Ao executar o exemplo, você pode usar o [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou a ferramenta [iothub-explorer](https://github.com/Azure/iothub-explorer) para monitorar as mensagens que o gateway do IoT Edge encaminha para o dispositivo SensorTag.</span><span class="sxs-lookup"><span data-stu-id="aff93-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="aff93-256">Por exemplo, usando o iothub-explorer, você pode monitorar as mensagens de dispositivo para nuvem usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="aff93-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="aff93-257">Envie mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="aff93-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="aff93-258">O módulo BLE também dá suporte ao envio de comandos do Hub IoT para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aff93-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="aff93-259">Você pode usar a ferramenta [Gerenciador de Dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou o [iothub-explorer](https://github.com/Azure/iothub-explorer) para enviar as mensagens JSON que o módulo de gateway BLE encaminha para o dispositivo BLE.</span><span class="sxs-lookup"><span data-stu-id="aff93-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="aff93-260">Se você estiver usando o dispositivo Texas Instruments SensorTag, você poderá ativar o LED vermelho, o LED verde ou a campainha enviando comandos do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aff93-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="aff93-261">Antes de enviar comandos do Hub IoT, primeiro envie as duas mensagens JSON a seguir nesta ordem.</span><span class="sxs-lookup"><span data-stu-id="aff93-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="aff93-262">Em seguida, você pode enviar um dos comandos para ligar as luzes ou a campainha.</span><span class="sxs-lookup"><span data-stu-id="aff93-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="aff93-263">Redefinir todos os LEDs e a campainha (desativá-los):</span><span class="sxs-lookup"><span data-stu-id="aff93-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="aff93-264">Configurar a E/S como 'remota':</span><span class="sxs-lookup"><span data-stu-id="aff93-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="aff93-265">Agora, você pode enviar um dos seguintes comandos para ligar as luzes ou a campainha no dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="aff93-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="aff93-266">Ativar o LED vermelho:</span><span class="sxs-lookup"><span data-stu-id="aff93-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="aff93-267">Ativar o LED verde:</span><span class="sxs-lookup"><span data-stu-id="aff93-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="aff93-268">Ativar a campainha:</span><span class="sxs-lookup"><span data-stu-id="aff93-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="aff93-269">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aff93-269">Next Steps</span></span>

<span data-ttu-id="aff93-270">Se você quiser compreender de maneira mais avançada o IoT Edge e experimentar alguns exemplos de código, acesse os seguintes recursos e tutoriais para desenvolvedores:</span><span class="sxs-lookup"><span data-stu-id="aff93-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="aff93-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="aff93-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="aff93-272">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="aff93-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="aff93-273">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="aff93-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
