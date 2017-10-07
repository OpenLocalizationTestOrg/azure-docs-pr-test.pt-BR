---
title: "recursos de barramento de serviço do Azure aaaUse PowerShell toomanage | Microsoft Docs"
description: "Usar toocreate de módulo do PowerShell e gerenciar recursos do barramento de serviço"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a>Usar recursos de barramento de serviço do PowerShell toomanage

Microsoft Azure PowerShell é um ambiente de script que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de serviços do Azure. Este artigo descreve como Olá toouse [módulo PowerShell do Gerenciador de recursos do barramento de serviço](/powershell/module/azurerm.servicebus) tooprovision e gerenciar entidades do barramento de serviço (namespaces, filas, tópicos e assinaturas) usando um console local do PowerShell do Azure ou script.

Também é possível gerenciar entidades do Barramento de Serviço usando modelos do Azure Resource Manager. Para obter mais informações, consulte o artigo Olá [recursos de barramento de serviço criar usando modelos do Azure Resource Manager](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, você precisará seguir hello:

* Uma assinatura do Azure. Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra][purchase options], [ofertas para membros][member offers] ou [conta gratuita][free account].
* Um computador com o PowerShell do Azure. Para obter instruções, consulte [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/get-started-azureps).
* Uma compreensão geral dos scripts do PowerShell, pacotes do NuGet e saudação do .NET Framework.

## <a name="get-started"></a>Introdução

Olá primeira etapa é toouse PowerShell toolog em tooyour conta do Azure e assinatura do Azure. Siga as instruções de saudação em [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/get-started-azureps) toolog tooyour conta do Azure e recuperar e acessar recursos de saudação em sua assinatura do Azure.

## <a name="provision-a-service-bus-namespace"></a>Provisionar um namespace do Barramento de Serviço

Ao trabalhar com namespaces de barramento de serviço, você pode usar o hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), e [AzureRmServiceBusNamespace conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.

Este exemplo cria algumas variáveis locais no script hello; `$Namespace` e `$Location`.

* `$Namespace`é o nome de saudação do namespace de barramento de serviço Olá com a qual queremos toowork.
* `$Location`identifica Olá data center em que podemos provisionará Olá namespace.
* `$CurrentNamespace`armazena o namespace de referência Olá recuperar (ou criar).

Em um script real, `$Namespace` e `$Location` podem ser passados como parâmetros.

Esta parte do script Olá Olá a seguir:

1. Tentativas tooretrieve um namespace de barramento de serviço com hello nome especificado.
2. Se Olá namespace for encontrado, ele informa o que foi encontrado.
3. Se Olá namespace não for encontrado, ele cria Olá namespace e recupera Olá recém-criado namespace.
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a>Criar uma regra de autorização de namespace

Olá exemplo a seguir mostra como regras de autorização de namespace toomanage usando Olá [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Conjunto AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), e [AzureRmServiceBusNamespaceAuthorizationRule remover cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a>Criar uma fila

toocreate uma fila ou tópico, execute uma verificação de namespace usando o script hello na seção anterior hello. Em seguida, crie uma fila de saudação:

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a>Modificar propriedades da fila

Depois de executar o script de saudação em Olá anterior seção, você pode usar o hello [AzureRmServiceBusQueue conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) propriedades de saudação do cmdlet tooupdate de uma fila, como no exemplo a seguir de saudação:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Provisionamento de outras entidades do Barramento de Serviço

Você pode usar o hello [módulo PowerShell do barramento de serviço](/powershell/module/azurerm.servicebus) tooprovision outras entidades, como tópicos e assinaturas. Esses cmdlets são sintaticamente semelhantes cmdlets de criação de fila toohello demonstrado na seção anterior hello.

## <a name="next-steps"></a>Próximas etapas

- Consulte a documentação completa de módulo PowerShell Gerenciador de recursos do barramento de serviço Olá [aqui](/powershell/module/azurerm.servicebus). Esta página lista todos os cmdlets disponíveis.
- Para obter informações sobre como usar modelos do Azure Resource Manager, consulte o artigo Olá [recursos de barramento de serviço criar usando modelos do Azure Resource Manager](service-bus-resource-manager-overview.md).
- Informações sobre [Bibliotecas de gerenciamento .NET do Barramento de Serviço](service-bus-management-libraries.md).

Há algumas formas alternativas toomanage entidades do barramento de serviço, conforme descrito nessas postagens de blog:

* [Como toocreate Service Bus filas, tópicos e assinaturas usando um script do PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Como toocreate um Namespace de barramento de serviço e um Hub de eventos usando um script do PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Scripts do PowerShell do Barramento de Serviço](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
