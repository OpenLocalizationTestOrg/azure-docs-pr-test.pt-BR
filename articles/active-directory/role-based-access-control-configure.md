---
title: "Controle de acesso com base em aaaRole no portal do Azure de saudação | Microsoft Docs"
description: "Introdução ao gerenciamento de acesso com controle de acesso baseado em função no hello Portal do Azure. Use função atribuições tooassign permissões tooyour recursos."
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
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="863d0-104">Usar os recursos do controle de acesso baseado em função toomanage acesso tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="863d0-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="863d0-105">Gerenciar o acesso por usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="863d0-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="863d0-106">Gerenciar o acesso por recurso</span><span class="sxs-lookup"><span data-stu-id="863d0-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="863d0-107">O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Azure.</span><span class="sxs-lookup"><span data-stu-id="863d0-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="863d0-108">Usando o RBAC, você pode conceder somente a quantidade Olá de acesso que os usuários precisam tooperform seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="863d0-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="863d0-109">Este artigo ajuda a colocar em funcionamento com RBAC em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="863d0-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="863d0-110">Se você quiser saber mais sobre como o RBAC ajuda você a gerenciar o acesso, confira [O que é Controle de Acesso Baseado em Função](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="863d0-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="863d0-111">Dentro de cada assinatura, você pode conceder a too2000 atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="863d0-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="863d0-112">Exibir o acesso</span><span class="sxs-lookup"><span data-stu-id="863d0-112">View access</span></span>
<span data-ttu-id="863d0-113">Você pode ver quem tem acesso tooa recursos, grupo de recursos ou assinatura de folha do principal Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="863d0-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="863d0-114">Por exemplo, queremos toosee quem tem acesso tooone dos nossos grupos de recursos:</span><span class="sxs-lookup"><span data-stu-id="863d0-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="863d0-115">Selecione **grupos de recursos** na barra de navegação Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="863d0-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="863d0-116">![Grupos de recursos - ícone](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="863d0-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="863d0-117">Nome de Select Olá Olá do grupo de recursos de saudação **grupos de recursos** folha.</span><span class="sxs-lookup"><span data-stu-id="863d0-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="863d0-118">Selecione **(IAM) do controle de acesso** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="863d0-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="863d0-119">folha de controle de acesso de saudação lista todos os usuários, grupos e aplicativos que receberam o grupo de recursos de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="863d0-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Folha Usuários - acesso herdado versus atribuído - captura de tela](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="863d0-121">Observe que algumas funções passam muito**esse recurso** enquanto outros são **herdadas** -o de outro escopo.</span><span class="sxs-lookup"><span data-stu-id="863d0-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="863d0-122">Acesso está atribuído especificamente o grupo de recursos de toohello ou herdado de uma assinatura de pai de toohello de atribuição.</span><span class="sxs-lookup"><span data-stu-id="863d0-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="863d0-123">Administradores de assinatura clássico e coadministradores são considerados proprietários de assinatura Olá no novo modelo de RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="863d0-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="863d0-124">Adicionar acesso</span><span class="sxs-lookup"><span data-stu-id="863d0-124">Add Access</span></span>
<span data-ttu-id="863d0-125">Conceda acesso de dentro de recurso hello, grupo de recursos ou assinatura que é Olá escopo de atribuição de função hello.</span><span class="sxs-lookup"><span data-stu-id="863d0-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="863d0-126">Selecione **adicionar** na folha de controle de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="863d0-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="863d0-127">Função hello selecione que você deseja tooassign de saudação **selecionar uma função** folha.</span><span class="sxs-lookup"><span data-stu-id="863d0-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="863d0-128">Selecione Olá usuário, grupo ou aplicativo no diretório que você deseja acesso toogrant ao.</span><span class="sxs-lookup"><span data-stu-id="863d0-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="863d0-129">Você pode pesquisar o diretório Olá com nomes de exibição, endereços de email e identificadores de objeto.</span><span class="sxs-lookup"><span data-stu-id="863d0-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Folha Adicionar usuários - pesquisar - captura de tela](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="863d0-131">Selecione **Okey** toocreate atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="863d0-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="863d0-132">Olá **Adicionando usuário** pop-up controla o progresso de saudação.</span><span class="sxs-lookup"><span data-stu-id="863d0-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="863d0-133">![Adicionando barra de progresso do usuário - captura de tela](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="863d0-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="863d0-134">Depois de adicionar com êxito uma atribuição de função, ele será exibido na Olá **usuários** folha.</span><span class="sxs-lookup"><span data-stu-id="863d0-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="863d0-135">Remover acesso</span><span class="sxs-lookup"><span data-stu-id="863d0-135">Remove Access</span></span>
1. <span data-ttu-id="863d0-136">Focalize o cursor sobre o nome de saudação da atribuição de saudação que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="863d0-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="863d0-137">Uma caixa de seleção é exibida próximo nome toohello.</span><span class="sxs-lookup"><span data-stu-id="863d0-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="863d0-138">Use Olá caixas de seleção tooselect uma ou mais atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="863d0-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="863d0-139">Selecione **Remover**.</span><span class="sxs-lookup"><span data-stu-id="863d0-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="863d0-140">Selecione **Sim** tooconfirm remoção de saudação.</span><span class="sxs-lookup"><span data-stu-id="863d0-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="863d0-141">Atribuições herdadas não podem ser removidas.</span><span class="sxs-lookup"><span data-stu-id="863d0-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="863d0-142">Se você precisar tooremove uma atribuição herdada, você precisa toodo-lo no hello escopo em que a atribuição de função hello foi criada.</span><span class="sxs-lookup"><span data-stu-id="863d0-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="863d0-143">Em Olá **escopo** coluna, next muito**herdadas** há um link que utiliza recursos toohello onde essa função foi atribuída.</span><span class="sxs-lookup"><span data-stu-id="863d0-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="863d0-144">Vá na lista de recursos de toohello atribuição de função tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="863d0-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Folha Usuários - botão remover desativa o acesso herdado - captura de tela](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="863d0-146">Acesso de toomanage outras ferramentas</span><span class="sxs-lookup"><span data-stu-id="863d0-146">Other tools toomanage access</span></span>
<span data-ttu-id="863d0-147">Você pode atribuir funções e gerenciar o acesso com comandos de RBAC do Azure em ferramentas diferentes Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="863d0-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="863d0-148">Siga Olá links toolearn mais sobre os pré-requisitos de saudação e começar a trabalhar com comandos do hello RBAC do Azure.</span><span class="sxs-lookup"><span data-stu-id="863d0-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="863d0-149">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="863d0-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="863d0-150">Interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="863d0-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="863d0-151">API REST</span><span class="sxs-lookup"><span data-stu-id="863d0-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="863d0-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="863d0-152">Next Steps</span></span>
* [<span data-ttu-id="863d0-153">Criar relatório de histórico de alterações de acesso</span><span class="sxs-lookup"><span data-stu-id="863d0-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="863d0-154">Consulte Olá [funções internas de RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="863d0-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="863d0-155">Defina suas próprias [Funções personalizadas no RBAC do Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="863d0-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

