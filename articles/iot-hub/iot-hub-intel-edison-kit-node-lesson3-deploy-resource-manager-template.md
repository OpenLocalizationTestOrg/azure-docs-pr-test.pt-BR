---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 3: criar a função de aplicativo | Microsoft Docs"
description: "aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenando dados em nuvem hello, dados armazenados na nuvem, o serviço de nuvem iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8ea0a4cdf978158d70e47eaed57e3de378b638d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure
[As funções do Azure](../../articles/azure-functions/functions-overview.md) é uma solução para executar facilmente *funções* (pequenos pedaços de código) na nuvem hello. Um aplicativo de função do Azure hospeda execução Olá das funções no Azure.

## <a name="what-will-you-do"></a>O que você fará
Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure. aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure. Olá conta de armazenamento é usada para ler Olá persistentes cópias das mensagens da tabela do Azure. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-will-you-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:
* Como toouse [do Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.
* Como toouse do Azure funcionam aplicativo tooprocess mensagens de hub IoT e gravá-los tooa tabela no armazenamento de tabela do Azure.

## <a name="what-do-you-need"></a>Do que você precisa
Você deve ter concluído com sucesso:
- [Introdução ao Intel Edison][get-started-with-your-intel-edison]
- [Criar seu Hub IoT do Azure][create-your-azure-iot-hub]

## <a name="open-hello-sample-app"></a>Aplicativo de exemplo hello aberto
Abra o projeto de exemplo hello no código do Visual Studio executando Olá comandos a seguir:

```bash
cd Lesson3
code .
```

![Estrutura do repositório][repo-structure]

* arquivo Olá Olá `app` subpasta é o arquivo de origem da chave de saudação. Esse arquivo de origem contém Olá código toosend uma mensagem 20 vezes tooyour IoT hub e intermitência Olá LED para cada mensagem que ele envia.
* Olá `arm-template.json` arquivo é hello Azure Resource Manager modelo que contém um aplicativo de função do Azure e uma conta de armazenamento do Azure.
* Olá `arm-template-param.json` arquivo é o arquivo de configuração de saudação usado pelo modelo do Azure Resource Manager hello.
* Olá `ReceiveDeviceMessages` subpasta contém o código de Node. js Olá para Olá função do Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurar modelos do Azure Resource Manager e criar recursos no Azure
Saudação de atualização `arm-template-param.json` arquivo no código do Visual Studio.

![Parâmetros do modelo do Azure Resource Manager][arm-template-parameters]

* Substitua **[o nome de seu Hub IoT]** por **{nome do meu hub}** que foi especificado quando você [criou o Hub IoT e registrou o Intel Edison][created-your-iot-hub-and-registered-intel-edison].
* Substitua **[cadeia de caracteres de prefixo para novos recursos]** pelo prefixo que quiser. prefixo de saudação garante que esse nome de recurso de saudação é globalmente exclusivo tooavoid conflito. Não use um traço ou o número inicial no prefixo de saudação.

Depois de atualizar Olá `arm-template-param.json` de arquivos, implante Olá recursos tooAzure executando Olá comando a seguir:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Leva aproximadamente cinco minutos toocreate esses recursos. Durante a criação do recurso hello está em andamento, você pode mover toohello próximo artigo.

## <a name="summary"></a>Resumo
Você criou seu tooprocess do aplicativo de função do Azure mensagens de hub IoT e o armazenamento do Azure conta toostore essas mensagens. Agora você pode implantar e executar mensagens de saudação do exemplo toosend dispositivo para nuvem em Edison.

## <a name="next-steps"></a>Próximas etapas
[Execute um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem no Intel Edison][send-device-to-cloud-messages].
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md