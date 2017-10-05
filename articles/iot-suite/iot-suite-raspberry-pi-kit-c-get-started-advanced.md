---
title: "Conectar um Raspberry Pi ao Azure IoT Suite usando C para oferecer suporte a atualizações de firmware | Microsoft Docs"
description: "Use o Microsoft Azure IoT Starter Kit para o Raspberry Pi 3 e o Azure IoT Suite. Use C para conectar seu Raspberry Pi à solução de monitoramento remoto, enviar telemetria de sensores para a nuvem e executar uma atualização de firmware remoto."
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
ms.openlocfilehash: f36f6512bb30e4b109b1bd1c3cdab10300f4edc9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a><span data-ttu-id="c22c4-104">Conectar o Raspberry Pi 3 à solução de monitoramento remoto e habilitar as atualizações de firmware remotas usando C</span><span class="sxs-lookup"><span data-stu-id="c22c4-104">Connect your Raspberry Pi 3 to the remote monitoring solution and enable remote firmware updates using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="c22c4-105">Este tutorial mostra como usar o Microsoft Azure IoT Starter Kit para Raspberry Pi 3 para:</span><span class="sxs-lookup"><span data-stu-id="c22c4-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to:</span></span>

* <span data-ttu-id="c22c4-106">Desenvolver um leitor de temperatura e umidade que possa se comunicar com a nuvem.</span><span class="sxs-lookup"><span data-stu-id="c22c4-106">Develop a temperature and humidity reader that can communicate with the cloud.</span></span>
* <span data-ttu-id="c22c4-107">Habilitar e executar uma atualização de firmware remota para atualizar o aplicativo cliente no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c22c4-107">Enable and perform a remote firmware update to update the client application on the Raspberry Pi.</span></span>

<span data-ttu-id="c22c4-108">O tutorial usa:</span><span class="sxs-lookup"><span data-stu-id="c22c4-108">The tutorial uses:</span></span>

* <span data-ttu-id="c22c4-109">SO Raspbian, a linguagem de programação C e o SDK do Microsoft Azure IoT para C a fim de implementar um dispositivo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c22c4-109">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
* <span data-ttu-id="c22c4-110">A solução pré-configurada de monitoramento remoto do IoT Suite como o back-end baseado na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c22c4-110">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="c22c4-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c22c4-111">Overview</span></span>

<span data-ttu-id="c22c4-112">Neste tutorial, você completa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c22c4-112">In this tutorial, you complete the following steps:</span></span>

* <span data-ttu-id="c22c4-113">Implantar uma instância da solução pré-configurada de monitoramento remoto em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c22c4-113">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="c22c4-114">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="c22c4-114">This step automatically deploys and configures multiple Azure services.</span></span>
* <span data-ttu-id="c22c4-115">Configurar seu dispositivo e sensores para comunicação com seu computador e com a solução de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="c22c4-115">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
* <span data-ttu-id="c22c4-116">Atualizar o exemplo de código de dispositivo para conectar-se à solução de monitoramento remoto e enviar telemetria, que pode ser exibida no painel da solução.</span><span class="sxs-lookup"><span data-stu-id="c22c4-116">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>
* <span data-ttu-id="c22c4-117">Use o exemplo de código de dispositivo para atualizar o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="c22c4-117">Use the sample device code to update the client application.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="c22c4-118">A solução de monitoramento remoto provisiona um conjunto de serviços do Azure na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c22c4-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="c22c4-119">A implantação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="c22c4-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="c22c4-120">Para evitar encargos desnecessários de consumo do Azure, exclua a instância da solução pré-configurada em azureiotsuite.com quando tiver terminado de realizar as tarefas nela.</span><span class="sxs-lookup"><span data-stu-id="c22c4-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="c22c4-121">Caso precise da solução novamente, você poderá recriá-la facilmente.</span><span class="sxs-lookup"><span data-stu-id="c22c4-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="c22c4-122">Para saber mais sobre como reduzir o consumo durante a execução da solução de monitoramento remoto, confira [Configuração de soluções pré-configuradas do Azure IoT Suite para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c22c4-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="c22c4-123">Baixar e configurar o exemplo</span><span class="sxs-lookup"><span data-stu-id="c22c4-123">Download and configure the sample</span></span>

