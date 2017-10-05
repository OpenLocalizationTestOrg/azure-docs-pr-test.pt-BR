---
title: Gerenciar os membros de um grupo no Azure Active Directory | Microsoft Docs
description: "Como adicionar ou remover usuários e dispositivos de um grupo no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="6cf8a-103">Gerenciar associação de grupo de usuários em seu locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cf8a-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="6cf8a-104">Este artigo explica como gerenciar os membros de um grupo no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6cf8a-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="6cf8a-105">Como localizo os membros e os gerencio?</span><span class="sxs-lookup"><span data-stu-id="6cf8a-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="6cf8a-106">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="6cf8a-107">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="6cf8a-109">Na folha **Usuários e grupos**, escolha **Todos os grupos**.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Abrir a folha de grupos](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="6cf8a-111">Na folha **Usuários e grupos - Todos os grupos** , escolha um grupo.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="6cf8a-112">Na folha **Grupo – *nomedogrupo*** , selecione **Membros**.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Abrir a folha Membros](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="6cf8a-114">Para adicionar membros ao grupo, na folha **Grupo - Membros**, selecione **Adicionar Membros**.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Comando Adicionar Membros](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="6cf8a-116">Na folha **Membros**, escolha um ou mais usuários ou dispositivos para adicionar ao grupo e escolha o botão **Selecionar** na parte inferior da folha para adicioná-los ao grupo.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="6cf8a-117">A caixa **Usuário** filtra a exibição com base na correspondência de sua entrada com qualquer parte de um nome de usuário ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="6cf8a-118">Caracteres curinga não são aceitos nessa caixa.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="6cf8a-119">Para remover membros do grupo, na folha **Grupo - Membros** , escolha um membro.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="6cf8a-120">Na folha ***membername***, selecione o comando **Remover** e confirme sua escolha no prompt.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Comando Remover Membros](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="6cf8a-122">Quando terminar de alterar os membros do grupo, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="6cf8a-123">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="6cf8a-123">Additional information</span></span>
<span data-ttu-id="6cf8a-124">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="6cf8a-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="6cf8a-125">Ver grupos existentes</span><span class="sxs-lookup"><span data-stu-id="6cf8a-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="6cf8a-126">Criar um novo grupo e adicionando membros</span><span class="sxs-lookup"><span data-stu-id="6cf8a-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="6cf8a-127">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="6cf8a-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="6cf8a-128">Gerenciar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="6cf8a-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="6cf8a-129">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="6cf8a-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
