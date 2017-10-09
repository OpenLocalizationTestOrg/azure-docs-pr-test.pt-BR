---
title: tooIoT de carregamento de arquivo aaaConfigure Hub usando a CLI do Azure (az.py) | Microsoft Docs
description: "Como tooconfigure fileuploads tooAzure Hub IoT usando Olá plataforma cruzada do Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Configurar uploads de arquivo do Hub IoT usando a CLI do Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Olá toouse [funcionalidade de carregamento de arquivo no IoT Hub][lnk-upload], primeiro você deve associar uma conta de armazenamento do Azure com o hub IoT. Você pode usar uma conta de armazenamento existente ou criar uma nova.

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [CLI do Azure 2.0][lnk-CLI-install].
* Um Hub IoT do Azure. Se você não tiver um hub IoT, você pode usar o hello `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate um ou use Olá portal muito [criar um hub IoT] [hub de portal lnk].
* Uma conta de armazenamento do Azure. Se você não tiver uma conta de armazenamento do Azure, você pode usar o hello [2.0 do CLI do Azure - gerenciar contas de armazenamento] [ lnk-manage-storage] toocreate um ou use Olá portal muito[criar uma conta de armazenamento] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Entre e configure sua conta do Azure

Entre no tooyour conta do Azure e selecione sua assinatura.

1. No prompt de comando do hello, execute Olá [comando login][lnk-login-command]:

    ```azurecli
    az login
    ```

    Siga Olá instruções tooauthenticate usando código hello e entrar tooyour conta do Azure por meio de um navegador da web.

1. Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall Olá associadas com suas credenciais de contas do Azure. Use os seguintes Olá [toolist comando Olá contas do Azure] [ lnk-az-account-command] disponíveis para você toouse:

    ```azurecli
    az account list
    ```

    Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toocreate seu hub IoT a seguir. Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Recupere os detalhes da sua conta de armazenamento

Olá etapas a seguir pressupõem que você criou sua conta de armazenamento usando Olá **Gerenciador de recursos de** modelo de implantação e não hello **clássico** modelo de implantação.

arquivo tooconfigure carregamentos de seus dispositivos, você precisa de cadeia de caracteres de conexão Olá para uma conta de armazenamento do Azure. conta de armazenamento Olá deve estar no hello mesma assinatura que o hub IoT. Você também precisa de nome de saudação de um contêiner de blob na conta de armazenamento hello. Use suas chaves de conta de armazenamento de Olá tooretrieve de comando a seguir:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Anote Olá **connectionString** valor. Necessário em Olá etapas a seguir.

Você pode usar um contêiner de blob existente para os uploads de arquivo ou criar um novo:

* toolist Olá existente contêineres de blob em sua conta de armazenamento, use Olá comando a seguir:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate um contêiner de blob em sua conta de armazenamento, use Olá comando a seguir:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Upload de arquivos

Agora você pode configurar seu tooenable de hub IoT [funcionalidade de carregamento de arquivo] [ lnk-upload] usando os detalhes da conta de armazenamento.

configuração de saudação requer Olá valores a seguir:

**Contêiner de armazenamento**: um contêiner de blob em uma conta de armazenamento do Azure no seu atual tooassociate de assinatura do Azure com o hub IoT. Você recuperar informações de conta de armazenamento necessários Olá em Olá anterior da seção. IoT Hub gera automaticamente os URIs de SAS com contêiner de blob de toothis de permissões de gravação para dispositivos toouse ao carregar arquivos.

**Receber notificações para os arquivos carregados**: habilitar ou desabilitar notificações de upload de arquivo.

**SAS TTL**: essa configuração é hello tempo de vida da saudação SAS URIs retornados toohello dispositivo pelo IoT Hub. Definir hora tooone por padrão.

**Notificação de tempo de vida padrão de configurações de arquivo**: Olá tempo de vida de uma notificação de carregamento de arquivo antes de expirar. Definir dia tooone por padrão.

**Contagem máxima de entrega de notificação de arquivo**: Olá número de vezes Olá toodeliver tentativas de IoT Hub uma notificação de carregamento de arquivo. Definir too10 por padrão.

Use configurações de carregamento de arquivo tooconfigure Olá do CLI do Azure comandos a seguir em seu hub IoT de saudação:

Em um shell de busca, use:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Em um prompt de comando do Windows, use:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Você pode examinar a configuração de carregamento de arquivo hello em seu hub IoT usando Olá comando a seguir:

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os recursos de carregamento de arquivo hello IoT Hub, consulte [carregar arquivos de um dispositivo][lnk-upload].

Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:

* [Gerenciamento em massa de dispositivos IoT][lnk-bulk]
* [Métricas do Hub IoT][lnk-metrics]
* [Monitoramento de operações][lnk-monitor]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com IoT Edge][lnk-iotedge]
* [Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create