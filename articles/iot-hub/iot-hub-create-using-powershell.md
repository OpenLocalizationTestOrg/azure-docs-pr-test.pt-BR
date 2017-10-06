---
title: aaaCreate um IoT Hub do Azure usando um cmdlet do PowerShell | Microsoft Docs
description: Como toouse uma toocreate de cmdlet do PowerShell um hub IoT.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Criar um hub IoT usando o cmdlet Olá AzureRmIotHub novo

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introdução

Você pode usar toocreate de cmdlets do PowerShell do Azure e gerenciar os hubs IoT do Azure. Este tutorial mostra como toocreate um hub IoT com o PowerShell.

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. <br/>Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [Cmdlets do Azure PowerShell][lnk-powershell-install].

## <a name="connect-tooyour-azure-subscription"></a>Conecte-se tooyour assinatura do Azure
Em um prompt de comando do PowerShell, digite Olá comando toosign em tooyour assinatura do Azure a seguir:

```powershell
Login-AzureRmAccount
```

Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais. Use Olá toolist Olá assinaturas do Azure para você toouse de comando a seguir:

```powershell
Get-AzureRMSubscription
```

Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toocreate seu hub IoT a seguir. Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a>Criar grupo de recursos

Você precisa de um grupo de recursos toodeploy um hub IoT. É possível usar um grupo de recursos existente ou criar um novo.

Você pode usar o hello seguintes comando toodiscover Olá locais onde você pode implantar um hub IoT:

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate um grupo de recursos para o hub IoT em um dos locais de saudação com suporte para o IoT Hub, use Olá comando a seguir. Este exemplo cria um grupo de recursos chamado **MyIoTRG1** em Olá **Leste dos EUA** região:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>Crie um hub IoT

toocreate um hub IoT no grupo de recursos de saudação criado na etapa anterior de saudação, Olá use comandos a seguir. Este exemplo cria um **S1** hub chamado **MyTestIoTHub** em Olá **Leste dos EUA** região:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

nome de saudação do hub IoT de saudação deve ser exclusivo.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


Você pode listar todos os hubs de IoT Olá em sua assinatura usando Olá comando a seguir:

```powershell
Get-AzureRmIotHub
```

exemplo anterior Hello adiciona um IoT Hub de padrão de S1 para o qual você é cobrado. Você pode excluir o hub IoT de saudação usando Olá comando a seguir:

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

Como alternativa, você pode remover um grupo de recursos e todos os recursos nele usando o comando a seguir de saudação de hello:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Próximas etapas

Agora que você implantou um hub IoT usando um cmdlet do PowerShell, você poderá desejar tooexplore adicional:

* Descubra outros [cmdlets do PowerShell para trabalhar com o hub IoT][lnk-iothub-cmdlets].
* Leia sobre os recursos de saudação do hello [provedor de recursos de IoT Hub API REST][lnk-rest-api].

toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:

* [Introdução tooC SDK][lnk-c-sdk]
* [SDKs do Azure IoT][lnk-sdks]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Simulando um dispositivo com IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
