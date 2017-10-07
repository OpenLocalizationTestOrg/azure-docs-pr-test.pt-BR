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
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Conecte-se a sua solução pré-configurada de monitoramento remoto do Azure IoT borda gateway toohello e enviar telemetria de um SensorTag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Este tutorial mostra como toouse os dados do Azure IoT borda temperatura e umidade de toosend de monitoramento remoto de SensorTag dispositivo toohello pré-configurado solução. Olá SensorTag conecta-se o gateway do Intel NUC toohello usando Bluetooth. tutorial de saudação usa:

- Azure IoT borda tooimplement um gateway de exemplo.
- monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.

## <a name="overview"></a>Visão geral

Neste tutorial, você deve concluir Olá etapas a seguir:

- Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure. Esta etapa implanta e configura automaticamente vários serviços do Azure.
- Configure seu toocommunicate de dispositivo de gateway Intel NUC com seu computador e a solução de monitoramento remoto hello.
- Configurar a telemetria de tooreceive Intel NUC gateway de um dispositivo SensorTag e enviá-lo toohello painel de monitoramento remoto.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas Instruments BLE SensorTag][lnk-sensortag]. Este tutorial recupera dados de telemetria via Bluetooth do dispositivo de SensorTag hello.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure. implantação de saudação reflete uma arquitetura empresarial real. encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele. Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Configurar a conectividade de Bluetooth

Configurar o Bluetooth Olá Intel NUC tooenable Olá SensorTag dispositivo tooconnect e enviar telemetria.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Localizar o endereço MAC Olá Olá SensorTag

1. No shell de saudação em Olá NUC Intel, execute Olá após comando toounblock Olá Bluetooth serviço:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Seguinte Olá execução comandos do serviço de Bluetooth Olá toostart em Olá Intel NUC e insira o shell de Bluetooth hello:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Execute Olá toopower de comando no controlador de Bluetooth Olá a seguir:

    ```bash
    power on
    ```

    Quando o controlador de saudação for no, você verá uma mensagem **alterando power em bem-sucedida**.

1. Execute Olá tooscan de comando para dispositivos Bluetooth próximos a seguir:

    ```bash
    scan on
    ```

1. Pressione Olá botão liga Olá SensorTag toomake-lo detectável. LED verde do Hello pisca.

1. Quando você vir uma mensagem no shell de saudação esse controlador Olá descobriu Olá SensorTag, anote Olá endereço MAC do dispositivo hello. Olá endereço MAC é semelhante **A0:E6:F8:B5:F6:00**. É necessário o endereço de MAC de Olá posteriormente no tutorial de saudação ao configurar o gateway de saudação.

1. Execute Olá tooturn comando off Bluetooth verificação a seguir:

    ```bash
    scan off
    ```

1. Execute Olá tooverify de comando que você pode conectar o dispositivo de SensorTag toohello a seguir:

    ```bash
    connect <SensorTag MAC address>
    ```

    Se você se conectar com êxito, o shell de saudação mostra a mensagem de saudação **Conexão bem-sucedida** e imprime as informações sobre o dispositivo de SensorTag hello. Se você não pode se conectar, verifique Olá que sensortag ainda está ligado.

1. Agora você pode desconectar Olá SensorTag e sair do shell de Bluetooth Olá executando Olá comandos a seguir:

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Criar o módulo personalizado de borda IoT Olá

Agora você pode criar hello módulo personalizado de borda IoT que permite Olá gateway toosend mensagens toohello remoto solução de monitoramento. Para obter mais informações sobre como configurar um gateway e módulos do IoT Edge, consulte [Conceitos do Azure IoT Edge][lnk-gateway-concepts].

Baixe o código-fonte Olá para módulos personalizados de borda IoT saudação do GitHub usando Olá comandos a seguir:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Crie o módulo de borda IoT personalizado hello usando Olá comandos a seguir:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script de compilação Olá coloca o módulo de borda IoT Olá libsensor2remotemonitoring.so personalizado na pasta de compilação de saudação.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurar e executar Olá gateway de borda IoT

Agora você pode configurar Olá telemetria de toosend de gateway de borda IoT da sua tooyour de dispositivo SensorTag painel de monitoramento remoto. Para obter mais informações sobre como configurar um gateway e módulos do IoT Edge, consulte [Conceitos do Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> Neste tutorial, você use o padrão de saudação `vi` editor de texto em Olá NUC Intel. Se você não usou `vi` antes, você deve concluir introdutório, tais como [Unix - Olá vi Tutorial do Editor de] [ lnk-vi-tutorial] toofamiliarize com este editor. Como alternativa, você pode instalar mais amigável do hello [nano](https://www.nano-editor.org/) editor usando o comando Olá `smart install nano -y`.

Arquivo de configuração de exemplo hello aberta no hello **vi** editor usando Olá comando a seguir:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

Localize Olá linhas na configuração de saudação do módulo de Hub IOT Olá a seguir:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Substitua o espaço reservado de saudação valores com hello informações de IoT Hub é criado e salvo no hello iniciar este tutorial. valor Olá para IoTHubName parecido com **yourrmsolution37e08**, e o valor Olá IoTSuffix é normalmente **azure devices.net**.

Localize Olá linhas na configuração de saudação do módulo de mapeamento Olá a seguir:

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Substituir saudação **macAddress** espaço reservado com hello endereço MAC de sua SensorTag que você anotou anteriormente. Substituir saudação **deviceID** e **deviceKey** espaços reservados com IDs de saudação e chaves para dispositivos Olá dois criado na solução de monitoramento remoto Olá anteriormente.

Localize Olá linhas na configuração de saudação do módulo de SensorTag Olá a seguir:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Substituir saudação **dispositivo\_mac\_endereço** espaço reservado com hello endereço MAC de sua SensorTag que você anotou anteriormente.

Salve suas alterações.

Agora você pode executar o gateway de saudação usando Olá comandos a seguir:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Olá gateway de borda IoT inicia no hello Intel NUC e envia a telemetria de saudação SensorTag toohello solução de monitoramento remota:

![Gateway de borda IoT envia Telemetria da saudação SensorTag][img-telemetry]

Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.

## <a name="view-hello-telemetry"></a>Telemetria de saudação do modo de exibição

gateway Olá agora está enviando a telemetria de saudação SensorTag dispositivo toohello remota solução de monitoramento. Você pode exibir a telemetria de saudação no painel de solução de saudação. Você também pode enviar o dispositivo de SensorTag tooyour comandos por meio do gateway de saudação do painel de solução de saudação.

- Navegue toohello painel de solução.
- Dispositivo Olá selecione configurada no gateway Olá que representa Olá SensorTag em Olá **tooView dispositivo** lista suspensa.
- Telemetria de saudação do dispositivo de SensorTag Olá exibe no painel de saudação.

![Telemetria de exibição dos dispositivos de SensorTag Olá][img-telemetry-display]

> [!WARNING]
> Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config]. Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.


## <a name="next-steps"></a>Próximas etapas

Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started