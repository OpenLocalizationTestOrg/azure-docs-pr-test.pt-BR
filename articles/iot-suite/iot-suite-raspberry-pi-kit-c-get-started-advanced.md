---
title: aaaConnect tooAzure um Pi framboesa IoT Suite usando C toosupport firmware atualiza | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Usar C tooconnect sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria de sensores toohello nuvem e executar uma atualização de firmware remoto."
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
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="4a8b8-104">Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e habilitar atualizações de firmware remoto usando C</span><span class="sxs-lookup"><span data-stu-id="4a8b8-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="4a8b8-105">Este tutorial mostra como toouse Olá Microsoft Azure IoT Starter Kit para framboesa Pi 3 para:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="4a8b8-106">Desenvolva um leitor de temperatura e umidade que pode se comunicar com a nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-106">Develop a temperature and humidity reader that can communicate with hello cloud.</span></span>
* <span data-ttu-id="4a8b8-107">Habilitar e executar um aplicativo de cliente remoto firmware update tooupdate hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-107">Enable and perform a remote firmware update tooupdate hello client application on hello Raspberry Pi.</span></span>

<span data-ttu-id="4a8b8-108">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-108">hello tutorial uses:</span></span>

* <span data-ttu-id="4a8b8-109">OS Raspbian, linguagem de programação Olá C e hello SDK do Microsoft Azure IoT para C tooimplement um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-109">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
* <span data-ttu-id="4a8b8-110">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-110">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="4a8b8-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4a8b8-111">Overview</span></span>

<span data-ttu-id="4a8b8-112">Neste tutorial, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-112">In this tutorial, you complete hello following steps:</span></span>

* <span data-ttu-id="4a8b8-113">Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-113">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="4a8b8-114">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="4a8b8-115">Configure seu toocommunicate sensores e dispositivos com o computador e Olá remotas de solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-115">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
* <span data-ttu-id="4a8b8-116">Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria que você pode exibir no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-116">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>
* <span data-ttu-id="4a8b8-117">Use aplicativo de cliente Olá exemplo dispositivo código tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-117">Use hello sample device code tooupdate hello client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="4a8b8-118">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="4a8b8-119">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="4a8b8-120">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="4a8b8-121">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="4a8b8-122">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="4a8b8-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="4a8b8-123">Baixar e configurar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="4a8b8-123">Download and configure hello sample</span></span>

<span data-ttu-id="4a8b8-124">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-124">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="4a8b8-125">Repositórios de saudação do clone</span><span class="sxs-lookup"><span data-stu-id="4a8b8-125">Clone hello repositories</span></span>

<span data-ttu-id="4a8b8-126">Se você ainda não tiver feito isso, Olá clone necessário repositórios executando Olá comandos a seguir em seu Pi:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-126">If you haven't done so already, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="4a8b8-127">Atualizar a cadeia de conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="4a8b8-127">Update hello device connection string</span></span>

<span data-ttu-id="4a8b8-128">Arquivo de configuração de exemplo hello aberta no hello **nano** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-128">Open hello sample configuration file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="4a8b8-129">Substitua os valores de espaço reservado Olá Olá ID e o IoT Hub informações do dispositivo é criado e salvo no início de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-129">Replace hello placeholder values with hello device ID and IoT Hub information you created and saved at hello start of this tutorial.</span></span>

<span data-ttu-id="4a8b8-130">Quando terminar, conteúdo de saudação do arquivo de deviceinfo Olá deve ter a aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-130">When you are done, hello contents of hello deviceinfo file should look like hello following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="4a8b8-131">Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="4a8b8-131">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="4a8b8-132">Compilar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="4a8b8-132">Build hello sample</span></span>

<span data-ttu-id="4a8b8-133">Se você ainda não tiver feito isso, instale pacotes de pré-requisitos de saudação para Olá SDK de dispositivo do Microsoft Azure IoT para C executando Olá seguindo os comandos em um terminal na Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-133">If you have not already done so, install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="4a8b8-134">Agora você pode criar a solução de exemplo hello em Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-134">You can now build hello sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="4a8b8-135">Agora você pode executar o programa de exemplo hello em Olá framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-135">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="4a8b8-136">Digite o comando hello:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-136">Enter hello command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="4a8b8-137">Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-137">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="4a8b8-139">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-139">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="4a8b8-140">No painel de solução de saudação, clique em **dispositivos** toovisit Olá **dispositivos** página.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-140">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="4a8b8-141">Selecione o Pi framboesa no hello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-141">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="4a8b8-142">Depois, escolha **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-142">Then choose **Methods**:</span></span>

    ![Listar dispositivos no painel][img-list-devices]

