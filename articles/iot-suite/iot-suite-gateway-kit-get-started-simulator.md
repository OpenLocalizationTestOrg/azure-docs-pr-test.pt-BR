---
title: aaaConnect tooAzure um gateway IoT Suite usando um NUC Intel | Microsoft Docs
description: "Use Olá Kit de Gateway Microsoft IoT comercial e hello remoto monitoramento pré-configurado solução. Saudação de uso do Azure IoT borda gateway tooconnect toohello remota solução de monitoramento, enviar telemetria simulada toohello nuvem e responder toomethods invocado no painel de solução de saudação."
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
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="e6751-104">Conecte-se a sua solução pré-configurada de monitoramento remoto do Azure IoT borda gateway toohello e enviar telemetria simulada</span><span class="sxs-lookup"><span data-stu-id="e6751-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="e6751-105">Este tutorial mostra como a temperatura do toouse Azure IoT borda toosimulate e monitoramento remoto de umidade dados toosend toohello pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="e6751-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="e6751-106">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="e6751-106">hello tutorial uses:</span></span>

- <span data-ttu-id="e6751-107">Azure IoT borda tooimplement um gateway de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e6751-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="e6751-108">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="e6751-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="e6751-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e6751-109">Overview</span></span>

<span data-ttu-id="e6751-110">Neste tutorial, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6751-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="e6751-111">Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6751-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="e6751-112">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6751-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="e6751-113">Configure seu toocommunicate de dispositivo de gateway Intel NUC com seu computador e a solução de monitoramento remoto hello.</span><span class="sxs-lookup"><span data-stu-id="e6751-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="e6751-114">Configure Olá toosend de gateway de borda IoT simulados telemetria que você pode exibir no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6751-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="e6751-115">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6751-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="e6751-116">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="e6751-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="e6751-117">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="e6751-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="e6751-118">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="e6751-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="e6751-119">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="e6751-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="e6751-120">Repita Olá anterior etapas tooadd um segundo dispositivo usando uma ID de dispositivo como **device02**.</span><span class="sxs-lookup"><span data-stu-id="e6751-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="e6751-121">exemplo Hello envia dados de dois dispositivos simulados em Olá gateway toohello remoto solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="e6751-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="e6751-122">Criar o módulo personalizado de borda IoT Olá</span><span class="sxs-lookup"><span data-stu-id="e6751-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="e6751-123">Agora você pode criar hello módulo personalizado de borda IoT que permite Olá gateway toosend mensagens toohello remoto solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="e6751-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="e6751-124">Para obter mais informações sobre como configurar um gateway e módulos do IoT Edge, consulte [Conceitos do Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="e6751-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="e6751-125">Baixe o código-fonte Olá para módulos personalizados de borda IoT saudação do GitHub usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6751-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="e6751-126">Crie o módulo de borda IoT personalizado hello usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6751-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="e6751-127">script de compilação Olá coloca o módulo de borda IoT Olá libsimulator.so personalizado na pasta de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6751-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="e6751-128">Configurar e executar Olá gateway de borda IoT</span><span class="sxs-lookup"><span data-stu-id="e6751-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="e6751-129">Agora você pode configurar Olá IoT borda gateway toosend telemetria simulada tooyour remoto painel de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="e6751-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="e6751-130">Para obter mais informações sobre como configurar um gateway e módulos do IoT Edge, consulte [Conceitos do Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="e6751-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="e6751-131">Neste tutorial, você use o padrão de saudação `vi` editor de texto em Olá NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="e6751-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="e6751-132">Se você não usou `vi` antes, você deve concluir introdutório, tais como [Unix - Olá vi Tutorial do Editor de] [ lnk-vi-tutorial] toofamiliarize com este editor.</span><span class="sxs-lookup"><span data-stu-id="e6751-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="e6751-133">Como alternativa, você pode instalar mais amigável do hello [nano](https://www.nano-editor.org/) editor usando o comando Olá `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="e6751-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="e6751-134">Arquivo de configuração de exemplo hello aberta no hello **vi** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6751-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="e6751-135">Localize Olá linhas na configuração de saudação do módulo de Hub IOT Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6751-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="e6751-136">Substitua o espaço reservado de saudação valores com hello informações de IoT Hub é criado e salvo no hello iniciar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e6751-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="e6751-137">valor Olá para IoTHubName parecido com **yourrmsolution37e08**, e o valor Olá IoTSuffix é normalmente **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="e6751-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="e6751-138">Localize Olá linhas na configuração de saudação do módulo de mapeamento Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6751-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="e6751-139">Substituir saudação **deviceID** e **deviceKey** espaços reservados com IDs de saudação e chaves para dispositivos Olá dois criado na solução de monitoramento remoto Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e6751-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="e6751-140">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="e6751-140">Save your changes.</span></span>

<span data-ttu-id="e6751-141">Agora você pode executar Olá comandos de gateway de borda IoT usando Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6751-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="e6751-142">gateway Olá inicia no hello Intel NUC e envia a solução de monitoramento remoto telemetria simulada toohello:</span><span class="sxs-lookup"><span data-stu-id="e6751-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![O gateway do IoT Edge gera telemetria simulada][img-simulated telemetry]

<span data-ttu-id="e6751-144">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e6751-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="e6751-145">Telemetria de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="e6751-145">View hello telemetry</span></span>

<span data-ttu-id="e6751-146">Olá gateway de borda IoT agora está enviando a telemetria simulada toohello solução de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="e6751-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="e6751-147">Você pode exibir a telemetria de saudação no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6751-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="e6751-148">Navegue toohello painel de solução.</span><span class="sxs-lookup"><span data-stu-id="e6751-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="e6751-149">Selecione um dos dispositivos Olá dois configurada no gateway Olá Olá **tooView dispositivo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="e6751-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="e6751-150">Telemetria de saudação de dispositivos de gateway Olá exibe no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6751-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Telemetria de exibição dos dispositivos de gateway Olá simulado][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="e6751-152">Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado.</span><span class="sxs-lookup"><span data-stu-id="e6751-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="e6751-153">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="e6751-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="e6751-154">Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.</span><span class="sxs-lookup"><span data-stu-id="e6751-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6751-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6751-155">Next steps</span></span>

<span data-ttu-id="e6751-156">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6751-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started