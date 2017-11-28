---
title: aaaUse toomanage portal do Azure recursos do Azure | Microsoft Docs
description: "Use o portal do Azure e gerenciamento de recursos do Azure toomanage seus recursos. Mostra como toowork com recursos de toomonitor painéis."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="09918-104">Gerenciar recursos do Azure por meio do portal</span><span class="sxs-lookup"><span data-stu-id="09918-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09918-105">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="09918-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="09918-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="09918-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="09918-107">Portal</span><span class="sxs-lookup"><span data-stu-id="09918-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="09918-108">API REST</span><span class="sxs-lookup"><span data-stu-id="09918-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="09918-109">Este tópico mostra como Olá toouse [portal do Azure](https://portal.azure.com) com [do Azure Resource Manager](resource-group-overview.md) toomanage seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="09918-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="09918-110">toolearn sobre a implantação de recursos por meio do portal hello, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="09918-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="09918-111">Atualmente, não cada serviço suporta Olá portal ou o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="09918-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="09918-112">Para esses serviços, você precisa Olá toouse [portal clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="09918-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="09918-113">Para obter o status de saudação de cada serviço, consulte [gráfico de disponibilidade do portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="09918-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="09918-114">Gerenciar grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="09918-114">Manage resource groups</span></span>

<span data-ttu-id="09918-115">Um grupo de recursos é um contêiner que mantém os recursos relacionados a uma solução do Azure.</span><span class="sxs-lookup"><span data-stu-id="09918-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="09918-116">grupo de recursos de saudação pode incluir todos os recursos de saudação para solução hello, ou apenas os recursos que você deseja toomanage como um grupo.</span><span class="sxs-lookup"><span data-stu-id="09918-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="09918-117">Decidir como deseja que os recursos de tooallocate tooresource grupos com base no que torna hello mais sentido para sua organização.</span><span class="sxs-lookup"><span data-stu-id="09918-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="09918-118">Geralmente, adicionar recursos que compartilham Olá mesmo toohello de ciclo de vida mesmo recurso de grupo para que você pode facilmente implantar, atualizar e excluí-los como um grupo.</span><span class="sxs-lookup"><span data-stu-id="09918-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="09918-119">grupo de recursos de saudação armazena metadados sobre os recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="09918-120">Portanto, quando você especificar um local para o grupo de recursos hello, você está especificando onde os metadados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="09918-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="09918-121">Por motivos de conformidade, talvez seja necessário tooensure que seus dados são armazenados em uma determinada região.</span><span class="sxs-lookup"><span data-stu-id="09918-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="09918-122">toosee todos os grupos de recursos de saudação em sua assinatura, selecione **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="09918-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![procurar grupos de recursos](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="09918-124">toocreate um grupo de recurso vazio, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="09918-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![adicionar grupo de recursos](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="09918-126">Forneça um nome e local para o novo grupo de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="09918-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="09918-127">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="09918-127">Select **Create**.</span></span>
   
    ![Criar grupo de recursos](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="09918-129">Talvez seja necessário tooselect **atualizar** toosee grupo de recursos de saudação criado recentemente.</span><span class="sxs-lookup"><span data-stu-id="09918-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![atualizar grupo de recursos](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="09918-131">toocustomize Olá informações exibidas para os grupos de recursos, selecione **colunas**.</span><span class="sxs-lookup"><span data-stu-id="09918-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personalizar colunas](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="09918-133">Selecione Olá colunas tooadd e, em seguida, selecione **atualização**.</span><span class="sxs-lookup"><span data-stu-id="09918-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![adicionar colunas](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="09918-135">toolearn sobre como implantar recursos tooyour novo grupo de recursos, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="09918-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="09918-136">Acesso rápido tooa grupo de recursos, você pode fixar o dashboard na tooyour Olá folha.</span><span class="sxs-lookup"><span data-stu-id="09918-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![fixar grupo de recursos](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="09918-138">painel Olá exibe o grupo de recursos de saudação e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="09918-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="09918-139">Você pode selecionar os grupos de recursos de saudação ou qualquer item de toohello de toonavigate seus recursos.</span><span class="sxs-lookup"><span data-stu-id="09918-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![fixar grupo de recursos](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="09918-141">Recursos de marca</span><span class="sxs-lookup"><span data-stu-id="09918-141">Tag resources</span></span>
<span data-ttu-id="09918-142">Você pode aplicar marcas tooresource grupos e recursos toologically organizar seus ativos.</span><span class="sxs-lookup"><span data-stu-id="09918-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="09918-143">Para obter informações sobre como trabalhar com marcas, consulte [usando marcas tooorganize seus recursos do Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="09918-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="09918-144">Monitorar recursos</span><span class="sxs-lookup"><span data-stu-id="09918-144">Monitor resources</span></span>
<span data-ttu-id="09918-145">Quando você seleciona um recurso, a folha de recursos Olá apresenta tabelas para o tipo de recurso de monitoramento e gráficos padrão.</span><span class="sxs-lookup"><span data-stu-id="09918-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="09918-146">Selecione um recurso e observe Olá **monitoramento** seção.</span><span class="sxs-lookup"><span data-stu-id="09918-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="09918-147">Ele inclui gráficos que são relevantes toohello tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="09918-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="09918-148">Olá imagem a seguir mostra dados de monitoramento de uma conta de armazenamento de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![mostrar o monitoramento](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="09918-150">Você pode fixar uma seção de saudação folha tooyour painel selecionando as reticências (...) do hello acima seção hello.</span><span class="sxs-lookup"><span data-stu-id="09918-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="09918-151">Você também pode personalizar Olá tamanho Olá seção na folha de saudação ou removê-lo completamente.</span><span class="sxs-lookup"><span data-stu-id="09918-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="09918-152">Hello imagem a seguir mostra como toopin, personalizar, ou remova a saudação da CPU e a seção de memória.</span><span class="sxs-lookup"><span data-stu-id="09918-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![fixar seção](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="09918-154">Depois de fixar o dashboard do hello seção toohello, você verá Olá resumo no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="09918-155">E, selecionando-o imediatamente leva toomore detalhes sobre dados saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![exibir painel](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="09918-157">toocompletely personalizar dados de saudação monitorar por meio do portal hello, navegar do painel de padrão de tooyour e selecione **novo painel**.</span><span class="sxs-lookup"><span data-stu-id="09918-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![painel Transações da Web](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="09918-159">Nomeie o novo painel e arrastar blocos no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="09918-160">Olá peças são filtradas pelo opções diferentes.</span><span class="sxs-lookup"><span data-stu-id="09918-160">hello tiles are filtered by different options.</span></span>
   
    ![painel Transações da Web](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="09918-162">toolearn sobre como trabalhar com os painéis, consulte [criação e compartilhamento de painéis no portal do Azure de saudação](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="09918-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="09918-163">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="09918-163">Manage resources</span></span>
<span data-ttu-id="09918-164">Na folha de saudação para um recurso, você ver opções Olá para gerenciar recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="09918-165">portal de saudação apresenta opções de gerenciamento para o tipo de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="09918-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="09918-166">Você ver os comandos de gerenciamento de saudação na superior de saudação da folha de recursos hello e no lado esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Gerenciar recursos](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="09918-168">Essas opções, você pode executar operações como iniciar e parar uma máquina virtual ou reconfigurar as propriedades de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="09918-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="09918-169">Mover recursos</span><span class="sxs-lookup"><span data-stu-id="09918-169">Move resources</span></span>
<span data-ttu-id="09918-170">Se você precisar de grupo de recursos de tooanother toomove recursos ou outra assinatura, consulte [Mover grupo de recursos toonew de recursos ou assinatura](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="09918-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="09918-171">Bloquear recursos</span><span class="sxs-lookup"><span data-stu-id="09918-171">Lock resources</span></span>
<span data-ttu-id="09918-172">Você pode bloquear uma assinatura, o grupo de recursos ou o recurso tooprevent outros usuários em sua organização acidentalmente excluir ou modificar recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="09918-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="09918-173">Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="09918-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="09918-174">Exibir sua assinatura e os custos</span><span class="sxs-lookup"><span data-stu-id="09918-174">View your subscription and costs</span></span>
<span data-ttu-id="09918-175">Você pode exibir informações sobre sua assinatura e custos de acumulados Olá para todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="09918-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="09918-176">Selecione **assinaturas** e assinatura Olá deseja toosee.</span><span class="sxs-lookup"><span data-stu-id="09918-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="09918-177">Você só pode ter um tooselect de assinatura.</span><span class="sxs-lookup"><span data-stu-id="09918-177">You might only have one subscription tooselect.</span></span>

![subscription](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="09918-179">Na folha de assinatura hello, você verá uma taxa de gravação.</span><span class="sxs-lookup"><span data-stu-id="09918-179">Within hello subscription blade, you see a burn rate.</span></span>

![taxa de gravação](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="09918-181">Haverá também uma divisão de custos por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="09918-181">And, a breakdown of costs by resource type.</span></span>

![custo de recurso](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="09918-183">Exportar modelo</span><span class="sxs-lookup"><span data-stu-id="09918-183">Export template</span></span>
<span data-ttu-id="09918-184">Depois de configurar o seu grupo de recursos, convém tooview modelo de Gerenciador de recursos de Olá Olá para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09918-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="09918-185">Exportar modelo de saudação oferece dois benefícios:</span><span class="sxs-lookup"><span data-stu-id="09918-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="09918-186">Você pode facilmente automatizar implantações futuras de solução Olá porque o modelo de saudação contém todos os Olá toda a infraestrutura do.</span><span class="sxs-lookup"><span data-stu-id="09918-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="09918-187">Você pode se familiarizar com sintaxe do modelo observando Olá notação JSON (JavaScript Object) que representa a sua solução.</span><span class="sxs-lookup"><span data-stu-id="09918-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="09918-188">Para obter as diretrizes passo a passo, confira [Exportar um modelo do Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="09918-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="09918-189">Excluir grupo de recursos ou recursos</span><span class="sxs-lookup"><span data-stu-id="09918-189">Delete resource group or resources</span></span>
<span data-ttu-id="09918-190">Excluir um grupo de recursos exclui todos os recursos de saudação contidos nele.</span><span class="sxs-lookup"><span data-stu-id="09918-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="09918-191">Você também pode excluir recursos individuais de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="09918-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="09918-192">Você deseja tooexercise cuidado quando você excluir um grupo de recursos porque pode haver recursos em outros grupos de recursos que estão vinculado tooit.</span><span class="sxs-lookup"><span data-stu-id="09918-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="09918-193">Gerenciador de recursos não exclui os recursos vinculados, mas eles podem não funcionar corretamente sem recursos Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="09918-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![excluir grupo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="09918-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09918-195">Next steps</span></span>
* <span data-ttu-id="09918-196">logs de atividade tooview, consulte [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="09918-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="09918-197">tooview detalhes sobre uma implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="09918-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="09918-198">recursos toodeploy por meio do portal hello, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="09918-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="09918-199">toomanage tooresources de acesso, consulte [usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="09918-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="09918-200">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="09918-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

