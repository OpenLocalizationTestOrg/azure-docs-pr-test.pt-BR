---
title: "grupos de saudação aaaManage seu grupo pertence tooin Active Directory do Azure | Microsoft Docs"
description: "Os grupos podem conter outros grupos no Azure Active Directory. Aqui está como toomanage essas associações."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="0e5b2-104">Gerenciar grupos de toowhich que pertence a um grupo no seu locatário do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0e5b2-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="0e5b2-105">Os grupos podem conter outros grupos no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="0e5b2-106">Aqui está como toomanage essas associações.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="0e5b2-107">Como localizar grupos Olá que meu grupo é membro?</span><span class="sxs-lookup"><span data-stu-id="0e5b2-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="0e5b2-108">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="0e5b2-109">Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="0e5b2-111">Em Olá **usuários e grupos** folha, selecione **todos os grupos de**.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Folha de grupos de saudação de abertura](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="0e5b2-113">Em Olá **usuários e grupos - todos os grupos** folha, selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="0e5b2-114">Em Olá **grupo - *groupname***  folha, selecione **as associações de grupo**.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Folha de associações de grupo abertura Olá](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="0e5b2-116">tooadd seu grupo como membro de outro grupo, em Olá **grupo - as associações de grupo** folha, selecione Olá **adicionar** comando.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="0e5b2-117">Selecione um grupo de saudação **Selecionar grupo** folha e, em seguida, selecione Olá **selecione** botão na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="0e5b2-118">Você pode adicionar o grupo tooonly um grupo por vez.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="0e5b2-119">Olá **usuário** caixa filtra Olá com base na correspondência de sua parte de tooany de entrada de um nome de usuário ou dispositivo de exibição.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="0e5b2-120">Caracteres curinga não são aceitos nessa caixa.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-120">No wildcard characters are accepted in that box.</span></span>

   ![Adicionar uma associação de grupo](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="0e5b2-122">tooremove seu grupo como membro de outro grupo, em Olá **grupo - as associações de grupo** folha, selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="0e5b2-123">Em Olá ***groupname*** folha, selecione Olá **remover** de comando e confirme sua escolha no prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![comando remover associação](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="0e5b2-125">Quando terminar de alterar as associações de grupo para o grupo, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="0e5b2-126">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="0e5b2-126">Additional information</span></span>
<span data-ttu-id="0e5b2-127">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e5b2-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="0e5b2-128">Ver grupos existentes</span><span class="sxs-lookup"><span data-stu-id="0e5b2-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="0e5b2-129">Criar um novo grupo e adicionando membros</span><span class="sxs-lookup"><span data-stu-id="0e5b2-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="0e5b2-130">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="0e5b2-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="0e5b2-131">Gerenciar membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="0e5b2-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="0e5b2-132">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="0e5b2-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
