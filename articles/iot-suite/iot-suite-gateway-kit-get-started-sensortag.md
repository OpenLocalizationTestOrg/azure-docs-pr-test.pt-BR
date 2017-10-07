---
title: aaaConnect tooAzure um gateway IoT Suite usando um NUC Intel | Microsoft Docs
description: "Use Olá Kit de Gateway Microsoft IoT comercial e hello remoto monitoramento pré-configurado solução. Use hello Azure IoT borda gateway tooenable uma solução de monitoramento remoto de toohello SensorTag do tooconnect do dispositivo, nuvem de toohello de telemetria de enviar e responder toomethods invocada a partir do painel de solução de saudação."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="c84e0-104">Conecte-se a sua solução pré-configurada de monitoramento remoto do Azure IoT borda gateway toohello e enviar telemetria de um SensorTag</span><span class="sxs-lookup"><span data-stu-id="c84e0-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="c84e0-105">Este tutorial mostra como toouse os dados do Azure IoT borda temperatura e umidade de toosend de monitoramento remoto de SensorTag dispositivo toohello pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="c84e0-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="c84e0-106">Olá SensorTag conecta-se o gateway do Intel NUC toohello usando Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="c84e0-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="c84e0-107">tutorial de saudação usa:</span><span class="sxs-lookup"><span data-stu-id="c84e0-107">hello tutorial uses:</span></span>

- <span data-ttu-id="c84e0-108">Azure IoT borda tooimplement um gateway de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c84e0-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="c84e0-109">monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.</span><span class="sxs-lookup"><span data-stu-id="c84e0-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="c84e0-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c84e0-110">Overview</span></span>

