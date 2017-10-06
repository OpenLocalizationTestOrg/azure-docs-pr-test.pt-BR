---
featureFlags: usabilla
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 1: implantar o aplicativo | Microsoft Docs"
description: "Clonar um aplicativo de Node.js do exemplo hello do GitHub e gulp toodeploy deste quadro de tooyour framboesa Pi 3 do aplicativo. Este aplicativo de exemplo pisca Olá LED conectado toohello placa a cada dois segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: piscar led raspberry pi, piscar led com raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Criar e implantar o aplicativo de intermitência hello
## <a name="what-you-will-do"></a>O que você fará
Clonar um aplicativo de Node.js do exemplo hello do GitHub e use Olá gulp ferramenta toodeploy Olá exemplo aplicativo tooyour framboesa Pi 3. aplicativo de exemplo Hello pisca Olá LED conectado toohello placa a cada dois segundos. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como Olá toouse `device-discover-cli` ferramenta tooretrieve obter informações sobre o Pi da rede.
* Como toodeploy e execução Olá aplicativo de exemplo no Pi.
* Como toodeploy e depurar aplicativos em execução remotamente no Pi.

## <a name="what-you-need"></a>O que você precisa
Você deve ter concluído Olá seguintes operações com êxito:

* [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [Obter ferramentas Olá](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Obter o nome de host e endereço IP de saudação do Pi
Abra um prompt de comando no Windows ou um terminal macOS ou Ubuntu e, em seguida, execute Olá comando a seguir:

```bash
devdisco list --eth
```

Você verá uma saída que é a seguir toohello semelhante:

![Descoberta de dispositivo](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Anote Olá `IP address` e `hostname` de Pi. Você precisará dessas informações mais adiante neste artigo.

> [!NOTE]
> Certifique-se de Pi é conectado toohello mesmo de rede do computador. Por exemplo, se o computador estiver rede sem fio conectada tooa enquanto Pi é conectado tooa rede com fio, talvez você não veja Olá IP endereço na saída de devdisco hello.

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello
Olá tooopen código de exemplo, siga estas etapas:

1. Clone o repositório de exemplo de saudação do GitHub executando Olá comando a seguir:
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Estrutura do repositório](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

Olá `app.js` arquivo hello `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toocontrol Olá LED.

### <a name="install-application-dependencies"></a>Instalar dependências de aplicativos
Instale bibliotecas de saudação e outros módulos, que é necessário para o aplicativo de exemplo hello executando Olá comando a seguir:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurar conexão do dispositivo Olá
tooconfigure Olá conexão do dispositivo, siga estas etapas:

1. Gere arquivo de configuração de dispositivo de saudação executando Olá comando a seguir:
   
   ```bash
   gulp init
   ```
   
   arquivo de configuração de saudação `config-raspberrypi.json` contém credenciais do usuário Olá use toolog em tooPi. vazamento de saudação tooavoid de credenciais de usuário, o arquivo de configuração Olá é gerado na subpasta Olá `.iot-hub-getting-started` da pasta base do hello em seu computador.

2. Abra o arquivo de configuração de dispositivo de saudação no código do Visual Studio executando Olá comando a seguir:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. Substitua o espaço reservado de saudação `[device hostname or IP address]` com o endereço IP hello ou nome de host de saudação que você obteve anteriormente em "Obter Olá IP endereço e nome do host de Pi."
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> Você pode usar a chave SSH, em vez de nome de usuário e senha ao conectar-se tooRaspberry Pi. Em ordem toodo isso você terá toogenerate Olá chave usando **ssh-keygen** e **pi ssh-copy-id @\<endereço do dispositivo\>**.
>
> No Windows, esses comandos estão disponíveis em **Git Bash**.
>
> Em MacOS precisar toorun **brew instalar ssh-copy-id**.
>
> Depois de carregar com êxito Olá chave toohello framboesa Pi, substitua **device_password** com **device_key_path** propriedade **raspberrypi.json config**.
>
> As linhas atualizadas devem parecer com o seguinte:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Parabéns! Você criou com êxito o primeiro aplicativo de exemplo hello de Pi.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
### <a name="install-nodejs-and-npm-on-pi"></a>Instalar o Node.js e o NPM no Pi
Instale o Node. js e NPM em Pi executando Olá comando a seguir:

```bash
gulp install-tools
```

Essa tarefa pode demorar Olá de toocomplete de 10 minutos primeiro que você executá-lo.

### <a name="deploy-and-run-hello-sample-app"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello executando Olá comando a seguir:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Verifique se Olá aplicativo funciona
Agora você deve ver Olá LED no Pi piscando a cada dois segundos.  Se você não vir Olá LED piscando, consulte Olá [guia de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md) para problemas de toocommon de soluções.
![LED piscando](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Resumo
Instalar Olá necessárias ferramentas toowork com Pi e implantado uma saudação do exemplo aplicativo tooPi tooblink LED. Você pode criar, implantar e executar outro aplicativo de exemplo que se conecta Pi tooAzure toosend de IoT Hub e receber mensagens.

## <a name="next-steps"></a>Próximas etapas
[Obter Olá ferramentas do Azure](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

