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
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Conecte-se a sua solução pré-configurada de monitoramento remoto do Azure IoT borda gateway toohello e enviar telemetria simulada

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Este tutorial mostra como a temperatura do toouse Azure IoT borda toosimulate e monitoramento remoto de umidade dados toosend toohello pré-configurado solução. tutorial de saudação usa:

- Azure IoT borda tooimplement um gateway de exemplo.
- monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.

## <a name="overview"></a>Visão geral

Neste tutorial, você deve concluir Olá etapas a seguir:

- Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure. Esta etapa implanta e configura automaticamente vários serviços do Azure.
- Configure seu toocommunicate de dispositivo de gateway Intel NUC com seu computador e a solução de monitoramento remoto hello.
- Configure Olá toosend de gateway de borda IoT simulados telemetria que você pode exibir no painel de solução de saudação.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure. implantação de saudação reflete uma arquitetura empresarial real. encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele. Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Repita Olá anterior etapas tooadd um segundo dispositivo usando uma ID de dispositivo como **device02**. exemplo Hello envia dados de dois dispositivos simulados em Olá gateway toohello remoto solução de monitoramento.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script de compilação Olá coloca o módulo de borda IoT Olá libsimulator.so personalizado na pasta de compilação de saudação.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurar e executar Olá gateway de borda IoT

Agora você pode configurar Olá IoT borda gateway toosend telemetria simulada tooyour remoto painel de monitoramento. Para obter mais informações sobre como configurar um gateway e módulos do IoT Edge, consulte [Conceitos do Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> Neste tutorial, você use o padrão de saudação `vi` editor de texto em Olá NUC Intel. Se você não usou `vi` antes, você deve concluir introdutório, tais como [Unix - Olá vi Tutorial do Editor de] [ lnk-vi-tutorial] toofamiliarize com este editor. Como alternativa, você pode instalar mais amigável do hello [nano](https://www.nano-editor.org/) editor usando o comando Olá `smart install nano -y`.

Arquivo de configuração de exemplo hello aberta no hello **vi** editor usando Olá comando a seguir:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
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

Substituir saudação **deviceID** e **deviceKey** espaços reservados com IDs de saudação e chaves para dispositivos Olá dois criado na solução de monitoramento remoto Olá anteriormente.

Salve suas alterações.

Agora você pode executar Olá comandos de gateway de borda IoT usando Olá a seguir:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

gateway Olá inicia no hello Intel NUC e envia a solução de monitoramento remoto telemetria simulada toohello:

![O gateway do IoT Edge gera telemetria simulada][img-simulated telemetry]

Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.

## <a name="view-hello-telemetry"></a>Telemetria de saudação do modo de exibição

Olá gateway de borda IoT agora está enviando a telemetria simulada toohello solução de monitoramento remoto. Você pode exibir a telemetria de saudação no painel de solução de saudação.

- Navegue toohello painel de solução.
- Selecione um dos dispositivos Olá dois configurada no gateway Olá Olá **tooView dispositivo** lista suspensa.
- Telemetria de saudação de dispositivos de gateway Olá exibe no painel de saudação.

![Telemetria de exibição dos dispositivos de gateway Olá simulado][img-telemetry-display]

> [!WARNING]
> Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config]. Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.

## <a name="next-steps"></a>Próximas etapas

Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started