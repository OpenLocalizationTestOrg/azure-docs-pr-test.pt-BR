---
title: "Portal do Azure para políticas de recurso | Microsoft Docs"
description: "Descreve como usar o portal do Azure para criar e gerenciar políticas do Resource Manager. As políticas podem ser aplicadas em grupos de recursos ou de assinatura."
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="ebb3c-104">Usar o portal do Azure para atribuir e gerenciar políticas de recurso</span><span class="sxs-lookup"><span data-stu-id="ebb3c-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="ebb3c-105">O portal do Azure permite que você atribua políticas de recurso a grupos de recursos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="ebb3c-106">A interface do usuário facilita a seleção da política que você deseja atribuir e a especificação de valores de parâmetros para essa política para personalizar as configurações de política.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="ebb3c-107">Para atribuir uma política por meio do portal, a definição de política já deve existir em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="ebb3c-108">Sua assinatura tem várias definições de políticas internas que estão prontas para serem atribuídas a grupos de recursos ou assinaturas.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="ebb3c-109">Você vê essas políticas internas e as políticas personalizadas definidas ao usar o portal para atribuir políticas.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="ebb3c-110">Para obter uma introdução às políticas e como definir uma política personalizada, consulte [Visão geral da política de recurso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ebb3c-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="ebb3c-111">As políticas são herdadas por todos os recursos filho.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="ebb3c-112">Então, se uma política for aplicada a um grupo de recursos, ela será aplicável a todos os recursos desse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="ebb3c-113">Neste artigo, o termo **escopo** refere-se ao grupo de recursos ou à assinatura que foi atribuído à política.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="ebb3c-114">Políticas são avaliadas durante a criação e atualização de recursos (PUT e operações de PATCHES).</span><span class="sxs-lookup"><span data-stu-id="ebb3c-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="ebb3c-115">Atribuir uma política</span><span class="sxs-lookup"><span data-stu-id="ebb3c-115">Assign a policy</span></span>

1. <span data-ttu-id="ebb3c-116">Para atribuir uma política a um grupo de recursos ou a uma assinatura, selecione uma assinatura ou um grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="ebb3c-117">Nas configurações, selecione **Políticas**.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-117">In the settings, select **Policies**.</span></span>

   ![selecionar políticas](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="ebb3c-119">Para criar uma atribuição de política para esse escopo, selecione **Adicionar atribuição**.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![adicionar atribuição](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="ebb3c-121">Selecione a política que você deseja atribuir.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-121">Select the policy you want to assign.</span></span> <span data-ttu-id="ebb3c-122">Mesmo que você não tenha adicionado nenhuma definição de política à sua assinatura, você vê as políticas internas disponíveis para atribuição.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="ebb3c-123">Essas políticas internas abrangem vários cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-123">These built-in policies cover many common scenarios.</span></span>

   ![selecionar definição](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="ebb3c-125">Depois de selecionar uma política, você verá uma descrição da política e seus parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="ebb3c-126">Por exemplo, a imagem a seguir mostra o parâmetro **Localizações permitidas**, que é necessário para a política que restringe as localizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![mostrar parâmetros](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="ebb3c-128">Por meio da interface do usuário, selecione os valores a serem especificados para os parâmetros da política (por exemplo, as localizações que podem ser usadas para implantação).</span><span class="sxs-lookup"><span data-stu-id="ebb3c-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![selecionar valores do parâmetro](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="ebb3c-130">Forneça valores para os outros parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-130">Provide values for the other parameters.</span></span> <span data-ttu-id="ebb3c-131">O escopo é atribuído automaticamente de acordo com a folha selecionada ao iniciar a atribuição de política.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="ebb3c-132">Selecione **OK** quando tiver concluído.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-132">Select **OK** when done.</span></span>

   ![definir parâmetros](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="ebb3c-134">Você atribuiu a política ao escopo especificado.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="ebb3c-135">Exibir atribuições de política</span><span class="sxs-lookup"><span data-stu-id="ebb3c-135">View policy assignments</span></span>

<span data-ttu-id="ebb3c-136">Depois de atribuir uma política, você a verá na lista de políticas desse escopo.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="ebb3c-137">A guia **Detalhes** mostra um resumo da atribuição de política.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![mostrar detalhes](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="ebb3c-139">A guia **Regra de atribuição** mostra o JSON para a definição de política.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![mostrar regra de atribuição](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="ebb3c-141">Alterar uma atribuição de política existente</span><span class="sxs-lookup"><span data-stu-id="ebb3c-141">Change an existing policy assignment</span></span>

<span data-ttu-id="ebb3c-142">Para alterar uma política, selecione **Editar atribuição** ou **Excluir**</span><span class="sxs-lookup"><span data-stu-id="ebb3c-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![editar ou excluir atribuição](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="ebb3c-144">Atribuir políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="ebb3c-144">Assign custom policies</span></span>

<span data-ttu-id="ebb3c-145">Se você tiver definido políticas personalizadas na assinatura, essas políticas estarão disponíveis para atribuição por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="ebb3c-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="ebb3c-146">Essas políticas são precedidas por **[Personalizada]**</span><span class="sxs-lookup"><span data-stu-id="ebb3c-146">Those policies are prefaced with **[Custom]**</span></span>

![políticas personalizadas](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="ebb3c-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebb3c-148">Next steps</span></span>
* <span data-ttu-id="ebb3c-149">Para saber mais sobre a sintaxe JSON para definição de políticas, consulte [Visão geral da política de recurso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ebb3c-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ebb3c-150">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ebb3c-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="ebb3c-151">O esquema da política é publicado em [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="ebb3c-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

