---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 4: piscar Olá LED | Microsoft Docs"
description: "Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: controlar led com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Alterar Olá ativa e desativa o comportamento de saudação LED
## <a name="what-you-will-do"></a>O que você fará
Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
Use Olá toochange de funções adicionais LED do ativa e desativa o comportamento.

## <a name="what-you-need"></a>O que você precisa
Você deve ter concluído com êxito [executar um aplicativo de exemplo na nuvem do Intel Edison tooreceive mensagens toodevice][receive-cloud-to-device-messages].

## <a name="add-functions-tooappjs-and-gulpfilejs"></a>Adicionar gulpfile.js e tooapp.js de funções
1. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:

   ```bash
   cd Lesson4
   code .
   ```
2. Olá abrir `app.js` arquivo e, em seguida, adicionar funções a seguir após a função blinkLED() de saudação:

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![arquivo app.js com funções adicionais](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. Adicionar hello condições a seguir antes de saudação 'blink' caso no bloco de caso de opção de saudação do hello `receiveMessageCallback` função:

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
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
   }
   ```

   ![Arquivo Gulpfile.js com funções adicionais][gulpfile]
5. Em Olá `sendMessage` funcionar, substitua a linha hello `var message = buildMessage(sentMessageCount);` com nova linha de Olá Olá trecho de código a seguir mostrada:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Salve todas as alterações de saudação.

### <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello Edison executando Olá comando a seguir:

```bash
gulp deploy && gulp run
```

Você verá Olá LED ativar por dois segundos e, em seguida, desligue por outro dois segundos. última mensagem de "stop" Hello interrompe o aplicativo de exemplo hello seja executado.

![liga e desliga][on-and-off]

Parabéns! Você personalizou mensagens de saudação enviadas tooEdison de seu hub IoT com êxito.

### <a name="summary"></a>Resumo
Essa seção demonstra como toocustomize mensagens para que o aplicativo de exemplo hello possa controlar Olá ativa e desativa o comportamento de saudação LED de maneira diferente.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
