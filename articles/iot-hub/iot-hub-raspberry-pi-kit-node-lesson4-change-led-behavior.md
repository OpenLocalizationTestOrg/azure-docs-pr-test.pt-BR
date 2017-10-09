---
title: "Conecte-se framboesa Pi (nó) tooAzure IoT – lição 4: modificar o aplicativo | Microsoft Docs"
description: "Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: led de controle com raspberry pi, controle de led de raspberry pi, led de controle de raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Alterar Olá ativa e desativa o comportamento de saudação LED
## <a name="what-you-will-do"></a>O que você fará
Personalize a saudação de toochange de mensagens de saudação LED do ativa e desativa o comportamento. Se você tiver problemas, buscar soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Use adicional Olá de Node. js funções toochange LED do ativa e desativa o comportamento.

## <a name="what-you-need"></a>O que você precisa
Você deve ter concluído com êxito [executar um aplicativo de exemplo em Pi framboesa tooreceive mensagens de nuvem para dispositivo](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).

## <a name="add-nodejs-functions"></a>Adicionar funções do Node.js
1. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:
   
   ```bash
   cd Lesson4
   code .
   ```
2. Olá abrir `app.js` de arquivo e depois adicione Olá funções final Olá a seguir:
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![Arquivo App.js com funções adicionais](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. Adicionar Olá condições antes de saudação padrão a seguir no bloco de caso de opção de saudação do hello `receiveMessageCallback` função:
   
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
   
   ![Arquivo Gulpfile.js com funções adicionais](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. Em Olá `sendMessage` funcionar, substitua a linha hello `var message = buildMessage(sentMessageCount);` com nova linha de Olá Olá trecho de código a seguir mostrada:
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Salve todas as alterações de saudação.

### <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello em Pi executando Olá comando a seguir:

```bash
gulp deploy && gulp run
```

Você verá Olá LED ativar por dois segundos e, em seguida, desligue por outro dois segundos. última mensagem de "stop" Hello interrompe o aplicativo de exemplo hello seja executado.

![Exemplo de aplicativo com mensagens de logon e logoff](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

Parabéns! Você personalizou mensagens de saudação enviadas tooPi de seu hub IoT com êxito.

### <a name="summary"></a>Resumo
Essa seção demonstra como toocustomize mensagens para que o aplicativo de exemplo hello possa controlar Olá ativa e desativa o comportamento de saudação LED de maneira diferente.

