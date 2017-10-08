---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 4: receber mensagens | Microsoft Docs"
description: "Um aplicativo de exemplo é executado no Edison e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens tooEdison do seu Olá de tooblink de hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: controlar led pela web com arduino, controlar led via web com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Executar um tooreceive do aplicativo de exemplo mensagens de nuvem para dispositivo
Neste artigo, você implanta um aplicativo de exemplo no Intel Edison. aplicativo de exemplo Hello monitora mensagens de entrada de seu hub IoT. Você também executar uma tarefa de vez em seu tooEdison de mensagens do computador toosend do seu hub IoT. Quando o aplicativo de exemplo hello recebe mensagens de saudação, pisca Olá LED. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-do"></a>O que você fará
* Conecte-se o hub IoT do hello exemplo aplicativo tooyour.
* Implante e execute o aplicativo de exemplo hello.
* Envie mensagens de seu saudação do IoT hub tooEdison tooblink LED.

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como toomonitor de mensagens de entrada do seu hub IoT.
* Como toosend de nuvem para dispositivo mensagens de seu tooEdison de hub IoT.

## <a name="what-you-need"></a>O que você precisa
* Intel Edison, configurado para uso. toolearn como tooset backup Edison, consulte [configurar seu dispositivo][configure-your-device].
* Um hub IoT criado em sua assinatura do Azure. toolearn como toocreate seu hub IoT, consulte [criar o Azure IoT Hub][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Conecte Olá exemplo aplicativo tooyour IoT hub
1. Certifique-se de que você está na pasta do repositório de saudação `iot-hub-node-edison-getting-started`. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:

   ```bash
   cd Lesson4
   code .
   ```

   arquivo Olá Olá `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toomonitor mensagens de entrada de hub IoT de saudação. Olá `blinkLED` função pisca Olá LED.

   ![Estrutura do repositório no aplicativo de exemplo hello][repo-structure]
2. Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   npm install
   gulp init
   ```

   Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] neste computador, todas as configurações de saudação são herdadas, portanto você pode ignorar a tarefa de toohello Olá etapa de implantação e executando o aplicativo de exemplo hello. Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] em um computador diferente, você precisa espaços reservados Olá tooreplace Olá `config-edison.json` arquivo. Olá `config-edison.json` arquivo está na subpasta de saudação da sua pasta base.

   ![Conteúdo do arquivo de configuração edison.json Olá](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Substituir **[nome de host do dispositivo ou endereço IP]** com endereço IP do dispositivo Olá marcado para baixo, quando você configurou seu dispositivo.
   * Substituir **[cadeia de conexão de dispositivo IoT]** com cadeia de conexão do dispositivo Olá obter executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.
   * Substituir **[cadeia de conexão de hub IoT]** com hello cadeia de conexão de hub IoT que você obtém executando Olá `az iot hub show-connection-string --name {my hub name}` comando.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello Edison executando Olá comandos a seguir:

```bash
gulp deploy && gulp run
```

comando de gulp Olá implanta Olá tooEdison de aplicativo de exemplo. Em seguida, ele é executado aplicativo hello Edison e uma tarefa separada em seu host tooEdison de mensagens do computador toosend 20 intermitência de seu hub IoT.

Depois que o aplicativo de exemplo hello é executado, ele inicia a escuta toomessages do seu hub IoT. Enquanto isso, a tarefa de gulp de saudação envia várias mensagens de "intermitência" de seu tooEdison de hub IoT. Para cada mensagem de intermitência Edison recebe, o aplicativo de exemplo hello chama Olá `blinkLED` Olá tooblink de função LED.

Você deve ver intermitência de LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens de seu tooEdison de hub IoT. Hello última um é uma mensagem "stop" que interrompe a execução do aplicativo hello.

![Exemplo de aplicativo com o comando gulp e mensagens de piscar][gulp-command-and-blink-messages]

## <a name="summary"></a>Resumo
Você enviou com êxito as mensagens de seu saudação do IoT hub tooEdison tooblink LED. Olá próxima tarefa é opcional: altere Olá ativa e desativa o comportamento de saudação LED.

## <a name="next-steps"></a>Próximas etapas
[Alterar Olá ativa e desativa o comportamento de saudação LED][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md