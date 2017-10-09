---
title: "Connect Arduino (C) tooAzure IoT – lição 4: modificar o aplicativo | Microsoft Docs"
description: "Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlar led com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Alterar Olá ativa e desativa o comportamento de saudação LED
## <a name="what-you-will-do"></a>O que você fará
Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento. Se você tiver problemas, procure por soluções em Olá [página de solução](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) para seu quadro Adafruit difusão M0 WiFi Arduino.

## <a name="what-you-will-learn"></a>O que você aprenderá
Use adicional Olá de Arduino funções toochange LED do ativa e desativa o comportamento.

## <a name="what-you-need"></a>O que você precisa
Você deve ter concluído com êxito [executar um aplicativo de exemplo na nuvem Arduino placa tooreceive toodevice mensagens][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Adicionar gulpfile.js e toomain.c de funções
1. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:

   ```bash
   cd Lesson4
   code .
   ```
2. Olá abrir `app.ino` arquivo e, em seguida, adicionar funções a seguir após a função blinkLED() de saudação:

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![Arquivo app.ino com funções adicionais][app-ino-file]
3. Adicionar Olá seguintes condições antes de saudação `else if` bloco de saudação `receiveMessageCallback` função:

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   Agora você configurou instruções de toomore de toorespond Olá exemplo aplicativo por meio de mensagens. Olá "em" instrução ativa Olá LED e hello "desativado" instrução desativa Olá LED.
4. Abrir o arquivo de gulpfile.js hello e, em seguida, adicionar uma nova função antes da função hello `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Arquivo Gulpfile.js com funções adicionais][gulp-file-js]
5. Em Olá `sendMessage` funcionar, substitua a linha hello `var message = buildMessage(sentMessageCount);` com nova linha de Olá Olá trecho de código a seguir mostrada:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Salve todas as alterações de saudação.

### <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello em seu quadro Arduino executando Olá comando a seguir:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Você verá Olá LED ativar por dois segundos e, em seguida, desligue por outro dois segundos. última mensagem de "stop" Hello interrompe o aplicativo de exemplo hello seja executado.

![liga e desliga][on-and-off]

Parabéns! Você personalizou mensagens de saudação enviadas tooyour Arduino placa de seu hub IoT com êxito.

### <a name="summary"></a>Resumo
Essa seção demonstra como toocustomize mensagens para que o aplicativo de exemplo hello possa controlar Olá ativa e desativa o comportamento de saudação LED de maneira diferente.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png