---
title: "Connect Raspberry PI (C) tooAzure IoT – lição 3: executar o exemplo | Microsoft Docs"
description: "Implantar e executar um aplicativo de exemplo tooRaspberry Pi 3 que envia o hub de IoT tooyour mensagens e pisca Olá LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi de nuvem do led de piscar, led de piscar da nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Executar um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem
## <a name="what-you-will-do"></a>O que você fará
Este artigo mostra como toodeploy e execute um aplicativo de exemplo no framboesa Pi 3 que envia mensagens tooyour IoT hub. Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Você aprenderá como Olá toouse gulp toodeploy de ferramenta e execute o aplicativo de Node.js do exemplo hello em Pi.

## <a name="what-you-need"></a>O que você precisa
* Antes de começar essa tarefa, você deve concluir com êxito [criar um aplicativo de função do Azure e um armazenamento conta tooprocess e o repositório de IoT hub mensagens](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obter as cadeias de conexão do dispositivo e do Hub IoT
cadeia de caracteres de conexão de dispositivo Olá é usada pelo seu hub IoT de tooyour de tooconnect de Pi. Olá cadeia de caracteres de conexão de hub IoT é um registro de identidade toohello tooconnect usados em dispositivos IoT hub toomanage Olá que são permitidas tooconnect tooyour IoT hub. 

* Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá após o comando CLI do Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.

* Obter cadeia de caracteres de conexão do hello IoT hub executando Olá após o comando CLI do Azure:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`é o nome de saudação que você especificou ao criar o hub IoT e registrado Pi.

* Obter cadeia de caracteres de conexão de dispositivo Olá executando Olá comando a seguir:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Use `myraspberrypi` como valor de saudação do `{device id}` se você não alterar o valor de saudação.

## <a name="configure-hello-device-connection"></a>Configurar conexão do dispositivo Olá
1. Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.

2. Arquivo de configuração de dispositivo aberto Olá `config-raspberrypi.json` no código do Visual Studio executando Olá comando a seguir:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Verifique Olá substituições em Olá a seguir `config-raspberrypi.json` arquivo:
   
   * Substituir **[nome de host do dispositivo ou endereço IP]** com o nome de host ou endereço IP de dispositivo do hello você obteve `device-discovery-cli` ou com valor de saudação herdadas quando você configurou seu dispositivo.
   * Substituir **[cadeia de conexão de dispositivo IoT]** com hello `device connection string` obtidas.
   * Substituir **[cadeia de conexão de hub IoT]** com hello `iot hub connection string` obtidas.

> [!NOTE]
> Você não precisa do `azure_storage_connection_string` neste artigo. Mantenha como está.

Saudação de atualização `config-raspberrypi.json` arquivos de forma que você pode implantar o aplicativo de exemplo hello do seu computador.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello em Pi executando Olá comando a seguir:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Verifique se o aplicativo de exemplo hello funciona
Você deve ver Olá LED que está conectada tooPi piscando a cada dois segundos. Sempre Olá LED pisca, o aplicativo de exemplo hello envia um hub de IoT tooyour mensagem e verifica que essa mensagem de saudação enviada com êxito tooyour IoT hub. Além disso, cada mensagem recebida pelo hub IoT de saudação é impressa na janela de console hello. aplicativo de exemplo Hello encerra automaticamente após o envio de mensagens de 20.

![Exemplo de aplicativo com mensagens enviadas e recebidas](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a>Resumo
Você tiver implantado e executar o novo aplicativo de exemplo de intermitência Olá no hub IoT do Pi toosend mensagens de dispositivo para nuvem tooyour. Agora você monitorar suas mensagens como eles são gravados toohello conta de armazenamento.

## <a name="next-steps"></a>Próximas etapas
[Ler mensagens mantidas no Armazenamento do Azure](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

