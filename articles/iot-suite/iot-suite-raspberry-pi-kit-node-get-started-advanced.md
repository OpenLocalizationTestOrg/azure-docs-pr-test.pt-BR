---
title: aaaConnect tooAzure um Pi framboesa IoT Suite usando Node. js toosupport firmware atualiza | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Use tooconnect Node. js sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria de sensores toohello nuvem e executar uma atualização de firmware remoto."
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
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a><span data-ttu-id="39d4e-104">Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e habilitar atualizações de firmware remoto usando o Node. js</span><span class="sxs-lookup"><span data-stu-id="39d4e-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="39d4e-105">Este tutorial mostra como toouse Olá Microsoft Azure IoT Starter Kit para framboesa Pi 3 para:</span><span class="sxs-lookup"><span data-stu-id="39d4e-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="39d4e-106">Desenvolva um leitor de temperatura e umidade que pode se comunicar com a nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="39d4e-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="39d4e-107">Habilitar e executar um aplicativo de cliente remoto firmware update tooupdate hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="39d4e-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="39d4e-108">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="39d4e-108">hello tutorial uses:</span></span>

- <span data-ttu-id="39d4e-109">OS Raspbian, Olá Node. js linguagem de programação e hello IoT do SDK do Microsoft Azure para Node.js tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="39d4e-109">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="39d4e-110">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="39d4e-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="39d4e-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="39d4e-111">Overview</span></span>

<span data-ttu-id="39d4e-112">Neste tutorial, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="39d4e-112">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="39d4e-113">Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d4e-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="39d4e-114">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d4e-114">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="39d4e-115">Configure seu toocommunicate sensores e dispositivos com o computador e Olá remotas de solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="39d4e-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="39d4e-116">Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria que você pode exibir no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="39d4e-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
- <span data-ttu-id="39d4e-117">Use aplicativo de cliente Olá exemplo dispositivo código tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="39d4e-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="39d4e-118">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d4e-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="39d4e-119">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="39d4e-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="39d4e-120">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="39d4e-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="39d4e-121">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="39d4e-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="39d4e-122">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="39d4e-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="39d4e-123">Baixar e configurar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="39d4e-123">Download and configure hello sample</span></span>

<span data-ttu-id="39d4e-124">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.</span><span class="sxs-lookup"><span data-stu-id="39d4e-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="39d4e-125">Instalar o Node. js</span><span class="sxs-lookup"><span data-stu-id="39d4e-125">Install Node.js</span></span>

<span data-ttu-id="39d4e-126">Caso ainda não tenha feito isso, instale o Node.js no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="39d4e-126">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="39d4e-127">Olá IoT SDK para Node.js requer a versão 0.11.5 do Node.js ou posterior.</span><span class="sxs-lookup"><span data-stu-id="39d4e-127">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="39d4e-128">Olá etapas a seguir mostram como tooinstall Node. js v6.10.2 em seu Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="39d4e-128">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="39d4e-129">Use Olá tooupdate de comando a seguir o Pi framboesa:</span><span class="sxs-lookup"><span data-stu-id="39d4e-129">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="39d4e-130">Use Olá comando toodownload Olá Node. js binários tooyour framboesa Pi a seguir:</span><span class="sxs-lookup"><span data-stu-id="39d4e-130">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="39d4e-131">Use Olá binários de saudação do tooinstall de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="39d4e-131">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="39d4e-132">Use Olá tooverify de comando que você instalou com êxito o Node. js v6.10.2 a seguir:</span><span class="sxs-lookup"><span data-stu-id="39d4e-132">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="39d4e-133">Repositórios de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="39d4e-133">Clone hello repositories</span></span>

<span data-ttu-id="39d4e-134">Se você ainda não tiver feito isso, Olá clone necessário repositórios executando Olá comandos a seguir em seu Pi:</span><span class="sxs-lookup"><span data-stu-id="39d4e-134">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="39d4e-135">Atualizar a cadeia de conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="39d4e-135">Update hello device connection string</span></span>

<span data-ttu-id="39d4e-136">Arquivo de configuração de exemplo hello aberta no hello **nano** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="39d4e-136">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="39d4e-137">Substitua valores de espaço reservado de saudação com id do dispositivo hello e informações de IoT Hub é criado e salvo no início de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="39d4e-137">Replace hello placeholder values with hello device id and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="39d4e-138">Quando terminar, conteúdo de saudação do arquivo de deviceinfo Olá deve ter a aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="39d4e-138">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="39d4e-139">Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="39d4e-139">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="39d4e-140">Executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="39d4e-140">Run hello sample</span></span>

