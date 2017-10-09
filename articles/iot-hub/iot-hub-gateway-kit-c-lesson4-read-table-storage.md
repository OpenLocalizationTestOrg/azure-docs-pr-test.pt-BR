---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 4: armazenamento de tabelas | Microsoft Docs"
description: "Salvar mensagens de hub do Intel NUC tooyour IoT, gravá-los tooAzure o armazenamento de tabela e, em seguida, lê-los da nuvem de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "recuperar dados da nuvem, serviço de nuvem de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Ler mensagens mantidas no Armazenamento de Tabelas do Azure

## <a name="what-you-will-do"></a>O que você fará

- Execute o aplicativo de exemplo hello gateway no gateway que envia o hub de IoT tooyour mensagens.
- Em seguida, execute um código de exemplo em suas mensagens de saudação do host computador tooread em seu armazenamento de tabela do Azure. 

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Como Olá toouse gulp ferramenta toorun Olá exemplo tooread mensagens de código em seu armazenamento de tabela do Azure.

## <a name="what-you-need"></a>O que você precisa

Você tem êxito Olá seguintes tarefas:

- [Criado Olá aplicativo de função do Azure e a conta de armazenamento do Azure Olá](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).
- [Execute o aplicativo de exemplo hello gateway](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).
- [Ler mensagens do Hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Obtenha cadeias de conexão do armazenamento do Azure

No início desta lição, você criou com êxito uma conta de armazenamento do Azure. cadeia de conexão tooget Olá Olá do Azure da conta de armazenamento, execute Olá comandos a seguir:

* Liste todas suas contas de armazenamento.

```bash
az storage account list -g iot-gateway --query [].name
```

* Obtenha a cadeia de conexão do armazenamento do Azure.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Usar gateway iot como valor de saudação do `{resource group name}` se você não alterar o valor de saudação na lição 2.

## <a name="configure-hello-device-connection"></a>Configurar conexão do dispositivo Olá

Saudação de atualização `config-azure.json` arquivos de forma que o código de exemplo hello que é executado no computador de host Olá pode ler a mensagem em seu armazenamento de tabela do Azure. tooconfigure Olá conexão do dispositivo, siga estas etapas:

1. Arquivo de configuração de dispositivo aberto Olá `config-azure.json` executando Olá comandos a seguir:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuração](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Substituir `[Azure storage connection string]` com hello cadeia de caracteres de conexão de armazenamento do Azure que você obteve.

   `[IoT hub connection string]` já deve ter sido substituído na seção [Ler mensagens do Hub IoT do Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md), na Lição 3.

## <a name="read-messages-in-your-azure-table-storage"></a>Ler mensagens no Armazenamento de Tabelas do Azure

Execute o aplicativo de exemplo hello gateway e ler mensagens de armazenamento de tabela do Azure por Olá comando a seguir:

```bash
gulp run --table-storage
```

O hub IoT dispara a mensagem de toosave do aplicativo de função do Azure em seu armazenamento de tabela do Azure quando a nova mensagem chega.
Olá `gulp run` comando executa o aplicativo de exemplo do gateway que envia o hub de IoT tooyour mensagens. Com `table-storage` parâmetro, ela também gera uma saudação de tooreceive do processo filho salva a mensagem em seu armazenamento de tabela do Azure.

mensagens de saudação que estão sendo enviadas e recebidos são todos Olá exibidos imediatamente na mesma janela do console Olá computador host. instância de aplicativo de exemplo Hello será encerrado automaticamente em 40 segundos.

   ![leitura de gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>Resumo

Executar mensagens de saudação tooread do código de exemplo hello em seu armazenamento de tabela do Azure salvo pelo seu aplicativo de função do Azure.
