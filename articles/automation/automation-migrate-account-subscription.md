---
title: "aaaMigrate conta de automação e os recursos | Microsoft Docs"
description: "Este artigo descreve como toomove uma automação conta de automação do Azure e os recursos associados de tooanother de uma assinatura."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>Migrar de Conta de Automação e recursos
Para contas de automação e seus recursos associados (ou seja, ativos, runbooks, módulos, etc.) que você criou no hello portal do Azure e deseja toomigrate de um recurso de grupo tooanother ou de tooanother de uma assinatura, você pode fazer isso facilmente com Olá [mover recursos](../azure-resource-manager/resource-group-move-resources.md) disponíveis no portal do Azure de saudação do recurso. No entanto, antes de prosseguir com esta ação, você deve examinar a seguir Olá [lista de verificação antes de mover recursos](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) e Além disso, a lista Olá abaixo tooAutomation específico.   

1. grupo de recursos/assinatura de destino Olá deve ser na mesma região que a origem de saudação.  Isso significa que contas de Automação não podem ser movidas entre regiões.
2. Ao mover recursos (por exemplo, runbooks, trabalhos, etc.), grupo de saudação de origem e o grupo de destino Olá são bloqueadas durante operação Olá Olá. Gravar e excluir operações são bloqueados em grupos de saudação até que seja concluída Olá move.  
3. Quaisquer runbooks ou variáveis que fazem referência a uma ID de assinatura ou o recurso de assinatura existente Olá precisará toobe atualizado após a migração for concluída.   

> [!NOTE]
> Esse recurso não dá suporte à movimentação de recursos de automação Clássicos.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>toomove Olá conta de automação usando o portal de saudação
1. Na sua conta de automação, clique em **mover** na parte superior de saudação da folha de saudação.<br> ![Opção de mover](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. Em Olá **mover recursos** folha, observe que ela apresenta tooboth de recursos relacionados os grupos de recursos e de sua conta de automação.  Selecione Olá **assinatura** e **grupo de recursos** de listas suspensas de saudação ou opção select Olá **criar um novo grupo de recursos** e digite um novo nome de grupo de recursos no campo Olá fornecido.  
3. Revisão e Olá selecione caixa de seleção tooacknowledge você *entender as ferramentas e scripts serão necessidade toobe atualizado toouse novas IDs de recurso depois de mover recursos* e, em seguida, clique em **Okey**.<br> ![Folha Mover Recursos](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Esta ação levará toocomplete de vários minutos.  Em **Notificações**, será exibido um status de cada ação que ocorre, incluindo validação, migração e, por fim, quando estiver concluído.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove Olá conta de automação usando o PowerShell
toomove existente grupo de recursos de tooanother de recursos de automação ou assinatura, use Olá **Get-AzureRmResource** conta de automação específica do cmdlet tooget hello e, em seguida, **Move-AzureRmResource** cmdlet tooperform Olá mover.

Olá primeiro exemplo mostra como a conta toomove uma automação tooa novo grupo de recursos.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Depois de executar Olá o exemplo de código acima, será solicitada tooverify deseja tooperform esta ação.  Depois de clicar em **Sim** e permitir Olá tooproceed de script, você não receberá notificações enquanto ele está executando a migração hello.  

toomove tooa nova assinatura, inclua um valor para Olá *DestinationSubscriptionId* parâmetro.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Como com o exemplo anterior de saudação, será solicitada tooconfirm Olá mover.  

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre como mover grupo de recursos toonew de recursos ou assinatura, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md)
* Para obter mais informações sobre o controle de acesso baseado em função na automação do Azure, consulte muito[controle de acesso baseado em função no Azure Automation](automation-role-based-access-control.md).
* toolearn sobre cmdlets do PowerShell para gerenciar sua assinatura, consulte [usando o PowerShell do Azure com o Gerenciador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md)
* toolearn sobre recursos do portal para gerenciar sua assinatura, consulte [usando os recursos de toomanage do Portal do Azure Olá](../azure-resource-manager/resource-group-portal.md).
