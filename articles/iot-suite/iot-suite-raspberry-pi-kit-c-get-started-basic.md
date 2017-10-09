---
title: aaaConnect tooAzure um Pi framboesa IoT Suite usando C com sensores reais | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Usar C tooconnect sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria de sensores toohello nuvem e responder toomethods invocada a partir do painel de solução de saudação."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="830c9-104">Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e enviar telemetria a partir de um sensor real usando C</span><span class="sxs-lookup"><span data-stu-id="830c9-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="830c9-105">Este tutorial mostra como toouse hello Microsoft Azure IoT Starter Kit para framboesa Pi 3 toodevelop um leitor de temperatura e umidade que pode se comunicar com a nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="830c9-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="830c9-106">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="830c9-106">hello tutorial uses:</span></span>

- <span data-ttu-id="830c9-107">OS Raspbian, linguagem de programação Olá C e hello SDK do Microsoft Azure IoT para C tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="830c9-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="830c9-108">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="830c9-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="830c9-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="830c9-109">Overview</span></span>

<span data-ttu-id="830c9-110">Neste tutorial, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="830c9-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="830c9-111">Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="830c9-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="830c9-112">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="830c9-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="830c9-113">Configure seu toocommunicate sensores e dispositivos com o computador e Olá remotas de solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="830c9-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="830c9-114">Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria que você pode exibir no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="830c9-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="830c9-115">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="830c9-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="830c9-116">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="830c9-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="830c9-117">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="830c9-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="830c9-118">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="830c9-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="830c9-119">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="830c9-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="830c9-120">Baixar e configurar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="830c9-120">Download and configure hello sample</span></span>

<span data-ttu-id="830c9-121">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.</span><span class="sxs-lookup"><span data-stu-id="830c9-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="830c9-122">Repositórios de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="830c9-122">Clone hello repositories</span></span>

<span data-ttu-id="830c9-123">Se você ainda não fez isso, Olá clone necessário Olá de repositórios executando comandos em um terminal a seguir em seu Pi:</span><span class="sxs-lookup"><span data-stu-id="830c9-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="830c9-124">Atualizar a cadeia de conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="830c9-124">Update hello device connection string</span></span>

<span data-ttu-id="830c9-125">Arquivo de origem de exemplo hello aberto em Olá **nano** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="830c9-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="830c9-126">Localize Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="830c9-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="830c9-127">Substitua os valores de espaço reservado Olá Olá e informações de IoT Hub é criado e salvo no início de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="830c9-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="830c9-128">Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="830c9-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="830c9-129">Compilar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="830c9-129">Build hello sample</span></span>

<span data-ttu-id="830c9-130">Instale pacotes de pré-requisitos de saudação para Olá SDK de dispositivo do Microsoft Azure IoT para C executando Olá seguindo os comandos em um terminal na Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="830c9-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="830c9-131">Agora você pode criar a solução de exemplo hello atualizado em Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="830c9-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="830c9-132">Agora você pode executar o programa de exemplo hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="830c9-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="830c9-133">Digite o comando hello:</span><span class="sxs-lookup"><span data-stu-id="830c9-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="830c9-134">Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="830c9-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="830c9-136">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="830c9-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="830c9-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="830c9-137">Next steps</span></span>

<span data-ttu-id="830c9-138">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="830c9-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
