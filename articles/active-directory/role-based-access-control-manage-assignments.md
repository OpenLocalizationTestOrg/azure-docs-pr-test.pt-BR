---
title: "Exibir atribuições de acesso a recursos do Azure | Microsoft Docs"
description: "Exibir e gerenciar todas as atribuições de Controle de Acesso Baseado em Função para um usuário ou grupo no portal do Azure"
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
ms.openlocfilehash: 72c695d08bdf5de003d51ffb0768184e1e4d00ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal"></a><span data-ttu-id="3b053-103">Exibir as atribuições de acesso para usuários e grupos no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3b053-103">View access assignments for users and groups in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b053-104">Gerenciar o acesso por usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="3b053-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="3b053-105">Gerenciar o acesso por recurso</span><span class="sxs-lookup"><span data-stu-id="3b053-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="3b053-106">Com RBAC (controle de acesso baseado em função) na visualização do Azure AD (Azure Active Directory), você pode gerenciar o acesso aos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b053-106">With role-based access control (RBAC) in the Azure Active Directory (Azure AD), you can manage access to your Azure resources.</span></span> 

<span data-ttu-id="3b053-107">O acesso atribuído com o RBAC é refinado porque há duas maneiras de restringir as permissões:</span><span class="sxs-lookup"><span data-stu-id="3b053-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="3b053-108">**Escopo:** as atribuições de função RBAC passam para uma assinatura, um grupo de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="3b053-108">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="3b053-109">Um usuário que recebe acesso a um recurso único não pode acessar os outros recursos na mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="3b053-109">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="3b053-110">**Função:** dentro do escopo da atribuição, o acesso é reduzido ainda mais com a atribuição de função.</span><span class="sxs-lookup"><span data-stu-id="3b053-110">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="3b053-111">Funções podem ser de alto nível, como proprietário, ou específicas, como leitor de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3b053-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="3b053-112">Funções só podem ser atribuídas de uma assinatura, grupo de recursos ou recurso que seja o escopo da atribuição.</span><span class="sxs-lookup"><span data-stu-id="3b053-112">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="3b053-113">Mas você pode exibir todas as atribuições de acesso para determinado usuário ou grupo em um mesmo lugar.</span><span class="sxs-lookup"><span data-stu-id="3b053-113">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="3b053-114">Em de cada assinatura, você pode ter até 2.000 atribuições de função.</span><span class="sxs-lookup"><span data-stu-id="3b053-114">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="3b053-115">Saiba mais sobre como [Usar atribuições de função para gerenciar o acesso aos recursos de assinatura do Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3b053-115">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="3b053-116">Exibir atribuições de acesso</span><span class="sxs-lookup"><span data-stu-id="3b053-116">View access assignments</span></span>
<span data-ttu-id="3b053-117">Para pesquisar as atribuições de acesso para um único usuário ou grupo, comece em Azure Active Directory no [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b053-117">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="3b053-118">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b053-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="3b053-119">Se essa opção não estiver visível na sua lista de navegação, selecione **Mais Serviços** e role para baixo até encontrar **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b053-119">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="3b053-120">Selecione **Usuários e Grupos** e **Todos os usuários** ou **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="3b053-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="3b053-121">Para este exemplo, vamos focar em usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="3b053-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="3b053-122">![Gerenciar usuários e grupos no Azure Active Directory – captura de tela](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="3b053-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="3b053-123">Pesquise o usuário por nome ou nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="3b053-123">Search for the user by name or username.</span></span>
4. <span data-ttu-id="3b053-124">Selecione **Recursos do Azure** na folha do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b053-124">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="3b053-125">Todas as atribuições de acesso para esse usuário são exibidas.</span><span class="sxs-lookup"><span data-stu-id="3b053-125">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="3b053-126">Permissões de leitura para exibir atribuições</span><span class="sxs-lookup"><span data-stu-id="3b053-126">Read permissions to view assignments</span></span>
<span data-ttu-id="3b053-127">Essa página mostra apenas as atribuições de acesso que você tem permissão para ler.</span><span class="sxs-lookup"><span data-stu-id="3b053-127">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="3b053-128">Por exemplo, você tem acesso de leitura para a assinatura A e vai para a folha de recursos do Azure a fim de verificar as atribuições do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b053-128">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="3b053-129">É possível ver as atribuições de acesso dele para a assinatura A, mas não é possível ver que ele também tem acesso a atribuições na assinatura B.</span><span class="sxs-lookup"><span data-stu-id="3b053-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="3b053-130">Excluir atribuições de acesso</span><span class="sxs-lookup"><span data-stu-id="3b053-130">Delete access assignments</span></span>
<span data-ttu-id="3b053-131">Nessa folha, você pode excluir atribuições de acesso que foram atribuídas diretamente a um usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="3b053-131">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="3b053-132">Se a atribuição de acesso foi herdada de um grupo pai, você precisará ir até o recurso ou a assinatura e gerenciar a atribuição lá.</span><span class="sxs-lookup"><span data-stu-id="3b053-132">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="3b053-133">Na lista de todas as atribuições de acesso para um usuário ou grupo, selecione aquela que deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="3b053-133">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="3b053-134">Selecione **Remover** e **Sim** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="3b053-134">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="3b053-135">![Remover atribuição de acesso – captura de tela](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="3b053-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b053-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b053-136">Next steps</span></span>

* <span data-ttu-id="3b053-137">Introdução ao Controle de Acesso Baseado em Função a fim de [Usar atribuições de função para gerenciar o acesso aos recursos de assinatura do Azure](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="3b053-137">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="3b053-138">Confira as [Funções internas do RBAC do Azure](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="3b053-138">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

