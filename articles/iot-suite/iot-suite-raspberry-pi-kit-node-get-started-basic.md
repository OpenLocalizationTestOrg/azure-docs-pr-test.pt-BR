---
title: aaaConnect tooAzure um Pi framboesa IoT Suite usando Node. js com sensores reais | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Use tooconnect Node. js sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria de sensores toohello nuvem e responder toomethods invocada a partir do painel de solução de saudação."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="f7df8-104">Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e enviar telemetria a partir de um sensor real usando Node. js</span><span class="sxs-lookup"><span data-stu-id="f7df8-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="f7df8-105">Este tutorial mostra como toouse hello Microsoft Azure IoT Starter Kit para framboesa Pi 3 toodevelop um leitor de temperatura e umidade que pode se comunicar com a nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7df8-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="f7df8-106">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="f7df8-106">hello tutorial uses:</span></span>

- <span data-ttu-id="f7df8-107">OS Raspbian, Olá Node. js linguagem de programação e hello IoT do SDK do Microsoft Azure para Node.js tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f7df8-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="f7df8-108">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="f7df8-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="f7df8-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f7df8-109">Overview</span></span>

<span data-ttu-id="f7df8-110">Neste tutorial, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7df8-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="f7df8-111">Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7df8-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="f7df8-112">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7df8-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="f7df8-113">Configure seu toocommunicate sensores e dispositivos com o computador e Olá remotas de solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="f7df8-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="f7df8-114">Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria que você pode exibir no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7df8-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="f7df8-115">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7df8-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="f7df8-116">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="f7df8-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="f7df8-117">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="f7df8-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="f7df8-118">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="f7df8-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="f7df8-119">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="f7df8-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="f7df8-120">Baixar e configurar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="f7df8-120">Download and configure hello sample</span></span>

<span data-ttu-id="f7df8-121">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.</span><span class="sxs-lookup"><span data-stu-id="f7df8-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="f7df8-122">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="f7df8-122">Install Node.js</span></span>

<span data-ttu-id="f7df8-123">Instale Node. js em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f7df8-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="f7df8-124">Olá IoT SDK para Node.js requer a versão 0.11.5 do Node.js ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f7df8-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="f7df8-125">Olá etapas a seguir mostram como tooinstall Node. js v6.10.2 em seu Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="f7df8-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="f7df8-126">Use Olá tooupdate de comando a seguir o Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="f7df8-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="f7df8-127">Use Olá comando toodownload Olá Node. js binários tooyour framboesa Pi a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7df8-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="f7df8-128">Use Olá binários de saudação do tooinstall de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7df8-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="f7df8-129">Use Olá tooverify de comando que você instalou com êxito o Node. js v6.10.2 a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7df8-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="f7df8-130">Repositórios de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="f7df8-130">Clone hello repositories</span></span>

<span data-ttu-id="f7df8-131">Se você ainda não fez isso, Olá clone necessário repositórios executando Olá comandos a seguir em seu Pi:</span><span class="sxs-lookup"><span data-stu-id="f7df8-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="f7df8-132">Atualizar a cadeia de conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="f7df8-132">Update hello device connection string</span></span>

<span data-ttu-id="f7df8-133">Arquivo de origem de exemplo hello aberto em Olá **nano** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7df8-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="f7df8-134">Localize a linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="f7df8-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="f7df8-135">Substitua os valores de espaço reservado Olá Olá e informações de IoT Hub é criado e salvo no início de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f7df8-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="f7df8-136">Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="f7df8-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="f7df8-137">Executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="f7df8-137">Run hello sample</span></span>

<span data-ttu-id="f7df8-138">A seguir Olá execução comandos tooinstall Olá pré-requisitos do pacote de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="f7df8-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="f7df8-139">Agora você pode executar o programa de exemplo hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="f7df8-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="f7df8-140">Digite o comando hello:</span><span class="sxs-lookup"><span data-stu-id="f7df8-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="f7df8-141">Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="f7df8-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="f7df8-143">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="f7df8-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="f7df8-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7df8-144">Next steps</span></span>

<span data-ttu-id="f7df8-145">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7df8-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
