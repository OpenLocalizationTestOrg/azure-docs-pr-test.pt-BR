---
title: "aaaUse um dispositivo físico com borda de IoT do Azure | Microsoft Docs"
description: "Como toouse um hub de IoT Texas instrumentos SensorTag dispositivo toosend dados tooan por meio de um gateway de borda IoT em execução em um dispositivo de framboesa Pi 3. gateway de saudação é criado usando o Azure IoT borda."
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
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="00e9e-104">Usar o Azure IoT borda em um tooIoT de mensagens de dispositivo para nuvem framboesa Pi tooforward Hub</span><span class="sxs-lookup"><span data-stu-id="00e9e-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="00e9e-105">Este passo a passo de saudação [exemplo de baixa energia Bluetooth] [ lnk-ble-samplecode] mostra como toouse [Azure IoT borda] [ lnk-sdk] para:</span><span class="sxs-lookup"><span data-stu-id="00e9e-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="00e9e-106">Encaminhe telemetria do dispositivo para nuvem tooIoT Hub de um dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="00e9e-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="00e9e-107">Comandos de rota do dispositivo físico do IoT Hub tooa.</span><span class="sxs-lookup"><span data-stu-id="00e9e-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="00e9e-108">Este passo a passo aborda:</span><span class="sxs-lookup"><span data-stu-id="00e9e-108">This walkthrough covers:</span></span>

* <span data-ttu-id="00e9e-109">**Arquitetura**: importantes informações arquitetônicas sobre Olá Bluetooth baixo consumo de energia de exemplo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="00e9e-110">**Compilar e executar**: Olá etapas necessárias toobuild e exemplo hello execução.</span><span class="sxs-lookup"><span data-stu-id="00e9e-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="00e9e-111">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="00e9e-111">Architecture</span></span>

<span data-ttu-id="00e9e-112">Olá passo a passo mostra como toobuild e execute um gateway de extremidade IoT em um framboesa Pi 3 que executa Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="00e9e-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="00e9e-113">gateway de saudação é criado usando a borda de IoT.</span><span class="sxs-lookup"><span data-stu-id="00e9e-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="00e9e-114">exemplo Hello usa um Texas instrumentos SensorTag Bluetooth baixa energia (var) dispositivo toocollect temperatura de dados.</span><span class="sxs-lookup"><span data-stu-id="00e9e-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="00e9e-115">Quando você executa Olá gateway de borda IoT-lo:</span><span class="sxs-lookup"><span data-stu-id="00e9e-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="00e9e-116">Conecta tooa SensorTag dispositivo usando o protocolo do hello Bluetooth baixa energia (var).</span><span class="sxs-lookup"><span data-stu-id="00e9e-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="00e9e-117">Conecta-se tooIoT Hub usando o protocolo de saudação HTTP.</span><span class="sxs-lookup"><span data-stu-id="00e9e-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="00e9e-118">Encaminha a telemetria de saudação SensorTag dispositivo tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="00e9e-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="00e9e-119">Rotas de comandos de dispositivo do IoT Hub toohello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="00e9e-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="00e9e-120">gateway Olá contém Olá módulos de borda IoT a seguir:</span><span class="sxs-lookup"><span data-stu-id="00e9e-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="00e9e-121">Um *módulo Bilitar* que interage com um dado de temperatura Bilitar dispositivo tooreceive de saudação dispositivo e enviar comandos toohello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="00e9e-122">Um *módulo do Bilitar nuvem toodevice* que converte mensagens JSON enviadas do IoT Hub em instruções Bilitar para Olá *módulo Bilitar*.</span><span class="sxs-lookup"><span data-stu-id="00e9e-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="00e9e-123">Um *módulo agente* que registra todos os gateway mensagens tooa arquivo local.</span><span class="sxs-lookup"><span data-stu-id="00e9e-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="00e9e-124">Um *módulo de mapeamento de identidade* que faz a conversão entre endereços MAC dos dispositivos BLE e identidades de dispositivos do Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="00e9e-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="00e9e-125">Um *módulo de IoT Hub* que carrega o hub IoT do telemetria dados tooan e recebe comandos de dispositivo de um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="00e9e-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="00e9e-126">Um *módulo de impressora Bilitar* que interprete a telemetria de dispositivo de Bilitar hello e imprime os dados formatados toohello console tooenable solução de problemas e depuração.</span><span class="sxs-lookup"><span data-stu-id="00e9e-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="00e9e-127">Como os dados fluem por meio do gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="00e9e-127">How data flows through hello gateway</span></span>

