---
title: Usar o Portal do Azure para implantar recursos do Azure | Microsoft Docs
description: Use o portal do Azure e o Azure Resource Manager para implantar seus recursos.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="044fe-103">Implantar recursos com modelos do Resource Manager e o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="044fe-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="044fe-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="044fe-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="044fe-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="044fe-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="044fe-106">Portal</span><span class="sxs-lookup"><span data-stu-id="044fe-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="044fe-107">API REST</span><span class="sxs-lookup"><span data-stu-id="044fe-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="044fe-108">Este tópico mostra como usar o [Portal do Azure](https://portal.azure.com) com o [Azure Resource Manager](resource-group-overview.md) para implantar seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="044fe-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="044fe-109">Para saber sobre como gerenciar seus recursos, confira [Gerenciar recursos do Azure por meio do portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="044fe-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="044fe-110">Atualmente, nem todo serviço dá suporte ao portal ou ao Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="044fe-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="044fe-111">Para esses serviços, você precisa usar o [Portal Clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="044fe-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="044fe-112">Para obter o status de cada serviço, confira o [Gráfico de disponibilidade do Portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="044fe-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="044fe-113">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="044fe-113">Create resource group</span></span>
1. <span data-ttu-id="044fe-114">Para criar um grupo de recursos vazio, selecione **Novo** > **Gerenciamento** > **Grupo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="044fe-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![criar grupo de recursos vazio](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="044fe-116">Dê a ele um nome e uma localização e, se necessário, selecione uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="044fe-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="044fe-117">Você precisa fornecer um local para o grupo de recursos pois o grupo de recursos armazena metadados sobre os recursos.</span><span class="sxs-lookup"><span data-stu-id="044fe-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="044fe-118">Por motivos de conformidade, talvez você queira especificar onde os metadados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="044fe-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="044fe-119">Em geral, é recomendável que você especifique um local em que a maioria de seus recursos residirá.</span><span class="sxs-lookup"><span data-stu-id="044fe-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="044fe-120">Usar o mesmo local pode simplificar seu modelo.</span><span class="sxs-lookup"><span data-stu-id="044fe-120">Using the same location can simplify your template.</span></span>
   
    ![definir valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="044fe-122">Implantar recursos do Marketplace</span><span class="sxs-lookup"><span data-stu-id="044fe-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="044fe-123">Após criar um grupo de recursos, você pode implantar recursos nele usando o Marketplace.</span><span class="sxs-lookup"><span data-stu-id="044fe-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="044fe-124">O Marketplace oferece soluções predefinidas para cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="044fe-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="044fe-125">Para iniciar uma implantação, selecione **Novo** e o tipo de recurso que você gostaria de implantar.</span><span class="sxs-lookup"><span data-stu-id="044fe-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="044fe-126">Em seguida, procure a versão específica do recurso que deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="044fe-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![implantar recurso](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="044fe-128">Se você não vir a solução específica que deseja implantar, você poderá pesquisá-lo no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="044fe-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![pesquisar no Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="044fe-130">Dependendo do tipo de recurso selecionado, você terá uma coleção de propriedades significativas para definir antes da implantação.</span><span class="sxs-lookup"><span data-stu-id="044fe-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="044fe-131">Essas opções não são mostradas aqui, pois elas variam com base no tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="044fe-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="044fe-132">Para todos os tipos, você deve selecionar um grupo de recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="044fe-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="044fe-133">A imagem a seguir mostra como criar um aplicativo Web e implantá-lo no grupo de recursos que você criou.</span><span class="sxs-lookup"><span data-stu-id="044fe-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![Criar grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="044fe-135">Como alternativa, você pode optar por criar um grupo de recursos ao implantar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="044fe-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="044fe-136">Selecione **Criar novo** e dê um nome ao grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="044fe-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![criar novo grupo de recursos](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="044fe-138">Sua implantação será iniciada.</span><span class="sxs-lookup"><span data-stu-id="044fe-138">Your deployment begins.</span></span> <span data-ttu-id="044fe-139">Ela pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="044fe-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="044fe-140">Quando a implantação for concluída, você verá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="044fe-140">When the deployment has finished, you see a notification.</span></span>
   
    ![exibir notificação](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="044fe-142">Após implantar seus recursos, você poderá adicionar mais deles ao grupo de recursos usando o comando **Adicionar** na folha do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="044fe-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![adicionar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="044fe-144">Implantar recursos de um modelo personalizado</span><span class="sxs-lookup"><span data-stu-id="044fe-144">Deploy resources from custom template</span></span>
<span data-ttu-id="044fe-145">Se quiser executar uma implantação, mas não usar nenhum dos modelos no Marketplace, você poderá criar um modelo personalizado que define a infraestrutura para sua solução.</span><span class="sxs-lookup"><span data-stu-id="044fe-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="044fe-146">Para saber mais sobre a criação de modelos, veja [Criando modelos do Gerenciador de Recursos do Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="044fe-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="044fe-147">Para implantar um modelo personalizado usando o portal, selecione **Novo** e comece a procurar pela **Implantação do Modelo** até conseguir selecioná-la nas opções.</span><span class="sxs-lookup"><span data-stu-id="044fe-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![procurar implantação de modelo](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="044fe-149">Selecione a **Implantação do Modelo** entre os recursos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="044fe-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![selecionar implantação de modelo](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="044fe-151">Depois de iniciar a implantação do modelo, abra o modelo em branco que está disponível para personalização.</span><span class="sxs-lookup"><span data-stu-id="044fe-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![criar modelo](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="044fe-153">No editor, adicione a sintaxe JSON que define os recursos que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="044fe-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="044fe-154">Selecione **Salvar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="044fe-154">Select **Save** when done.</span></span> <span data-ttu-id="044fe-155">Para obter as diretrizes sobre como escrever a sintaxe JSON, confira o [Passo a passo do modelo do Resource Manager](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="044fe-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![editar modelo](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="044fe-157">Ou você pode selecionar um modelo já existente entre os [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="044fe-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="044fe-158">Esses modelos são fornecidos como contribuição pela comunidade.</span><span class="sxs-lookup"><span data-stu-id="044fe-158">These templates are contributed by the community.</span></span> <span data-ttu-id="044fe-159">Eles abrangem vários cenários comuns, e alguém pode ter adicionado um modelo parecido com o que você está tentando implantar.</span><span class="sxs-lookup"><span data-stu-id="044fe-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="044fe-160">Você pode pesquisar nos modelos para encontrar algo que corresponda ao seu cenário.</span><span class="sxs-lookup"><span data-stu-id="044fe-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![selecionar modelo de início rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="044fe-162">Você pode exibir o modelo selecionado no editor.</span><span class="sxs-lookup"><span data-stu-id="044fe-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="044fe-163">Depois de fornecer todos os outros valores, selecione **Criar** para implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="044fe-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![implantar modelo](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="044fe-165">Implantar recursos de um modelo salvo em sua conta</span><span class="sxs-lookup"><span data-stu-id="044fe-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="044fe-166">O portal permite que você salve um modelo em sua conta do Azure e o reimplante mais tarde.</span><span class="sxs-lookup"><span data-stu-id="044fe-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="044fe-167">Para obter mais informações sobre como trabalhar com esses modelos salvos, confira [Introdução aos modelos privados no Portal do Azure](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="044fe-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="044fe-168">Para localizar os modelos salvos, selecione **Procurar** > **Modelos**.</span><span class="sxs-lookup"><span data-stu-id="044fe-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![procurar modelos](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="044fe-170">Na lista de modelos salvos em sua conta, selecione aquele no qual deseja trabalhar.</span><span class="sxs-lookup"><span data-stu-id="044fe-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![modelos salvos](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="044fe-172">Selecione **Implantar** para reimplantar o modelo salvo.</span><span class="sxs-lookup"><span data-stu-id="044fe-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![implantar modelo salvo](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="044fe-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="044fe-174">Next steps</span></span>
* <span data-ttu-id="044fe-175">Para exibir os logs de auditoria, confira [Operações de auditoria com o Gerenciador de Recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="044fe-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="044fe-176">Para solucionar erros de implantação, confira [View deployment operations](resource-manager-deployment-operations.md) (Exibir operações de implantação).</span><span class="sxs-lookup"><span data-stu-id="044fe-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="044fe-177">Para recuperar um modelo de uma implantação ou de um grupo de recursos, confira [Exportar um modelo do Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="044fe-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="044fe-178">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="044fe-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

