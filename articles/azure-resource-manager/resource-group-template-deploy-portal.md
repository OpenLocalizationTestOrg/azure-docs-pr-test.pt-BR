---
title: aaaUse toodeploy portal do Azure recursos do Azure | Microsoft Docs
description: Use o portal do Azure e gerenciamento de recursos do Azure toodeploy seus recursos.
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
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="ccf7d-103">Implantar recursos com modelos do Resource Manager e o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf7d-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ccf7d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccf7d-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="ccf7d-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf7d-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="ccf7d-106">Portal</span><span class="sxs-lookup"><span data-stu-id="ccf7d-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="ccf7d-107">API REST</span><span class="sxs-lookup"><span data-stu-id="ccf7d-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="ccf7d-108">Este tópico mostra como Olá toouse [portal do Azure](https://portal.azure.com) com [do Azure Resource Manager](resource-group-overview.md) toodeploy seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="ccf7d-109">toolearn sobre como gerenciar seus recursos, consulte [recursos de gerenciamento Azure por meio do portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="ccf7d-110">Atualmente, não cada serviço suporta Olá portal ou o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="ccf7d-111">Para esses serviços, você precisa Olá toouse [portal clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ccf7d-112">Para obter o status de saudação de cada serviço, consulte [gráfico de disponibilidade do portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="ccf7d-113">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ccf7d-113">Create resource group</span></span>
1. <span data-ttu-id="ccf7d-114">toocreate um grupo de recurso vazio, selecione **novo** > **gerenciamento** > **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![criar grupo de recursos vazio](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="ccf7d-116">Dê a ele um nome e uma localização e, se necessário, selecione uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="ccf7d-117">É necessário tooprovide um local para o grupo de recursos Olá porque o grupo de recursos de saudação armazena metadados sobre os recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="ccf7d-118">Por motivos de conformidade, talvez você queira toospecify onde os metadados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="ccf7d-119">Em geral, é recomendável que você especifique um local em que a maioria de seus recursos residirá.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="ccf7d-120">Usando Olá mesmo local pode simplificar seu modelo.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-120">Using hello same location can simplify your template.</span></span>
   
    ![definir valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="ccf7d-122">Implantar recursos do Marketplace</span><span class="sxs-lookup"><span data-stu-id="ccf7d-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="ccf7d-123">Depois de criar um grupo de recursos, você pode implantar recursos tooit de saudação Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="ccf7d-124">Olá Marketplace fornece soluções predefinidas para cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="ccf7d-125">toostart uma implantação, selecione **novo** e o tipo de saudação do recurso que deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="ccf7d-126">Em seguida, procure versão específica de saudação do recurso Olá você gostaria que toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![implantar recurso](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="ccf7d-128">Se você não vir a solução em particular Olá você gostaria que toodeploy, você pode pesquisar Olá Marketplace para ele.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![pesquisar no Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="ccf7d-130">Dependendo do tipo de saudação do recurso selecionado, você tem uma coleção de propriedades relevantes tooset antes da implantação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="ccf7d-131">Essas opções não são mostradas aqui, pois elas variam com base no tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="ccf7d-132">Para todos os tipos, você deve selecionar um grupo de recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="ccf7d-133">imagem a seguir Olá mostra como toocreate um aplicativo web e implantá-lo toohello grupo de recursos que você criou.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![Criar grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="ccf7d-135">Como alternativa, você pode decidir toocreate um grupo de recursos ao implantar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="ccf7d-136">Selecione **criar novo** e dê um nome de grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![criar novo grupo de recursos](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="ccf7d-138">Sua implantação será iniciada.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-138">Your deployment begins.</span></span> <span data-ttu-id="ccf7d-139">implantação de saudação pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="ccf7d-140">Quando Olá implantação for concluída, você verá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![exibir notificação](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="ccf7d-142">Depois de implantar seus recursos, você pode adicionar mais grupo de recursos toohello de recursos usando Olá **adicionar** comando folha de grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![adicionar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="ccf7d-144">Implantar recursos de um modelo personalizado</span><span class="sxs-lookup"><span data-stu-id="ccf7d-144">Deploy resources from custom template</span></span>
<span data-ttu-id="ccf7d-145">Se você quiser tooexecute uma implantação, mas não usa qualquer um dos modelos de saudação em Olá Marketplace, você pode criar um modelo personalizado que define a infraestrutura de saudação para sua solução.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="ccf7d-146">toolearn sobre a criação de modelos, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="ccf7d-147">toodeploy um modelo personalizado por meio do portal hello, selecione **novo**e iniciar a pesquisa **implantação de modelo** até que você pode selecionar opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![procurar implantação de modelo](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="ccf7d-149">Selecione **implantação de modelo** de recursos disponíveis do hello.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![selecionar implantação de modelo](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="ccf7d-151">Depois de iniciar a implantação de modelo Olá, abra o modelo em branco Olá disponível para personalizar.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![criar modelo](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="ccf7d-153">No editor de hello, adicione a sintaxe JSON Olá que define os recursos de saudação deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="ccf7d-154">Selecione **Salvar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-154">Select **Save** when done.</span></span> <span data-ttu-id="ccf7d-155">Para obter orientação sobre como escrever a sintaxe JSON hello, consulte [passo a passo do Gerenciador de recursos modelo](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![editar modelo](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="ccf7d-157">Ou, você pode selecionar um modelo pré-existente de saudação [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="ccf7d-158">Esses modelos são contribuídos pela comunidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="ccf7d-159">Abrangem vários cenários comuns e alguém pode ter adicionado um modelo semelhante toowhat que você está tentando toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="ccf7d-160">Você pode pesquisar Olá modelos toofind algo que corresponde ao seu cenário.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![selecionar modelo de início rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="ccf7d-162">Você pode exibir o modelo selecionado Olá no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="ccf7d-163">Depois de fornecer Olá todos os outros valores, selecione **criar** toodeploy modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![implantar modelo](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="ccf7d-165">Implantar recursos de um modelo salvo tooyour conta</span><span class="sxs-lookup"><span data-stu-id="ccf7d-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="ccf7d-166">Olá portal permite que você toosave tooyour um modelo conta do Azure e reimplantá-lo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="ccf7d-167">Para obter mais informações sobre como trabalhar com esses salvo modelos, [começar com modelos privados no portal do Azure de saudação](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="ccf7d-168">Selecione de seus modelos salvos, toofind **procurar** > **modelos**.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![procurar modelos](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="ccf7d-170">Na lista de saudação de modelos salvos tooyour conta, selecione Olá aquele que você deseja toowork em.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![modelos salvos](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="ccf7d-172">Selecione **implantar** tooredeploy Isso salva o modelo.</span><span class="sxs-lookup"><span data-stu-id="ccf7d-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![implantar modelo salvo](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="ccf7d-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ccf7d-174">Next steps</span></span>
* <span data-ttu-id="ccf7d-175">Consulte os logs de auditoria tooview [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="ccf7d-176">tootroubleshoot erros de implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="ccf7d-177">tooretrieve um modelo de uma implantação ou o grupo de recursos, consulte [exportar do Azure Resource Manager modelo de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="ccf7d-178">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ccf7d-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