<span data-ttu-id="00e9e-128">Olá bloco diagrama a seguir ilustra o pipeline de fluxo de dados de carregamento do hello telemetria:</span><span class="sxs-lookup"><span data-stu-id="00e9e-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Pipeline de gateway de upload de telemetria](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="00e9e-130">etapas de saudação que viajam de um tooIoT de dispositivo Bilitar entra em um item de telemetria Hub são:</span><span class="sxs-lookup"><span data-stu-id="00e9e-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="00e9e-131">dispositivo de Bilitar Hello gera uma amostra de temperatura e envia módulo de Bilitar toohello Bluetooth no gateway hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="00e9e-132">módulo de Bilitar Olá recebe exemplo hello e publica broker toohello junto com o endereço MAC de saudação do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="00e9e-133">módulo de mapeamento de identidade de saudação pega essa mensagem e usa uma saudação tootranslate de tabela interna endereço MAC do dispositivo de saudação em uma identidade de dispositivo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="00e9e-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="00e9e-134">Uma identidade de dispositivo do Hub IoT consiste em uma ID de dispositivo e na chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="00e9e-135">módulo de mapeamento de identidade Olá publica uma nova mensagem que contém dados de exemplo hello temperatura, o endereço MAC de saudação do dispositivo de hello, ID do dispositivo hello e chave do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="00e9e-136">Olá módulo IoT Hub recebe essa mensagem nova (gerada pelo módulo de mapeamento de identidade de saudação) e publica tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="00e9e-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="00e9e-137">módulo de agente Olá registra todas as mensagens de arquivo local da saudação broker tooa.</span><span class="sxs-lookup"><span data-stu-id="00e9e-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="00e9e-138">Olá bloco diagrama a seguir ilustra Olá pipeline de fluxo de dados de comando de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="00e9e-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Pipeline do gateway de comando do dispositivo](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="00e9e-140">Olá IoT Hub módulo periodicamente sonda Olá hub IoT para novas mensagens de comando.</span><span class="sxs-lookup"><span data-stu-id="00e9e-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="00e9e-141">Quando Olá módulo IoT Hub recebe uma nova mensagem de comando, ela publica toohello broker.</span><span class="sxs-lookup"><span data-stu-id="00e9e-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="00e9e-142">módulo de mapeamento de identidade Olá pega a mensagem de saudação do comando e usa uma saudação tootranslate de tabela interna IoT Hub dispositivo ID tooa dispositivo endereço MAC.</span><span class="sxs-lookup"><span data-stu-id="00e9e-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="00e9e-143">Em seguida, publica uma nova mensagem que inclui o endereço MAC de saudação do dispositivo de destino Olá no mapa de propriedades de saudação de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="00e9e-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="00e9e-144">módulo de nuvem para dispositivo Bilitar Olá pega essa mensagem e converte em instrução Bilitar adequada de Olá para o módulo de Bilitar Olá.</span><span class="sxs-lookup"><span data-stu-id="00e9e-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="00e9e-145">Em seguida, ele publica uma nova mensagem.</span><span class="sxs-lookup"><span data-stu-id="00e9e-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="00e9e-146">módulo de Bilitar Olá pega essa mensagem e executa a instrução de e/s de saudação comunicando-se com o dispositivo de Bilitar hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="00e9e-147">módulo de agente Olá registra todas as mensagens do arquivo de disco Olá broker tooa.</span><span class="sxs-lookup"><span data-stu-id="00e9e-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00e9e-148">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00e9e-148">Prerequisites</span></span>

<span data-ttu-id="00e9e-149">toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="00e9e-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="00e9e-150">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="00e9e-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="00e9e-151">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="00e9e-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="00e9e-152">Você precisa cliente SSH no seu tooenable computador desktop você tooremotely acesso Olá linha de comando em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="00e9e-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="00e9e-153">O Windows não inclui um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="00e9e-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="00e9e-154">Recomendamos o uso de [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="00e9e-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="00e9e-155">A maioria das distribuições do Linux e Mac OS incluem o utilitário SSH de linha de comando do hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="00e9e-156">Para obter mais informações, consulte [SSH usando o Linux ou Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="00e9e-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="00e9e-157">Prepare seu hardware</span><span class="sxs-lookup"><span data-stu-id="00e9e-157">Prepare your hardware</span></span>

<span data-ttu-id="00e9e-158">Este tutorial presume que você está usando um [Texas instrumentos SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo conectado tooa framboesa Pi 3 executando Raspbian.</span><span class="sxs-lookup"><span data-stu-id="00e9e-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="00e9e-159">Instalar Raspbian</span><span class="sxs-lookup"><span data-stu-id="00e9e-159">Install Raspbian</span></span>

<span data-ttu-id="00e9e-160">Você pode usar qualquer um dos Olá opções tooinstall Raspbian a seguir em seu dispositivo framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="00e9e-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="00e9e-161">versão mais recente do hello tooinstall de Raspbian, use Olá [NOOBS] [ lnk-noobs] interface gráfica do usuário.</span><span class="sxs-lookup"><span data-stu-id="00e9e-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="00e9e-162">Manualmente [baixar] [ lnk-raspbian] e gravar a imagem mais recente de saudação do cartão de saudação Raspbian sistema operacional tooan SD.</span><span class="sxs-lookup"><span data-stu-id="00e9e-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="00e9e-163">Entrar e acessar terminal Olá</span><span class="sxs-lookup"><span data-stu-id="00e9e-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="00e9e-164">Você tem um ambiente de terminal tooaccess de duas opções com seu Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="00e9e-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="00e9e-165">Se você tiver um teclado e monitorar tooyour conectado framboesa Pi, você pode usar o hello GUI Raspbian tooaccess uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="00e9e-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="00e9e-166">Acesso a linha de comando do hello no seu Pi framboesa usando SSH em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="00e9e-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="00e9e-167">Use uma janela de terminal Olá GUI</span><span class="sxs-lookup"><span data-stu-id="00e9e-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="00e9e-168">credenciais de padrão de saudação para Raspbian são o nome de usuário **pi** e a senha **framboesa**.</span><span class="sxs-lookup"><span data-stu-id="00e9e-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="00e9e-169">Na barra de tarefas de saudação em Olá GUI, você pode iniciar Olá **Terminal** utilitário usando o ícone de saudação que se parece com um monitor.</span><span class="sxs-lookup"><span data-stu-id="00e9e-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="00e9e-170">Entre com o SSH</span><span class="sxs-lookup"><span data-stu-id="00e9e-170">Sign in with SSH</span></span>

<span data-ttu-id="00e9e-171">Você pode usar o SSH para acesso de linha de comando tooyour framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="00e9e-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="00e9e-172">artigo Olá [SSH (Secure Shell)] [ lnk-pi-ssh] descreve como tooconfigure SSH com o Pi framboesa e como tooconnect de [Windows] [ lnk-ssh-windows] ou [Sistema operacional Linux e Mac][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="00e9e-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="00e9e-173">Entre com o nome de usuário **pi** e a senha **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="00e9e-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="00e9e-174">Instalar o BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="00e9e-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="00e9e-175">módulos de Bilitar Olá falam toohello Bluetooth hardware por meio da pilha de BlueZ hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="00e9e-176">Você precisa versão 5.37 do BlueZ para Olá módulos toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="00e9e-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="00e9e-177">Essas instruções Certifique-se de saudação a versão correta do BlueZ está instalada.</span><span class="sxs-lookup"><span data-stu-id="00e9e-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="00e9e-178">Pare o daemon do hello atual bluetooth:</span><span class="sxs-lookup"><span data-stu-id="00e9e-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="00e9e-179">Instale dependências de BlueZ hello:</span><span class="sxs-lookup"><span data-stu-id="00e9e-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="00e9e-180">Baixe o código-fonte Olá BlueZ do bluez.org:</span><span class="sxs-lookup"><span data-stu-id="00e9e-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="00e9e-181">Descompacte o código-fonte hello:</span><span class="sxs-lookup"><span data-stu-id="00e9e-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="00e9e-182">Alterar pasta de toohello recém-criado de diretórios:</span><span class="sxs-lookup"><span data-stu-id="00e9e-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="00e9e-183">Configure Olá BlueZ código toobe criado:</span><span class="sxs-lookup"><span data-stu-id="00e9e-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="00e9e-184">Compile o BlueZ:</span><span class="sxs-lookup"><span data-stu-id="00e9e-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="00e9e-185">Após compilar o BlueZ, instale-o:</span><span class="sxs-lookup"><span data-stu-id="00e9e-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="00e9e-186">Alteração da configuração do serviço systemd para bluetooth para que ele aponte toohello novo daemon bluetooth no arquivo hello `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="00e9e-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="00e9e-187">Substitua linha de 'ExecStart' hello Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="00e9e-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="00e9e-188">Habilitar o dispositivo de SensorTag toohello conectividade do dispositivo framboesa Pi 3</span><span class="sxs-lookup"><span data-stu-id="00e9e-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="00e9e-189">Antes de exemplo hello em execução, é necessário tooverify seu framboesa Pi 3 pode conectar-se toohello SensorTag dispositivo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="00e9e-190">Certifique-se de saudação `rfkill` utilitário é instalado:</span><span class="sxs-lookup"><span data-stu-id="00e9e-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="00e9e-191">Desbloquear bluetooth em Olá framboesa Pi 3 e verifique se o número de versão de saudação é **5.37**:</span><span class="sxs-lookup"><span data-stu-id="00e9e-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="00e9e-192">tooenter shell de bluetooth interativo hello, iniciar o serviço de bluetooth hello e executar Olá **bluetoothctl** comando:</span><span class="sxs-lookup"><span data-stu-id="00e9e-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="00e9e-193">Digite o comando Olá **ligado** toopower controlador do hello bluetooth.</span><span class="sxs-lookup"><span data-stu-id="00e9e-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="00e9e-194">comando Olá retorna a seguir toohello semelhante saída:</span><span class="sxs-lookup"><span data-stu-id="00e9e-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="00e9e-195">No shell de bluetooth interativo hello, digite o comando de saudação **a varredura em** tooscan dispositivos bluetooth.</span><span class="sxs-lookup"><span data-stu-id="00e9e-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="00e9e-196">comando Olá retorna a seguir toohello semelhante saída:</span><span class="sxs-lookup"><span data-stu-id="00e9e-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="00e9e-197">Torne dispositivo de SensorTag Olá detectável pressionando Olá pequeno botão (Olá piscarão LED verde).</span><span class="sxs-lookup"><span data-stu-id="00e9e-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="00e9e-198">Olá framboesa Pi 3 deve descobrir dispositivos de SensorTag hello:</span><span class="sxs-lookup"><span data-stu-id="00e9e-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="00e9e-199">Neste exemplo, você pode ver que Olá endereço MAC de saudação SensorTag dispositivo **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="00e9e-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="00e9e-200">Desativar a verificação inserindo Olá **verificação** comando:</span><span class="sxs-lookup"><span data-stu-id="00e9e-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="00e9e-201">Conectar tooyour SensorTag dispositivo usando seu endereço MAC inserindo **conectar \<endereço MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="00e9e-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="00e9e-202">saudação de saída de exemplo a seguir é abreviada para maior clareza:</span><span class="sxs-lookup"><span data-stu-id="00e9e-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="00e9e-203">Você pode listar Olá GATT características de saudação dispositivo novamente usando Olá **lista atributos** comando.</span><span class="sxs-lookup"><span data-stu-id="00e9e-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="00e9e-204">Agora você pode desconectar de dispositivo de saudação usando Olá **desconectar** de comando e, em seguida, saia do shell de bluetooth hello usando Olá **sair** comando:</span><span class="sxs-lookup"><span data-stu-id="00e9e-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="00e9e-205">Agora você está exemplo de borda de IoT Bilitar hello toorun pronto em seu framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="00e9e-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="00e9e-206">Executar Olá IoT borda Bilitar exemplo</span><span class="sxs-lookup"><span data-stu-id="00e9e-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="00e9e-207">exemplo de IoT borda Bilitar hello toorun, é necessário toocomplete três tarefas:</span><span class="sxs-lookup"><span data-stu-id="00e9e-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="00e9e-208">Configurar dois dispositivos de exemplo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="00e9e-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="00e9e-209">Crie o IoT Edge em seu dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="00e9e-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="00e9e-210">Configurar e executar o exemplo de Bilitar hello em seu dispositivo framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="00e9e-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="00e9e-211">No momento da saudação de gravação, borda IoT só dá suporte a módulos Bilitar em gateways em execução no Linux.</span><span class="sxs-lookup"><span data-stu-id="00e9e-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="00e9e-212">Configurar dois dispositivos de exemplo em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="00e9e-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="00e9e-213">[Criar um hub IoT] [ lnk-create-hub] na sua assinatura do Azure, você precisará Olá nome do seu hub toocomplete este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="00e9e-214">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="00e9e-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="00e9e-215">Adicionar um dispositivo chamado **SensorTag_01** tooyour IoT hub e anote sua chave de id e o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="00e9e-216">Você pode usar o hello [Gerenciador de dispositivo ou Gerenciador de Hub IOT] [ lnk-explorer-tools] ferramentas tooadd este hub IoT de toohello de dispositivo criado na etapa anterior hello e tooretrieve sua chave.</span><span class="sxs-lookup"><span data-stu-id="00e9e-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="00e9e-217">Você mapeia esse dispositivo toohello SensorTag dispositivo ao configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="00e9e-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="00e9e-218">Criar o Azure IoT Edge no Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="00e9e-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="00e9e-219">Instalar dependências para o Azure IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="00e9e-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="00e9e-220">A seguir Olá use comandos tooclone IoT borda e todos os seu submódulos tooyour diretório base:</span><span class="sxs-lookup"><span data-stu-id="00e9e-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="00e9e-221">Quando você tiver uma cópia completa de saudação repositório IoT borda em seu framboesa Pi 3, você pode criar usando Olá comando a seguir na pasta Olá contém Olá SDK:</span><span class="sxs-lookup"><span data-stu-id="00e9e-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="00e9e-222">Configurar e executar o exemplo de Bilitar de saudação em seu framboesa Pi 3</span><span class="sxs-lookup"><span data-stu-id="00e9e-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="00e9e-223">toobootstrap e exemplo hello execução, você deve configurar cada módulo de borda IoT participa no gateway hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="00e9e-224">Essa configuração é fornecida em um arquivo JSON e você precisa configurar todos os cinco módulos IoT Edge participantes.</span><span class="sxs-lookup"><span data-stu-id="00e9e-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="00e9e-225">Há um arquivo JSON de exemplo no repositório de saudação chamado **gateway\_sample.json** que você pode usar como ponto de partida para criar seu próprio arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="00e9e-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="00e9e-226">Esse arquivo está em Olá **ble_gateway/exemplos/src** pasta na cópia local do hello repositório IoT borda.</span><span class="sxs-lookup"><span data-stu-id="00e9e-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="00e9e-227">Olá seções a seguir descrevem como tooedit essa configuração do arquivo de exemplo de Bilitar hello e suponha que Olá repositório IoT borda está em Olá **/home/pi/iot-edge /** pasta no seu framboesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="00e9e-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="00e9e-228">Se o repositório de saudação estiver em outro lugar, ajuste caminhos Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="00e9e-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="00e9e-229">Configuração do agente</span><span class="sxs-lookup"><span data-stu-id="00e9e-229">Logger configuration</span></span>

<span data-ttu-id="00e9e-230">Supondo que o repositório de gateway hello está localizado em Olá **/home/pi/iot-edge /** pasta, configure o módulo de agente de log de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="00e9e-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="00e9e-231">Configuração do módulo BLE</span><span class="sxs-lookup"><span data-stu-id="00e9e-231">BLE module configuration</span></span>

<span data-ttu-id="00e9e-232">configuração de exemplo Hello para dispositivo de Bilitar Olá pressupõe um dispositivo SensorTag de instrumentos Texas.</span><span class="sxs-lookup"><span data-stu-id="00e9e-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="00e9e-233">Qualquer dispositivo Bilitar padrão que pode funcionar como um GATT periférico deve funcionar, mas você pode precisar característica de GATT tooupdate Olá IDs e dados.</span><span class="sxs-lookup"><span data-stu-id="00e9e-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="00e9e-234">Adicione o endereço MAC de saudação do seu dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="00e9e-234">Add hello MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="00e9e-235">Se você não estiver usando um dispositivo SensorTag, revise a documentação de saudação para sua toodetermine de dispositivo Bilitar se você precisa de característica de GATT tooupdate Olá IDs e valores de dados.</span><span class="sxs-lookup"><span data-stu-id="00e9e-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="00e9e-236">módulo do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="00e9e-236">IoT Hub module</span></span>

<span data-ttu-id="00e9e-237">Adicione nome de saudação do seu IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="00e9e-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="00e9e-238">valor de sufixo de saudação é normalmente **devices.net azure**:</span><span class="sxs-lookup"><span data-stu-id="00e9e-238">hello suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="00e9e-239">Configuração do módulo de mapeamento de identidade</span><span class="sxs-lookup"><span data-stu-id="00e9e-239">Identity mapping module configuration</span></span>

<span data-ttu-id="00e9e-240">Adicione o endereço MAC de saudação do seu dispositivo de SensorTag e a ID do dispositivo Olá e a chave da saudação **SensorTag_01** dispositivo adicionado tooyour IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="00e9e-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="00e9e-241">Configuração do módulo de impressora BLE</span><span class="sxs-lookup"><span data-stu-id="00e9e-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="00e9e-242">Configuração do módulo BLEC2D</span><span class="sxs-lookup"><span data-stu-id="00e9e-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="00e9e-243">Configuração de roteamento</span><span class="sxs-lookup"><span data-stu-id="00e9e-243">Routing Configuration</span></span>

<span data-ttu-id="00e9e-244">configuração a seguir Hello assegura seguir Olá roteamento entre módulos IoT borda:</span><span class="sxs-lookup"><span data-stu-id="00e9e-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="00e9e-245">Olá **agente** módulo recebe e registra todas as mensagens.</span><span class="sxs-lookup"><span data-stu-id="00e9e-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="00e9e-246">Olá **SensorTag** módulo envia Olá de tooboth mensagens **mapeamento** e **Bilitar impressora** módulos.</span><span class="sxs-lookup"><span data-stu-id="00e9e-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="00e9e-247">Olá **mapeamento** módulo envia mensagens toohello **hub IOT** toobe módulo enviado tooyour IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="00e9e-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="00e9e-248">Olá **hub IOT** módulo envia de volta toohello **mapeamento** módulo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="00e9e-249">Olá **mapeamento** módulo envia mensagens toohello **BLEC2D** módulo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="00e9e-250">Olá **BLEC2D** módulo envia de volta toohello **marca Sensor** módulo.</span><span class="sxs-lookup"><span data-stu-id="00e9e-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

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

<span data-ttu-id="00e9e-251">exemplo de hello toorun, passagem Olá caminho toohello arquivo de configuração JSON como um parâmetro toohello **bilitar\_gateway** binário.</span><span class="sxs-lookup"><span data-stu-id="00e9e-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="00e9e-252">Olá comando a seguir presume que você está usando Olá **gateway_sample.json** arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="00e9e-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="00e9e-253">Executar esse comando de saudação **iot borda** pasta Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="00e9e-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="00e9e-254">Talvez seja necessário toopress Olá pequeno botão Olá SensorTag dispositivo toomake-lo detectável antes de executar o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="00e9e-255">Quando você executar o exemplo hello, você pode usar o hello [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) ferramenta toomonitor Olá mensagens Olá encaminha o gateway de borda de IoT de dispositivo de SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="00e9e-256">Por exemplo, usando o Gerenciador de Hub IOT você pode monitorar mensagens de dispositivo para nuvem usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="00e9e-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="00e9e-257">Envie mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="00e9e-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="00e9e-258">módulo de Bilitar Olá também oferece suporte a comandos de enviados do dispositivo do IoT Hub toohello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="00e9e-259">Você pode usar o hello [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) ou hello [Gerenciador de Hub IOT](https://github.com/Azure/iothub-explorer) mensagens JSON toosend ferramenta módulo Olá Bilitar gateway encaminha no dispositivo de Bilitar toohello.</span><span class="sxs-lookup"><span data-stu-id="00e9e-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="00e9e-260">Se você estiver usando um dispositivo de Texas instrumentos SensorTag hello, você pode ativar LED Olá vermelho, LED verde ou campainha enviando comandos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="00e9e-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="00e9e-261">Antes de enviar comandos de IoT Hub, primeiro envie Olá duas mensagens JSON em ordem a seguir.</span><span class="sxs-lookup"><span data-stu-id="00e9e-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="00e9e-262">Em seguida, você pode enviar qualquer Olá comandos tooturn luzes hello ou campainha.</span><span class="sxs-lookup"><span data-stu-id="00e9e-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="00e9e-263">Redefina todos os LEDs e campainha hello (desativá-los):</span><span class="sxs-lookup"><span data-stu-id="00e9e-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="00e9e-264">Configurar a E/S como 'remota':</span><span class="sxs-lookup"><span data-stu-id="00e9e-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="00e9e-265">Agora você pode enviar qualquer Olá tooturn comandos a seguir em luzes hello ou campainha no dispositivo de SensorTag hello:</span><span class="sxs-lookup"><span data-stu-id="00e9e-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="00e9e-266">Ative o LED Olá vermelho:</span><span class="sxs-lookup"><span data-stu-id="00e9e-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="00e9e-267">Ative o LED verde do hello:</span><span class="sxs-lookup"><span data-stu-id="00e9e-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="00e9e-268">Ative campainha hello:</span><span class="sxs-lookup"><span data-stu-id="00e9e-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="00e9e-269">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00e9e-269">Next Steps</span></span>

<span data-ttu-id="00e9e-270">Se você quiser toogain uma compreensão mais avançada de IoT borda e fazer experiências com alguns exemplos de código, visite Olá tutoriais de desenvolvedor e recursos:</span><span class="sxs-lookup"><span data-stu-id="00e9e-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="00e9e-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="00e9e-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="00e9e-272">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="00e9e-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="00e9e-273">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="00e9e-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
