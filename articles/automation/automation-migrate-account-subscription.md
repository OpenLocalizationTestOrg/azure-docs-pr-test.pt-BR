---
title: "Migrar de Conta de Automação e Recursos | Microsoft Docs"
description: "Este artigo descreve como mover uma conta de Automação na Automação do Azure e recursos associados de uma assinatura para outra."
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
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="7b6ba-103">Migrar de Conta de Automação e recursos</span><span class="sxs-lookup"><span data-stu-id="7b6ba-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="7b6ba-104">Para contas de Automação e seus recursos associados (ou seja, ativos, runbooks, módulos, etc.) que você criou no portal do Azure e deseja migrar de um grupo de recursos para outro ou de uma assinatura para outra, você pode fazer isso facilmente com a funcionalidade [mover recursos](../azure-resource-manager/resource-group-move-resources.md) disponível no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="7b6ba-105">No entanto, antes de prosseguir com esta ação, consulte primeiro a seguinte [lista de verificação antes de mover os recursos](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) e, além dessa, a lista abaixo específica para Automação.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="7b6ba-106">A assinatura/grupo de recursos de destino deve estar na mesma região que a origem.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="7b6ba-107">Isso significa que contas de Automação não podem ser movidas entre regiões.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="7b6ba-108">Ao mover recursos (como runbooks, trabalhos, etc.), ambos o grupo de origem e o grupo de destino estão bloqueados pela duração da operação.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="7b6ba-109">As operações de gravação e exclusão são bloqueadas nos grupos até que a migração seja concluída.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="7b6ba-110">Quaisquer runbooks ou variáveis que fazem referência a um recursos ou ID de assinatura da assinatura existente precisará ser atualizado depois que a migração for concluída.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="7b6ba-111">Esse recurso não dá suporte à movimentação de recursos de automação Clássicos.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="7b6ba-112">Para mover a conta de Automação usando o portal</span><span class="sxs-lookup"><span data-stu-id="7b6ba-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="7b6ba-113">Em sua conta de Automação, clique em **Mover** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="7b6ba-114">![Opção de mover](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="7b6ba-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="7b6ba-115">Na folha **Mover recursos** , observe que ele apresenta recursos relacionados a sua conta de Automação e a seus grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="7b6ba-116">Selecione a **assinatura** e o **grupo de recursos** nas listas suspensas ou selecione a opção **criar um novo grupo de recursos** e digite um novo nome de grupo de recursos no campo fornecido.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="7b6ba-117">Examine e marque a caixa de seleção para confirmar que você *entende que as ferramentas e scripts precisarão ser atualizados para usar as novas ID de recurso depois de mover recursos* e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="7b6ba-118">![Folha Mover Recursos](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="7b6ba-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="7b6ba-119">Essa ação pode levar vários minutos para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="7b6ba-120">Em **Notificações**, será exibido um status de cada ação que ocorre, incluindo validação, migração e, por fim, quando estiver concluído.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="7b6ba-121">Para mover a Conta de Automação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b6ba-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="7b6ba-122">Para mover os recursos de Automação existentes para outro grupo de recursos ou assinatura, use o cmdlet **Get-AzureRmResource** para obter a conta de Automação específica e, em seguida, o cmdlet **Move-AzureRmResource** para realizar a movimentação.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="7b6ba-123">O primeiro exemplo mostra como mover uma conta de Automação para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="7b6ba-124">Depois de executar o exemplo de código acima, você deverá confirmar se deseja executar esta ação.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="7b6ba-125">Após clicar em **Sim** e permitir que o script continue, você não receberá nenhuma notificação durante a execução da migração.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="7b6ba-126">Para mover para uma nova assinatura, inclua um valor para o parâmetro *DestinationSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="7b6ba-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="7b6ba-127">Assim como no exemplo anterior, será solicitado que você confirme a mudança.</span><span class="sxs-lookup"><span data-stu-id="7b6ba-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7b6ba-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b6ba-128">Next steps</span></span>
* <span data-ttu-id="7b6ba-129">Para saber mais sobre como mover os recursos para um novo grupo de recursos ou assinatura, consulte [Mover recursos para um novo grupo de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="7b6ba-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="7b6ba-130">Para saber mais sobre o Controle de Acesso baseado em Função na Automação do Azure, consulte [Controle de acesso baseado em função na Automação do Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="7b6ba-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="7b6ba-131">Para saber mais sobre os cmdlets do PowerShell para gerenciar sua assinatura, consulte [Como usar o Azure PowerShell com o Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="7b6ba-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="7b6ba-132">Para saber mais sobre os recursos do portal para gerenciar sua assinatura, consulte [Como usar o Portal do Azure para gerenciar recursos](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b6ba-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
