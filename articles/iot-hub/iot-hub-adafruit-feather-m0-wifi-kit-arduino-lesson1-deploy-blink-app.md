---
title: "Conecte-se Arduino tooAzure IoT - lição 1: implantar o aplicativo | Microsoft Docs"
description: "Clonar um aplicativo de Arduino exemplo hello do GitHub e, em seguida, execute o gulp toodeploy tooyour esse aplicativo Adafruit difusão M0 WiFi. Este aplicativo de exemplo pisca Olá GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projetos led arduino, piscar led arduino, código piscar led arduino, programa de piscar arduino, exemplo de piscar arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Criar e implantar o aplicativo de intermitência hello
## <a name="what-you-will-do"></a>O que você fará
Clonar um aplicativo de Arduino exemplo hello do GitHub e use Olá gulp ferramenta toodeploy Olá exemplo aplicativo tooyour Adafruit difusão M0 WiFi Arduino quadro. Olá exemplo aplicativo pisca Olá GPIO 13 barod LEVOU a cada dois segundos.

Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting-page].

## <a name="what-you-will-learn"></a>O que você aprenderá
* Como toodeploy e execução Olá aplicativo de exemplo em seu quadro Arduino.

## <a name="what-you-need"></a>O que você precisa
Você deve ter concluído Olá seguintes operações com êxito:

* [Configurar seu dispositivo][configure-your-device]
* [Obter ferramentas Olá][get-the-tools]

## <a name="open-hello-sample-application"></a>Aplicativo de exemplo hello aberto
Olá tooopen aplicativo de exemplo, siga estas etapas:

1. Clone o repositório de exemplo de saudação do GitHub executando Olá comando a seguir:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

Olá `app.ino` arquivo hello `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toocontrol Olá LED.

### <a name="install-application-dependencies"></a>Instalar dependências de aplicativos
Instale bibliotecas de saudação e outros módulos, que é necessário para o aplicativo de exemplo hello executando Olá comando a seguir:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurar conexão do dispositivo Olá
tooconfigure Olá conexão do dispositivo, siga estas etapas:

1. Obter a porta serial saudação do dispositivo Olá Olá CLI de descoberta do dispositivo:

   ```bash
   devdisco list --usb
   ```

   Você deve ver uma saída que é a seguir toohello semelhante e encontrar a porta COM hello usb para a sua placa Arduino: ![a descoberta de dispositivos][device-discovery]

2. Arquivo hello abrir `config.json` em Olá pasta lição e adicionar valor Olá Olá encontrado número da porta COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > Para a porta de saudação COM, na plataforma Windows, tem um formato de Olá `COM1, COM2, ...`. No macOS ou Ubuntu, começa com `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Instalar as ferramentas de saudação necessários para seu quadro Arduino

Instale o hello Azure IoT Hub SDK para seu quadro Arduino executando Olá comando a seguir:

```bash
gulp install-tools
```

Essa tarefa pode levar um longo tempo toocomplete, dependendo de sua conexão de rede.

> [!NOTE]
> Saia do hello executando a instância de Arduino IDE quando você executar tarefas de gulp: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello executando Olá comando a seguir:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Verifique se Olá aplicativo funciona
Se você não vir Olá LED piscando, consulte Olá [guia de solução de problemas] [ troubleshooting-page] para problemas de toocommon de soluções.

![LED piscando][led-blinking]

## <a name="summary"></a>Resumo
Instalar Olá necessárias ferramentas toowork com seu quadro Arduino e implantado uma saudação de quadro tooblink do exemplo aplicativo tooyour Arduino LED. Você pode criar, implantar e executar outro aplicativo de exemplo que se conecta a seu quadro de Arduino tooAzure toosend de IoT Hub e receber mensagens.

## <a name="next-steps"></a>Próximas etapas
[Obter Olá ferramentas do Azure][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md