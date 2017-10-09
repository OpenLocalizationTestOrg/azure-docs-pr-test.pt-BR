---
title: aaaConnect tooAzure um Pi framboesa IoT Suite usando C com a telemetria simulada | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Usar C tooconnect sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria simulada toohello nuvem e responder toomethods invocada a partir do painel de solução de saudação."
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="2293a-104">Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e enviar telemetria simulada usando C</span><span class="sxs-lookup"><span data-stu-id="2293a-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="2293a-105">Este tutorial mostra como toouse Olá framboesa Pi 3 toosimulate temperatura e umidade dados toosend toohello de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2293a-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="2293a-106">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="2293a-106">hello tutorial uses:</span></span>

- <span data-ttu-id="2293a-107">OS Raspbian, linguagem de programação Olá C e hello SDK do Microsoft Azure IoT para C tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="2293a-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="2293a-108">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="2293a-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="2293a-109">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2293a-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="2293a-110">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="2293a-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="2293a-111">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="2293a-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="2293a-112">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="2293a-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="2293a-113">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="2293a-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="2293a-114">Baixar e configurar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="2293a-114">Download and configure hello sample</span></span>

<span data-ttu-id="2293a-115">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.</span><span class="sxs-lookup"><span data-stu-id="2293a-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="2293a-116">Repositórios de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="2293a-116">Clone hello repositories</span></span>

<span data-ttu-id="2293a-117">Se você ainda não fez isso, Olá clone necessário Olá de repositórios executando comandos em um terminal a seguir em seu Pi:</span><span class="sxs-lookup"><span data-stu-id="2293a-117">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="2293a-118">Atualizar a cadeia de conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="2293a-118">Update hello device connection string</span></span>

<span data-ttu-id="2293a-119">Arquivo de origem de exemplo hello aberto em Olá **nano** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2293a-119">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="2293a-120">Localize Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="2293a-120">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="2293a-121">Substitua os valores de espaço reservado Olá Olá e informações de IoT Hub é criado e salvo no início de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="2293a-121">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="2293a-122">Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="2293a-122">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="2293a-123">Compilar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="2293a-123">Build hello sample</span></span>

<span data-ttu-id="2293a-124">Instale pacotes de pré-requisitos de saudação para Olá SDK de dispositivo do Microsoft Azure IoT para C executando Olá seguindo os comandos em um terminal na Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="2293a-124">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="2293a-125">Agora você pode criar a solução de exemplo hello atualizado em Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="2293a-125">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="2293a-126">Agora você pode executar o programa de exemplo hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="2293a-126">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="2293a-127">Digite o comando hello:</span><span class="sxs-lookup"><span data-stu-id="2293a-127">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="2293a-128">Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="2293a-128">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="2293a-130">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="2293a-130">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="2293a-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2293a-131">Next steps</span></span>

<span data-ttu-id="2293a-132">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="2293a-132">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
