---
title: Usar o Portal do Azure para gerenciar os recursos do Azure | Microsoft Docs
description: "Use o portal do Azure e o Azure Resource Manager para gerenciar seus recursos. Mostra como trabalhar com painéis para monitorar recursos."
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
ms.openlocfilehash: 7a94fd5065de93384460e851627a9813d439956b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="59489-104">Gerenciar recursos do Azure por meio do portal</span><span class="sxs-lookup"><span data-stu-id="59489-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59489-105">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="59489-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="59489-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="59489-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="59489-107">Portal</span><span class="sxs-lookup"><span data-stu-id="59489-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="59489-108">API REST</span><span class="sxs-lookup"><span data-stu-id="59489-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="59489-109">Este tópico mostra como usar o [Portal do Azure](https://portal.azure.com) com o [Azure Resource Manager](resource-group-overview.md) para gerenciar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="59489-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="59489-110">Para saber mais sobre a implantação de recursos por meio do portal, confira [Implantar recursos com modelos do Resource Manager e o Portal do Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="59489-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="59489-111">Atualmente, nem todo serviço dá suporte ao portal ou ao Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="59489-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="59489-112">Para esses serviços, você precisa usar o [Portal Clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="59489-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="59489-113">Para obter o status de cada serviço, confira o [Gráfico de disponibilidade do Portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="59489-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="59489-114">Gerenciar grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="59489-114">Manage resource groups</span></span>

<span data-ttu-id="59489-115">Um grupo de recursos é um contêiner que mantém os recursos relacionados a uma solução do Azure.</span><span class="sxs-lookup"><span data-stu-id="59489-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="59489-116">O grupo de recursos pode incluir todos os recursos para a solução ou apenas os recursos que você deseja gerenciar como um grupo.</span><span class="sxs-lookup"><span data-stu-id="59489-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="59489-117">Você decide como deseja alocar recursos para grupos de recursos com base no que faz mais sentido para sua organização.</span><span class="sxs-lookup"><span data-stu-id="59489-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="59489-118">Em geral, adicione recursos que compartilham o mesmo ciclo de vida no mesmo grupo de recursos, para que você possa implantar, atualizar e excluí-los como um grupo facilmente.</span><span class="sxs-lookup"><span data-stu-id="59489-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="59489-119">O grupo de recursos armazena metadados sobre os recursos.</span><span class="sxs-lookup"><span data-stu-id="59489-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="59489-120">Portanto, quando você especifica um local para o grupo de recursos, especifica onde os metadados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="59489-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="59489-121">Por motivos de conformidade, você precisa fazer com que os dados sejam armazenados em determinada região.</span><span class="sxs-lookup"><span data-stu-id="59489-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="59489-122">Para ver todos os grupos de recursos em sua assinatura, selecione **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="59489-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![procurar grupos de recursos](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="59489-124">Para criar um grupo de recursos vazio, escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="59489-124">To create an empty resource group, select **Add**.</span></span>
   
    ![adicionar grupo de recursos](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="59489-126">Forneça um nome e local para o novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="59489-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="59489-127">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="59489-127">Select **Create**.</span></span>
   
    ![criar grupo de recursos](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="59489-129">Talvez seja necessário selecionar **Atualizar** para ver o grupo de recursos recém-criado.</span><span class="sxs-lookup"><span data-stu-id="59489-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![atualizar grupo de recursos](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="59489-131">Para personalizar as informações exibidas para os grupos de recursos, escolha **Colunas**.</span><span class="sxs-lookup"><span data-stu-id="59489-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personalizar colunas](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="59489-133">Selecione as colunas para adicionar e, em seguida, selecione **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="59489-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![adicionar colunas](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="59489-135">Para saber mais sobre a implantação de recursos em seu novo grupo de recursos, confira [Implantar recursos com modelos do Resource Manager e o Portal do Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="59489-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="59489-136">Para obter acesso rápido a um grupo de recursos, você pode fixar a folha em seu painel.</span><span class="sxs-lookup"><span data-stu-id="59489-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![fixar grupo de recursos](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="59489-138">Este painel exibe o grupo de recursos e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="59489-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="59489-139">Você pode selecionar os grupos de recursos, ou qualquer um dos seus recursos, para navegar até o item.</span><span class="sxs-lookup"><span data-stu-id="59489-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![fixar grupo de recursos](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="59489-141">Recursos de marca</span><span class="sxs-lookup"><span data-stu-id="59489-141">Tag resources</span></span>
<span data-ttu-id="59489-142">Você pode aplicar marcas a recursos e grupos de recursos para organizar seus ativos de modo lógico.</span><span class="sxs-lookup"><span data-stu-id="59489-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="59489-143">Para obter informações sobre como trabalhar com marcas, confira [Usando marcas para organizar os recursos do Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="59489-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="59489-144">Monitorar recursos</span><span class="sxs-lookup"><span data-stu-id="59489-144">Monitor resources</span></span>
<span data-ttu-id="59489-145">Quando você seleciona um recurso, a folha do recurso apresenta gráficos e tabelas padrão para esse tipo de recurso de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="59489-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="59489-146">Selecione um recurso e observe a seção **Monitoramento** .</span><span class="sxs-lookup"><span data-stu-id="59489-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="59489-147">Ela inclui gráficos que são relevantes para o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="59489-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="59489-148">A imagem a seguir mostra os dados de monitoramento padrão de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="59489-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![mostrar o monitoramento](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="59489-150">Você pode fixar uma seção da folha no painel selecionando as reticências (...) acima da seção.</span><span class="sxs-lookup"><span data-stu-id="59489-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="59489-151">Você também pode personalizar o tamanho da seção na folha ou removê-los completamente.</span><span class="sxs-lookup"><span data-stu-id="59489-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="59489-152">A imagem a seguir mostra como fixar, personalizar ou remover a seção CPU e Memória.</span><span class="sxs-lookup"><span data-stu-id="59489-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![fixar seção](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="59489-154">Depois de fixar a seção no painel, você verá o resumo nele.</span><span class="sxs-lookup"><span data-stu-id="59489-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="59489-155">E selecioná-lo imediatamente conduz você a mais detalhes sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="59489-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![exibir painel](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="59489-157">Para personalizar completamente os dados que você monitora por meio do portal, navegue até o painel padrão e selecione **Novo painel**.</span><span class="sxs-lookup"><span data-stu-id="59489-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![painel Transações da Web](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="59489-159">Nomeie o novo painel e arraste os blocos para ele.</span><span class="sxs-lookup"><span data-stu-id="59489-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="59489-160">Os blocos são filtrados por opções diferentes.</span><span class="sxs-lookup"><span data-stu-id="59489-160">The tiles are filtered by different options.</span></span>
   
    ![painel Transações da Web](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="59489-162">Para aprender a trabalhar com painéis, confira [Criar compartilhar painéis personalizados no Portal do Azure](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="59489-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="59489-163">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="59489-163">Manage resources</span></span>
<span data-ttu-id="59489-164">Na folha de um recurso, você vê as opções para gerenciá-lo.</span><span class="sxs-lookup"><span data-stu-id="59489-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="59489-165">O portal apresenta as opções de gerenciamento para este tipo de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="59489-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="59489-166">Você pode ver os comandos de gerenciamento na parte superior da folha de recursos e à esquerda.</span><span class="sxs-lookup"><span data-stu-id="59489-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![Gerenciar recursos](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="59489-168">Dessas opções, você pode executar operações como iniciar e parar uma máquina virtual ou reconfigurar suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="59489-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="59489-169">Mover recursos</span><span class="sxs-lookup"><span data-stu-id="59489-169">Move resources</span></span>
<span data-ttu-id="59489-170">Se você precisar mover um recurso para outro grupo de recursos ou outra assinatura, confira [Mover recursos para um novo grupo de recursos ou uma nova assinatura](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="59489-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="59489-171">Bloquear recursos</span><span class="sxs-lookup"><span data-stu-id="59489-171">Lock resources</span></span>
<span data-ttu-id="59489-172">Você pode bloquear uma assinatura, um recurso ou um grupo de recursos para impedir que outros usuários em sua organização excluam ou modifiquem recursos críticos acidentalmente.</span><span class="sxs-lookup"><span data-stu-id="59489-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="59489-173">Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="59489-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="59489-174">Exibir sua assinatura e os custos</span><span class="sxs-lookup"><span data-stu-id="59489-174">View your subscription and costs</span></span>
<span data-ttu-id="59489-175">Você pode exibir as informações sobre sua assinatura e os custos acumulados para todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="59489-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="59489-176">Selecione **Assinaturas** e a assinatura que você deseja ver.</span><span class="sxs-lookup"><span data-stu-id="59489-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="59489-177">Talvez você só tenha uma assinatura para selecionar.</span><span class="sxs-lookup"><span data-stu-id="59489-177">You might only have one subscription to select.</span></span>

![subscription](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="59489-179">Na folha da assinatura, você verá uma taxa de gravação.</span><span class="sxs-lookup"><span data-stu-id="59489-179">Within the subscription blade, you see a burn rate.</span></span>

![taxa de gravação](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="59489-181">Haverá também uma divisão de custos por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="59489-181">And, a breakdown of costs by resource type.</span></span>

![custo de recurso](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="59489-183">Exportar modelo</span><span class="sxs-lookup"><span data-stu-id="59489-183">Export template</span></span>
<span data-ttu-id="59489-184">Depois de configurar o grupo de recursos, convém exibir o modelo do Resource Manager para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="59489-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="59489-185">A exportação do modelo oferece dois benefícios:</span><span class="sxs-lookup"><span data-stu-id="59489-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="59489-186">Você pode automatizar com facilidade as implantações futuras da solução, pois o modelo contém a infraestrutura completa.</span><span class="sxs-lookup"><span data-stu-id="59489-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="59489-187">Você pode se familiarizar com a sintaxe do modelo analisando o JSON (JavaScript Object Notation) que representa sua solução.</span><span class="sxs-lookup"><span data-stu-id="59489-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="59489-188">Para obter as diretrizes passo a passo, confira [Exportar um modelo do Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="59489-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="59489-189">Excluir grupo de recursos ou recursos</span><span class="sxs-lookup"><span data-stu-id="59489-189">Delete resource group or resources</span></span>
<span data-ttu-id="59489-190">Excluir um grupo de recursos exclui todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="59489-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="59489-191">Você também pode excluir recursos individuais de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="59489-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="59489-192">Tenha cuidado ao excluir um grupo de recursos, pois pode haver recursos em outros grupos de recursos vinculados a ele.</span><span class="sxs-lookup"><span data-stu-id="59489-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="59489-193">O Resource Manager não exclui os recursos vinculados, mas talvez eles não funcionem corretamente sem os recursos esperados.</span><span class="sxs-lookup"><span data-stu-id="59489-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![excluir grupo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="59489-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59489-195">Next steps</span></span>
* <span data-ttu-id="59489-196">Para exibir os logs de atividade, consulte [Operações de auditoria com o Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="59489-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="59489-197">Para exibir detalhes sobre uma implantação, confira [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="59489-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="59489-198">Para implantar recursos por meio do portal, confira [Implantar recursos com modelos do Resource Manager e o Portal do Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="59489-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="59489-199">Para gerenciar o acesso aos recursos, confira [Usar as atribuições de função para gerenciar o acesso aos recursos de assinatura do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="59489-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="59489-200">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="59489-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

