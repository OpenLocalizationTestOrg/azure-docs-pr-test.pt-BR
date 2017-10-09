---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 4: criar aplicativo de funções | Microsoft Docs"
description: "Salvar mensagens de hub do Intel NUC tooyour IoT, gravá-los tooAzure o armazenamento de tabela e, em seguida, lê-los da nuvem de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenando dados em nuvem hello, dados armazenados na nuvem, o serviço de nuvem iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Criar um aplicativo de funções do Azure e uma conta de armazenamento

As funções do Azure é uma solução para executar facilmente _funções_ (pequenos pedaços de código) na nuvem hello. Um aplicativo de função do Azure hospeda execução Olá das funções no Azure. 

## <a name="what-you-will-do"></a>O que você fará

- Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure. aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure.

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).


## <a name="what-you-will-learn"></a>O que você aprenderá

Nesta lição, você aprenderá:

- Como toouse toodeploy do Gerenciador de recursos do Azure recursos do Azure.
- Como toouse do Azure funcionam aplicativo tooprocess mensagens de IoT Hub e gravá-los tooa tabela no armazenamento de tabela do Azure.

## <a name="what-you-need"></a>O que você precisa

Você deve ter concluído lições anteriores Olá com êxito:

- [Lesson 1: Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Lição 1: Configurar a NUC da Intel como um gateway IoT)
- [Lesson 2: Get your host computer and Azure IoT hub ready](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md) (Lição 2: Prepare seu computador host e hub do IoT do Azure)
- [Lição 3: Receber mensagens de SensorTag e ler mensagens do Hub IoT](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>Abrir um aplicativo de exemplo

Vá tooyour `iot-hub-c-intel-nuc-gateway-getting-started` pasta do repositório, arquivos de configuração de saudação inicializar e projeto de exemplo hello, em seguida, abra no código do Visual Studio executando Olá comando a seguir:

```bash
cd Lesson4
npm install
gulp init
code .
```

![estrutura do repositório](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Olá `arm-template.json` arquivo é hello Azure Resource Manager modelo que contém um aplicativo de função do Azure e uma conta de armazenamento do Azure.
- Olá `arm-template-param.json` arquivo é o arquivo de configuração de saudação usado pelo modelo do Azure Resource Manager hello.
- Olá `ReceiveDeviceMessages` subpasta contém o código de Node. js Olá para Olá função do Azure.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Configurar modelos do Azure Resource Manager e criar recursos no Azure

Saudação de atualização `arm-template-param.json` arquivo no código do Visual Studio.

![arm template json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Substitua `[your IoT Hub name]` pelo `{my hub name}` especificado na Lição 2.

Depois de atualizar Olá `arm-template-param.json` de arquivos, implante Olá recursos tooAzure executando Olá comando a seguir:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Use `iot-gateway` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação na lição 2.

## <a name="summary"></a>Resumo

Você criou seu tooprocess do aplicativo de função do Azure mensagens de hub IoT e o armazenamento do Azure conta toostore essas mensagens. Agora você pode ler as mensagens enviadas pelo hub IoT de tooyour de gateway.

## <a name="next-steps"></a>Próximas etapas
[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md) (Ler as mensagens persistidas no Armazenamento de Tabelas do Azure).
