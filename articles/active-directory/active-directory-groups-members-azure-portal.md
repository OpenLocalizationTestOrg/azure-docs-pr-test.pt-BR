---
title: "membros de saudação aaaManage para um grupo no Active Directory do Azure | Microsoft Docs"
description: "Como tooadd ou remover usuários e dispositivos de um grupo no Active Directory do Azure"
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
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="d49e1-103">Gerenciar associação de grupo de usuários em seu locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d49e1-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="d49e1-104">Este artigo explica como toomanage Olá membros de um grupo no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d49e1-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="d49e1-105">Como localizar membros hello e gerenciá-los?</span><span class="sxs-lookup"><span data-stu-id="d49e1-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="d49e1-106">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="d49e1-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="d49e1-107">Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d49e1-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="d49e1-109">Em Olá **usuários e grupos** folha, selecione **todos os grupos de**.</span><span class="sxs-lookup"><span data-stu-id="d49e1-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Folha de grupos de saudação de abertura](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="d49e1-111">Em Olá **usuários e grupos - todos os grupos** folha, selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="d49e1-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="d49e1-112">Em Olá **grupo - *groupname***  folha, selecione **membros**.</span><span class="sxs-lookup"><span data-stu-id="d49e1-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![Folha de membros de saudação de abertura](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="d49e1-114">tooadd membros toohello grupo Olá **grupo - membros** folha, selecione **adicionar membros**.</span><span class="sxs-lookup"><span data-stu-id="d49e1-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![Comando Adicionar Membros](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="d49e1-116">Em Olá **membros** folha, selecione um ou mais usuários ou dispositivos de grupo de toohello de tooadd e selecione Olá **selecione** botão na parte inferior de saudação do hello folha tooadd-los toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="d49e1-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="d49e1-117">Olá **usuário** caixa filtra Olá com base na correspondência de sua parte de tooany de entrada de um nome de usuário ou dispositivo de exibição.</span><span class="sxs-lookup"><span data-stu-id="d49e1-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="d49e1-118">Caracteres curinga não são aceitos nessa caixa.</span><span class="sxs-lookup"><span data-stu-id="d49e1-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="d49e1-119">os membros do grupo Olá Olá tooremove **grupo - membros** folha, selecione um membro.</span><span class="sxs-lookup"><span data-stu-id="d49e1-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="d49e1-120">Em Olá ***membername*** folha, selecione Olá **remover** de comando e confirme sua escolha no prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="d49e1-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Comando Remover Membros](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="d49e1-122">Quando terminar de alterar os membros do grupo de saudação, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="d49e1-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="d49e1-123">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="d49e1-123">Additional information</span></span>
<span data-ttu-id="d49e1-124">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d49e1-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="d49e1-125">Ver grupos existentes</span><span class="sxs-lookup"><span data-stu-id="d49e1-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d49e1-126">Criar um novo grupo e adicionando membros</span><span class="sxs-lookup"><span data-stu-id="d49e1-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="d49e1-127">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="d49e1-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="d49e1-128">Gerenciar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="d49e1-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="d49e1-129">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="d49e1-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
