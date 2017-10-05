---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 4: piscar o LED| Microsoft Docs"
description: Personalize as mensagens para alterar o comportamento liga e desliga do LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlar led com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4852b1cca4c6186ef4857b903b771f76cc20adb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Alterar o comportamento de ativar e desativar do LED
## <a name="what-you-will-do"></a>O que você fará
Personalize as mensagens para alterar o comportamento liga e desliga do LED. Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
Utilizar funções adicionais para alterar o comportamento de ligar e desligar do LED.

## <a name="what-you-need"></a>O que você precisa
Você deve ter concluído com sucesso [Executar um aplicativo de exemplo no Intel Edison para receber mensagens da nuvem para o dispositivo][receive-cloud-to-device-messages].

## <a name="add-functions-to-mainc-and-gulpfilejs"></a>Adicionar funções ao main.c e ao gulpfile.js
1. Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:

   ```bash
   cd Lesson4
   code .
   ```
2. Abra o arquivo `main.c` e, em seguida, adicione as seguintes funções após a função blinkLED():

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![arquivo main.c com funções adicionais](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Adicione as seguintes condições antes do bloco `else if` da função `receiveMessageCallback`:

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   Agora você configurou o aplicativo de exemplo para responder a mais instruções por meio de mensagens. A instrução "on" ativa o LED e a instrução "off" desativa o LED.
4. Abra o arquivo gulpfile.js e, em seguida, adicione uma nova função antes da função `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![Arquivo Gulpfile.js com funções adicionais][gulpfile]
5. Na função `sendMessage`, substitua a linha `var message = buildMessage(sentMessageCount);` com a nova linha mostrada no trecho a seguir:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Salve todas as alterações.

### <a name="deploy-and-run-the-sample-application"></a>Implantar e executar o aplicativo de exemplo
Implante e execute o aplicativo de exemplo no Edison executando o seguinte comando:

```bash
gulp deploy && gulp run
```

Você deve ver o LED ativar por dois segundos e, em seguida, desativar por outros dois segundos. A última mensagem "stop" interrompe a execução do aplicativo de exemplo.

![liga e desliga][on-and-off]

Parabéns! Você personalizou com sucesso as mensagens que são enviadas do Hub IoT para o Edison.

### <a name="summary"></a>Resumo
Essa seção opcional demonstra como personalizar as mensagens para que o aplicativo de exemplo controle o comportamento liga e desliga do LED de maneira diferente.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
