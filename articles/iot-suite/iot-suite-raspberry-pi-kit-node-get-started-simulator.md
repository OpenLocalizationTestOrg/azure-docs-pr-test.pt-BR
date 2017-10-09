---
title: aaaConnect tooAzure um Pi framboesa IoT Suite com Node. js telemetria simulada | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Use tooconnect Node. js sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria simulada toohello nuvem e responder toomethods invocada a partir do painel de solução de saudação."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="7c4a0-104">Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e enviar telemetria simulada usando Node. js</span><span class="sxs-lookup"><span data-stu-id="7c4a0-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="7c4a0-105">Este tutorial mostra como toouse Olá framboesa Pi 3 toosimulate temperatura e umidade dados toosend toohello de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="7c4a0-106">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-106">hello tutorial uses:</span></span>

- <span data-ttu-id="7c4a0-107">OS Raspbian, Olá Node. js linguagem de programação e hello IoT do SDK do Microsoft Azure para Node.js tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="7c4a0-108">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="7c4a0-109">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="7c4a0-110">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="7c4a0-111">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="7c4a0-112">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="7c4a0-113">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="7c4a0-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="7c4a0-114">Baixar e configurar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="7c4a0-114">Download and configure hello sample</span></span>

<span data-ttu-id="7c4a0-115">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="7c4a0-116">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="7c4a0-116">Install Node.js</span></span>

<span data-ttu-id="7c4a0-117">Caso ainda não tenha feito isso, instale o Node.js no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="7c4a0-118">Olá IoT SDK para Node.js requer a versão 0.11.5 do Node.js ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-118">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="7c4a0-119">Olá etapas a seguir mostram como tooinstall Node. js v6.10.2 em seu Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-119">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="7c4a0-120">Use Olá tooupdate de comando a seguir o Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-120">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="7c4a0-121">Use Olá comando toodownload Olá Node. js binários tooyour framboesa Pi a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-121">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7c4a0-122">Use Olá binários de saudação do tooinstall de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-122">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7c4a0-123">Use Olá tooverify de comando que você instalou com êxito o Node. js v6.10.2 a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-123">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="7c4a0-124">Repositórios de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="7c4a0-124">Clone hello repositories</span></span>

<span data-ttu-id="7c4a0-125">Se você ainda não fez isso, Olá clone necessário Olá de repositórios executando comandos em um terminal a seguir em seu Pi:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-125">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="7c4a0-126">Atualizar a cadeia de conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="7c4a0-126">Update hello device connection string</span></span>

<span data-ttu-id="7c4a0-127">Arquivo de origem de exemplo hello aberto em Olá **nano** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-127">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="7c4a0-128">Localize a linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-128">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="7c4a0-129">Substitua os valores de espaço reservado Olá Olá e informações de IoT Hub é criado e salvo no início de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-129">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="7c4a0-130">Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="7c4a0-130">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="7c4a0-131">Executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="7c4a0-131">Run hello sample</span></span>

<span data-ttu-id="7c4a0-132">A seguir Olá execução comandos tooinstall Olá pré-requisitos do pacote de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-132">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="7c4a0-133">Agora você pode executar o programa de exemplo hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-133">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="7c4a0-134">Digite o comando hello:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-134">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="7c4a0-135">Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="7c4a0-135">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="7c4a0-137">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-137">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="7c4a0-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c4a0-138">Next steps</span></span>

<span data-ttu-id="7c4a0-139">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4a0-139">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
