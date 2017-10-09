---
title: aaaConnect tooAzure um Pi framboesa IoT Suite com Node. js telemetria simulada | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Use tooconnect Node. js sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria simulada toohello nuvem e responder toomethods invocada a partir do painel de solução de saudação."
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
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a>Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e enviar telemetria simulada usando Node. js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Este tutorial mostra como toouse Olá framboesa Pi 3 toosimulate temperatura e umidade dados toosend toohello de nuvem. tutorial de saudação usa:

- OS Raspbian, Olá Node. js linguagem de programação e hello IoT do SDK do Microsoft Azure para Node.js tooimplement um dispositivo de exemplo.
- monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure. implantação de saudação reflete uma arquitetura empresarial real. encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele. Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>Baixar e configurar o exemplo hello

Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.

### <a name="install-nodejs"></a>Instalar o Node. js

Caso ainda não tenha feito isso, instale o Node.js no Raspberry Pi. Olá IoT SDK para Node.js requer a versão 0.11.5 do Node.js ou posterior. Olá etapas a seguir mostram como tooinstall Node. js v6.10.2 em seu Pi framboesa:

1. Use Olá tooupdate de comando a seguir o Pi framboesa:

    ```sh
    sudo apt-get update
    ```

1. Use Olá comando toodownload Olá Node. js binários tooyour framboesa Pi a seguir:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Use Olá binários de saudação do tooinstall de comando a seguir:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Use Olá tooverify de comando que você instalou com êxito o Node. js v6.10.2 a seguir:

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Repositórios de saudação do clone

Se você ainda não fez isso, Olá clone necessário Olá de repositórios executando comandos em um terminal a seguir em seu Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Atualizar a cadeia de conexão do dispositivo Olá

Arquivo de origem de exemplo hello aberto em Olá **nano** editor usando Olá comando a seguir:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Localize a linha de saudação:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Substitua os valores de espaço reservado Olá Olá e informações de IoT Hub é criado e salvo no início de saudação deste tutorial. Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).

## <a name="run-hello-sample"></a>Executar o exemplo hello

A seguir Olá execução comandos tooinstall Olá pré-requisitos do pacote de exemplo hello:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

Agora você pode executar o programa de exemplo hello em Olá framboesa Pi. Digite o comando hello:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Próximas etapas

Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