<span data-ttu-id="c84e0-111">Neste tutorial, você deve concluir Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="c84e0-112">Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c84e0-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="c84e0-113">Esta etapa implanta e configura automaticamente vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="c84e0-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="c84e0-114">Configure seu toocommunicate de dispositivo de gateway Intel NUC com seu computador e a solução de monitoramento remoto hello.</span><span class="sxs-lookup"><span data-stu-id="c84e0-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="c84e0-115">Configurar a telemetria de tooreceive Intel NUC gateway de um dispositivo SensorTag e enviá-lo toohello painel de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="c84e0-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="c84e0-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="c84e0-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="c84e0-117">Este tutorial recupera dados de telemetria via Bluetooth do dispositivo de SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="c84e0-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="c84e0-118">Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c84e0-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="c84e0-119">implantação de saudação reflete uma arquitetura empresarial real.</span><span class="sxs-lookup"><span data-stu-id="c84e0-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="c84e0-120">encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele.</span><span class="sxs-lookup"><span data-stu-id="c84e0-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="c84e0-121">Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="c84e0-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="c84e0-122">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c84e0-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="c84e0-123">Configurar a conectividade de Bluetooth</span><span class="sxs-lookup"><span data-stu-id="c84e0-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="c84e0-124">Configurar o Bluetooth Olá Intel NUC tooenable Olá SensorTag dispositivo tooconnect e enviar telemetria.</span><span class="sxs-lookup"><span data-stu-id="c84e0-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="c84e0-125">Localizar o endereço MAC Olá Olá SensorTag</span><span class="sxs-lookup"><span data-stu-id="c84e0-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="c84e0-126">No shell de saudação em Olá NUC Intel, execute Olá após comando toounblock Olá Bluetooth serviço:</span><span class="sxs-lookup"><span data-stu-id="c84e0-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="c84e0-127">Seguinte Olá execução comandos do serviço de Bluetooth Olá toostart em Olá Intel NUC e insira o shell de Bluetooth hello:</span><span class="sxs-lookup"><span data-stu-id="c84e0-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="c84e0-128">Execute Olá toopower de comando no controlador de Bluetooth Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="c84e0-129">Quando o controlador de saudação for no, você verá uma mensagem **alterando power em bem-sucedida**.</span><span class="sxs-lookup"><span data-stu-id="c84e0-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="c84e0-130">Execute Olá tooscan de comando para dispositivos Bluetooth próximos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="c84e0-131">Pressione Olá botão liga Olá SensorTag toomake-lo detectável.</span><span class="sxs-lookup"><span data-stu-id="c84e0-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="c84e0-132">LED verde do Hello pisca.</span><span class="sxs-lookup"><span data-stu-id="c84e0-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="c84e0-133">Quando você vir uma mensagem no shell de saudação esse controlador Olá descobriu Olá SensorTag, anote Olá endereço MAC do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="c84e0-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="c84e0-134">Olá endereço MAC é semelhante **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="c84e0-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="c84e0-135">É necessário o endereço de MAC de Olá posteriormente no tutorial de saudação ao configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="c84e0-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="c84e0-136">Execute Olá tooturn comando off Bluetooth verificação a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="c84e0-137">Execute Olá tooverify de comando que você pode conectar o dispositivo de SensorTag toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="c84e0-138">Se você se conectar com êxito, o shell de saudação mostra a mensagem de saudação **Conexão bem-sucedida** e imprime as informações sobre o dispositivo de SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="c84e0-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="c84e0-139">Se você não pode se conectar, verifique Olá que sensortag ainda está ligado.</span><span class="sxs-lookup"><span data-stu-id="c84e0-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="c84e0-140">Agora você pode desconectar Olá SensorTag e sair do shell de Bluetooth Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="c84e0-141">Criar o módulo personalizado de borda IoT Olá</span><span class="sxs-lookup"><span data-stu-id="c84e0-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="c84e0-142">Agora você pode criar hello módulo personalizado de borda IoT que permite Olá gateway toosend mensagens toohello remoto solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="c84e0-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="c84e0-143">Para obter mais informações sobre como configurar um gateway e módulos do IoT Edge, consulte [Conceitos do Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="c84e0-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="c84e0-144">Baixe o código-fonte Olá para módulos personalizados de borda IoT saudação do GitHub usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="c84e0-145">Crie o módulo de borda IoT personalizado hello usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="c84e0-146">script de compilação Olá coloca o módulo de borda IoT Olá libsensor2remotemonitoring.so personalizado na pasta de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c84e0-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="c84e0-147">Configurar e executar Olá gateway de borda IoT</span><span class="sxs-lookup"><span data-stu-id="c84e0-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="c84e0-148">Agora você pode configurar Olá telemetria de toosend de gateway de borda IoT da sua tooyour de dispositivo SensorTag painel de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="c84e0-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="c84e0-149">Para obter mais informações sobre como configurar um gateway e módulos do IoT Edge, consulte [Conceitos do Azure IoT Edge][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="c84e0-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="c84e0-150">Neste tutorial, você use o padrão de saudação `vi` editor de texto em Olá NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="c84e0-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="c84e0-151">Se você não usou `vi` antes, você deve concluir introdutório, tais como [Unix - Olá vi Tutorial do Editor de] [ lnk-vi-tutorial] toofamiliarize com este editor.</span><span class="sxs-lookup"><span data-stu-id="c84e0-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="c84e0-152">Como alternativa, você pode instalar mais amigável do hello [nano](https://www.nano-editor.org/) editor usando o comando Olá `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="c84e0-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="c84e0-153">Arquivo de configuração de exemplo hello aberta no hello **vi** editor usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="c84e0-154">Localize Olá linhas na configuração de saudação do módulo de Hub IOT Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="c84e0-155">Substitua o espaço reservado de saudação valores com hello informações de IoT Hub é criado e salvo no hello iniciar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c84e0-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="c84e0-156">valor Olá para IoTHubName parecido com **yourrmsolution37e08**, e o valor Olá IoTSuffix é normalmente **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="c84e0-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="c84e0-157">Localize Olá linhas na configuração de saudação do módulo de mapeamento Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="c84e0-158">Substituir saudação **macAddress** espaço reservado com hello endereço MAC de sua SensorTag que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c84e0-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="c84e0-159">Substituir saudação **deviceID** e **deviceKey** espaços reservados com IDs de saudação e chaves para dispositivos Olá dois criado na solução de monitoramento remoto Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c84e0-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="c84e0-160">Localize Olá linhas na configuração de saudação do módulo de SensorTag Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="c84e0-161">Substituir saudação **dispositivo\_mac\_endereço** espaço reservado com hello endereço MAC de sua SensorTag que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c84e0-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="c84e0-162">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="c84e0-162">Save your changes.</span></span>

<span data-ttu-id="c84e0-163">Agora você pode executar o gateway de saudação usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c84e0-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="c84e0-164">Olá gateway de borda IoT inicia no hello Intel NUC e envia a telemetria de saudação SensorTag toohello solução de monitoramento remota:</span><span class="sxs-lookup"><span data-stu-id="c84e0-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![Gateway de borda IoT envia Telemetria da saudação SensorTag][img-telemetry]

<span data-ttu-id="c84e0-166">Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="c84e0-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="c84e0-167">Telemetria de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="c84e0-167">View hello telemetry</span></span>

<span data-ttu-id="c84e0-168">gateway Olá agora está enviando a telemetria de saudação SensorTag dispositivo toohello remota solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="c84e0-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="c84e0-169">Você pode exibir a telemetria de saudação no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="c84e0-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="c84e0-170">Você também pode enviar o dispositivo de SensorTag tooyour comandos por meio do gateway de saudação do painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="c84e0-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="c84e0-171">Navegue toohello painel de solução.</span><span class="sxs-lookup"><span data-stu-id="c84e0-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="c84e0-172">Dispositivo Olá selecione configurada no gateway Olá que representa Olá SensorTag em Olá **tooView dispositivo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="c84e0-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="c84e0-173">Telemetria de saudação do dispositivo de SensorTag Olá exibe no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="c84e0-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Telemetria de exibição dos dispositivos de SensorTag Olá][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="c84e0-175">Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado.</span><span class="sxs-lookup"><span data-stu-id="c84e0-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="c84e0-176">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c84e0-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="c84e0-177">Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.</span><span class="sxs-lookup"><span data-stu-id="c84e0-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c84e0-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c84e0-178">Next steps</span></span>

<span data-ttu-id="c84e0-179">Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="c84e0-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started