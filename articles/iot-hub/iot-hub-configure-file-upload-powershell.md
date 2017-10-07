---
title: carregamento de arquivo aaaUse hello Azure PowerShell tooconfigure | Microsoft Docs
description: "Como toouse hello Azure PowerShell cmdlets tooconfigure seu arquivo de tooenable de hub IoT carregamentos de dispositivos conectados. Inclui informações sobre como configurar a conta de armazenamento do Azure de destino hello."
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
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Configurar uploads de arquivo do Hub IoT usando o PowerShell

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Olá toouse [funcionalidade de carregamento de arquivo no IoT Hub][lnk-upload], primeiro você deve associar uma conta de armazenamento do Azure com o hub IoT. Você pode usar uma conta de armazenamento existente ou criar uma nova.

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [Cmdlets do Azure PowerShell][lnk-powershell-install].
* Um Hub IoT do Azure. Se você não tiver um hub IoT, você pode usar o hello [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate um ou use Olá portal muito[criar um hub IoT] [ lnk-portal-hub].
* Uma conta de armazenamento do Azure. Se você não tiver uma conta de armazenamento do Azure, você pode usar o hello [cmdlets do PowerShell do armazenamento do Azure] [ lnk-powershell-storage] toocreate um ou use Olá portal muito[criar uma conta de armazenamento] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Entre e configure sua conta do Azure

Entre no tooyour conta do Azure e selecione sua assinatura.

1. No prompt do PowerShell hello, executar Olá **AzureRmAccount Login** cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais. Use Olá toolist Olá assinaturas do Azure para você toouse de comando a seguir:

    ```powershell
    Get-AzureRMSubscription
    ```

    Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toomanage seu hub IoT a seguir. Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>Recupere os detalhes da sua conta de armazenamento

Olá etapas a seguir pressupõem que você criou sua conta de armazenamento usando Olá **Gerenciador de recursos de** modelo de implantação e não hello **clássico** modelo de implantação.

arquivo tooconfigure carregamentos de seus dispositivos, você precisa de cadeia de caracteres de conexão Olá para uma conta de armazenamento do Azure. conta de armazenamento Olá deve estar no hello mesma assinatura que o hub IoT. Você também precisa de nome de saudação de um contêiner de blob na conta de armazenamento hello. Use suas chaves de conta de armazenamento de Olá tooretrieve de comando a seguir:

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Anote Olá **key1** valor de chave de conta de armazenamento. Necessário em Olá etapas a seguir.

Você pode usar um contêiner de blob existente para os uploads de arquivo ou criar um novo:

* toolist Olá existente contêineres de blob em sua conta de armazenamento, use Olá comandos a seguir:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate um contêiner de blob em sua conta de armazenamento, use Olá comandos a seguir:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>Configurar seu Hub IoT

Agora você pode configurar seu tooenable de hub IoT [funcionalidade de carregamento de arquivo] [ lnk-upload] usando os detalhes da conta de armazenamento.

configuração de saudação requer Olá valores a seguir:

**Contêiner de armazenamento**: um contêiner de blob em uma conta de armazenamento do Azure no seu atual tooassociate de assinatura do Azure com o hub IoT. Você recuperar informações de conta de armazenamento necessários Olá em Olá anterior da seção. IoT Hub gera automaticamente os URIs de SAS com contêiner de blob de toothis de permissões de gravação para dispositivos toouse ao carregar arquivos.

**Receber notificações para os arquivos carregados**: habilitar ou desabilitar notificações de upload de arquivo.

**SAS TTL**: essa configuração é hello tempo de vida da saudação SAS URIs retornados toohello dispositivo pelo IoT Hub. Definir hora tooone por padrão.

**Notificação de tempo de vida padrão de configurações de arquivo**: Olá tempo de vida de uma notificação de carregamento de arquivo antes de expirar. Definir dia tooone por padrão.

**Contagem máxima de entrega de notificação de arquivo**: Olá número de vezes Olá toodeliver tentativas de IoT Hub uma notificação de carregamento de arquivo. Definir too10 por padrão.

Use Olá configurações de carregamento do arquivo de saudação do PowerShell cmdlet tooconfigure a seguir em seu hub IoT:

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
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

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md