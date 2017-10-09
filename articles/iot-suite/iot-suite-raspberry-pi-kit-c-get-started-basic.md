---
title: aaaConnect tooAzure um Pi framboesa IoT Suite usando C com sensores reais | Microsoft Docs
description: "Use hello Microsoft Azure IoT Starter Kit para Olá framboesa Pi 3 e o Azure IoT Suite. Usar C tooconnect sua solução de monitoramento remoto de toohello framboesa Pi, enviar telemetria de sensores toohello nuvem e responder toomethods invocada a partir do painel de solução de saudação."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a>Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e enviar telemetria a partir de um sensor real usando C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Este tutorial mostra como toouse hello Microsoft Azure IoT Starter Kit para framboesa Pi 3 toodevelop um leitor de temperatura e umidade que pode se comunicar com a nuvem de saudação. tutorial de saudação usa:

- OS Raspbian, linguagem de programação Olá C e hello SDK do Microsoft Azure IoT para C tooimplement um dispositivo de exemplo.
- monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.

## <a name="overview"></a>Visão geral

Neste tutorial, você deve concluir Olá etapas a seguir:

- Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure. Esta etapa implanta e configura automaticamente vários serviços do Azure.
- Configure seu toocommunicate sensores e dispositivos com o computador e Olá remotas de solução de monitoramento.
- Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria que você pode exibir no painel de solução de saudação.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure. implantação de saudação reflete uma arquitetura empresarial real. encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele. Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Baixar e configurar o exemplo hello

Agora você pode baixar e configurar o aplicativo cliente de monitoramento remoto Olá em seu Pi framboesa.

### <a name="clone-hello-repositories"></a>Repositórios de saudação do clone

Se você ainda não fez isso, Olá clone necessário Olá de repositórios executando comandos em um terminal a seguir em seu Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a>Atualizar a cadeia de conexão do dispositivo Olá

Arquivo de origem de exemplo hello aberto em Olá **nano** editor usando Olá comando a seguir:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

Localize Olá linhas seguintes:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Substitua os valores de espaço reservado Olá Olá e informações de IoT Hub é criado e salvo no início de saudação deste tutorial. Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).

## <a name="build-hello-sample"></a>Compilar o exemplo hello

Instale pacotes de pré-requisitos de saudação para Olá SDK de dispositivo do Microsoft Azure IoT para C executando Olá seguindo os comandos em um terminal na Olá framboesa Pi:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Agora você pode criar a solução de exemplo hello atualizado em Olá framboesa Pi:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

Agora você pode executar o programa de exemplo hello em Olá framboesa Pi. Digite o comando hello:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Próximas etapas

Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