<span data-ttu-id="c22c4-124">Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c22c4-124">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="c22c4-125">Clonar os repositórios</span><span class="sxs-lookup"><span data-stu-id="c22c4-125">Clone the repositories</span></span>

<span data-ttu-id="c22c4-126">Caso ainda não tenha feito isso, clone os repositórios necessários executando os seguintes comandos em seu Pi:</span><span class="sxs-lookup"><span data-stu-id="c22c4-126">If you haven't done so already, clone the required repositories by running the following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="c22c4-127">Atualizar a cadeia de conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="c22c4-127">Update the device connection string</span></span>

<span data-ttu-id="c22c4-128">Abra o exemplo de arquivo de configuração no editor **nano** usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c22c4-128">Open the sample configuration file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

<span data-ttu-id="c22c4-129">Substitua os valores do espaço reservado pelas informações de ID do dispositivo e do Hub IoT que você criou e salvou no início deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="c22c4-129">Replace the placeholder values with the device ID and IoT Hub information you created and saved at the start of this tutorial.</span></span>

<span data-ttu-id="c22c4-130">Quando terminar, o conteúdo do arquivo deviceinfo deverá parecer com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c22c4-130">When you are done, the contents of the deviceinfo file should look like the following example:</span></span>

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

<span data-ttu-id="c22c4-131">Salve suas alterações (**Ctrl-O**, **Enter**) e saia do editor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="c22c4-131">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="c22c4-132">Compilar o exemplo</span><span class="sxs-lookup"><span data-stu-id="c22c4-132">Build the sample</span></span>

<span data-ttu-id="c22c4-133">Se você ainda não tiver feito isso, instale os pacotes de pré-requisito para o SDK do dispositivo IoT do Microsoft Azure para C executando os seguintes comandos em um terminal no Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="c22c4-133">If you have not already done so, install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="c22c4-134">Agora você pode compilar a solução de exemplo no Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="c22c4-134">You can now build the sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

<span data-ttu-id="c22c4-135">Agora você pode executar o programa de exemplo no Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c22c4-135">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="c22c4-136">Insira o comando:</span><span class="sxs-lookup"><span data-stu-id="c22c4-136">Enter the command:</span></span>

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

<span data-ttu-id="c22c4-137">O que você vê a seguir é um exemplo da saída vista no prompt de comando do Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="c22c4-137">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

<span data-ttu-id="c22c4-139">Pressione **Ctrl-C** para sair do programa a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="c22c4-139">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. <span data-ttu-id="c22c4-140">No painel de solução, clique em **Dispositivos** para visitar a página **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="c22c4-140">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="c22c4-141">Selecione seu Raspberry Pi na **Lista de Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="c22c4-141">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="c22c4-142">Depois, escolha **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="c22c4-142">Then choose **Methods**:</span></span>

    ![Listar dispositivos no painel][img-list-devices]

1. <span data-ttu-id="c22c4-144">Na página **Invocar Método** escolha **InitiateFirmwareUpdate** na lista suspensa **Método**.</span><span class="sxs-lookup"><span data-stu-id="c22c4-144">On the **Invoke Method** page, choose **InitiateFirmwareUpdate** in the **Method** dropdown.</span></span>

1. <span data-ttu-id="c22c4-145">No campo **FWPackageURI**, insira **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span><span class="sxs-lookup"><span data-stu-id="c22c4-145">In the **FWPackageURI** field, enter **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**.</span></span> <span data-ttu-id="c22c4-146">Esse arquivo contém a implementação da versão 2.0 do firmware.</span><span class="sxs-lookup"><span data-stu-id="c22c4-146">This archive file contains the implementation of version 2.0 of the firmware.</span></span>

