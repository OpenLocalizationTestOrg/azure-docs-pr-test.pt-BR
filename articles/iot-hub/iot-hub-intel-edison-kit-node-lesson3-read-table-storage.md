---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 3: monitorar mensagens | Microsoft Docs"
description: "Monitorar mensagens de saudação do dispositivo para nuvem, como eles são gravados tooyour armazenamento de tabela do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem hello, coleta de dados de nuvem, o serviço de nuvem iot, iot dados"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f6371482123bc9aa12db55b38d3e8863645f981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Ler mensagens mantidas no Armazenamento do Azure
## <a name="what-you-will-do"></a>O que você fará
Monitor Olá dispositivo para nuvem as mensagens são enviadas do hub do Intel Edison tooyour IoT como mensagens de saudação são gravadas tooyour armazenamento de tabela do Azure. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá como mensagens de tooread toouse saudação gulp tarefa Ler mensagem persistente em seu armazenamento de tabela do Azure.

## <a name="what-you-need"></a>O que você precisa
Antes de iniciar esse processo, você deve foi concluído com êxito [executar o aplicativo de exemplo hello intermitência do Azure em Edison Intel][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Ler novas mensagens de sua conta de armazenamento
Artigo anterior de saudação, você executou um aplicativo de exemplo em Edison. Olá exemplo aplicativo enviado mensagens tooyour Azure IoT hub. mensagens de saudação enviadas tooyour IoT hub são armazenadas em seu armazenamento de tabela do Azure por meio do aplicativo de função do Azure hello. Você precisa de armazenamento do Azure conexão cadeia de caracteres tooread mensagens de saudação do seu armazenamento de tabela do Azure.

mensagens de tooread armazenadas em seu armazenamento de tabela do Azure, siga estas etapas:

1. Obter cadeia de caracteres de conexão Olá executando Olá comandos a seguir:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Olá primeiro comando recupera Olá `storage name` que é usado em Olá segundo comando tooget Olá conexão cadeia de caracteres. Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.
2. Arquivo de configuração de saudação abrir `config-edison.json` no código do Visual Studio executando Olá comando a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Substituir `[Azure storage connection string]` com a cadeia de caracteres de conexão de saudação você obteve na etapa 1.
4. Salvar Olá `config-edison.json` arquivo.
5. Enviar mensagens novamente e lê-los do seu armazenamento de tabela do Azure executando Olá comando a seguir:

   ```bash
   gulp run --read-storage
   ```

   Olá lógica para leitura do armazenamento de tabela do Azure está em Olá `azure-table.js` arquivo.

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a>Resumo
Já conectado IoT hub tooyour Edison nuvem Olá e usado mensagens de dispositivo para nuvem toosend do aplicativo de exemplo de intermitência Olá com êxito. Você também usou hello Azure função aplicativo toostore entrada IoT hub mensagens tooyour Azure armazenamento de tabela. Agora você pode enviar mensagens de nuvem para dispositivo de sua tooEdison de hub IoT.

## <a name="next-steps"></a>Próximas etapas
[Executar um tooreceive do aplicativo de exemplo mensagens de nuvem para dispositivo][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md