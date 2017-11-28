---
title: Conectar um Raspberry Pi ao Azure IoT Suite usando o Node.js com telemetria simulada | Microsoft Docs
description: "Use o Microsoft Azure IoT Starter Kit para o Raspberry Pi 3 e o Azure IoT Suite. Use o Node.js para conectar o Raspberry Pi à solução de monitoramento remoto, enviar telemetria simulada à nuvem e responder aos métodos invocados no painel da solução."
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
ms.openlocfilehash: 43fbfe2f2c5fb86e496c4419f9565365cf89830a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="0e018-104">Conectar o Raspberry Pi3 à solução de monitoramento remoto e enviar telemetria simulada usando o Node.js</span><span class="sxs-lookup"><span data-stu-id="0e018-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="0e018-105">Este tutorial mostra como usar o Raspberry Pi 3 para simular dados de temperatura e umidade e enviar para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="0e018-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="0e018-106">O tutorial usa:</span><span class="sxs-lookup"><span data-stu-id="0e018-106">The tutorial uses:</span></span>

- <span data-ttu-id="0e018-107">SO Raspbian, a linguagem de programação Node.js, e o SDK do Microsoft Azure IoT para Node.js para implementar um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0e018-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="0e018-108">A solução pré-configurada de monitoramento remoto do IoT Suite como o back-end baseado na nuvem.</span><span class="sxs-lookup"><span data-stu-id="0e018-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="0e018-109">A solução de monitoramento remoto provisiona um conjunto de serviços do Azure na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e018-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="0e018-110">A implantação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="0e018-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="0e018-111">Para evitar encargos desnecessários de consumo do Azure, exclua a instância da solução pré-configurada em azureiotsuite.com quando tiver terminado de realizar as tarefas nela.</span><span class="sxs-lookup"><span data-stu-id="0e018-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="0e018-112">Caso precise da solução novamente, você poderá recriá-la facilmente.</span><span class="sxs-lookup"><span data-stu-id="0e018-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="0e018-113">Para saber mais sobre como reduzir o consumo durante a execução da solução de monitoramento remoto, confira [Configuração de soluções pré-configuradas do Azure IoT Suite para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="0e018-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="0e018-114">Baixar e configurar o exemplo</span><span class="sxs-lookup"><span data-stu-id="0e018-114">Download and configure the sample</span></span>

<span data-ttu-id="0e018-115">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0e018-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="0e018-116">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="0e018-116">Install Node.js</span></span>

<span data-ttu-id="0e018-117">Caso ainda não tenha feito isso, instale o Node.js no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0e018-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="0e018-118">O SDK do IoT para Node.js exige a versão 0.11.5 do Node.js ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0e018-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="0e018-119">As seguintes etapas mostram como instalar o Node.js v6.10.2 no Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0e018-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="0e018-120">Use o seguinte comando para atualizar o Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0e018-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="0e018-121">Use o seguinte comando para baixar os binários do Node.js no Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0e018-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="0e018-122">Use o seguinte comando para instalar os binários:</span><span class="sxs-lookup"><span data-stu-id="0e018-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="0e018-123">Use o seguinte comando para verificar se você instalou com êxito o Node.js v6.10.2:</span><span class="sxs-lookup"><span data-stu-id="0e018-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="0e018-124">Clonar os repositórios</span><span class="sxs-lookup"><span data-stu-id="0e018-124">Clone the repositories</span></span>

<span data-ttu-id="0e018-125">Caso ainda não tenha feito isso, clone os repositórios necessários executando os seguintes comandos em um terminal no Pi:</span><span class="sxs-lookup"><span data-stu-id="0e018-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="0e018-126">Atualizar a cadeia de conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="0e018-126">Update the device connection string</span></span>

<span data-ttu-id="0e018-127">Abra o arquivo de origem de exemplo no editor **nano** usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0e018-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="0e018-128">Localize a linha:</span><span class="sxs-lookup"><span data-stu-id="0e018-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="0e018-129">Substitua os valores do espaço reservado pelas informações de dispositivo e Hub IoT que você criou e salvou no início deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e018-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="0e018-130">Salve suas alterações (**Ctrl-O**, **Enter**) e saia do editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="0e018-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="0e018-131">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="0e018-131">Run the sample</span></span>

<span data-ttu-id="0e018-132">Execute os seguintes comandos para instalar os pacotes de pré-requisito do exemplo:</span><span class="sxs-lookup"><span data-stu-id="0e018-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="0e018-133">Agora você pode executar o programa de exemplo no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0e018-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="0e018-134">Insira o comando:</span><span class="sxs-lookup"><span data-stu-id="0e018-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="0e018-135">O que você vê a seguir é um exemplo da saída vista no prompt de comando do Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="0e018-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="0e018-137">Pressione **Ctrl-C** para sair do programa a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="0e018-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="0e018-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0e018-138">Next steps</span></span>

<span data-ttu-id="0e018-139">Visite o [Centro de Desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e a documentação sobre o Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="0e018-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