<span data-ttu-id="39d4e-141">A seguir Olá execução comandos tooinstall Olá pré-requisitos do pacote de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="39d4e-141">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

<span data-ttu-id="39d4e-142">Agora você pode executar o programa de exemplo hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="39d4e-142">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="39d4e-143">Digite o comando hello:</span><span class="sxs-lookup"><span data-stu-id="39d4e-143">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

<span data-ttu-id="39d4e-144">Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="39d4e-144">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="39d4e-146">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="39d4e-146">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="39d4e-147">No painel de solução de saudação, clique em **dispositivos** toovisit Olá **dispositivos** página.</span><span class="sxs-lookup"><span data-stu-id="39d4e-147">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="39d4e-148">Selecione o Pi framboesa no hello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="39d4e-148">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="39d4e-149">Depois, escolha **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="39d4e-149">Then choose **Methods**:</span></span>

    ![Listar dispositivos no painel][img-list-devices]

1. <span data-ttu-id="39d4e-151">Em Olá **invocar o método** escolha **InitiateFirmwareUpdate** em Olá **método** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="39d4e-151">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="39d4e-152">Em Olá **FWPackageURI** , digite **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span><span class="sxs-lookup"><span data-stu-id="39d4e-152">In hello **FWPackageURI** field, enter **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**.</span></span> <span data-ttu-id="39d4e-153">Este arquivo contém a implementação de saudação da versão 2.0 do firmware hello.</span><span class="sxs-lookup"><span data-stu-id="39d4e-153">This file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="39d4e-154">Escolha **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="39d4e-154">Choose **InvokeMethod**.</span></span> <span data-ttu-id="39d4e-155">aplicativo Olá Olá framboesa Pi envia um painel de solução de backup toohello confirmação.</span><span class="sxs-lookup"><span data-stu-id="39d4e-155">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="39d4e-156">Então, ele iniciará o processo de atualização de firmware de saudação baixando a nova versão de saudação do firmware hello:</span><span class="sxs-lookup"><span data-stu-id="39d4e-156">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Mostrar o histórico do método][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="39d4e-158">Observe o processo de atualização de firmware Olá</span><span class="sxs-lookup"><span data-stu-id="39d4e-158">Observe hello firmware update process</span></span>

<span data-ttu-id="39d4e-159">Você pode observar o processo de atualização de firmware Olá conforme ele é executado no dispositivo hello e exibindo Olá relatados propriedades no painel de solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="39d4e-159">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="39d4e-160">Você pode exibir o progresso de saudação em saudação do processo de atualização em Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="39d4e-160">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Mostrar progresso da atualização][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="39d4e-162">aplicativo de monitoramento remoto Olá silenciosamente reinicia quando Olá atualização for concluída.</span><span class="sxs-lookup"><span data-stu-id="39d4e-162">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="39d4e-163">Use o comando Olá `ps -ef` tooverify está em execução.</span><span class="sxs-lookup"><span data-stu-id="39d4e-163">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="39d4e-164">Se desejar que o processo de saudação tooterminate, use Olá `kill` comando com a id de processo hello.</span><span class="sxs-lookup"><span data-stu-id="39d4e-164">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="39d4e-165">Você pode exibir o status de saudação da atualização de firmware hello, conforme relatado pelo dispositivo hello, no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="39d4e-165">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="39d4e-166">Hello seguinte captura de tela mostra o status de saudação e a duração de cada estágio do processo de atualização de saudação e a nova versão de firmware Olá:</span><span class="sxs-lookup"><span data-stu-id="39d4e-166">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Mostrar status do trabalho][img-job-status]

    <span data-ttu-id="39d4e-168">Se você navegar toohello back painel, você pode verificar o dispositivo Olá ainda está enviando a telemetria após a atualização de firmware de saudação.</span><span class="sxs-lookup"><span data-stu-id="39d4e-168">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="39d4e-169">Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado.</span><span class="sxs-lookup"><span data-stu-id="39d4e-169">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="39d4e-170">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="39d4e-170">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="39d4e-171">Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.</span><span class="sxs-lookup"><span data-stu-id="39d4e-171">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39d4e-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39d4e-172">Next steps</span></span>

<span data-ttu-id="39d4e-173">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d4e-173">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
