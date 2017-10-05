---
title: "Controle de acesso baseado em função no portal do Azure | Microsoft Docs"
description: "Introdução ao gerenciamento de acesso com o Controle de Acesso Baseado em Função no Portal do Azure. Use as atribuições de função para atribuir permissões a seus recursos."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 9df7f7851ef1fc6b4ed03b981aa5062d6b0913ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-role-based-access-control-to-manage-access-to-your-azure-subscription-resources"></a><span data-ttu-id="859ee-104">Usar o Controle de Acesso Baseado em Funções para gerenciar o acesso aos recursos de sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="859ee-104">Use Role-Based Access Control to manage access to your Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="859ee-105">Gerenciar o acesso por usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="859ee-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="859ee-106">Gerenciar o acesso por recurso</span><span class="sxs-lookup"><span data-stu-id="859ee-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="859ee-107">O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Azure.</span><span class="sxs-lookup"><span data-stu-id="859ee-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="859ee-108">Usando o RBAC, você pode conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="859ee-108">Using RBAC, you can grant only the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="859ee-109">Este artigo ajuda você a começar a usar o RBAC no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="859ee-109">This article helps you get up and running with RBAC in the Azure portal.</span></span> <span data-ttu-id="859ee-110">Se você quiser saber mais sobre como o RBAC ajuda você a gerenciar o acesso, confira [O que é Controle de Acesso Baseado em Função](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="859ee-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="859ee-111">Dentro de cada assinatura, você pode conceder até 2000 atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="859ee-111">Within each subscription, you can grant up to 2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="859ee-112">Exibir o acesso</span><span class="sxs-lookup"><span data-stu-id="859ee-112">View access</span></span>
<span data-ttu-id="859ee-113">Você pode ver quem tem acesso a um recurso, grupo de recursos ou assinatura em sua folha principal no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="859ee-113">You can see who has access to a resource, resource group, or subscription from its main blade in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="859ee-114">Por exemplo, queremos ver quem tem acesso a um dos nossos grupos de recursos:</span><span class="sxs-lookup"><span data-stu-id="859ee-114">For example, we want to see who has access to one of our resource groups:</span></span>

1. <span data-ttu-id="859ee-115">Selecione o ícone **Grupo de recursos** na barra de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="859ee-115">Select **Resource groups** in the navigation bar on the left.</span></span>  
    <span data-ttu-id="859ee-116">![Grupos de recursos - ícone](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="859ee-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="859ee-117">Na folha **Grupos de recursos** , selecione o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="859ee-117">Select the name of the resource group from the **Resource groups** blade.</span></span>
3. <span data-ttu-id="859ee-118">Selecione **Controle de acesso (IAM)** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="859ee-118">Select **Access control (IAM)** from the left menu.</span></span>  
4. <span data-ttu-id="859ee-119">A folha Controle de acesso lista todos os usuários, grupos e aplicativos que receberam acesso ao grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="859ee-119">The Access control blade lists all users, groups, and applications that have been granted access to the resource group.</span></span>  
   
    ![Folha Usuários - acesso herdado versus atribuído - captura de tela](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="859ee-121">Observe que algumas funções são definidas para **Este recurso** enquanto outras são **Herdadas** de outro escopo.</span><span class="sxs-lookup"><span data-stu-id="859ee-121">Notice that some roles are scoped to **This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="859ee-122">O acesso é atribuído especificamente ao grupo de recursos ou herdado de uma atribuição à assinatura pai.</span><span class="sxs-lookup"><span data-stu-id="859ee-122">Access is either assigned specifically to the resource group or inherited from an assignment to the parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="859ee-123">Os administradores e coadministradores de assinatura clássicos são, na realidade, os proprietários da assinatura no novo modelo de RBAC.</span><span class="sxs-lookup"><span data-stu-id="859ee-123">Classic subscription admins and co-admins are considered owners of the subscription in the new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="859ee-124">Adicionar acesso</span><span class="sxs-lookup"><span data-stu-id="859ee-124">Add Access</span></span>
<span data-ttu-id="859ee-125">Conceda acesso de dentro do recurso, do grupo de recursos ou da assinatura que é o escopo da atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="859ee-125">You grant access from within the resource, resource group, or subscription that is the scope of the role assignment.</span></span>

1. <span data-ttu-id="859ee-126">Selecione **Adicionar** na folha Controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="859ee-126">Select **Add** on the Access control blade.</span></span>  
2. <span data-ttu-id="859ee-127">Selecione a função que você deseja atribuir na folha **Selecionar uma função** .</span><span class="sxs-lookup"><span data-stu-id="859ee-127">Select the role that you wish to assign from the **Select a role** blade.</span></span>
3. <span data-ttu-id="859ee-128">Selecione o usuário, o grupo ou o aplicativo ao qual você deseja conceder acesso.</span><span class="sxs-lookup"><span data-stu-id="859ee-128">Select the user, group, or application in your directory that you wish to grant access to.</span></span> <span data-ttu-id="859ee-129">Você pode pesquisar o diretório por nomes para exibição, endereços de email e identificadores de objeto.</span><span class="sxs-lookup"><span data-stu-id="859ee-129">You can search the directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Folha Adicionar usuários - pesquisar - captura de tela](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="859ee-131">Selecione **OK** para criar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="859ee-131">Select **OK** to create the assignment.</span></span> <span data-ttu-id="859ee-132">O pop-up **Adicionando usuário** rastreia o progresso.</span><span class="sxs-lookup"><span data-stu-id="859ee-132">The **Adding user** popup tracks the progress.</span></span>  
    <span data-ttu-id="859ee-133">![Adicionando barra de progresso do usuário - captura de tela](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="859ee-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="859ee-134">Após a adição de uma atribuição de função com êxito, ela será exibida na folha **Usuários** .</span><span class="sxs-lookup"><span data-stu-id="859ee-134">After successfully adding a role assignment, it will appear on the **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="859ee-135">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="859ee-135">Remove Access</span></span>
1. <span data-ttu-id="859ee-136">Focalize o cursor sobre o nome da atribuição que você deseja remover.</span><span class="sxs-lookup"><span data-stu-id="859ee-136">Hover your cursor over the name of the assignment that you want to remove.</span></span> <span data-ttu-id="859ee-137">Uma caixa de seleção aparece ao lado do nome.</span><span class="sxs-lookup"><span data-stu-id="859ee-137">A check box appears next to the name.</span></span>
2. <span data-ttu-id="859ee-138">Use as caixas de seleção para selecionar uma ou mais atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="859ee-138">Use the check boxes to select one or more role assignments.</span></span>
2. <span data-ttu-id="859ee-139">Selecione **Remover**.</span><span class="sxs-lookup"><span data-stu-id="859ee-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="859ee-140">Clique em **Sim** para confirmar a remoção.</span><span class="sxs-lookup"><span data-stu-id="859ee-140">Select **Yes** to confirm the removal.</span></span>

<span data-ttu-id="859ee-141">Atribuições herdadas não podem ser removidas.</span><span class="sxs-lookup"><span data-stu-id="859ee-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="859ee-142">Se você precisar remover uma atribuição herdada, será necessário fazê-lo no escopo em que a atribuição de função foi criada.</span><span class="sxs-lookup"><span data-stu-id="859ee-142">If you need to remove an inherited assignment, you need to do it at the scope where the role assignment was created.</span></span> <span data-ttu-id="859ee-143">Na coluna **Escopo**, ao lado de **Herdado**, há um link que leva aos recursos em que essa função foi atribuída.</span><span class="sxs-lookup"><span data-stu-id="859ee-143">In the **Scope** column, next to **Inherited** there is a link that takes you to the resources where this role was assigned.</span></span> <span data-ttu-id="859ee-144">Vá para o recurso listado ali a fim de remover a atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="859ee-144">Go to the resource listed there to remove the role assignment.</span></span>

![Folha Usuários - botão remover desativa o acesso herdado - captura de tela](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-to-manage-access"></a><span data-ttu-id="859ee-146">Outras ferramentas para gerenciar o acesso</span><span class="sxs-lookup"><span data-stu-id="859ee-146">Other tools to manage access</span></span>
<span data-ttu-id="859ee-147">Você pode atribuir funções e gerenciar o acesso com comandos do RBAC do Azure em ferramentas que não sejam o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="859ee-147">You can assign roles and manage access with Azure RBAC commands in tools other than the Azure portal.</span></span>  <span data-ttu-id="859ee-148">Siga os links para saber mais sobre os pré-requisitos e começar a usar os comandos do RBAC do Azure.</span><span class="sxs-lookup"><span data-stu-id="859ee-148">Follow the links to learn more about the prerequisites and get started with the Azure RBAC commands.</span></span>

* [<span data-ttu-id="859ee-149">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="859ee-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="859ee-150">Interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="859ee-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="859ee-151">API REST</span><span class="sxs-lookup"><span data-stu-id="859ee-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="859ee-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="859ee-152">Next Steps</span></span>
* [<span data-ttu-id="859ee-153">Criar relatório de histórico de alterações de acesso</span><span class="sxs-lookup"><span data-stu-id="859ee-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="859ee-154">Confira as [Funções internas do RBAC do Azure](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="859ee-154">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="859ee-155">Defina suas próprias [Funções personalizadas no RBAC do Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="859ee-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

