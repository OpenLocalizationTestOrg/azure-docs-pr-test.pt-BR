---
title: aaaCreate um IoT Hub usando a CLI do Azure (az.py) | Microsoft Docs
description: "Como toocreate um hub IoT do Azure usando Olá plataforma cruzada do Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Criar um hub IoT usando Olá 2.0 do CLI do Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introdução

Você pode usar a CLI do Azure 2.0 (az.py) toocreate e gerenciar programaticamente os hubs de IoT do Azure. Este artigo mostra como toouse Olá CLI do Azure 2.0 (az.py) toocreate um hub IoT.

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

* [CLI do Azure (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.
* Azure CLI 2.0 (az.py) - Olá próxima geração CLI para Olá recurso Gerenciamento modelo de implantação conforme descrito neste artigo.

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [CLI do Azure 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Entre e configure sua conta do Azure

Entre no tooyour conta do Azure e selecione sua assinatura.

1. No prompt de comando do hello, execute Olá [comando login][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Siga Olá instruções tooauthenticate usando código hello e entrar tooyour conta do Azure por meio de um navegador da web.

2. Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall Olá associadas com suas credenciais de contas do Azure. Use os seguintes Olá [toolist comando Olá contas do Azure] [ lnk-az-account-command] disponíveis para você toouse:
    
    ```azurecli
    az account list 
    ```

    Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toocreate seu hub IoT a seguir. Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>Crie um Hub IoT

Use Olá CLI do Azure toocreate um grupo de recursos e, em seguida, adicione um hub IoT.

1. Quando cria um Hub IoT, você deve criá-lo em um grupo de recursos. Use um grupo de recursos existente, ou execute seguinte Olá [comando toocreate um grupo de recursos][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > exemplo de anterior Olá cria o grupo de recursos Olá Olá local Oeste dos EUA. Você pode exibir uma lista de locais disponíveis, executando o comando Olá `az account list-locations -o table`.
    >
    >

2. Execute seguinte Olá [toocreate comando um hub IoT] [ lnk-az-iot-command] no seu grupo de recursos, usando um nome exclusivo para o hub IoT:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> comando anterior Olá cria um hub IoT no hello S1 preço para o qual você é cobrado. Para saber mais, confira [Preço do Hub IoT do Azure][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>Remover um Hub IoT

Você pode usar o hello CLI do Azure muito[excluir um recurso individual][lnk-az-resource-command], como um hub IoT ou excluir um grupo de recursos e todos os seus recursos, incluindo qualquer hubs IoT.

toodelete um hub IoT, executar Olá comando a seguir:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete um grupo de recursos e todos os seus recursos, Olá execução seguinte comando:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Usando Olá toomanage portal do Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
