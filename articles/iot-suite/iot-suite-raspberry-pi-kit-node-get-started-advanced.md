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
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a>Conecte-se a sua solução de monitoramento remoto de toohello framboesa Pi 3 e habilitar atualizações de firmware remoto usando o Node. js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Este tutorial mostra como toouse Olá Microsoft Azure IoT Starter Kit para framboesa Pi 3 para:

* Desenvolva um leitor de temperatura e umidade que pode se comunicar com a nuvem de saudação.
* Habilitar e executar um aplicativo de cliente remoto firmware update tooupdate hello em Olá framboesa Pi.

tutorial de saudação usa:

- OS Raspbian, Olá Node. js linguagem de programação e hello IoT do SDK do Microsoft Azure para Node.js tooimplement um dispositivo de exemplo.
- monitoramento remoto Olá IoT Suite pré-configurado solução como Olá baseado em nuvem back-end.

## <a name="overview"></a>Visão geral

Neste tutorial, você deve concluir Olá etapas a seguir:

- Implante uma instância do hello remoto monitoramento solução pré-configurada tooyour assinatura do Azure. Esta etapa implanta e configura automaticamente vários serviços do Azure.
- Configure seu toocommunicate sensores e dispositivos com o computador e Olá remotas de solução de monitoramento.
- Atualizar Olá exemplo dispositivo código tooconnect toohello remoto solução de monitoramento e enviar telemetria que você pode exibir no painel de solução de saudação.
- Use aplicativo de cliente Olá exemplo dispositivo código tooupdate hello.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Olá provisões de solução de monitoramento remoto de um conjunto de serviços do Azure em sua assinatura do Azure. implantação de saudação reflete uma arquitetura empresarial real. encargos de consumo do Azure desnecessário tooavoid, excluir a instância da solução de saudação pré-configurado no azureiotsuite.com quando você tiver terminado com ele. Se você precisar hello solução pré-configurada novamente, você poderá recriá-lo facilmente. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

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

Se você ainda não tiver feito isso, Olá clone necessário repositórios executando Olá comandos a seguir em seu Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Atualizar a cadeia de conexão do dispositivo Olá

Arquivo de configuração de exemplo hello aberta no hello **nano** editor usando Olá comando a seguir:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Substitua valores de espaço reservado de saudação com id do dispositivo hello e informações de IoT Hub é criado e salvo no início de saudação deste tutorial.

Quando terminar, conteúdo de saudação do arquivo de deviceinfo Olá deve ter a aparência Olá exemplo a seguir:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Salvar as alterações (**Ctrl-O**, **Enter**) e feche o editor de saudação (**Ctrl-X**).

## <a name="run-hello-sample"></a>Executar o exemplo hello

A seguir Olá execução comandos tooinstall Olá pré-requisitos do pacote de exemplo hello:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

Agora você pode executar o programa de exemplo hello em Olá framboesa Pi. Digite o comando hello:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

Olá seguinte saída de exemplo é um exemplo de saída de hello que consulte no prompt de comando Olá Olá framboesa Pi:

![Saída do aplicativo Raspberry Pi][img-raspberry-output]

Pressione **Ctrl-C** programa de saudação tooexit a qualquer momento.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. No painel de solução de saudação, clique em **dispositivos** toovisit Olá **dispositivos** página. Selecione o Pi framboesa no hello **lista de dispositivos**. Depois, escolha **Métodos**:

    ![Listar dispositivos no painel][img-list-devices]

1. Em Olá **invocar o método** escolha **InitiateFirmwareUpdate** em Olá **método** lista suspensa.

1. Em Olá **FWPackageURI** , digite **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**. Este arquivo contém a implementação de saudação da versão 2.0 do firmware hello.

1. Escolha **InvokeMethod**. aplicativo Olá Olá framboesa Pi envia um painel de solução de backup toohello confirmação. Então, ele iniciará o processo de atualização de firmware de saudação baixando a nova versão de saudação do firmware hello:

    ![Mostrar o histórico do método][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Observe o processo de atualização de firmware Olá

Você pode observar o processo de atualização de firmware Olá conforme ele é executado no dispositivo hello e exibindo Olá relatados propriedades no painel de solução de saudação:

1. Você pode exibir o progresso de saudação em saudação do processo de atualização em Olá framboesa Pi:

    ![Mostrar progresso da atualização][img-update-progress]

    > [!NOTE]
    > aplicativo de monitoramento remoto Olá silenciosamente reinicia quando Olá atualização for concluída. Use o comando Olá `ps -ef` tooverify está em execução. Se desejar que o processo de saudação tooterminate, use Olá `kill` comando com a id de processo hello.

1. Você pode exibir o status de saudação da atualização de firmware hello, conforme relatado pelo dispositivo hello, no portal de solução de saudação. Hello seguinte captura de tela mostra o status de saudação e a duração de cada estágio do processo de atualização de saudação e a nova versão de firmware Olá:

    ![Mostrar status do trabalho][img-job-status]

    Se você navegar toohello back painel, você pode verificar o dispositivo Olá ainda está enviando a telemetria após a atualização de firmware de saudação.

> [!WARNING]
> Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado. Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config]. Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.

## <a name="next-steps"></a>Próximas etapas

Visite Olá [Centro de desenvolvimento do Azure IoT](https://azure.microsoft.com/develop/iot/) para obter mais exemplos e documentação sobre IoT do Azure.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
