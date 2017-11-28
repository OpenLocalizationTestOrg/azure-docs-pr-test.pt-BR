---
title: "portal de aaaAzure para políticas de recursos | Microsoft Docs"
description: "Descreve como toouse toocreate portal do Azure e gerenciar políticas de Gerenciador de recursos. Políticas podem ser aplicadas a grupos de assinatura ou o recurso de saudação."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="119c7-104">Usar tooassign portal do Azure e gerenciar políticas de recursos</span><span class="sxs-lookup"><span data-stu-id="119c7-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="119c7-105">Olá portal do Azure permite que você tooassign políticas tooresource grupos de recursos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="119c7-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="119c7-106">interface do usuário Olá torna fácil tooselect política de saudação que você deseja tooassign e especifica valores de parâmetro para configurações de política que política toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="119c7-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="119c7-107">tooassign uma política por meio do portal hello, definição de política de saudação já deve existir em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="119c7-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="119c7-108">Sua assinatura tem várias definições de políticas internas que estão prontas para você tooassign tooresource grupos ou assinaturas.</span><span class="sxs-lookup"><span data-stu-id="119c7-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="119c7-109">Você verá essas políticas internas e as políticas personalizadas que você definiu usando Olá tooassign portal políticas.</span><span class="sxs-lookup"><span data-stu-id="119c7-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="119c7-110">Para uma introdução toopolicies e como toodefine personalizada política, consulte [visão geral do recurso política](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="119c7-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="119c7-111">As políticas são herdadas por todos os recursos filho.</span><span class="sxs-lookup"><span data-stu-id="119c7-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="119c7-112">Portanto, se uma política for aplicada tooa grupo de recursos, é aplicável tooall recursos de saudação desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="119c7-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="119c7-113">Neste artigo, o termo de saudação **escopo** refere-se o grupo de recursos de toohello ou assinatura que é atribuída a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="119c7-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="119c7-114">Políticas são avaliadas durante a criação e atualização de recursos (PUT e operações de PATCHES).</span><span class="sxs-lookup"><span data-stu-id="119c7-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="119c7-115">Atribuir uma política</span><span class="sxs-lookup"><span data-stu-id="119c7-115">Assign a policy</span></span>

1. <span data-ttu-id="119c7-116">tooassign tooeither uma política um grupo de recursos ou assinatura, selecione esse grupo de recursos ou a assinatura.</span><span class="sxs-lookup"><span data-stu-id="119c7-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="119c7-117">Em configurações de saudação, selecione **políticas**.</span><span class="sxs-lookup"><span data-stu-id="119c7-117">In hello settings, select **Policies**.</span></span>

   ![selecionar políticas](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="119c7-119">toocreate uma atribuição de diretiva para este escopo, selecione **Adicionar atribuição**.</span><span class="sxs-lookup"><span data-stu-id="119c7-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![adicionar atribuição](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="119c7-121">Selecione a política de saudação tooassign desejado.</span><span class="sxs-lookup"><span data-stu-id="119c7-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="119c7-122">Mesmo se você não adicionou nenhuma assinatura de tooyour de definições de política, você pode ver políticas internas de saudação que estão disponíveis para atribuição.</span><span class="sxs-lookup"><span data-stu-id="119c7-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="119c7-123">Essas políticas internas abrangem vários cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="119c7-123">These built-in policies cover many common scenarios.</span></span>

   ![selecionar definição](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="119c7-125">Depois de selecionar uma política, você pode ver uma descrição da política de saudação e os parâmetros para essa política.</span><span class="sxs-lookup"><span data-stu-id="119c7-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="119c7-126">Por exemplo, hello imagem a seguir mostra Olá **permitido locais** parâmetro, que é necessário para a política de saudação que restringe os locais disponíveis Olá.</span><span class="sxs-lookup"><span data-stu-id="119c7-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![mostrar parâmetros](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="119c7-128">Por meio da interface do usuário hello, selecione Olá toospecify de valores para parâmetros de política de saudação (como locais de saudação que podem ser usados para implantação).</span><span class="sxs-lookup"><span data-stu-id="119c7-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![selecionar valores do parâmetro](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="119c7-130">Forneça valores para Olá outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="119c7-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="119c7-131">escopo de saudação é atribuído automaticamente com base na folha de saudação selecionado ao iniciar a atribuição de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="119c7-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="119c7-132">Selecione **OK** quando tiver concluído.</span><span class="sxs-lookup"><span data-stu-id="119c7-132">Select **OK** when done.</span></span>

   ![definir parâmetros](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="119c7-134">Você atribuiu uma política de saudação toohello especificado escopo.</span><span class="sxs-lookup"><span data-stu-id="119c7-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="119c7-135">Exibir atribuições de política</span><span class="sxs-lookup"><span data-stu-id="119c7-135">View policy assignments</span></span>

<span data-ttu-id="119c7-136">Depois de atribuir uma política, você vê-lo na lista de saudação de políticas para esse escopo.</span><span class="sxs-lookup"><span data-stu-id="119c7-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="119c7-137">Olá **detalhes** guia mostra um resumo da atribuição de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="119c7-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![mostrar detalhes](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="119c7-139">Olá **regra de atribuição** guia mostra hello JSON para definição de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="119c7-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![mostrar regra de atribuição](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="119c7-141">Alterar uma atribuição de política existente</span><span class="sxs-lookup"><span data-stu-id="119c7-141">Change an existing policy assignment</span></span>

<span data-ttu-id="119c7-142">toochange uma política, selecione **Editar atribuição de** ou **excluir**</span><span class="sxs-lookup"><span data-stu-id="119c7-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![editar ou excluir atribuição](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="119c7-144">Atribuir políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="119c7-144">Assign custom policies</span></span>

<span data-ttu-id="119c7-145">Se você tiver definido as políticas personalizadas em sua assinatura, essas políticas estão disponíveis para atribuição por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="119c7-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="119c7-146">Essas políticas são precedidas por **[Personalizada]**</span><span class="sxs-lookup"><span data-stu-id="119c7-146">Those policies are prefaced with **[Custom]**</span></span>

![políticas personalizadas](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="119c7-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="119c7-148">Next steps</span></span>
* <span data-ttu-id="119c7-149">toolearn sobre a sintaxe do hello JSON para definir políticas, consulte [visão geral do recurso política](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="119c7-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="119c7-150">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="119c7-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="119c7-151">esquema de política de saudação é publicado em [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="119c7-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

