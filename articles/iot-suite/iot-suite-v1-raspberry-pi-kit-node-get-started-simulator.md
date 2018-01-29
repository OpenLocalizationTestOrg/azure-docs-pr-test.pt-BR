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
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: 53297049fd36eae3839c6a8146afc336b8f5cd02
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a>Conectar o Raspberry Pi3 à solução de monitoramento remoto e enviar telemetria simulada usando o Node.js

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

Este tutorial mostra como usar o Raspberry Pi 3 para simular dados de temperatura e umidade e enviar para a nuvem. O tutorial usa:

- SO Raspbian, a linguagem de programação Node.js, e o SDK do Microsoft Azure IoT para Node.js para implementar um dispositivo de exemplo.
- A solução pré-configurada de monitoramento remoto do IoT Suite como o back-end baseado na nuvem.

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> A solução de monitoramento remoto provisiona um conjunto de serviços do Azure na sua assinatura do Azure. A implantação reflete uma arquitetura empresarial real. Para evitar encargos desnecessários de consumo do Azure, exclua a instância da solução pré-configurada em azureiotsuite.com quando tiver terminado de realizar as tarefas nela. Caso precise da solução novamente, você poderá recriá-la facilmente. Para saber mais sobre como reduzir o consumo durante a execução da solução de monitoramento remoto, confira [Configuração de soluções pré-configuradas do Azure IoT Suite para fins de demonstração][lnk-demo-config].

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a>Baixar e configurar o exemplo

Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto em seu Raspberry Pi.

### <a name="install-nodejs"></a>Instalar o Node. js

Caso ainda não tenha feito isso, instale o Node.js no Raspberry Pi. O SDK do IoT para Node.js exige a versão 0.11.5 do Node.js ou posterior. As seguintes etapas mostram como instalar o Node.js v6.10.2 no Raspberry Pi:

1. Use o seguinte comando para atualizar o Raspberry Pi:

    ```sh
    sudo apt-get update
    ```

1. Use o seguinte comando para baixar os binários do Node.js no Raspberry Pi:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Use o seguinte comando para instalar os binários:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Use o seguinte comando para verificar se você instalou com êxito o Node.js v6.10.2:

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a>Clonar os repositórios

Caso ainda não tenha feito isso, clone os repositórios necessários executando os seguintes comandos em um terminal no Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a>Atualizar a cadeia de conexão do dispositivo

Abra o arquivo de origem de exemplo no editor **nano** usando o seguinte comando:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Localize a linha:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Substitua os valores do espaço reservado pelas informações de dispositivo e Hub IoT que você criou e salvou no início deste tutorial. Salve suas alterações (**Ctrl-O**, **Enter**) e saia do editor (**Ctrl-X**).

## <a name="run-the-sample"></a>Execute o exemplo

Execute os seguintes comandos para instalar os pacotes de pré-requisito do exemplo:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

Agora você pode executar o programa de exemplo no Raspberry Pi. Insira o comando:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

O que você vê a seguir é um exemplo da saída vista no prompt de comando do Raspberry Pi:

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

Pressione **Ctrl-C** para sair do programa a qualquer momento.

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Próximas etapas

Visite o [Centro de Desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e a documentação sobre o Azure IoT.

[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