1. <span data-ttu-id="c22c4-147">Escolha **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="c22c4-147">Choose **InvokeMethod**.</span></span> <span data-ttu-id="c22c4-148">O aplicativo no Raspberry Pi envia uma confirmação de volta para o painel da solução.</span><span class="sxs-lookup"><span data-stu-id="c22c4-148">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard.</span></span> <span data-ttu-id="c22c4-149">Em seguida, ele inicia o processo de atualização de firmware baixando a nova versão do firmware:</span><span class="sxs-lookup"><span data-stu-id="c22c4-149">It then starts the firmware update process by downloading the new version of the firmware:</span></span>

    ![Mostrar o histórico do método][img-method-history]

## <a name="observe-the-firmware-update-process"></a><span data-ttu-id="c22c4-151">Observar o processo de atualização do firmware</span><span class="sxs-lookup"><span data-stu-id="c22c4-151">Observe the firmware update process</span></span>

<span data-ttu-id="c22c4-152">Observe o processo de atualização do firmware enquanto ele é executado no dispositivo e exibindo as propriedades relatadas no painel de solução:</span><span class="sxs-lookup"><span data-stu-id="c22c4-152">You can observe the firmware update process as it runs on the device and by viewing the reported properties in the solution dashboard:</span></span>

1. <span data-ttu-id="c22c4-153">Você pode exibir o progresso no processo de atualização no Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="c22c4-153">You can view the progress in of the update process on the Raspberry Pi:</span></span>

    ![Mostrar progresso da atualização][img-update-progress]

    > [!NOTE]
    > <span data-ttu-id="c22c4-155">O aplicativo de monitoramento remoto reinicia silenciosamente após a conclusão da atualização.</span><span class="sxs-lookup"><span data-stu-id="c22c4-155">The remote monitoring app restarts silently when the update completes.</span></span> <span data-ttu-id="c22c4-156">Use o comando `ps -ef` para verificar se ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="c22c4-156">Use the command `ps -ef` to verify it is running.</span></span> <span data-ttu-id="c22c4-157">Se você quiser encerrar o processo, use o comando `kill` com a id do processo.</span><span class="sxs-lookup"><span data-stu-id="c22c4-157">If you want to terminate the process, use the `kill` command with the process id.</span></span>

1. <span data-ttu-id="c22c4-158">Veja o status da atualização de firmware, conforme indicado pelo dispositivo, no portal da solução.</span><span class="sxs-lookup"><span data-stu-id="c22c4-158">You can view the status of the firmware update, as reported by the device, in the solution portal.</span></span> <span data-ttu-id="c22c4-159">A captura de tela a seguir mostra o status e a duração de cada estágio do processo de atualização e a nova versão do firmware:</span><span class="sxs-lookup"><span data-stu-id="c22c4-159">The following screenshot shows the status and duration of each stage of the update process, and the new firmware version:</span></span>

    ![Mostrar status do trabalho][img-job-status]

    <span data-ttu-id="c22c4-161">Se você navegar de volta para o painel, poderá verificar que o dispositivo ainda está enviando telemetria após a atualização do firmware.</span><span class="sxs-lookup"><span data-stu-id="c22c4-161">If you navigate back to the dashboard, you can verify the device is still sending telemetry following the firmware update.</span></span>

> [!WARNING]
> <span data-ttu-id="c22c4-162">Se você deixar a solução de monitoramento remoto em execução em sua conta do Azure, você receberá uma cobrança pelo tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c22c4-162">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="c22c4-163">Para saber mais sobre como reduzir o consumo durante a execução da solução de monitoramento remoto, confira [Configuração de soluções pré-configuradas do Azure IoT Suite para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c22c4-163">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="c22c4-164">Exclua a solução pré-configurada de sua conta do Azure quando terminar de usá-la.</span><span class="sxs-lookup"><span data-stu-id="c22c4-164">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c22c4-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c22c4-165">Next steps</span></span>

<span data-ttu-id="c22c4-166">Visite o [Centro de Desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e a documentação sobre o Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="c22c4-166">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md