1. <span data-ttu-id="4a8b8-144">Em Olá **invocar o método** escolha **InitiateFirmwareUpdate** em Olá **método** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-144">On hello **Invoke Method** page, choose **InitiateFirmwareUpdate** in hello **Method** dropdown.</span></span>

1. <span data-ttu-id="4a8b8-145">Em Olá **FWPackageURI** , digite **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-145">In hello **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="4a8b8-146">Esse arquivo contém a implementação de saudação da versão 2.0 do firmware hello.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-146">This archive file contains hello implementation of version 2.0 of hello firmware.</span></span>

1. <span data-ttu-id="4a8b8-147">Escolha **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="4a8b8-148">aplicativo Olá Olá framboesa Pi envia um painel de solução de backup toohello confirmação.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-148">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard.</span></span> <span data-ttu-id="4a8b8-149">Então, ele iniciará o processo de atualização de firmware de saudação baixando a nova versão de saudação do firmware hello:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-149">It then starts hello firmware update process by downloading hello new version of hello firmware:</span></span>

    ![Mostrar o histórico do método][img-method-history]

## <a name="observe-hello-firmware-update-process"></a><span data-ttu-id="4a8b8-151">Observe o processo de atualização de firmware Olá</span><span class="sxs-lookup"><span data-stu-id="4a8b8-151">Observe hello firmware update process</span></span>

<span data-ttu-id="4a8b8-152">Você pode observar o processo de atualização de firmware Olá conforme ele é executado no dispositivo hello e exibindo Olá relatados propriedades no painel de solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-152">You can observe hello firmware update process as it runs on hello device and by viewing hello reported properties in hello solution dashboard:</span></span>

1. <span data-ttu-id="4a8b8-153">Você pode exibir o progresso de saudação em saudação do processo de atualização em Olá framboesa Pi:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-153">You can view hello progress in of hello update process on hello Raspberry Pi:</span></span>

    ![Mostrar progresso da atualização][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="4a8b8-155">aplicativo de monitoramento remoto Olá silenciosamente reinicia quando Olá atualização for concluída.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-155">hello remote monitoring app restarts silently when hello update completes.</span></span> <span data-ttu-id="4a8b8-156">Use o comando Olá `ps -ef` tooverify está em execução.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-156">Use hello command `ps -ef` tooverify it is running.</span></span> <span data-ttu-id="4a8b8-157">Se desejar que o processo de saudação tooterminate, use Olá `kill` comando com a id de processo hello.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-157">If you want tooterminate hello process, use hello `kill` command with hello process id.</span></span>

1. <span data-ttu-id="4a8b8-158">Você pode exibir o status de saudação da atualização de firmware hello, conforme relatado pelo dispositivo hello, no portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-158">You can view hello status of hello firmware update, as reported by hello device, in hello solution portal.</span></span> <span data-ttu-id="4a8b8-159">Hello seguinte captura de tela mostra o status de saudação e a duração de cada estágio do processo de atualização de saudação e a nova versão de firmware Olá:</span><span class="sxs-lookup"><span data-stu-id="4a8b8-159">hello following screenshot shows hello status and duration of each stage of hello update process, and hello new firmware version:</span></span>

    ![Mostrar status do trabalho][img-job-status]

    <span data-ttu-id="4a8b8-161">Se você navegar toohello back painel, você pode verificar o dispositivo Olá ainda está enviando a telemetria após a atualização de firmware de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-161">If you navigate back toohello dashboard, you can verify hello device is still sending telemetry following hello firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="4a8b8-162">Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-162">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="4a8b8-163">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="4a8b8-163">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="4a8b8-164">Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-164">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a8b8-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a8b8-165">Next steps</span></span>

<span data-ttu-id="4a8b8-166">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a8b8-166">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md