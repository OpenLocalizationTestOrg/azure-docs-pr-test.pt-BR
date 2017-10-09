---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 3: enviar mensagens | Microsoft Docs"
description: "Implantar e executar um aplicativo de exemplo tooIntel Edison que envia o hub de IoT tooyour mensagens e pisca Olá LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem de IOT arduino enviar dados toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Executar um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem
## <a name="what-you-will-do"></a>O que você fará
Este artigo mostra como toodeploy e execute um aplicativo de exemplo no Intel Edison que envia mensagens tooyour IoT hub. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
Você saiba como Olá toouse gulp ferramenta toodeploy e executará o aplicativo de C do exemplo hello em Edison.

## <a name="what-you-need"></a>O que você precisa
* Antes de começar essa tarefa, você deve concluir com êxito [criar um aplicativo de função do Azure e um armazenamento conta tooprocess e o repositório de IoT hub mensagens][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obter as cadeias de conexão do dispositivo e do Hub IoT
cadeia de caracteres de conexão de dispositivo Olá é usado tooconnect hub de IoT tooyour Edison. Olá a cadeia de caracteres de conexão de hub IoT é usado tooconnect sua identidade de dispositivo de toohello de hub IoT representando Edison no hub IoT de saudação.

* Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá após o comando CLI do Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.

* Obter cadeia de caracteres de conexão do hello IoT hub executando Olá após o comando CLI do Azure:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`é o nome de saudação que você especificou ao criar o hub IoT e registrado Edison.

* Obter cadeia de caracteres de conexão de dispositivo Olá executando Olá comando a seguir:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Use `myinteledison` como valor de saudação do `{device id}` se você não alterar o valor de saudação.

## <a name="configure-hello-device-connection"></a>Configurar conexão do dispositivo Olá
1. Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:

   ```bash
   npm install
   gulp init
   ```

2. Arquivo de configuração de dispositivo aberto Olá `config-edison.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. Verifique Olá substituições em Olá a seguir `config-edison.json` arquivo:

   * Substituir **[nome de host do dispositivo ou endereço IP]** com endereço IP do dispositivo Olá marcado para baixo, quando você configurou seu dispositivo.
   * Substituir **[cadeia de conexão de dispositivo IoT]** com hello `device connection string` obtidas.
   * Substituir **[cadeia de conexão de hub IoT]** com hello `iot hub connection string` obtidas.

   > [!NOTE]
   > Você não precisa do `azure_storage_connection_string` neste artigo. Mantenha como está.

## <a name="deploy-and-run-hello-sample-application"></a>Implantar e executar o aplicativo de exemplo hello
Implantar e executar o aplicativo de exemplo hello Edison executando Olá comando a seguir:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Verifique se o aplicativo de exemplo hello funciona
Você deve ver Olá LED que está conectada tooEdison piscando a cada dois segundos. Sempre Olá LED pisca, o aplicativo de exemplo hello envia um hub de IoT tooyour mensagem e verifica que essa mensagem de saudação enviada com êxito tooyour IoT hub. Além disso, cada mensagem recebida pelo hub IoT de saudação é impressa na janela de console hello. aplicativo de exemplo Hello encerra automaticamente após o envio de mensagens de 20.

![Exemplo de aplicativo com mensagens enviadas e recebidas][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Resumo
Você tiver implantado e execute o novo aplicativo de exemplo de intermitência Olá em Edison hub IoT do toosend mensagens de dispositivo para nuvem tooyour. Agora você monitorar suas mensagens como eles são gravados toohello conta de armazenamento.

## <a name="next-steps"></a>Próximas etapas
[Ler mensagens persistentes no Armazenamento do Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md