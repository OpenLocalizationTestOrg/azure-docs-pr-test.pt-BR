---
title: "Connect Arduino (C) tooAzure IoT – lição 4: dispositivos de nuvem | Microsoft Docs"
description: "Um aplicativo de exemplo é executado no Adafruit Feather M0 WiFi e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens tooAdafruit difusão M0 WiFi do seu Olá de tooblink de hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: controlar led pela web com arduino, controlar led via web com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Executar um tooreceive do aplicativo de exemplo mensagens de nuvem para dispositivo
Neste artigo, você implanta um aplicativo de exemplo na placa Adafruit difusão M0 WiFi Arduino.

aplicativo de exemplo Hello monitora mensagens de entrada de seu hub IoT. Você também executar uma tarefa de vez em seu tooyour de mensagens do computador toosend Arduino quadro do seu hub IoT. Quando o aplicativo de exemplo hello recebe mensagens de saudação, pisca Olá LED. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-do"></a>O que você fará
* Conecte-se o hub IoT do hello exemplo aplicativo tooyour.
* Implante e execute o aplicativo de exemplo hello.
* Envie mensagens de seu Olá de quadro tooblink do IoT hub tooyour Arduino LED.

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como toomonitor de mensagens de entrada do seu hub IoT.
* Como toosend de nuvem para dispositivo mensagens de seu tooyour de hub IoT Arduino quadro.

## <a name="what-you-need"></a>O que você precisa
* Sua placa Arduino, configurada para uso. toolearn como tooset a placa Arduino, consulte [configurar seu dispositivo][configure-your-device].
* Um hub IoT criado em sua assinatura do Azure. toolearn como toocreate seu hub IoT, consulte [criar o Azure IoT Hub][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Conecte Olá exemplo aplicativo tooyour IoT hub

1. Certifique-se de que você está na pasta do repositório de saudação `iot-hub-c-feather-m0-getting-started`.

   Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:

   ```bash
   cd Lesson4
   code .
   ```

   Saudação de aviso `app.ino` arquivo hello `app` subpasta. Olá `app.ino` é arquivo de origem da chave de saudação que contém Olá código toomonitor mensagens de entrada de hub IoT de saudação. Olá `blinkLED` função pisca Olá LED.

   ![Estrutura do repositório no aplicativo de exemplo hello][repo-structure]

2. Obter a porta serial saudação do dispositivo Olá Olá CLI de descoberta do dispositivo:

   ```bash
   devdisco list --usb
   ```

   Você deve ver uma saída que é a seguir toohello semelhante e encontrar hello usb porta COM para a sua placa Arduino:

   ![Descoberta de dispositivo][device-discovery]

3. Arquivo hello abrir `config.json` na pasta de lição do hello e o valor de entrada hello da saudação encontrada número da porta COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Para a porta de saudação COM, na plataforma Windows, tem um formato de Olá `COM1, COM2, ...`. No macOS ou Ubuntu, começará com `/dev/`.

4. Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Verifique Olá substituições em Olá a seguir `config-arduino.json` arquivo:

   Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] neste computador, todas as configurações de saudação são herdadas, portanto você pode ignorar a tarefa de toohello Olá etapa de implantação e executando o aplicativo de exemplo hello. Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] em um computador diferente, você precisa espaços reservados Olá tooreplace Olá `config-arduino.json` arquivo. Olá `config-arduino.json` arquivo está na subpasta de saudação da sua pasta base.

   ![Conteúdo do arquivo de configuração arduino.json Olá][config-arduino-json]

   * Substituir **[Wi-Fi SSID]** com o seu SSID de Wi-Fi que conectado toohello da Internet.
   * Substitua **[senha Wi-Fi]** pela senha de Wi-Fi. Remova cadeia de caracteres de saudação se o Wi-Fi não exigir uma senha.
   * Substituir **[cadeia de conexão de dispositivo IoT]** com cadeia de conexão do dispositivo Olá obter executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.
   * Substituir **[cadeia de conexão de hub IoT]** com hello cadeia de conexão de hub IoT que você obtém executando Olá `az iot hub show-connection-string --name {my hub name}` comando.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello em seu quadro Arduino executando Olá comandos a seguir:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

comando de gulp Olá implanta quadro do hello exemplo aplicativo tooyour Arduino. Em seguida, ele é executado aplicativo hello em seu quadro Arduino e uma tarefa separada em seu host placa Arduino tooyour de mensagens do computador toosend 20 intermitência de seu hub IoT.

Depois que o aplicativo de exemplo hello é executado, ele inicia a escuta toomessages do seu hub IoT. Enquanto isso, a tarefa de gulp de saudação envia várias mensagens de "intermitência" de seu tooyour de hub IoT Arduino quadro. Para cada mensagem de intermitência Olá placa recebe, o aplicativo de exemplo hello chama Olá `blinkLED` Olá tooblink de função LED.

Você deve ver Olá LED piscar a cada dois segundos como tarefa de gulp Olá envia 20 mensagens da sua tooyour de hub IoT Arduino quadro. Hello última um é uma mensagem "stop" que interrompe a execução do aplicativo hello.

![Exemplo de aplicativo com o comando gulp e mensagens de piscar][sample-application]

## <a name="summary"></a>Resumo
Você enviou com êxito as mensagens de seu Olá de quadro tooblink do IoT hub tooyour Arduino LED. Olá próxima tarefa é opcional: altere Olá ativa e desativa o comportamento de saudação LED.

## <a name="next-steps"></a>Próximas etapas
[Alterar Olá ativa e desativa o comportamento de saudação LED][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md