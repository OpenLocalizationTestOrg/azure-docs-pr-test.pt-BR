---
title: "Connect Arduino (C) tooAzure IoT – lição 3: executar o exemplo | Microsoft Docs"
description: "Implantar e executar um aplicativo de exemplo tooAdafruit difusão M0 Wi-Fi que envia o hub de IoT tooyour mensagens e pisca Olá LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem de IOT arduino enviar dados toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Executar um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem
## <a name="what-you-will-do"></a>O que você fará
Este artigo mostra como toodeploy e execute um aplicativo de exemplo no seu Arduino de Wi-Fi Adafruit difusão M0 placa envia mensagens tooyour IoT hub.

Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
Você aprenderá como Olá toouse gulp toodeploy de ferramenta e execute o aplicativo de Arduino exemplo hello em seu quadro Arduino.

## <a name="what-you-need"></a>O que você precisa
* Antes de começar essa tarefa, você deve concluir com êxito [criar um aplicativo de função do Azure e um armazenamento conta tooprocess e o repositório de IoT hub mensagens][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obter as cadeias de conexão do dispositivo e do Hub IoT
Olá a cadeia de caracteres de conexão de dispositivo é usado tooconnect seu hub de IoT tooyour Arduino quadro. cadeia de caracteres de conexão do Hello IoT hub é usado tooconnect sua identidade de dispositivo de toohello de hub IoT que representa o Arduino placa no hub IoT de saudação.

* Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá após o comando CLI do Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.

* Obter cadeia de caracteres de conexão do hello IoT hub executando Olá após o comando CLI do Azure:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`é o nome de saudação que você especificou ao criar o hub IoT e registrado seu quadro Arduino.

* Obter cadeia de caracteres de conexão de dispositivo Olá executando Olá comando a seguir:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Use `mym0wifi` como valor de saudação do `{device id}` se você não alterar o valor de saudação.
## <a name="configure-hello-device-connection"></a>Configurar conexão do dispositivo Olá
tooconfigure Olá conexão do dispositivo, siga estas etapas:

1. Obter a porta serial saudação do dispositivo Olá Olá CLI de descoberta do dispositivo:

   ```bash
   devdisco list --usb
   ```

   Você deve ver uma saída que é a seguir toohello semelhante e encontrar hello usb porta COM para a sua placa Arduino:

   ![Descoberta de dispositivo][device-discovery]

2. Arquivo hello abrir `config.json` em Olá pasta lição e adicionar valor Olá Olá encontrado número da porta COM:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Para a porta de saudação COM, na plataforma Windows, tem um formato de Olá `COM1, COM2, ...`. No macOS ou Ubuntu, começa com `/dev/`.

3. Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Arquivo de configuração de dispositivo aberto Olá `config-arduino.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. Verifique Olá substituições em Olá a seguir `config-arduino.json` arquivo:

   * Substituir **[Wi-Fi SSID]** com o seu SSID de Wi-Fi que conectado toohello da Internet.
   * Substitua **[senha Wi-Fi]** pela senha de Wi-Fi. Remova cadeia de caracteres de saudação se o Wi-Fi não exigir uma senha.
   * Substituir **[cadeia de conexão de dispositivo IoT]** com hello `device connection string` obtidas.
   * Substituir **[cadeia de conexão de hub IoT]** com hello `iot hub connection string` obtidas.

   > [!NOTE]
   > Você não precisa do `azure_storage_connection_string` neste artigo. Mantenha como está.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello em seu quadro Arduino executando Olá comando a seguir:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Olá padrão gulp tarefa é executada `install-tools` e `run` em sequência de tarefas. Quando você [implantado Olá intermitência aplicativo][deployed-the-blink-app], você executou estas tarefas separadamente.

## <a name="verify-that-hello-sample-application-works"></a>Verifique se o aplicativo de exemplo hello funciona
Você deve ver o LED integrado de saudação GPIO #0 piscando cada dois segundos. Sempre Olá LED pisca, o aplicativo de exemplo hello envia um hub de IoT tooyour mensagem e verifica que essa mensagem de saudação enviada com êxito tooyour IoT hub. Além disso, cada mensagem recebida pelo hub IoT de saudação é impressa na janela de console hello. aplicativo de exemplo Hello encerra automaticamente após o envio de mensagens de 20.

![Exemplo de aplicativo com mensagens enviadas e recebidas][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Resumo
Você tiver implantado e execute o novo aplicativo de exemplo de intermitência Olá em seu hub IoT Arduino placa toosend mensagens de dispositivo para nuvem tooyour. Agora você monitorar suas mensagens como eles são gravados toohello conta de armazenamento.

## <a name="next-steps"></a>Próximas etapas
[Ler mensagens persistentes no Armazenamento do Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md