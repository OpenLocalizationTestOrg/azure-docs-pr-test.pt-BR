---
title: aaaCreate um IoT Hub do Azure usando um modelo (PowerShell) | Microsoft Docs
description: Como toouse uma toocreate de modelo do Azure Resource Manager um IoT Hub com o PowerShell.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Criar um Hub IoT usando um modelo do Azure Resource Manager (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Você pode usar o Gerenciador de recursos do Azure toocreate e gerenciar programaticamente os hubs de IoT do Azure. Este tutorial mostra como toouse uma toocreate de modelo do Azure Resource Manager um hub IoT com o PowerShell.

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.

toocomplete neste tutorial, você precisa Olá a seguir:

* Uma conta ativa do Azure. <br/>Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.
* [Azure PowerShell 1.0][lnk-powershell-install] ou posterior.

> [!TIP]
> artigo Olá [usando o PowerShell do Azure com o Azure Resource Manager] [ lnk-powershell-arm] fornece mais informações sobre como toouse PowerShell e o Azure Resource Manager modelos toocreate Azure recursos.

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

Você pode usar o hello comandos toodiscover onde você pode implantar um hub IoT e versões de API Olá atualmente com suporte a seguir:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Crie um toocontain do grupo de recursos o hub IoT usando Olá seguinte comando em um dos locais de saudação com suporte para o IoT Hub. Este exemplo cria um grupo de recursos chamado **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Enviar um toocreate modelo um hub IoT

Use um modelo JSON toocreate um hub IoT no grupo de recursos. Você também pode usar um hub de IoT do Azure Resource Manager modelo toomake alterações tooan existente.

1. Usar um toocreate do editor de texto chamado de um modelo do Azure Resource Manager **template.json** com hello toocreate de definição de recurso a seguir um novo hub IoT padrão. Este exemplo adiciona Olá IoT Hub Olá **Leste dos EUA** região, cria dois grupos de consumidores (**cg1** e **cg2**) no ponto de extremidade Olá compatível com o Hub de eventos e usa Olá **2016-02-03** versão da API. Esse modelo também que toopass no nome do hub IoT hello como um parâmetro chamado **hubName**. Para obter a lista atual Olá locais que dão suporte ao IoT Hub consulte [Status do Azure][lnk-status].

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. Salve arquivo de modelo de Gerenciador de recursos do Azure Olá em seu computador local. Este exemplo pressupõe que você o salvará em uma pasta chamada **c:\templates**.

3. Execute Olá toodeploy de comando a seguir o novo hub IoT, passando o nome de saudação do seu hub IoT como um parâmetro. Neste exemplo, o nome de saudação do hub IoT de saudação é `abcmyiothub`. nome de saudação do seu hub IoT deve ser globalmente exclusivo:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. saída de Hello exibe chaves Olá para o hub IoT de saudação criado por você.

5. tooverify seu aplicativo adicionado Olá novo hub IoT, visite Olá [portal do Azure] [ lnk-azure-portal] e exibir a lista de recursos. Como alternativa, use Olá **Get-AzureRmResource** cmdlet do PowerShell.

> [!NOTE]
> Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado. Você pode excluir o hub IoT de saudação por meio de saudação [portal do Azure] [ lnk-azure-portal] ou usando Olá **Remove-AzureRmResource** cmdlet do PowerShell quando tiver terminado.

## <a name="next-steps"></a>Próximas etapas

Agora que você implantou um hub IoT usando um modelo do Gerenciador de recursos do Azure com o PowerShell, você poderá desejar tooexplore adicional:

* Leia sobre os recursos de saudação do hello [provedor de recursos de IoT Hub API REST][lnk-rest-api].
* Leitura [visão geral do Gerenciador de recursos do Azure] [ lnk-azure-rm-overview] toolearn mais sobre os recursos de saudação do Gerenciador de recursos do Azure.

toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:

* [Introdução tooC SDK][lnk-c-sdk]
* [SDKs do Azure IoT][lnk-sdks]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
