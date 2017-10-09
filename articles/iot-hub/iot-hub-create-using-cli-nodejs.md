---
title: aaaCreate um hub IoT usando a CLI do Azure (azure.js) | Microsoft Docs
description: "Como toocreate um hub IoT do Azure usando Olá CLI do Azure de plataforma cruzada (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Criar um hub IoT usando Olá CLI do Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introdução

Você pode usar a CLI do Azure (azure.js) toocreate e gerenciar programaticamente os hubs de IoT do Azure. Este artigo mostra como toouse Olá CLI do Azure (azure.js) toocreate um hub IoT.

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

* CLI do Azure (azure.js) – hello CLI para hello clássico e modelos de implantação de gerenciamento de recurso conforme descrito neste artigo.
* [2.0 do CLI do Azure (az.py)](iot-hub-create-using-cli.md) -Olá próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. Se não tiver uma, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [CLI do Azure 0.10.4][lnk-CLI-install] ou posterior. Se você já tiver Olá CLI do Azure instalado, você pode validar a versão atual Olá no prompt de comando Olá com hello comando a seguir:

```azurecli
azure --version
```

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Olá CLI do Azure deve estar no modo do Azure Resource Manager:
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Definir sua conta e assinatura do Azure

1. No prompt de comando hello, logon digitando Olá comando a seguir:

   ```azurecli
    azure login
   ```

   Saudação de uso sugerido navegador da web e tooauthenticate de código.
1. Se você tiver várias assinaturas do Azure, conectar-se tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais. Você pode exibir hello assinaturas do Azure e identificar qual é o padrão de saudação, usando o comando hello:

   ```azurecli
    azure account list
   ```

   uso de comandos de contexto de assinatura de saudação tooset sob a qual você deseja toorun restante Olá Olá:

   ```azurecli
    azure account set <subscription name>
   ```

1. Caso não tenha um grupo de recursos, você poderá criar um chamado **exampleResourceGroup**:

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> artigo Olá [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos] [ lnk-CLI-arm] fornece mais informações sobre como toouse Olá CLI do Azure toomanage Azure recursos.

## <a name="create-an-iot-hub"></a>Crie um Hub IoT

Parâmetros requeridos:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resource-group**. nome do grupo de recursos de saudação. formato de saudação é sublinhado alfanumérico, não diferencia maiusculas de minúsculas e hífen, comprimento de 1 a 64.
* **name**. nome de saudação do hello IoT hub toobe criado. formato de saudação é sublinhado alfanumérico, não diferencia maiusculas de minúsculas e hífen, comprimento de 3 a 50.
* **location**. hub Olá local (região/datacenter do azure) tooprovision Olá IoT.
* **sku-name**. nome de saudação do sku hello, um dos: [F1, S1, S2, S3]. Para lista de completo mais recente Olá, consulte toohello página de preços para o IoT Hub.
* **units**. número de saudação de unidades provisionadas. Intervalo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10]. Unidades de IoT Hub são baseadas no número de contagem e hello sua mensagem total de dispositivos que você deseja tooconnect.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee todos os parâmetros disponíveis para a criação de hello, você pode usar o comando de ajuda de saudação no prompt de comando:

```azurecli
azure iothub create -h
```

Exemplo rápido: toocreate chamado de um IoT Hub **exampleIoTHubName** no grupo de recursos de saudação **exampleResourceGroup**, execute hello seguinte comando:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> Este comando da CLI do Azure cria um Hub IoT Standard S1 pelo qual você será cobrado. Você pode excluir o hub IoT de saudação **exampleIoTHubName** usando o seguinte comando:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigo a seguir:

* [SDKs do IoT][lnk-sdks]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Usando Olá toomanage portal do Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
