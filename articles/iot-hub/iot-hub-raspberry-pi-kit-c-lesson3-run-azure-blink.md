---
title: "Conectar o Raspberry Pi (C) ao IoT do Azure - Lição 3: executar exemplo | Microsoft Docs"
description: Implante e execute um aplicativo de exemplo para o Raspberry Pi 3 que envie mensagens ao seu Hub IoT e pisque o LED.
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
ms.openlocfilehash: e583ba455a94f9afcc7b31e49425b518d7968919
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Executar um aplicativo de exemplo para enviar mensagens do dispositivo para a nuvem
## <a name="what-you-will-do"></a>O que você fará
Esse artigo mostrará como implantar e executar um aplicativo de exemplo para seu Raspberry Pi 3 que envie mensagens ao Hub IoT. Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá
Você aprenderá como usar a ferramenta gulp para implantar e executar o aplicativo de exemplo Node.js no Pi.

## <a name="what-you-need"></a>O que você precisa
* Antes de iniciar essa tarefa, você deve ter concluído com sucesso [Criar um aplicativo de funções do Azure e uma conta de armazenamento para processar e armazenar mensagens do Hub IoT](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obter as cadeias de conexão do dispositivo e do Hub IoT
A cadeia de conexão do dispositivo é usada pelo seu Pi para conectar ao seu Hub IoT. A cadeia de conexão do Hub IoT é usada para se conectar ao Registro de identidade em seu Hub IoT para gerenciar os dispositivos que têm permissão para se conectar ao seu Hub IoT. 

* Liste todos os Hubs IoT no seu grupo de recursos executando o seguinte comando da CLI do Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Use `iot-sample` como o valor de `{resource group name}` se não tiver alterado o valor.

* Obtenha a cadeia de conexão do hub IoT executando o seguinte comando da CLI do Azure:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}` é o nome que você especificou quando criou o Hub IoT e registrou o Pi.

* Obtenha a cadeia de conexão do dispositivo executando o seguinte comando:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Use `myraspberrypi` como o valor de `{device id}` se não tiver alterado o valor.

## <a name="configure-the-device-connection"></a>Configurar a conexão do dispositivo
1. Inicialize o arquivo de configuração executando os seguintes comandos:
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.

2. Abra o arquivo de configuração `config-raspberrypi.json` do dispositivo no Visual Studio Code executando o seguinte comando:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Faça as seguintes substituições no arquivo `config-raspberrypi.json`:
   
   * Substitua **[nome do host ou endereço IP do dispositivo]** pelo endereço IP ou o nome de host do dispositivo que você obteve de `device-discovery-cli` ou pelo valor herdado quando você configurou o seu dispositivo.
   * Substitua **[cadeia de conexão do dispositivo IoT]** pelo `device connection string` que você obteve.
   * Substitua **[cadeia de conexão do hub IoT]** pelo `iot hub connection string` que você obteve.

> [!NOTE]
> Você não precisa do `azure_storage_connection_string` neste artigo. Mantenha como está.

Atualize o arquivo `config-raspberrypi.json` para que você possa implantar o aplicativo de exemplo de seu computador.

## <a name="deploy-and-run-the-sample-application"></a>Implantar e executar o aplicativo de exemplo
Implante e execute o aplicativo de exemplo no Pi executando o seguinte comando:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Verificar se o aplicativo de exemplo funciona
Você deve ver o LED que está conectado ao Pi piscar a cada dois segundos. Sempre que o LED pisca, o aplicativo de exemplo envia uma mensagem ao hub IoT e verifica se a mensagem foi enviada com êxito para o hub IoT. Além disso, cada mensagem recebida pelo Hub IoT é impressa na janela do console. O aplicativo de exemplo é encerrado automaticamente após o envio de 20 mensagens.

![Exemplo de aplicativo com mensagens enviadas e recebidas](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a>Resumo
Você implantou e executou o novo aplicativo de exemplo de piscar no Pi para enviar mensagens do dispositivo para a nuvem para o Hub IoT. Agora, você monitorara suas mensagens conforme elas são gravadas na conta de armazenamento.

## <a name="next-steps"></a>Próximas etapas
[Ler mensagens mantidas no Armazenamento do Azure](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

