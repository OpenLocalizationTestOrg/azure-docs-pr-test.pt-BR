---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 3: ler mensagens | Microsoft Docs"
description: "Execute um código de exemplo em suas mensagens de saudação do tooread de computador host do seu hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem hello, coleta de dados de nuvem, o serviço de nuvem iot, iot dados"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a>Ler mensagens de seu Hub IoT

## <a name="what-you-will-do"></a>O que você fará

- Execute código de exemplo no host do seu computador tooread mensagens de seu hub IoT.

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Como Olá toouse gulp mensagens de tooread ferramenta do seu hub IoT.

## <a name="what-you-need"></a>O que você precisa

- exemplo de dispositivo simulado Olá [configurar e executar uma nuvem de dispositivo simulado carregar o aplicativo de exemplo](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Obter as cadeias de conexão do dispositivo e do Hub IoT

cadeia de caracteres de conexão de dispositivo Olá é usada pelo seu hub do dispositivo simulado tooconnect tooyour IoT. Olá cadeia de caracteres de conexão de hub IoT é um registro de identidade toohello tooconnect usados em dispositivos IoT hub toomanage Olá que são permitidas tooconnect tooyour IoT hub.

- Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá comando a seguir:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Use `iot-gateway` como valor de saudação do `{resource group name}` se você não alterá-lo.
- Obter cadeia de caracteres de conexão do hello IoT hub executando Olá comando a seguir:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`é o nome de saudação que você especificou na lição 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Configurar conexão do dispositivo Olá para o código de exemplo hello

Atualizar IoT hub e dispositivo configurações de conexão em `config-azure.json` executando Olá etapas a seguir:

1. Abra `config-azure.json` no código do Visual Studio executando Olá comando na janela do console a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Verifique Olá substituições em Olá a seguir `config-azure.json` arquivo:

   ![instantâneo de configuração do Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Substituir `[IoT hub connection string]` com hello cadeia de caracteres de conexão de hub IoT.

## <a name="read-messages-from-your-iot-hub"></a>Ler mensagens de seu Hub IoT

Executar aplicativo de exemplo do dispositivo Olá simulado e ler mensagens de IoT Hub por Olá comando a seguir:

```bash
gulp run --iot-hub
```

comando Olá executa o aplicativo hello que envia hub de IoT tooyour mensagens a cada 2 segundos. Ela também gera uma mensagem de saudação do tooreceive de processo filho.

mensagens de saudação que estão sendo enviadas e recebidos são todos Olá exibidos imediatamente na mesma janela do console Olá computador host. aplicativo Hello será encerrado em 40 segundos.

![O aplicativo de exemplo simulado com mensagens enviadas e recebidas](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a>Resumo

Executar tooyour IoT hub de saudação exemplo aplicativo toosend dados com êxito com o dispositivo simulado. Você leu também mensagens de saudação que enviaram tooyour IoT hub.

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


