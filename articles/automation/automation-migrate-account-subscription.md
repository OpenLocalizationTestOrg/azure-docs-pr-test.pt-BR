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
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="fbfe4-103">Migrar de Conta de Automação e recursos</span><span class="sxs-lookup"><span data-stu-id="fbfe4-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="fbfe4-104">Para contas de automação e seus recursos associados (ou seja, ativos, runbooks, módulos, etc.) que você criou no hello portal do Azure e deseja toomigrate de um recurso de grupo tooanother ou de tooanother de uma assinatura, você pode fazer isso facilmente com Olá [mover recursos](../azure-resource-manager/resource-group-move-resources.md) disponíveis no portal do Azure de saudação do recurso.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="fbfe4-105">No entanto, antes de prosseguir com esta ação, você deve examinar a seguir Olá [lista de verificação antes de mover recursos](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) e Além disso, a lista Olá abaixo tooAutomation específico.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="fbfe4-106">grupo de recursos/assinatura de destino Olá deve ser na mesma região que a origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="fbfe4-107">Isso significa que contas de Automação não podem ser movidas entre regiões.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="fbfe4-108">Ao mover recursos (por exemplo, runbooks, trabalhos, etc.), grupo de saudação de origem e o grupo de destino Olá são bloqueadas durante operação Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="fbfe4-109">Gravar e excluir operações são bloqueados em grupos de saudação até que seja concluída Olá move.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="fbfe4-110">Quaisquer runbooks ou variáveis que fazem referência a uma ID de assinatura ou o recurso de assinatura existente Olá precisará toobe atualizado após a migração for concluída.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="fbfe4-111">Esse recurso não dá suporte à movimentação de recursos de automação Clássicos.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="fbfe4-112">toomove Olá conta de automação usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="fbfe4-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="fbfe4-113">Na sua conta de automação, clique em **mover** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="fbfe4-114">![Opção de mover](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="fbfe4-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="fbfe4-115">Em Olá **mover recursos** folha, observe que ela apresenta tooboth de recursos relacionados os grupos de recursos e de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="fbfe4-116">Selecione Olá **assinatura** e **grupo de recursos** de listas suspensas de saudação ou opção select Olá **criar um novo grupo de recursos** e digite um novo nome de grupo de recursos no campo Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="fbfe4-117">Revisão e Olá selecione caixa de seleção tooacknowledge você *entender as ferramentas e scripts serão necessidade toobe atualizado toouse novas IDs de recurso depois de mover recursos* e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="fbfe4-118">![Folha Mover Recursos](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="fbfe4-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="fbfe4-119">Esta ação levará toocomplete de vários minutos.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="fbfe4-120">Em **Notificações**, será exibido um status de cada ação que ocorre, incluindo validação, migração e, por fim, quando estiver concluído.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="fbfe4-121">toomove Olá conta de automação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbfe4-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="fbfe4-122">toomove existente grupo de recursos de tooanother de recursos de automação ou assinatura, use Olá **Get-AzureRmResource** conta de automação específica do cmdlet tooget hello e, em seguida, **Move-AzureRmResource** cmdlet tooperform Olá mover.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="fbfe4-123">Olá primeiro exemplo mostra como a conta toomove uma automação tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="fbfe4-124">Depois de executar Olá o exemplo de código acima, será solicitada tooverify deseja tooperform esta ação.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="fbfe4-125">Depois de clicar em **Sim** e permitir Olá tooproceed de script, você não receberá notificações enquanto ele está executando a migração hello.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="fbfe4-126">toomove tooa nova assinatura, inclua um valor para Olá *DestinationSubscriptionId* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="fbfe4-127">Como com o exemplo anterior de saudação, será solicitada tooconfirm Olá mover.</span><span class="sxs-lookup"><span data-stu-id="fbfe4-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="fbfe4-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbfe4-128">Next steps</span></span>
* <span data-ttu-id="fbfe4-129">Para obter mais informações sobre como mover grupo de recursos toonew de recursos ou assinatura, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="fbfe4-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="fbfe4-130">Para obter mais informações sobre o controle de acesso baseado em função na automação do Azure, consulte muito[controle de acesso baseado em função no Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="fbfe4-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="fbfe4-131">toolearn sobre cmdlets do PowerShell para gerenciar sua assinatura, consulte [usando o PowerShell do Azure com o Gerenciador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="fbfe4-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="fbfe4-132">toolearn sobre recursos do portal para gerenciar sua assinatura, consulte [usando os recursos de toomanage do Portal do Azure Olá](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fbfe4-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
