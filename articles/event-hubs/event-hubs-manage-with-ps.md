---
title: recursos de Hubs de eventos do Azure aaaUse PowerShell toomanage | Microsoft Docs
description: "Usar toocreate de módulo do PowerShell e gerenciar os Hubs de eventos"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a>Usar recursos de Hubs de eventos do PowerShell toomanage

Microsoft Azure PowerShell é um ambiente de script que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de serviços do Azure. Este artigo descreve como Olá toouse [módulo PowerShell do Gerenciador de recursos de Hubs de evento](/powershell/module/azurerm.eventhub) tooprovision e gerenciar entidades de Hubs de eventos (namespaces, os hubs de eventos individuais e grupos de consumidores) usando um console local do PowerShell do Azure ou script.

Também é possível gerenciar recursos dos Hubs de Eventos usando modelos do Azure Resource Manager. Para obter mais informações, consulte o artigo Olá [criar um namespace de Hubs de eventos com o grupo de consumidor e hub de eventos usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, você precisará seguir hello:

* Uma assinatura do Azure. Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra][purchase options], [ofertas para membros][member offers] ou [conta gratuita][free account].
* Um computador com o PowerShell do Azure. Para obter instruções, consulte [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/get-started-azureps).
* Uma compreensão geral dos scripts do PowerShell, pacotes do NuGet e saudação do .NET Framework.

## <a name="get-started"></a>Introdução

Olá primeira etapa é toouse PowerShell toolog em tooyour conta do Azure e assinatura do Azure. Siga as instruções de saudação em [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/get-started-azureps) toolog em tooyour conta do Azure, em seguida, recuperar e acessar recursos de saudação em sua assinatura do Azure.

## <a name="provision-an-event-hubs-namespace"></a>Provisionar um namespace dos Hubs de Eventos

Ao trabalhar com namespaces de Hubs de eventos, você pode usar o hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [AzureRmEventHubNamespace remover](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , e [AzureRmEventHubNamespace conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.

Este exemplo cria algumas variáveis locais no script hello; `$Namespace` e `$Location`.

* `$Namespace`é o nome de saudação do namespace de Hubs de eventos de saudação com a qual queremos toowork.
* `$Location`identifica Olá data center em que podemos provisionará Olá namespace.
* `$CurrentNamespace`armazena o namespace de referência Olá recuperar (ou criar).

Em um script real, `$Namespace` e `$Location` podem ser passados como parâmetros.

Esta parte do script Olá Olá a seguir:

1. Tentativas tooretrieve um namespace de Hubs de eventos com hello nome especificado.
2. Se Olá namespace for encontrado, ele informa o que foi encontrado.
3. Se Olá namespace não for encontrado, ele cria Olá namespace e recupera Olá recém-criado namespace.

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a>Criar um Hub de Evento

toocreate um hub de eventos, execute uma verificação de namespace usando o script hello na seção anterior hello. Em seguida, use Olá [AzureRmEventHub novo](/powershell/module/azurerm.eventhub/new-azurermeventhub) hub de eventos do cmdlet toocreate hello:

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a>Criar um grupo de consumidores

toocreate um grupo de consumidor dentro de um hub de eventos, executar Olá namespace e o evento de hub verificações usando scripts de saudação na seção anterior Olá. Em seguida, use Olá [AzureRmEventHubConsumerGroup novo](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) grupo de consumidores do cmdlet toocreate Olá no hub de eventos de saudação. Por exemplo:

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a>Definir metadados do usuário

Depois de executar scripts de saudação em Olá anterior seções, você pode usar o hello [AzureRmEventHubConsumerGroup conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) propriedades de saudação do cmdlet tooupdate de um grupo de consumidores, como no exemplo a seguir de saudação:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Remover hub de eventos

hubs de eventos de saudação tooremove criado, você pode usar o hello `Remove-*` cmdlets, como no exemplo a seguir de saudação:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Próximas etapas

- Consulte a documentação completa de módulo evento Hubs Gerenciador de recursos do PowerShell Olá [aqui](/powershell/module/azurerm.eventhub). Esta página lista todos os cmdlets disponíveis.
- Para obter informações sobre como usar modelos do Azure Resource Manager, consulte o artigo Olá [criar um namespace de Hubs de eventos com o grupo de consumidor e hub de eventos usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).
- Informações sobre [Bibliotecas de gerenciamento .NET dos Hubs de Eventos](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
