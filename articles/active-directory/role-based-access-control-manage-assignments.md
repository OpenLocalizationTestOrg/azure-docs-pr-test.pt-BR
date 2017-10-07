---
title: "atribuições de acesso de recursos do Azure aaaView | Microsoft Docs"
description: "Exibir e gerenciar todas as atribuições de controle de acesso baseado em função Olá para qualquer usuário ou grupo no hello portal do Azure"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="31c06-103">Exibir as atribuições de acesso para usuários e grupos no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="31c06-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31c06-104">Gerenciar o acesso por usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="31c06-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="31c06-105">Gerenciar o acesso por recurso</span><span class="sxs-lookup"><span data-stu-id="31c06-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="31c06-106">Com controle de acesso baseado em função (RBAC) em hello Azure Active Directory (AD do Azure), você pode gerenciar o acesso tooyour Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="31c06-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="31c06-107">Acesso atribuído com RBAC é refinado porque você pode restringir as permissões de saudação de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="31c06-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="31c06-108">**Escopo:** atribuições de função RBAC são assinatura específica tooa no escopo, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="31c06-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="31c06-109">Um usuário recebe acesso tooa único recurso não é possível acessar outros recursos Olá mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="31c06-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="31c06-110">**Função:** no escopo de saudação de atribuição de saudação, o acesso é reduzido ainda mais atribuindo uma função.</span><span class="sxs-lookup"><span data-stu-id="31c06-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="31c06-111">Funções podem ser de alto nível, como proprietário, ou específicas, como leitor de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="31c06-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="31c06-112">Funções podem ser atribuídas somente de dentro de assinatura Olá, grupo de recursos ou recurso que é Olá escopo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="31c06-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="31c06-113">Mas você pode exibir todas as atribuições de acesso de saudação para um determinado usuário ou grupo em um único lugar.</span><span class="sxs-lookup"><span data-stu-id="31c06-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="31c06-114">Você pode ter até too2000 atribuições de função em cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="31c06-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="31c06-115">Obter mais informações sobre como muito[usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="31c06-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="31c06-116">Exibir atribuições de acesso</span><span class="sxs-lookup"><span data-stu-id="31c06-116">View access assignments</span></span>
<span data-ttu-id="31c06-117">toolook backup atribuições de acesso Olá para um único usuário ou grupo, iniciar no Active Directory do Azure no hello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31c06-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="31c06-118">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31c06-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="31c06-119">Se essa opção não estiver visível na sua lista de navegação, selecione **mais serviços** e, em seguida, role para baixo toofind **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="31c06-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="31c06-120">Selecione **Usuários e Grupos** e **Todos os usuários** ou **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="31c06-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="31c06-121">Para este exemplo, vamos focar em usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="31c06-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="31c06-122">![Gerenciar usuários e grupos no Azure Active Directory – captura de tela](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="31c06-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="31c06-123">Pesquisa de usuário Olá por nome ou o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="31c06-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="31c06-124">Selecione **recursos do Azure** na folha de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="31c06-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="31c06-125">Todas as atribuições de acesso Olá para esse usuário são exibidos.</span><span class="sxs-lookup"><span data-stu-id="31c06-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="31c06-126">Tooview atribuições de permissões de leitura</span><span class="sxs-lookup"><span data-stu-id="31c06-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="31c06-127">Esta página mostra apenas as atribuições de acesso de saudação que você tenha permissão tooread.</span><span class="sxs-lookup"><span data-stu-id="31c06-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="31c06-128">Por exemplo, você tem acesso de leitura toosubscription A e vá toohello toocheck de folha de recursos do Azure atribuições do usuário.</span><span class="sxs-lookup"><span data-stu-id="31c06-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="31c06-129">É possível ver as atribuições de acesso dele para a assinatura A, mas não é possível ver que ele também tem acesso a atribuições na assinatura B.</span><span class="sxs-lookup"><span data-stu-id="31c06-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="31c06-130">Excluir atribuições de acesso</span><span class="sxs-lookup"><span data-stu-id="31c06-130">Delete access assignments</span></span>
<span data-ttu-id="31c06-131">Desta folha, você pode excluir atribuições de acesso que foram atribuídas diretamente tooa usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="31c06-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="31c06-132">Se a atribuição de acesso de saudação foi herdada de um grupo pai, você precisa toogo toohello recursos ou assinatura e gerenciar a atribuição de saudação existe.</span><span class="sxs-lookup"><span data-stu-id="31c06-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="31c06-133">Na lista de saudação de todas as atribuições de acesso de saudação para um usuário ou grupo, selecione Olá um deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="31c06-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="31c06-134">Selecione **remover** e **Sim** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="31c06-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="31c06-135">![Remover atribuição de acesso – captura de tela](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="31c06-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="31c06-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31c06-136">Next steps</span></span>

* <span data-ttu-id="31c06-137">Introdução ao controle de acesso baseado em função muito[usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="31c06-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="31c06-138">Consulte Olá [funções internas de RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="31c06-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

