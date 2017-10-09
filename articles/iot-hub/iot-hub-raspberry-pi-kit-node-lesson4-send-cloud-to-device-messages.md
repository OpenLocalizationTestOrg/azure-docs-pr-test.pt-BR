---
featureFlags: usabilla
title: "Conecte-se framboesa Pi (nó) tooAzure IoT – lição 4: dispositivos de nuvem | Microsoft Docs"
description: "aplicativo de exemplo Hello executa em Pi e monitora mensagens de entrada de seu hub IoT. Uma nova tarefa gulp envia mensagens tooPi do seu Olá de tooblink de hub IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: nuvem toodevice, mensagem de nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>Executar mensagens de nuvem para dispositivo tooreceive do aplicativo de exemplo de hello
Neste artigo, implante um aplicativo de exemplo no Raspberry Pi 3. aplicativo de exemplo Hello monitora mensagens de entrada de seu hub IoT. Você também executar uma tarefa de vez em seu tooPi de mensagens do computador toosend do seu hub IoT. Quando o aplicativo de exemplo hello recebe mensagens de saudação, pisca Olá LED. Se você tiver problemas, buscar soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>O que você fará
* Conecte-se o hub IoT do hello exemplo aplicativo tooyour.
* Implante e execute o aplicativo de exemplo hello.
* Envie mensagens de seu saudação do IoT hub tooPi tooblink LED.

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como mensagens de entrada toomonitor do seu hub IoT
* Como toosend de nuvem para dispositivo mensagens de seu tooPi de hub IoT.

## <a name="what-you-need"></a>O que você precisa
* Raspberry Pi 3, configuração para uso. toolearn como tooset o Pi, consulte [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Um hub IoT criado em sua assinatura do Azure. toolearn como toocreate seu hub IoT, consulte [criar o hub IoT e registrar framboesa Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Conecte Olá exemplo aplicativo tooyour IoT hub
1. Certifique-se de que você está na pasta do repositório de saudação `iot-hub-node-raspberrypi-getting-started`. Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Saudação de aviso `app.js` arquivo hello `app` subpasta. Olá `app.js` é arquivo de origem da chave de saudação que contém Olá código toomonitor mensagens de entrada de hub IoT de saudação. Olá `blinkLED` função pisca Olá LED.
   
   ![Estrutura do repositório no aplicativo de exemplo hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Inicialize o arquivo de configuração de saudação usando Olá comandos a seguir:
   
   ```bash
   npm install
   gulp init
   ```
   
   Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) neste computador, todas as configurações de saudação são herdadas, para que você possa ignorar toohello tarefas de implantação e execução de aplicativo de exemplo hello. Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) em um computador diferente, você precisa espaços reservados Olá tooreplace Olá `config-raspberrypi.json` arquivo. Olá `config-raspberrypi.json` arquivo está na subpasta de saudação da sua pasta base.
   
   ![Conteúdo do arquivo de configuração raspberrypi.json Olá](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Substituir **[nome de host do dispositivo ou endereço IP]** com endereço IP hello Pi ou hello nome de host que você obtém executando Olá `devdisco list --eth` comando.
* Substituir **[cadeia de conexão de dispositivo IoT]** com cadeia de conexão do dispositivo Olá obter executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` comando.
* Substituir **[cadeia de conexão de hub IoT]** com hello cadeia de conexão de hub IoT que você obtém executando Olá `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` comando.

> [!NOTE]
> Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello em Pi executando Olá comando a seguir:

```bash
gulp deploy && gulp run
```

comando Olá implanta Olá tooPi de aplicativo de exemplo. Em seguida, ele é executado aplicativo hello Pi e uma tarefa separada em seu host tooPi de mensagens do computador toosend 20 intermitência de seu hub IoT.

Depois que o aplicativo de exemplo hello é executado, ele inicia a escuta toomessages do seu hub IoT. Enquanto isso, a tarefa de gulp de saudação envia várias mensagens de "intermitência" de seu tooPi de hub IoT. Para cada mensagem de intermitência que recebe de Pi, o aplicativo de exemplo hello chama Olá `blinkLED` Olá tooblink de função LED.

Você deve ver intermitência de LED Olá cada dois segundos como Olá gulp tarefa envia 20 mensagens de seu tooPi de hub IoT. Olá última um é uma mensagem "stop" que informa Olá toostop de aplicativo em execução.

![Exemplo de aplicativo com o comando gulp e mensagens de piscar](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Resumo
Você enviou com êxito as mensagens de seu saudação do IoT hub tooPi tooblink LED. Olá próxima tarefa é opcional: altere Olá ativa e desativa o comportamento de saudação LED.

## <a name="next-steps"></a>Próximas etapas
[Alterar Olá ativa e desativa o comportamento de saudação LED](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

