---
title: Gerenciar os grupos aos quais seu grupo pertence no Azure Active Directory | Microsoft Docs
description: "Os grupos podem conter outros grupos no Azure Active Directory. Veja como gerenciar essas associações."
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
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="52c0b-104">Gerenciar a quais grupos um grupo pertence no seu locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52c0b-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="52c0b-105">Os grupos podem conter outros grupos no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52c0b-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="52c0b-106">Veja como gerenciar essas associações.</span><span class="sxs-lookup"><span data-stu-id="52c0b-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="52c0b-107">Como localizo os grupos dos quais meu grupo é um membro?</span><span class="sxs-lookup"><span data-stu-id="52c0b-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="52c0b-108">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="52c0b-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="52c0b-109">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="52c0b-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="52c0b-111">Na folha **Usuários e grupos**, escolha **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="52c0b-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Abrir a folha de grupos](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="52c0b-113">Na folha **Usuários e grupos - Todos os grupos** , escolha um grupo.</span><span class="sxs-lookup"><span data-stu-id="52c0b-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="52c0b-114">Na folha **Grupo – *nomedogrupo*** selecione **Associações de grupo** .</span><span class="sxs-lookup"><span data-stu-id="52c0b-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Abrir a folha de associações de grupo](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="52c0b-116">Para adicionar seu grupo como membro de outro grupo, na folha **Grupo - Associações de grupo**, selecione o comando **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="52c0b-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="52c0b-117">Selecione um grupo na folha **Selecionar Grupo** e pressione o botão **Selecionar** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="52c0b-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="52c0b-118">Você só pode adicionar o grupo a um grupo por vez.</span><span class="sxs-lookup"><span data-stu-id="52c0b-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="52c0b-119">A caixa **Usuário** filtra a exibição com base na correspondência de sua entrada com qualquer parte de um nome de usuário ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="52c0b-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="52c0b-120">Caracteres curinga não são aceitos nessa caixa.</span><span class="sxs-lookup"><span data-stu-id="52c0b-120">No wildcard characters are accepted in that box.</span></span>

   ![Adicionar uma associação de grupo](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="52c0b-122">Para remover seu grupo como um membro de outro grupo, na folha **Grupo - Associações de grupo** , escolha um grupo.</span><span class="sxs-lookup"><span data-stu-id="52c0b-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="52c0b-123">Na folha ***groupname***, selecione o comando **Remover** e confirme sua escolha no prompt.</span><span class="sxs-lookup"><span data-stu-id="52c0b-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![comando remover associação](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="52c0b-125">Quando terminar de alterar as associações de grupo para o grupo, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="52c0b-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="52c0b-126">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="52c0b-126">Additional information</span></span>
<span data-ttu-id="52c0b-127">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="52c0b-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="52c0b-128">Ver grupos existentes</span><span class="sxs-lookup"><span data-stu-id="52c0b-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="52c0b-129">Criar um novo grupo e adicionando membros</span><span class="sxs-lookup"><span data-stu-id="52c0b-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="52c0b-130">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="52c0b-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="52c0b-131">Gerenciar membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="52c0b-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="52c0b-132">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="52c0b-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
